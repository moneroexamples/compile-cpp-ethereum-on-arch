# Compile cpp-ethereum and solidity on Arch Linux

The example shows how to compile the current github version (as of 05 April 2016) of C++ version of [ethereum](http://ethereum.org/), i.e., [cpp-ethereum](https://github.com/ethereum/cpp-ethereum), on [Arch Linux](https://www.archlinux.org/).

## Dependencies
Before proceeding with the compilation, the following packages are required:

```bash
# from Arch official repositories
sudo pacman -Sy git base-devel cmake leveldb libmicrohttpd
```

## Compilation: cpp-ethereum

```bash

# clone webthree-umbrella repository 
git clone --recursive https://github.com/ethereum/cpp-ethereum.git

# enter the folder after cloning its github repository
cd cpp-ethereum

# make a build folder and enter into it
mkdir -p build && cd build

# create build files and specify Ethereum installation folder
cmake .. -DCMAKE_INSTALL_PREFIX=/opt/eth

# compile the source code
make

# alternatively it is possible to specify number of compilation threads
# for example to use 4 threads execute make as follows:
# make -j 4

# install the resulting binaries, shared libraries and header files into /opt
sudo make install
```

## Compilation: solidity

```bash
# go to your homefolder if still in ~/cpp-ethereum/build
cd ~

# clone webthree-umbrella repository 
git clone --recursivehttps://github.com/ethereum/solidity.git

# enter the folder after cloning its github repository
cd solidity

# make a build folder and enter into it
mkdir -p build && cd build

# create build files and specify Ethereum installation folder
cmake .. -DCMAKE_INSTALL_PREFIX=/opt/eth

# compile the source code
make

# alternatively it is possible to specify number of compilation threads
# for example to use 4 threads execute make as follows:
# make -j 4

# install the resulting binaries, shared libraries and header files into /opt
sudo make install
```

After compilation and istallation of the cpp-ethereum and solidity, the `/opt/eth` should look as follows:

```bash
/opt/eth/
├── bin
│   ├── eth
│   ├── ethminer
│   ├── ethvm
│   ├── lllc
│   └── solc
└── lib
    ├── liblll.so
    ├── libsoldevcore.so
    ├── libsolevmasm.so
    └── libsolidity.so
```


## Other examples
Other examples can be found on [github](https://github.com/moneroexamples?tab=repositories).
Please know that some of the examples/repositories are not
finished and may not work as intended.

## How can you help?

Constructive criticism, code and website edits are always good. They can be made through github.
