# Compile cpp-ethereum (aka webthree-umbrella) on Arch Linux

The example shows how to compile the current github version (as of 25 May 2016) of C++ version of [ethereum](http://ethereum.org/), i.e., [webthree-umbrella](https://github.com/ethereum/webthree-umbrella), on [Arch Linux](https://www.archlinux.org/).

## Dependencies
Before proceeding with the compilation, the following packages are required:

```bash
# from Arch official repositories
sudo pacman -Sy git base-devel cmake boost crypto++ leveldb llvm miniupnpc libcl opencl-headers libmicrohttpd qt5-base qt5-webengine

# from Arch User Repository (i.e. Aur) we need libjson-rpc-cpp
yaourt -Sy libjson-rpc-cpp
```

[yaourt](http://archlinux.fr/yaourt-en) installation instruction are [here](http://revryl.com/2013/07/11/yaourt-installation-arch-linux/). Off course any other [aur helper](https://wiki.archlinux.org/index.php/AUR_helpers) can be used to install dependencies from the aur.

## Compilation

```bash
# download the latest webthree-umbrella source code from github
git clone --recursive https://github.com/ethereum/webthree-umbrella.git

# go into webthree-umbrella folder, make build folder and go into it
cd webthree-umbrella && mkdir build && cd build

# build a compilation system and specify installation patch
# path can be any, but I ususaly use /opt for stuff that I compile myself
cmake .. -DCMAKE_INSTALL_PREFIX=/opt

# compile
make # -j numer_of_threads

# install into /opt
sudo make install
```

After successful compilation, the Ethereum binaries should be
located in `/opt/eth/bin`

## Other examples
Other examples can be found on  [github](https://github.com/moneroexamples?tab=repositories).
Please know that some of the examples/repositories are not
finished and may not work as intended.

## How can you help?

Constructive criticism, code and website edits are always good. They can be made through github.

Some Monero are also welcome:
```
48daf1rG3hE1Txapcsxh6WXNe9MLNKtu7W7tKTivtSoVLHErYzvdcpea2nSTgGkz66RFP4GKVAsTV14v6G3oddBTHfxP6tU
```
