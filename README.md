# lingeling-cmake

This is a fork of the [Lingeling](https://github.com/arminbiere/lingeling) 1.0.0 SAT
solver, with a CMake-based build and experimental support for building Lingeling on
Windows with MinGW32. No original source files are changed in this fork.

See also the [original README file](README). This version of Lingeling is published
under the MIT license, see [COPYING](COPYING).


## Building `lingeling-cmake`

`lingeling-cmake` builds Lingeling both as a static and as a shared library. The
build artifacts are placed in the `target` subdirectory of your build.

The Lingeling executables are built using the static Lingeling library. If you only
need the Lingeling libraries, set the CMake option `LGL_BUILD_TOOLS` to `OFF`.

When building with MinGW32, pass `-DLGL_BUILD_FAKE_POSIX=ON` to CMake. This option
currently provides a very simple implementation of the POSIX `getrusage()` function,
as far as it is used by the Lingeling library. This option disables building the
Lingeling executables, since they use further POSIX functions which cannot be faked
easily. To help static linking into clients that might define `getrusage()`
otherwise (other libraries might do similar tricks, for example), a custom function
symbol is used for the fake implementation.


## Integrating `lingeling-cmake`

If the `lingeling-cmake` sources are included in your source tree (for example as a
git submodule), you can simply create the targets by adding it via `add_subdirectory()`.

Otherwise, a `lingeling-cmake` installation can be used as a CMake package in the
usual fashion:
- When setting up the `lingeling-cmake` build, pass an installation directory to
  CMake via `CMAKE_INSTALL_PREFIX`
- Build the `install` target
- Add the installation directory to your client's `CMAKE_PREFIX_PATH`
- In your client CMake code, add `find_package(Lingeling)`
