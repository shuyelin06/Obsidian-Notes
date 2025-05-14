---
title: CMSC427
tags:
- cmsc427
---

- [[Geometry]]
- [[Culling]]
- [[Textures]]


--- Lighting ---

# Lighting

# Shadows
Shadows are a key part of any rendering engine, as they communicate essential information to the viewer.
- How far objects are from surfaces
- Where objects are contacting surfaces

A shadow is defined by 2 parts. It's **umbra** is the fully-shadowed region, and the **penumbra** is the partially-shadowed region.
> The penumbra exists, as if we have an area light, there are regions that only parts of the light touches.

Because of their ease to compute, most engines focus on hard shadows, and approximate soft shadows. To create hard shadows, there are two widely used techniques:
- Shadow Mapping
- Shadow Volumes

> This is still an active area of research!

## Shadow Mapping
**Shadow mapping** creates shadows by considering that a point is only lit by a light if it is **visible** from the light source. So, we can if a point is shadowed by rendering the scene from the light's point of view, and seeing if the light can see the point.
1. **Depth Pass**: In the first pass, we will render the scene from the light's point of view, by treating it as a "camera". This rendered image will be stored into a texture (**shadow map**).
2. **Render Pass**: In the render pass, we render the scene from the camera position as normal. At each pixel, compare the distance of the pixel to the light to the the value in the shadow map.
   - If the distance is less than the shadow map distance, then the pixel is lit.
   - If the distance is greater than the shadow map distance, then the pixel is in shadow.
   
While great, shadow maps can have a variety of aliasing artifacts. We discuss a few below.

### Z-Fighting
Because we have limited precision when storing depth values, pixel depths close to the shadowmap depth could be greater or less than the stored sheerly due to numerical imprecision. 

This z-fighting creates **shadow acne**, where objects will appear to self-shadow themselves. 

To resolve this, we need to add a very small bias in the depth comparison test, to filter for these false positives.

### Sampling Problems
Sometimes, a shadow map pixel can project to many image pixels. This can create "stair-stepping" artifacts, as there aren't enough samples.

One way to resolve this, is by making it so our shadow map can store more data:
- Increase the resolution of the shadow map
- Split the shadow map into several slices, with different resolutions
- Tweak the projection for shadow map rendering (see light space perspective shadow maps)

We could also resolve this by filtering our shadow, to reduce the visual artifacts. One way to do this is by using **percentage closer filtering**.


----


# Ray Tracing
## Context
**Ray Tracing** is another method of rendering 3D scenes. In ray tracing, we shoot light rays in the scene and figure out which ones hit the camera.

Because we are modeling the light rays themselves, ray tracing offers a great deal of versatility! In particular, ray tracing lets us account for the indirect rays in a scene, which can oftentimes make up a great deal of the lighting in a scene.

We do this as follows. Typically, ray tracers will perform **backward tracing**, as it is the most efficient way:
1. For every pixel, cast a ray from the camera into the scene. This is the **primary ray**.
2. When the ray intersects an object, we cast **secondary rays** to accumulate the light at that object. We repeat this intersection process on these rays.
   - Specular Ray
   - Refracted Ray
   - Etc.
   
> [!Info] Acceleration Structures
> A large part of ray-tracing's research is focused on acceleration strutures that make ray casting faster. The faster we can cast our rays, the more rays we can cast in total! This makes for a more realistic image.

However, traditional ray tracing only casts rays in preset main directions, which can miss lots of indirect lighting sources. To resolve this, we want to shoot more rays in randomized directions.
> If we only cast one ray per pixel, we may also get **aliasing**. We can fix this by casting multiple rays.

In **path tracing**, we also randomly cast other secondary rays in various directions. This accounts for additional indirect lighting. The directions in which we sample in are defined by the **Bidirectional Scatter Distribution Function**, which defines where most light for a given lighting component comes from. 
- **BRDF**: Reflected Scatter Distribution
- **BTDR**: Transmitted Scatter Distribution

Path tracing makes it so we sample secondary rays in random directions


## Refraction
When light rays travel between mediums, they appear to "bend". This is because as light crosses mediums, its speed changes, which in turn changes its angle.

The degree of which a light bends after ending a medium is given by the **index of refraction** $n = \frac{c}{v}$, where 
- $c$ is the speed of light in a vacuum
- $v$ is the speed of light in the medium

The actual bend of the light ray is given by **Snell's Law**, which defines a relationship between the angle of incidence and refraction
$$
\frac{\sin \theta_1}{\sin \theta_2} = \frac{n_2}{n_1}
$$
In vector form, this is also given as
$$
r = \frac{n_1}{n_2} v + ( \frac{n_1}{n_2} \cos \theta_1 + \cos \theta_2 ) n
$$
Where $v$ is the viewing direction, $r$ is the refracted direction, and $n$ is the normal.

Between mediums, light can also totally reflect. If the angle of the refracted ray is given as
$$
\theta_2 = \arcsin (\theta_1 \frac{n_1}{n_2})
$$
Then, for critical angle 
$$
\theta_c = \frac{n_2}{n_1}
$$
If the incident angle is greater than the critical angle ($\theta_1 > \theta_c$), then the light will instead reflect, and not cross the interface between the media.

The relationship between reflection and refraction is given by the **Freshnel Equations**, which define a ratio $F$ between reflected and refracted light. As this is often complex to compute, most graphics programs instead use **Schlick's Approximation**
$$
f = \frac{(1 - \frac{n_1}{n_2})^2}{(1 + \frac{n_1}{n_2})^2}
$$
