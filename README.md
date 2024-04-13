# lingeling-cmake

This is a fork of the [Lingeling](https://github.com/arminbiere/lingeling) 1.0.0 SAT
solver, with support for CMake. No original source files are changed in this fork.

See also the [original README file](README). This version of Lingeling is published
under the MIT license, see [COPYING](COPYING).


## Building `lingeling-cmake`

`lingeling-cmake` builds Lingeling both as a static and as a shared library. The
build artifacts are placed in the `target` subdirectory of your build.

The Lingeling executables are built using the static Lingeling library. If you only
need the Lingeling libraries, set the CMake option `LGL_BUILD_TOOLS` to `OFF`.


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
