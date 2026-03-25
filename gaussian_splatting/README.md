# 3D Gaussian Splatting Viewer

Real-time 3D Gaussian Splatting renderer with head-tracked stereoscopic 3D for light field displays.

## Features

- GPU-accelerated 3D Gaussian Splatting via Vulkan compute shaders (8-stage pipeline)
- Loads `.ply` (point cloud) and `.spz` (Niantic compressed) scene formats
- Kooima asymmetric frustum projection for physically-correct stereo
- Multi-view rendering for N-view light field displays
- Eye-tracked head position via DisplayXR runtime
- Sample scene included: `scenes/KAWS_FAMILY.spz`

## Architecture

```
3dgs_common/          Shared Vulkan compute renderer (gs_renderer)
├── shaders/          8 GLSL compute shaders (preprocess, sort, render, etc.)
├── gs_renderer.*     GsRenderer class — renderEye() for each view
├── gs_scene_loader.* PLY and SPZ format loaders
└── gs_spz_loader.*   Niantic SPZ binary format parser

macos/main.mm         macOS app (Cocoa + MoltenVK + XR_EXT_cocoa_window_binding)
windows/main.cpp      Windows app (Win32 + Vulkan + XR_EXT_win32_window_binding)
```

## Dependencies

- Vulkan SDK (with `glslangValidator` for shader compilation)
- OpenXR loader (from DisplayXR runtime or Khronos SDK)
- zlib + Niantic SPZ (fetched automatically via CMake FetchContent)
