# TL;DR

This repo contains geckodriver binaries compiled for ARMv6. These should work for example on Raspberry Pi Zero W and similar hardware. GeckoDriver version you are going to download has to match with your selenium version and Firefox version. You should find necessary information in Selenium documentation.

## How to download
Open [Releases tab](https://github.com/d0ku/GeckoDriver_ARMv6/releases), find version that suits you, click on Assets and download attached geckodriver binary.

## Disclaimer
Sad thing is, if you own RPi Zero or anything of similar computing capacities, it's probably too slow to run firefox anyway. First try to run firefox alone and check if it's performance is enough for you. If it is, have some fun with binaries in these repo.

I have not used binaries newer than v.0.18.0 so I am not sure whether they work or not. Download and try your luck with those.

### Issues
Please DO NOT open issues which are about Selenium or Firefox. If your program does not run and it outputs some error, first try to google for answer, take a quick look at documentation and if this does not help then consider adding issue to adequate repository ([Selenium](https://github.com/SeleniumHQ/selenium), [GeckoDriver](https://github.com/mozilla/geckodriver)). Remember that you should always try to find answer for your problems first, and only if you don't find anything open a new issue.

If output of your program clearly indicates that there was a problem with this particular compiled binary, you should:

1. Redownload binary and try again
2. Give binary permission to execute (chmod +x geckodriver) and run it. If it runs, it means that binary probably is not the problem. If you get some strange error trying just to run the binary, then open a new issue.


### How the build is done
Requirements:
* [rustup](https://github.com/rust-lang/rustup)
* Mercurial

```
# Get rust toolchain in specific version for reproducibility
rustup toolchain install 1.65.0

# Install the cross-compilation helper
cargo install cross --git https://github.com/cross-rs/cross --tag v0.2.4

# Checkout the geckodriver source code and enter the directory
hg clone --rev 1 https://hg.mozilla.org/mozilla-central checkout
cd checkout

# Checkout specific hash for the version, can be found in geckodriver releasenotes, e.g. for 0.32 it's 4563dd583110
# This will take a long time, get some tea
hg pull --rev=4563dd583110
hg update

# Enter the directory and build the binary in release variant
cross build --target=arm-unknown-linux-gnueabihf --bin geckodriver --release

# The binary will be located in `checkout/target/arm-unknown-linux-gnueabihf/release/geckodriver`
```

### Inspiration:
I could not find any compiled geckodriver binaries for my RPi Zero W. That was quite frustrating so I googled a bit, found [Docker crosscompiler for Rust image by dlecan](https://github.com/dlecan/rust-crosscompiler-arm), and decided to give it a try.

In the "newer iterations" (geckodriver newer than `v0.26.0`) a great [cross](https://github.com/cross-rs/cross) tool is used to run the builds.
Builds are also done via github action.
