<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/DisplayXR/displayxr-runtime/main/doc/displayxr_white.png" width="120">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/DisplayXR/displayxr-runtime/main/doc/displayxr.png" width="120">
  <img alt="DisplayXR" src="https://raw.githubusercontent.com/DisplayXR/displayxr-runtime/main/doc/displayxr.png" width="120">
</picture>

# DisplayXR Demos

Demo applications showcasing [DisplayXR](https://github.com/DisplayXR/displayxr-runtime) — an open-source OpenXR runtime for glasses-free 3D displays.

## Demos

### 3D Gaussian Splatting Viewer (Vulkan)

Real-time 3D Gaussian Splatting renderer with head-tracked stereoscopic 3D. Load `.ply` or `.spz` scenes and view them in full 3D on a light field display.

- **Platforms:** Windows, macOS
- **Graphics API:** Vulkan (MoltenVK on macOS)
- **Includes:** A sample scene (`KAWS_FAMILY.spz`) so it works out of the box

**Controls:**
| Key | Action |
|-----|--------|
| WASD / QE | Fly camera |
| Mouse drag | Look around |
| Scroll | Zoom |
| L / Load button | Open file dialog to load `.ply` / `.spz` scene |
| V | Cycle rendering mode (2D, stereo, multiview) |
| 0-3 | Select rendering mode directly |
| Tab | Toggle HUD overlay |
| Space | Reset camera |
| F11 | Fullscreen |
| ESC | Quit |

### Spatial OS — Collaboration War Room (D3D11)

Multi-layer composition demo showing a 3D cube surrounded by floating 2D panels (participants, chat, agenda, action items). Demonstrates `XrCompositionLayerWindowSpaceEXT` for depth-aware UI.

- **Platform:** Windows only
- **Graphics API:** D3D11

**Controls:**
| Key | Action |
|-----|--------|
| WASD / QE | Fly camera (3D scene) |
| Mouse | Look around |
| Tab | Cycle selected panel |
| Space | Focus mode (enlarge selected panel) |
| 3 | Toggle panel disparity (promote to 3D depth) |
| V | Cycle rendering mode |
| F11 | Fullscreen |
| ESC | Reset layout |

## Prerequisites

1. **DisplayXR runtime** installed — [download](https://github.com/DisplayXR/displayxr-runtime/releases) or [build from source](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/getting-started/building.md)
2. **Vulkan SDK** — [download](https://vulkan.lunarg.com/sdk/home) (required for Gaussian Splatting demos)
3. **CMake** (3.16+) and **Ninja** build system

## Build Instructions

### macOS — Gaussian Splatting

```bash
brew install cmake ninja vulkan-sdk

cd gaussian_splatting/macos
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

Run:
```bash
XR_RUNTIME_JSON=/path/to/openxr_displayxr.json \
DYLD_LIBRARY_PATH=/path/to/DisplayXR-macOS/lib \
VK_ICD_FILENAMES=/opt/homebrew/etc/vulkan/icd.d/MoltenVK_icd.json \
SIM_DISPLAY_ENABLE=1 SIM_DISPLAY_OUTPUT=anaglyph \
./build/gaussian_splatting_handle_vk_macos
```

### Windows — Gaussian Splatting

```bash
cd gaussian_splatting\windows
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

### Windows — Spatial OS

```bash
cd spatial_os\windows
cmake -B build -G Ninja -DCMAKE_BUILD_TYPE=Release
cmake --build build
```

### Running (Windows)

Set the runtime JSON path and run:
```bash
set XR_RUNTIME_JSON=C:\Program Files\DisplayXR\Runtime\DisplayXR_win64.json
gaussian_splatting\windows\build\gaussian_splatting_handle_vk_win.exe
```

Or if using the simulation driver:
```bash
set SIM_DISPLAY_ENABLE=1
set SIM_DISPLAY_OUTPUT=anaglyph
```

## Pre-Built Binaries

Check [Releases](https://github.com/DisplayXR/displayxr-demos/releases) for pre-built executables.

## Documentation

- [DisplayXR Getting Started](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/getting-started/overview.md) — what is DisplayXR
- [Building Your First App](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/getting-started/first-handle-app.md) — tutorial
- [Extension Specs](https://github.com/DisplayXR/displayxr-runtime/tree/main/docs/specs) — XR_EXT_display_info, window bindings
- [Extension Headers](https://github.com/DisplayXR/displayxr-extensions) — standalone headers for SDK integration

## Auto-Synced

Demo source code is auto-synced from the [displayxr-runtime](https://github.com/DisplayXR/displayxr-runtime) repository on tagged releases. To contribute, open a PR on the runtime repo under `demos/`.

## License

[ISC License](LICENSE) — same as the DisplayXR runtime.
