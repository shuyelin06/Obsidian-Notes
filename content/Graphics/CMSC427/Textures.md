---
title: Textures
tags:
- cmsc427
---

# Textures
To get complex scenes, we can't just use objects that have constant material properties. At the same time, we can't use millions of triangles to add micro-details to a surface (too expensive)! 

Instead, a rendering engine will often use **textures** to add extra, finer details onto the object. These are essentially 2D images, where every pixel contains some sort of data that can be used in the shader.

## Texture Mapping
To do this, we first associate triangles with 2-dimensional $(u,v)$ coordinates, where $u,v \in [0,1]$. These correspond to locations on a 2D image, with the top-left corner being at $(0,0)$, and the bottom-right corner being at $(1,1)$.

Between the vertex and pixel shader, these $u,v$ coordinates are interpolated across the triangle. After that, they can be used to sample the image for the data at that location. 

Textures can be used for a variety of purposes. However, they can only be useful if we have a good $uv$ mapping onto the object. To do this, we will generally compute $u,v$ using two functions of vertex positions, $f_u (x,y,z), f_v (x,y,z)$.
> If we don't have a good mapping, we can get weird visual artifacts or seams.

### Cylinder Mapping
In 3D space, we can represent $(x,y,z)$ coordinates in cylindrical coordinates as:
$$
\begin{align*}
x = r \cos(2 \pi u) \\
y = hv \\
z = r \sin(2 \pi u)
\end{align*}
$$

In **Cylinder Mapping**, we choose $u$ to represent the angle of the point on the cylinder, and $v$ to represent the height. 

We can also use this mapping with non-cylinder objects, by projecting the object's points onto the surface of a cylinder.

### Spherical Mapping
In 3D space, we can also represent $(x,y,z)$ coordinates in spherical coordinates...


## Mip-Mapping
When using textures, we can sometimes get aliasing artifacts for texture coordinates sufficiently far from the camera. For example, consider the following checkerboard pattern.
![[Graphics/CMSC427/Resources/MipmapE1.png]]

As we get far from the camera, we start seeing these "C" patterns. Why is this? 

This occurs because as the distance to the camera increases, for every pixel, we only sample the texture data once. In other words, for a single pixel that may cover multiple texels, we only take 1 sample. This means we sample the texture inconsistently along varying distances, effectively making us see a different texture than what we originally had. 
> Intuitively, if we sample a texture at every other pixel, then our resultant texture could be different! In fact, if we used a checkerboard, then sampling every other pixel could yield all black / white! 

To resolve this, we need far-away pixels "sample" more texels, so that the texture sampling is consistent regardless of distance. We can do this by computing the "average" of texels over the covered pixel area. 

> [!Warning] Inefficiency of Naive Averaging
> If we just naively average texels, things would easily get really expensive! This is because as objects get smaller, we need to average many texels. This creates a very high memory access and computation cost!

To do this at a relatively low cost, we can use **mip maps**. These are pre-computed, filtered versions of textures. The filtering on the texture performs a "local" averaging, which is good enough for our purposes.
- Every mip-map level is $\frac{1}{4}^{th}$ the size of the previous, and is the result of filtering the previous level.

Note that mip-maps don't actually increase our memory cost by a terrible amount. In fact, they only increase the cost by $\frac{1}{3}$.
$$
\frac{1}{3} = \frac{1}{4} + \frac{1}{16} + \frac{1}{64} + \dots
$$

> [!Info] Using Mip-Maps
> By precomputing several filtured textures of varying sizes, we can remove most of our aliasing! 
>
> Now, after interpolating the texture coordinate, we will:
> 1. First, compute the approximate size of the pixel in texture space
> 2. Look-up the color in the nearest mip-map. "Nearest" corresponds to the mip-map level where one texel covers approximately the same number of texels as our pixel.
>    - We could also look-up in multiple nearest mip-maps, and do an interpolation between the results.
>
> > We can approximate the size of the pixel, by taking the partial derivatives of the mapping.

Mip-maps do not completely solve the problem.
- Mip-map texels always represent square areas, but pixel area is not always square in texture space.
- Mip-maps are an approximate solution to the problem.


## Texturing Techniques
### Bump Maps
Surface detail is often the result of small changes in the surface geometry. 

Instead of modeling this with an unreasonable number of triangles, we can use a texture! **Bump Mapping** is a technique where we use a texture to alter the normal of a surface, according to a texture. This provides the illusion of small-scale surface detail, without needing more triangles.

We typically generate bump maps in a pre-processing step. First, we start with a texture map that has small surface displacements, typically as a height field. 
- For every location in the texture, find the normal by crossing the partial derivatives in both directions.
  $$
  n(u,v) = \frac{d(u + \Delta u, v) - d(u - \Delta u, v), 2 \Delta u, 0] }{2 \Delta u} \times \frac{d(u, v + \Delta v) - d(u, v - \Delta v), 0, 2 \Delta v] }{2 \Delta v}
  $$
- Then, normalize the normal and encode it in the texture's RGB channels.

Now, to use the bump map with a surface, we first assert that the normals are defined **relative** to the local tangent-normal vectors of the surface. 
- First, compute the triangle's tangent vector, and average the tangents over adjacent triangles to get smooth transitions. Pass this into the shader.
- In the vertex shader, cross the triangle's tangent with its normal to get the bi-normal. 
- In the pixel shader,
  - Use the tangent, binormal, normal as a basis for the components of the bump map normal. This gives us a normal for the object.
  - Transform this normal to the camera space.

### Environment Mapping
To create more realistic scenes, we may want to add a background to our scene. This could be a sky, a landscape, etc.

**Environmental Mapping** does this using textures. Using textures, we can encode a 3D image, to create a function $f(D)$, which, given a direction, returns the color in that direction. Then, if the depth in that direction is infinite, we can use this color to create a more realistic background.
