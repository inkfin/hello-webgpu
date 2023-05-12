# "Hello, Triangle" WebGPU and Dawn

[![MSVC workflow](/../../actions/workflows/msbuild.yml/badge.svg)](/../../actions/workflows/msbuild.yml) [![Xcode workflow](/../../actions/workflows/xcode.yml/badge.svg)](/../../actions/workflows/xcode.yml) [![Emscripten workflow](/../../actions/workflows/emscripten.yml/badge.svg)](/../../actions/workflows/emscripten.yml)

Starter project for C++ [WebGPU](//gpuweb.github.io/gpuweb/)/[Emscripten](//emscripten.org) and [Dawn](//dawn.googlesource.com/dawn). Build for Windows using Visual Studio from 2015 onwards. Build for Emscripten using CMake (or on Windows using `build-web.bat`). Build for Mac using the Xcode project (tested with Xcode 11 onwards, and macOS 10.14 onwards).

![Chrome and native side-by-side](screenshot.png)

The included `libdawn` is pre-built for Windows/MSVC and Mac; [see instructions](lib/README.md) if you wish to build it yourself for Windows (out of the box Dawn on Windows builds with [Depot Tools](//commondatastorage.googleapis.com/chrome-infra-docs/flat/depot_tools/docs/html/depot_tools.html)/Clang so MSVC's linker fails with the exposed `std` types).

As of May 2023 the API should be stable enough, with Chrome being the first browser to enable WebGPU by default. The code is [tested and working](//wip.numfum.com/cw/2023-05-12/index.html) with Chrome 113 (other browsers may need flags to enable) and Emscripten 3.1.38.

Emscripten build instructions:
```
clone https://github.com/cwoffenden/hello-webgpu.git
cd hello-webgpu
mkdir out
emcmake cmake -B out -DCMAKE_BUILD_TYPE=Release
cmake --build out
```
Then serve this locally, otherwise CORS will probably stop the `file://` URL loading the Wasm:
```
python3 -m http.server --directory out
```
Recalling to have enabled WebGPU in the browser and launched Chrome with the WebGPU flag, e.g. for Mac:
```
/Applications/Google\ Chrome.app/Contents/MacOS/Google\ Chrome --enable-unsafe-webgpu
```

Dawn is Apache 2.0 licensed (see [LICENSE](lib/dawn/LICENSE)). The example code is released under a [Creative Commons Zero license](//creativecommons.org/publicdomain/zero/1.0/) (or Public Domain, whichever is applicable in your jurisdiction).
