# AssimpNet for Unity

### Current project status ###
[![Build Status](https://intelligide.visualstudio.com/Assimp%20for%20Unity/_apis/build/status/intelligide.assimpnet-unity?branchName=master)](https://intelligide.visualstudio.com/Assimp%20for%20Unity/_build/latest?definitionId=1&branchName=master)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/ac1e60e80292426abf975b7172266eed)](https://www.codacy.com/app/intelligide/assimpnet-unity?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=intelligide/assimpnet-unity&amp;utm_campaign=Badge_Grade)
[![Total alerts](https://img.shields.io/lgtm/alerts/g/intelligide/assimpnet-unity.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/intelligide/assimpnet-unity/alerts/)

## Introduction ##

This is a fork of [**AssimpNet**](https://bitbucket.org/Starnick/assimpnet), the cross-platform .NET wrapper for the Open Asset Import Library (otherwise known as [Assimp](https://github.com/assimp/assimp)), which is a 3D model import-export library. 

The primary motivation for this fork is to provide Assimp API for Unity users. The official AssimpNet is compatible with standalone Unity players but not for others platforms such as mobile or web.

Please see the Assimp website for a full list of supported formats and features. Each version of the managed wrapper tries to maintain parity with the features of the native version.

P/Invoke is used to communicate with the C-API of the native library. The managed assembly is compiled as **AnyCpu** and the native binaries are loaded dynamically for either 32 or 64 bit applications.

The library is split between two parts, a low level and a high level. The intent is to give as much freedom as possible to the developer to work with the native library from managed code.

### Low level ###

* Native methods are exposed via the AssimpLibrary singleton.
* Structures corresponding to unmanaged structures are prefixed with the name **Ai** and generally contain IntPtrs to the unmanaged data.
* Located in the *Assimp.Unmanaged* namespace.

### High level ###

* Replicates the native library's C++ API, but in a way that is more familiar to C# developers.
* Marshaling to and from managed memory handled automatically, all you need to worry about is processing your data.
* Located in the *Assimp* namespace.

## Supported Frameworks ##

The library runs on both **.NET Core** and **.NET Framework**, targeting specifically:

* **.NET Standard 2.0**
* **.NET Framework 4.0**
* **.NET Framework 3.5**

When targeting .NET Framework, the package uses a MSBuild targets file to copy native binaries to your application output folder. For .NET Core applications, the native binaries are resolved by the *deps.json* dependency graph automatically.

The library can be compiled on any platform that supports  the DotNet CLI build tools or Visual Studio 2017/2019. There is a single **build-time only** dependency, an IL Patcher also distributed as a cross-platform NuGet package. The patcher requires .NET Core 2.0+ or .NET Framework 4.7+ to be installed on your machine to build.

## Supported Platforms ##

* **Windows** 
	* x86, x64 (Tested on Windows 10)
* **Linux**
	* x64 (Tested on Ubuntu 18.04 Bionic Beaver)
* **MacOS**
	* x64 (Tested on MacOS 10.13 High Sierra)
* **Android**

## Installation

- Build the project (with msbuild, Visual Studio or another tool).
- Copy `AssimpNet.dll` from build folder to `Plugins` folder (in your unity project)

- Build [Assimp](https://github.com/assimp/assimp) native binaries for the platforms you want and place them in the `Plugins` folder. The native binaries must respect naming rules for being loaded:
    - Windows: `libassimp.dylib`
    - Mac OS: `assimp.dll`
    - Linux & Android: `libassimp.so`

  We use `assimp` as library name for DllImport. See [Unity Native plug-ins docs](https://docs.unity3d.com/Manual/NativePlugins.html) and [Mono Interop with native libraries](https://www.mono-project.com/docs/advanced/pinvoke/#library-names) for further information.

## Licensing ##

The library is licensed under the [MIT](https://opensource.org/licenses/MIT) license. This means you're free to modify the source and use the library in whatever way you want, as long as you attribute the original authors. The native library is licensed under the [3-Clause BSD](https://opensource.org/licenses/BSD-3-Clause) license. Please be kind enough to include the licensing text file (it contains both licenses).
