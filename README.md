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
git clone --recursive https://github.com/ethereum/solidity.git

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

## Synchronize into Ropsten Revival testnet

To synchronize into [Ropsten Revival](https://github.com/ethereum/ropsten/blob/master/revival.md) testnet
network, the following command can be used. It is presented as an bash alias that can be 
added you your `.bashrc` for easier use:

```
/opt/eth/bin/eth -j --rpccorsdomain "*" --ropsten --pin -t 1 --unsafe-transactions --peerset "required:20c9ad97c081d63397d7b685a412227a40e23c8bdc6688c6f37e97cfbc22d2b4d1db1510d8f61e6a8866ad7f0e17c02b14182d37ea7c3c8b9c2683aeb6b733a1@52.169.14.227:30303 required:6ce05930c72abc632c58e2e4324f7c7ea478cec0ed4fa2528982cf34483094e9cbc9216e7aa349691242576d552a2a56aaeae426c5303ded677ce455ba1acd9d@13.84.180.240:30303" --rpccorsdomain "http://127.0.0.1:8080" -a "0xdf9f93fe406920ae5335021b3fc016de3ab7070e" 
```

`--unsafe-transactions` don't need to be used for synchrnonization. But later its easier to make test transactions using `geth` console. When using `mist` wallet, it does not matter.

`-j --rpccorsdomain "*"` are for working local copy of [browser-solidity](https://github.com/ethereum/browser-solidity).

`-a "0xdf9f93fe406920ae5335021b3fc016de3ab7070e"` is my coinbase address. You should replace it with yours when you create your first ropsten ether account.

`-t 1` sets number of mining threads 

`--rpccorsdomain "http://127.0.0.1:8080"` is for when using  [browser-solidity](https://github.com/ethereum/browser-solidity). Without this there might be CORS problems connectin to your `cpp-ethereum` node.

## Install geth

`cpp-ethereum` does not provide console interface. To interact with the `eth` node, `geth` JavaScript console can be used.

```
sudo pacman -S geth
```

To connect to eth node:

```
#in terminal 1: start eth node using eth alias created above
ethtestnet

#in terminal 2: 
geth attach
```

Once connected can execute `eth.syncing` or `eth.blockNumber` to check current synchronization status.

```
> eth.syncing
{
  currentBlock: 682915,
  highestBlock: 688999,
  startingBlock: 682603
}
> eth.blockNumber
683452
```

When fully sunced, mining can be started:

```
miner.start(1); // number in parenthesis does not matter.
```

Check mining hashrate:

```
> eth.mining
true
> eth.hashrate
56937
> 
```

Check if we mined something, i.e., check coinbase balance:

```
> web3.fromWei(eth.getBalance(eth.coinbase))
51.7183586
```

## Other examples
Other examples can be found on [github](https://github.com/moneroexamples?tab=repositories).
Please know that some of the examples/repositories are not
finished and may not work as intended.

## How can you help?

Constructive criticism, code and website edits are always good. They can be made through github.
