# Summary
**Morton Ordering** is a technique that maps a multi-dimensional space into a single dimension (it effectively "linearizes" a higher order space). Importantly, it does this by maintaining a sense of **spatial locality** between points in space. This is useful in practice as keeping items spatially coherent in a program will often lead to better cache performance.

Morton Ordering is also known as "Z-Ordering", as the technique effectively carves a "Z-shaped path" through space.
> Contrast this with the commonly used **lexicographical ordering** (storing row by row), where points that are next to each other in space (last point of a row vs the first point of the net) may be very far in memory.

> [!Info]- Example of Morton Ordering
> ![[Graphics/Resources/Morton Ordering Example.png]]

# Mechanism + Benefits
Under the hood, Morton Ordering works by cleverly using bit shuffling.

Let's consider the binary representations of a point $(x,y)$ in an 8x8 space, and let's interpret what the binary representation is telling us about how to navigate the space.
- The first bit in the number tells us which **1/2** of the space we're in
- The second bit in the number tells us which **1/4** of the space we're in
- The third bit in the number tell us which **1/8** of the space we're in

So for a number like $x = 5$ with binary $(101)_2$, the binary is telling us:
- Our number is in the 2nd half of the space
- Within that half, our number is in the first quarter
- Within that quarter, our number is in the second eighth 

We have an analogous set of "navigation instructions" for $y$. Morton Order takes these instructions and interleaves their bits, alternating the bits of x and y to create a single longer number.
In other words given $(x,y)$, Morton order would give us number
$$
\dots y_2 x_2 y_1 x_1 y_0 x_0
$$

Doing this for every point on a grid gives us a "Z-shape" through space!

We can extend this to higher dimensions by simply interleaving more bits. For example for $(x,y,z)$, we get
$$z_2 y_2 x_2 z_1 y_1 x_1 z_0 y_0 x_0$$

> [!Example] x = 5, y = 3
> Let $(x,y) = (5,3)$. The binary representations are $(101_2, 011_2)$. So Morton Order would produce
> $$
> 011011 = 27
> $$
> In other words, the coordinate $(5,3)$ maps to index 27 in linear space.

This is a simple mechanism, but produces remarkable results.

Because we are interleaving bits from most significant to least significant, all points lying in the same quadrant of space will share the same higher order bits for their Morton index. This gives us a property known as **subtree contiguity**. This is very important in spatial data structures like quadtrees and octrees.

> [!Info] Subtree Contiguity
> **Subtree Contiguity** is a property guaranteeing that for any quadrant in a quadtree (or octree), all points in that quadrant will map to a single, contiguous, unbroken block of indices in 1D, because they all share the same higher order bits! 
> 
> This is incredibly good for cache locality!!

In code this can be implemented using a for loop. But it can also be implemented much faster using bit shifts and masks.
The key is realizing that to add a 0 bit between each bit in a number, we can do it by moving **whole ranges** at once.

```cpp
// Decoder is the exact opposite case to this
uint32_t spread_bits_16(uint16_t x)
{
    // 00000000 00000000 11111111 11111111
	uint32_t out = x;
	// Shift upper 8 bits over by 8 bits
	// 00000000 11111111 00000000 11111111
	out = (out | (out << 8)) & 0x00FF00FF;
	// Shift upper 4 bits over by 4 bits
	// 00001111 00001111 00001111 00001111
	out = (out | (out << 4)) & 0x0F0F0F0F;
	// Shift upper 2 bits over by 2 bits
	// 00110011 00110011 00110011 00110011
	out = (out | (out << 2)) & 0x33333333;
	// Shift upper 1 bit over by 1 bit
	// 01010101 01010101 01010101 01010101
	out = (out | (out << 1)) & 0x55555555;
	return out;
}

uin32_t encode(uint16_t x, uint16_t y)
{
	return spread_bits_16(x) | (spread_bits_16(y) << 1);
}
```

> [!Warning] Limitations of Morton Ordering 
> Morton Ordering is not perfect. The Z shape path does give better spatial locality, but after you finished a Z-shaped block you are still jumping to the beginning of the next one. This jump in practice can be large which can be undesirable.
> 
> A famous alternative is the **Hilbert Curve**, which never makes these large scale jumps, and often will give subdomains that are more compact than the Morton Ordering. But Hilbert Ordering has a slightly higher cost of computing the index.

# Resources
- https://www.bohrium.com/en/sciencepedia/feynman/keyword/morton_order#principles-and-mechanisms