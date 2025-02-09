# Vulkan examples and demos

<img src="./images/vulkanlogoscene.png" alt="Vulkan demo scene" height="256px">

Assorted C++ examples for [Vulkan(tm)](https://www.khronos.org/vulkan/), the new graphics and compute API from Khronos.

## Building

The repository contains everything required to compile the examples out of the box on windows and Linux. All required dependencies and libraries are included.

### Visual Studio
A Visual Studio (2015) solution file for compiling all examples is included with the repository.

### CMake
For Linux (or if you want to use a different IDE) there is also a a CMakeLists.txt to be used with [CMake](https://cmake.org).

Use it to generate a platform-specific build configuration for building all examples. It should work with different compilers on Windows and Linux (C++11 required).

### Android

The repository also contains a few Android examples to get started, check the [Android readme](./android/README.md) for details.

## Binaries

Precompiled binaries for Windows (x64), Linux (x64) and Android can be [found here](http://vulkan.gpuinfo.org/examples.php). I'll try keep them up-to-date with the repositry.

Note that these only contain the binaries, you still need the repository for the data (shaders, models, textures) and put the binaries into to bin subfolder.

## Vendor support
The examples have been tested on different vendors, but since **most drivers are beta** not all examples may work with all vendors.

Currently all examples should run on NVIDIA, and most of them on AMD too. Demos that currently won't work with one IHV will be fixed as soon as possible.

The android examples have only been tested on NVIDIA hardware yet.

## API-Version

The examples are build against **API Version 1.0.3** and support **implementations starting with 1.0.1**. This ensures that beta drivers not updated to the most recent API-Version can run the examples.

## Examples

## Triangle
<img src="./screenshots/basic_triangle.png" height="96px" align="right">

Most basic example. Renders a colored triangle using an indexed vertex buffer, only one pipeline with very simple shaders. Uses a single uniform buffer for the matrices.

This example won't make use of helper functions or initializers (like the other examples) and is much more of an explicit example then the others included in this repository. It contains lot's of boiler plate that you'd usually encapsulate in helper functions and classes.
<br><br>

## Texture mapping
<img src="./screenshots/basic_texture.png" height="96px" align="right">

Loads a single texture and displays it on a simple quad. Shows how to upload a texture including mip maps to the gpu in an optimal (tiling) format. Also demonstrates how to display the texture using a combined image sampler with anisotropic filtering enabled.
<br><br>

## Cubemap
<img src="./screenshots/texture_cubemap.png" height="96px" align="right">

Building on the basic texture loading example a cubemap is loaded into host visible memory and then transformed into an optimal format for the GPU.
The demo uses two different pipelines (and shader sets) to display the cubemap as a skybox (background) and as a source for reflections.
<br><br>

## Texture array
<img src="./screenshots/texture_array.png" height="96px" align="right">

Texture arrays allow storing of multiple images in different layers without any interpolation between the layers.
This example demonstrates the use of a 2D texture array with instanced rendering. Each instance samples from a different layer of the texture array.
<br><br>

## Distance field fonts
<img src="./screenshots/font_distancefield.png" height="96px" align="right">

Instead of just sampling a bitmap font texture, a texture with per-character signed distance fields is used to generate high quality glyphs in the fragment shader. This results in a much higher quality than common bitmap fonts, even if heavily zoomed.

Distance field font textures can be generated with tools like [Hiero](https://github.com/libgdx/libgdx/wiki/Hiero).
<br><br>

## Pipelines
<img src="./screenshots/basic_pipelines.png" height="96px" align="right">

Pipelines replace the huge (and cumbersome) state machine of OpenGL. This example creates different pipelines with different states and shader setups.
<br><br>

## Gears
<img src="./screenshots/basic_gears.png" height="96px" align="right">

Vulkan interpretation of glxgears. Procedurally generates separate meshes for each gear, with every mesh having it's own uniform buffer object for animation. Also demonstrates how to use different descriptor sets.
<br><br>

## Mesh loading and rendering
<img src="./screenshots/basic_mesh.png" height="96px" align="right">

Uses [assimp](https://github.com/assimp/assimp) to load and a mesh from a common 3D format including a color map. The mesh data is then converted to a fixed vertex layout matching the pipeline (and shader) layout descriptions.
<br><br>

## Mesh instancing
<img src="./screenshots/instancing.png" height="96px" align="right">

Shows the use of instancing for rendering the same mesh with differing uniforms with one single draw command. This saves performance if the same mesh has to be rendered multiple times.
<br><br>

## Skeletal animation
<img src="./screenshots/mesh_skeletalanimation.png" height="96px" align="right">

Based on the mesh loading example, this example loads and displays a rigged COLLADA model including animations. Bone weights are extracted for each vertex and are passed to the vertex shader together with the final bone transformation matrices for vertex position calculations.
<br><br>

## Push constants
<img src="./screenshots/push_constants.png" height="96px" align="right">

Demonstrates the use of push constants for updating small blocks of shader data with high speed (and without having to use a uniform buffer). Displays several light sources with position updates through a push constant block in a separate command buffer.
<br><br>

## Occlusion queries
<img src="./screenshots/occlusion_queries.png" height="96px" align="right">

Shows how to use occlusion queries to determine object visibility depending on the number of passed samples for a given object. Does an occlusion pass first, drawing all objects (and the occluder) with basic shaders, then reads the query results to conditionally color the objects during the final pass depending on their visibility.
<br><br>

## Offscreen rendering
<img src="./screenshots/basic_offscreen.png" height="96px" align="right">

Uses a separate framebuffer (that is not part of the swap chain) and a texture target for offscreen rendering. The texture is then used as a mirror.
<br><br>

## Radial blur
<img src="./screenshots/radial_blur.png" height="96px" align="right">

Demonstrates basic usage of fullscreen shader effects. The scene is rendered offscreen first, gets blitted to a texture target and for the final draw this texture is blended on top of the 3D scene with a radial blur shader applied.
<br><br>

## Bloom
<img src="./screenshots/bloom.png" height="96px" align="right">

Implements a bloom effect to simulate glowing parts of a 3D mesh. A two pass gaussian blur (horizontal and then vertical) is used to generate a blurred low res version of the scene only containing the glowing parts of th the 3D mesh. This then gets blended onto the scene to add the blur effect.
<br><br>

## Deferred shading
<img src="./screenshots/deferred_shading.png" height="96px" align="right">

Demonstrates the use of multiple render targets to fill a G-Buffer for deferred shading.

Deferred shading collects all values (color, normal, position) into different render targets in one pass thanks to multiple render targets, and then does all shading and lighting calculations based on these in scree space, thus allowing for much more light sources than traditional forward renderers.
<br><br>

## Omnidirectional shadow mapping
<img src="./screenshots/shadow_omnidirectional.png" height="96px" align="right">

Uses a dynamic 32 bit floating point cube map for a point light source that casts shadows in all directions (unlike projective shadow mapping).
The cube map faces contain thee distances from the light sources, which are then used in the scene rendering pass to determine if the fragment is shadowed or not.
<br><br>

## Spherical environment mapping
<img src="./screenshots/spherical_env_mapping.png" height="96px" align="right">

Uses a matcap texture (spherical reflection map) to fake complex lighting. It's based on [this article](https://github.com/spite/spherical-environment-mapping).
<br><br>

## Parallax mapping
<img src="./screenshots/parallax_mapping.jpg" height="96px" align="right">

Like normal mapping, parallax mapping simulates geometry on a flat surface. In addition to normal mapping a heightmap is used to offset texture coordinates depending on the viewing angle giving the illusion of added depth.
<br><br>

## (Tessellation shader) PN-Triangles
<img src="./screenshots/tess_pntriangles.jpg" height="96px" align="right">

Generating curved PN-Triangles on the GPU using tessellation shaders to add details to low-polygon meshes, based on [this paper](http://alex.vlachos.com/graphics/CurvedPNTriangles.pdf), with shaders from [this tutorial](http://onrendering.blogspot.de/2011/12/tessellation-on-gpu-curved-pn-triangles.html).
<br><br>

## (Tessellation shader) Displacement mapping
<img src="./screenshots/tess_displacement.jpg" height="96px" align="right">

Uses tessellation shaders to generate and displace geometry based on a displacement map (heightmap).
<br><br>

## (Compute shader) Particle system
<img src="./screenshots/compute_particles.png" height="96px" align="right">

Attraction based particle system. A shader storage buffer is used to store particle data and updated by a compute shader. The buffer is then used by the graphics pipeline for rendering.
<br><br>

## (Compute shader) Image processing
<img src="./screenshots/compute_imageprocessing.png" height="96px" align="right">

Demonstrates the use of a separate compute queue (and command buffer) to apply different convolution kernels on an input image.
<br><br>

## (Geometry shader) Normal debugging
----
<img src="./screenshots/geom_normals.png" height="96px" align="right">

Renders the vertex normals of a complex mesh with the use of a geometry shader. The mesh is rendered solid first and the a geometry shader that generates lines from the face normals is used in the second pass.
<br><br>

## Vulkan demo scene
<img src="./screenshots/vulkan_scene.png" height="96px" align="right">

More of a playground than an actual example. Renders multiple meshes with different shaders (and pipelines) including a background.
<br><br>

<br>
## Android

This repository also contains a few Android examples that are (for now) separated from the rest of the examples. See the [Android readme](./android/README.md) for details on what is included and how to build the examples.

The examples already share a few source files with existing examples and might be integrated into them at some point.

## Additional documentation
- [Vulkan example base class](./documentation/examplebaseclass.md)
- more to come...

## Credits
Thanks to the authors of these libraries :
- [OpenGL Mathematics (GLM)](https://github.com/g-truc/glm)
- [OpenGL Image (GLI)](https://github.com/g-truc/gli)
- [Open Asset Import Library](https://github.com/assimp/assimp)
- [Tiny obj loader](https://github.com/syoyo/tinyobjloader)

And a huge thanks to the Vulkan Working Group, Vulkan Adivsory Panel, the fine people at LunarG and everyone from the different IHVs that helped me get the examples up and working on their hardware!

## Attributions
- Cubemap used in cubemap example by [Emil Persson(aka Humus)](http://www.humus.name/)
- Armored knight model used in deferred example by [Gabriel Piacenti](http://opengameart.org/users/piacenti)
- Voyager model by [NASA](http://nasa3d.arc.nasa.gov/models)
- Astroboy COLLADA model copyright 2008 Sony Computer Entertainment Inc.
- Bear mug model used in tessellation example by [Aare](http://opengameart.org/users/aare)
- Textures used in some examples by [Hugues Muller](www.yughues-folio.com)

## External resources
- [LunarG Vulkan SDK](https://vulkan.lunarg.com)
- [Official list of Vulkan resources](https://www.khronos.org/vulkan/resources)
- [SPIR-V specifications](https://www.khronos.org/registry/spir-v/specs/1.0/SPIRV.html)
- [My personal view on Vulkan (as a hobby developer)](http://www.saschawillems.de/?p=1886)
