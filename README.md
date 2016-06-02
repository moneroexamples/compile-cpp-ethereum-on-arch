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

# clone webthree-umbrella repository 
git clone --recursive https://github.com/ethereum/webthree-umbrella.git

# enter webthree-umbrella folder after cloning its github repository
cd webthree-umbrella

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


Since Ethereum was installed in /opt/eth, executing its binaries can result in linker error due to not being able to find the Ethereum shared libraries. To rectify this issue, it is needed to add the folder containing Ethereum shared libraries into LD_LIBRARY_PATH environmental variable:


```bash
# update ~/.bashrc
echo "export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/opt/eth/lib" >> ~/.bashrc

# reload ~/.bashrc
source ~/.bashrc
```



After compilation, the Ethereum binaries, header and shared libraries should be located in `/opt/eth`:

```bash
tree -L 2 /opt/eth/
/opt/eth/
├── bin
│   ├── alethzero
│   ├── bench
│   ├── eth
│   ├── ethkey
│   ├── ethminer
│   ├── ethrpctest
│   ├── ethvm
│   ├── lllc
│   ├── mix-ide
│   ├── rlp
│   └── solc
├── include
│   ├── devcore
│   ├── devcrypto
│   ├── ethash-cl
│   ├── ethashseal
│   ├── ethcore
│   ├── ethereum
│   ├── evmasm
│   ├── evmcore
│   ├── include
│   ├── libethereum
│   ├── lll
│   ├── natspec
│   ├── p2p
│   ├── scrypt
│   ├── solidity
│   ├── testutils
│   ├── web3jsonrpc
│   ├── webthree
│   └── whisper
└── lib
   ├── libdevcore.so
   ├── libdevcrypto.so
   ├── libethash-cl.so
   ├── libethashseal.so
   ├── libethash.so
   ├── libethcore.so
   ├── libethereum.so
   ├── libevmasm.so
   ├── libevmcore.so
   ├── libevmjit.so -> libevmjit.so.0.9
   ├── libevmjit.so.0.9 -> libevmjit.so.0.9.0.2
   ├── libevmjit.so.0.9.0.2
   ├── libevm.so
   ├── liblll.so
   ├── libnatspec.so
   ├── libp2p.so
   ├── libscrypt.so
   ├── libsolidity.so
   ├── libtestutils.so
   ├── libweb3jsonrpc.so
   ├── libwebthree.so
   └── libwhisper.so
```

Full file tree is [here](http://pastebin.com/raw/sdEvi9rA).

## Compile Mist browser and Ethereum wallet

To compile and run the [Mist](https://github.com/ethereum/mist) browser and
the [Ethereum wallet](https://github.com/ethereum/meteor-dapp-wallet),
[meteor](https://www.meteor.com/) and [electron](http://electron.atom.io/) frameworks, and [mongodb](https://www.mongodb.com/) database are required. The meteor can be easily installed from AUR repositories,
while the electron using node package manager [npm](https://www.npmjs.com/). Mongodb
will be installed automatically as part of meteor's dependencies.

#### Install dependencies:

```bash
# this installs meteor along with nodejs (with npm) and mongodb
yaourt -Sy meteor-js

# install npm
sudo pacman -Sy npm

# install electron
sudo npm -g install electron-prebuilt

# to start the mongodb service manually
sudo systemctl start mongodb.service

# and/or to make it autostart at system boot
# sudo systemctl enable mongodb.service
```

#### Install and run Mist browser

```bash
git clone https://github.com/ethereum/mist.git
cd mist
git submodule update --init
npm install
```

Running the Mist browser can be tricky. The reason is that we need to run
three programs at the same time: (i) Ethereum node, (ii) meteor and (iii) electron.
The easiest thing to do is run them in three separate terminal windows.

**Terminal 1: Start the eth node**

```bash
/opt/eth/bin/eth
```
It will start synchronizing, so be patient.

**Terminal 2: Start meteor**

Meteor must be started from withing `mist/interface` folder.

```bash
# enter interface folder in the mist folder
cd mist/interface

# start meteor
meteor
```

**Terminal 3: Start electron**

Electron must be started from withing `mist` folder.

```bash
# enter mist folder
cd mist

# start electron
electron .
```

The example of the three terminals are shown below:

![mist_browser_01.png](https://raw.githubusercontent.com/moneroexamples/compile-cpp-ethereum-on-arch/master/img/mist_browser_01.png)


#### Install and run Ethereum wallet

```bash
git clone https://github.com/ethereum/meteor-dapp-wallet
cd meteor-dapp-wallet
```

## Example usage

**Start Ethereum node on the mainnet:**

```bash
/opt/bin/eth
```

**Start Ethereum node on the morden testnet:**

```bash
/opt/bin/eth --morden
```

To get some testnet ether can go to [faucet.ma.cx:3000](http://faucet.ma.cx:3000/)

**Do some CPU mining on the mainet:**

Start eth node in one terminal window with json-rpc enable (`-j`):

```bash
/opt/bin/eth -j -a your_eth_address
```

In the second terminal, start `ethminer`:

```bash
/opt/eth/bin/ethminer -C --mining-threads 2
```

## Other examples
Other examples can be found on [github](https://github.com/moneroexamples?tab=repositories).
Please know that some of the examples/repositories are not
finished and may not work as intended.

## How can you help?

Constructive criticism, code and website edits are always good. They can be made through github.

Some Monero are also welcome:
```
48daf1rG3hE1Txapcsxh6WXNe9MLNKtu7W7tKTivtSoVLHErYzvdcpea2nSTgGkz66RFP4GKVAsTV14v6G3oddBTHfxP6tU
```
