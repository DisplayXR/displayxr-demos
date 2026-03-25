# Spatial OS — Collaboration War Room

Multi-layer composition demo for DisplayXR showing a 3D scene with floating 2D UI panels.

## Features

- Stereo 3D cube rendered via `XrCompositionLayerProjection`
- Four 2D panels (Participants, Chat, Agenda, Actions) via `XrCompositionLayerWindowSpaceEXT`
- Panels positioned in fractional window coordinates — auto-scale on resize
- Per-panel disparity control (promote 2D panels to 3D depth)
- Focus mode: enlarge selected panel
- DirectWrite text rendering for panel content

## Architecture

```
windows/
├── main.cpp           Win32 window + OpenXR render loop
├── spatial_app.*      Multi-layer composition logic (4 panels + 3D scene)
├── panel.*            Panel data structure (position, size, content)
├── panel_render.*     D2D1/DirectWrite text rendering for panels
└── xr_session.*       OpenXR session management with XR_EXT_win32_window_binding
```

## Window-Space Layers

This demo showcases `XrCompositionLayerWindowSpaceEXT` — a DisplayXR extension that positions composition layers in fractional window coordinates. Each panel is submitted as a separate layer with its own swapchain, allowing the runtime to composite them with correct stereo disparity.

See the [window binding spec](https://github.com/DisplayXR/displayxr-runtime/blob/main/docs/specs/XR_EXT_win32_window_binding.md) for full details.
