# Template for arcdps plugin built with cmake and linux

The goal of this repository is to provide a template for an [arcdps](https://www.deltaconnected.com/arcdps/) plugin that compiles with cmake on linux.
The `arcdps_combatdemo.cpp` is the one from the [arcdps website](https://www.deltaconnected.com/arcdps/api/arcdps_combatdemo.cpp) but minor fixes were applied that g++ refused to compile with.

The appropriate version of imgui (1.80) is cloned into its subdirectory.
The resulting library statically includes all dependencies except imgui where the shared version is used.

Interestingly, the resulting `libarcdps_addon_2.so` is an `.so` instead of `.dll`.
Just change the file extension and copy it to `Guild Wars 2/bin64` to work.

## CLion

Got to `Settings > Build, Executions, Deployment > Toolchains` and add one for cross compiling. On Ubuntu 22.04 the C Compiler is `/usr/bin/x86_64-w64-mingw32-gcc` and C++ is `x86_64-w64-mingw32-g++`. CMake and Debugger is Bundled and the Build Tool is detected as ninja for me.

Under `Settings > Build, Executions, Deployment > CMake` Add a profile and use the created cross compile toolchain from the previous step.

To be able to build it seems that a run configuration is needed. As target select "arcdps_addon_2". The build button (green hammer) should now be green and able to be pressed.

Using it should call cmake which should run through without errors (hopefully) and state `[8/8] Linking CXX shared library libarcdps_addon_2.so` at the end.
This is the .dll we want and can give to arcdps after changing the extension.

## Arcdps not loading

The provided `d3dcompiler_43.dll` from wine is not really expected so it does not work.
You need to get a redist from somewhere else.
One way is through winetricks, but it is also possible to extract it from the Github or Firefox installer.
Just put it alongside the arcdps dll.

## Legal

I did nothing interesting. [ImGui belongs to the ImGui authors](https://github.com/ocornut/imgui).
[Arcdps belongs to the arcdps authors](https://www.deltaconnected.com/arcdps/). Guild Wars 2 to NCsoft.

Essentially, this repo is just a cmake list that ties everything together.
Also, it shows how to work with it on Ubuntu.
