# Native AROS GLES support

This branch starts at upstream WGPU 3b3506ea31154edc04de64debda0e780cba2639c
(version 30.0.0) and provides an explicit Intuition window path for GLES.
It uses ArosWindowHandle/ArosDisplayHandle from the sibling
raw-window-handle-aros fork, based on raw-window-handle 0.6.2.

AROS EGL entry points link through libEGL.a to egl.library. No Unix shared
object loader or Wayland service is required. The native window is an actual
Intuition struct Window pointer; its owner must keep it alive until all WGPU
surfaces referring to it have been destroyed. The default EGL display and
buffered native window surface are selected explicitly.

Build with an installed AROS Rust SDK, its cargo-config.toml and the application's
native crate-store patches; enable only the gles backend. Host checks can use
`cargo +stable check -p wgpu-hal --no-default-features --features gles`.
The native HAL compile check is not GPU runtime acceptance. GPUI renderer,
shader capabilities, window resize and surface/window destruction must also
be exercised before claiming application acceleration.

Only the GLES backend has AROS platform support. Other backend features do not
acquire AROS support merely because this fork builds.
