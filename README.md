[![Tests](https://github.com/belluikit/gl-js/actions/workflows/tests.yml/badge.svg)](https://github.com/belluikit/gl-js/actions/workflows/tests.yml)
[![Static Analysis](https://github.com/belluikit/gl-js/actions/workflows/analysis.yml/badge.svg)](https://github.com/belluikit/gl-js/actions/workflows/analysis.yml)
[![Go Reference](https://pkg.go.dev/badge/github.com/belluikit/gl-js.svg)](https://pkg.go.dev/github.com/belluikit/gl-js)

# GL

**Fork of [fyne-io/gl-js](https://github.com/fyne-io/gl-js)**, maintained for
[Bellui](https://bellui.com) ([belluikit/bellui](https://github.com/belluikit/bellui)).
The module path is `github.com/belluikit/gl-js`.

Lineage: [golang.org/x/mobile/gl](https://pkg.go.dev/golang.org/x/mobile/gl)
→ [goxjs/gl](https://github.com/goxjs/gl)
→ [fyne-io/gl-js](https://github.com/fyne-io/gl-js)
→ belluikit/gl-js. It remains under the original BSD-style license
([LICENSE](LICENSE), The Go Authors).

Package gl is a Go cross-platform binding for OpenGL, with an OpenGL ES 2-like API.

It supports:

- **macOS**, **Linux** and **Windows** via OpenGL 2.1 backend,

- **iOS** and **Android** via OpenGL ES 2.0 backend,

- **Modern Browsers** (desktop and mobile) via WebGL 1.0 backend.

This is a fork of golang.org/x/mobile/gl package with [CL 8793](https://go-review.googlesource.com/8793)
merged in and Windows support added. This package is fully functional, but may eventually become superceded by
the new x/mobile/gl plan. It will exist and be fully supported until it can be safely replaced by a better package.

## Installation

```bash
go get github.com/belluikit/gl-js
```

## Usage

This OpenGL binding has a ContextWatcher, which implements [glfw.ContextWatcher](https://pkg.go.dev/github.com/belluikit/glfw-js#ContextWatcher)
interface. Recommended usage is with the [github.com/belluikit/glfw-js](https://github.com/belluikit/glfw-js) package, which accepts a ContextWatcher in its Init, and takes on the responsibility
of notifying it when context is made current or detached.

```go
if err := glfw.Init(gl.ContextWatcher); err != nil {
	// Handle error.
}
defer glfw.Terminate()
```

If you're not using a ContextWatcher-aware glfw library, you must call methods of gl.ContextWatcher yourself whenever
you make a context current or detached.

```Go
window.MakeContextCurrent()
gl.ContextWatcher.OnMakeCurrent(nil)

glfw.DetachCurrentContext()
gl.ContextWatcher.OnDetach()
```
