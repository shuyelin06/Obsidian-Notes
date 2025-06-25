---
title: Culling
tags:
- cmsc427
---

What we can't see is often equally as important as what we can see. This is true with both performance and visual implications.
- In a scene with potentially millions of triangles, certain triangles should not be visible to the camera.
- Being able to prevent triangles from being rendered saves computational resources.

This section will discuss a variety of **culling techniques**. These are techniques that let us prevent triangles (or parts of triangles) from being rendered.

# Hardware Culling
Here, we discuss some culling techniques that the hardware can perform for us.

## Backface Culling
Recall that a triangle is defined by 3 points, $P_0, P_1, P_2$, and the winding direction of this triangle defines the direction of the triangle's normal in space. **Backface Culling** culls the triangles whose surface normals are not facing our camera. By default, typical convention is to treat the CCW winding order as the front face of the triangle.

If $D$ is our view direction (triangle to camera), and $N$ is the triangle's normal, then we can do a cull check by computing:
$$
\text{dot}(D,N) > 0
$$
> In other words, check if the angle between the two directional vectors is is within 90 degrees.

If the dot product is 0 or less, we cull the triangle as it is not facing the triangle. 

## Viewport Clipping
After projecting triangles into the viewport, the hardware also performs **viewport clipping**, where the parts of triangles outside of the viewport will be clipped.


## Depth Testing (Z-Testing)
Even after rendering a triangle to the screen, we can't be sure this triangle is what we want to see in the final image. This is because there could still be other triangles closer to the camera that would occlude our current triangle. 

In fact, without storing any depth information about the rendered triangles, what we see in the final image depends on the order in which we render our triangles. This can create weird visual artifacts.

To resolve this, we can use **depth buffering (z-buffering)**. 
1. For every pixel in our screen, we will store it's "depth"
   - Typically, we store $1/w$ as this is already computed for rasterization already.
2. During rasterization, we will compare the computed pixel's value to the stored value.
3. We will update our pixel only if the new pixel is closer than the stored pixel.

Below are some common issues that may arise while depth testing.

> [!Info] Z-Fighting
> If triangles are very close to each other, then numerical imprecision may cause them to be alternatively chosen in the z-buffer, creating a "stitching" pattern.
>
> This can be excacerbated by the fact that the highest depth precision occurs closest to 0. 
