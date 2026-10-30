# Native AROS GLES support (WGPU 29)

This branch adapts the same native Intuition/EGL provider as the `aros` WGPU30
branch to upstream v29.0.4, for GPUI's published gpui-pre 0.3.8 snapshots.
The ArosWindowHandle and ArosDisplayHandle dependency is pinned to the public
PomAROS raw-window-handle fork. No X11/Wayland handle or Unix shared-object
loader is substituted for the AROS platform.

EGL entry stubs link to egl.library. AROS uses the EGL1.4 native display/window
API and accepts a WINDOW_BIT configuration independently of native non-EGL
drawing interoperability. Duplicate SURFACE_TYPE attributes are combined as in
the selected upstream WGPU30 implementation before choosing a configuration.

Window owners destroy surfaces before closing Intuition windows. Build with
only the GLES backend and the managed AROS SDK plus native crate-store patches.
Compilation is distinct from native scene and application qualification.

The two maintained branches match the two consumer GPUI API versions. They
implement the same native provider contract; they are not separate OS trees.
