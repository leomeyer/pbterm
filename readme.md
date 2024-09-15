# pbterm - Terminal emulator for PocketBook
## Fork for newer devices (SDK 6.8)

Please see the [original README file](https://github.com/leomeyer/pbterm?tab=readme-ov-file#readme) for instructions on installation and usage.

### Tested devices

- Verse Pro Color (PB634; firmware version U634k3.6.8.3806)

### Precompiled binaries

Downloads are available on the [Releases page](https://github.com/leomeyer/pbterm/releases).

### Building and installation instructions

These instructions have been tested on Ubuntu 22.04 LTS (Linux Mint 22).

Building this app requires basic build tools and a current [Pocketbook SDK from https://github.com/pocketbook/SDK_6.3.0](https://github.com/pocketbook/SDK_6.3.0).

The current SDK (6.8 at the time of writing) contains separate toolchains for different CPUs. It supports building for:

- Allwinner B288 (dual-core SoC used in older devices)
- Allwinner B300 (quad-core SoC with more power, apparently used in the Color models)

Please use the CPU version that applies to your target device by adjusting the `TOOLCHAIN_PATH` variable in `CMakeLists.txt`, e. g.

`SET (TOOLCHAIN_PATH "../SDK/SDK_6.3.0/SDK-B300")`

After that, execute

`> cmake .`

and then

`> make`

Copy the file `pbterm.app` in the `bin` folder to the `application` directory of your device (e. g. via USB cable).

The program will appear as `@pbterm` in the lower section of the *Apps* page.

### Known bugs

- Scrolling only works partially on Verse Pro Color. A part of the screen buffer wraps around and appears on top, overwriting previous output.
- Missing interpretation of terminal control sequences such as emitted by `clear`.

### Discussion

[mobileread forum thread](https://www.mobileread.com/forums/showthread.php?t=221543)
