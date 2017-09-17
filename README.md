# GeckoDriver_ARMv6
Compiled binaries of Gecko Driver for ARMv6 architecture (cross-compiled)

Current compilation version: Release v.0.19.0

I could not find any compiled geckodriver binaries for ARMv6 (for example my Raspberry Pi Zero W, first series of Raspberry Pi etc.). They might come in handy, if someone ever needs them.

I had luck in cross-compiling release 0.19.0 for ARMv6 architecture. 

I've used Docker image from https://github.com/dlecan/rust-crosscompiler-arm . 

Feel free to use compiled binaries, I don't guarantee that they are completely working, but they should be functional at the moment.

In the near future I will probably compile all releases of geckodriver, maybe someone will make use of them.

To access specified version just change the branch.

Already compiled:

- Release v.0.19.0
