# BasisUniversalUnity

Demo project, integrating [Binomial LLC](http://www.binomial.info)'s [Basis Universal transcoder](https://github.com/BinomialLLC/basis_universal) into a Unity game engine project.

Special thanks to Binomial and everyone involved in making Basis Universal available!

## Building the native library

Check out this repository and make sure the sub-module `basis_universal` is also cloned.

### Prerequisites

You'll need [CMake](https://cmake.org)

All build platform variants will have an `install` build target, that does the following:

This does the following:
- The final library will be installed to the correct place within `BasisUniversalUnity/BasisUniversalUnity/Assets/Plugins`.
- The source code for the transcoder + wrapper is copied to `BasisUniversalUnity/BasisUniversalUnity/Assets/Plugins/WebGL`. This way it gets compiled and included when you build the Unity project for WebGL.
- Two sample basis files get copied to the StreamingAssets folder.

### macOS

Install Xcode and its command line tools.

#### Build (for macOS Unity Editor and standalone builds)

Open up a terminal and navigate into the repository.

```
cd /path/to/BasisUniversalUnity
```

Create a subfolder `build`, enter it and call CMake like this:

```
mkdir build
cd build
cmake .. -G Xcode
```

This will generate an Xcode project called `open basisu_transcoder.xcodeproj`.

Open it and build it (target `ALL_BUILD` or `basisu`).

After this was successful, build the target `install`.

### Android

You'll need the Android NDK

Create a subfolder `build_android_arm64`, enter it and call CMake like this:

```
mkdir build_android_arm64
cd build_android_arm64
cmake .. \
-DANDROID_ABI=arm64-v8a \
-DCMAKE_BUILD_TYPE=RelWithDebInfo \
-DANDROID_NDK=/path/to/your/android/sdk/ndk-bundle \
-DCMAKE_TOOLCHAIN_FILE=/path/to/your/android/sdk/ndk-bundle/build/cmake/android.toolchain.cmake \
-DANDROID_STL=c++_static
```

Replace `/path/to/your/android/sdk/ndk-bundle` with the actual path to your Android NDK install.

To build and install
```
make && make install
```

### Other platforms (Linux,Windows,iOS)

Not tested at the moment. Probably needs some minor tweaks to run.

## Running the Unity project

This can only work if you've build the native library before.

In the project view, navigate to the file `BasisUniversalUnity/BasisUniversalUnity/Assets/Plugins/x86_64/basisu`, select it and make sure the option *Load on startup* is checked.

Other than that, open the `SampleScene` and click play. Two basis textures on planes should appear in front of you.

## Building Unity project

Just build like a regular project.

Note: Only WebGL and Android is tested at the moment.

## Support

Like this demo? You can show your appreciation and ...

[![Buy me a coffee](https://az743702.vo.msecnd.net/cdn/kofi1.png?v=0)](https://ko-fi.com/C0C3BW7G)

## TODO

### Platform support
- Provide fallback to bitmap format if none of the GPU formats are supported (iOS Safari for example)
- Provide fallback to separate alpha-channel texture if no alpha channel format is supported.
- iOS support

### General
- Remove memory leaks
- Create proper C# API
- Create DownloadHandler that provides a Texture2D
- Make a package (library)

### Basis Universal library
- Build for iOS
- Build for Android
- Watch out for useful changes in in Basis Universal project
  + public C bindings/interface
  + Separate encoder/transcoder libs
  + Multi platform support
