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

After successful compilation, the Ethereum binaries, header and shared libraries should be
located in `/opt/eth`:

```bash
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
│   │   ├── Assertions.h
│   │   ├── Base58.h
│   │   ├── Base64.h
│   │   ├── CommonData.h
│   │   ├── Common.h
│   │   ├── CommonIO.h
│   │   ├── CommonJS.h
│   │   ├── concurrent_queue.h
│   │   ├── db.h
│   │   ├── debugbreak.h
│   │   ├── Diff.h
│   │   ├── Exceptions.h
│   │   ├── FileSystem.h
│   │   ├── FixedHash.h
│   │   ├── Guards.h
│   │   ├── Hash.h
│   │   ├── Log.h
│   │   ├── MemoryDB.h
│   │   ├── OverlayDB.h
│   │   ├── picosha2.h
│   │   ├── RangeMask.h
│   │   ├── RLP.h
│   │   ├── SHA3.h
│   │   ├── Terminal.h
│   │   ├── TransientDirectory.h
│   │   ├── TrieCommon.h
│   │   ├── TrieDB.h
│   │   ├── TrieHash.h
│   │   ├── UndefMacros.h
│   │   ├── vector_ref.h
│   │   └── Worker.h
│   ├── devcrypto
│   │   ├── AES.h
│   │   ├── Common.h
│   │   ├── CryptoPP.h
│   │   ├── ECDHE.h
│   │   ├── Exceptions.h
│   │   ├── SecretStore.h
│   │   └── WordList.h
│   ├── ethash-cl
│   │   ├── ethash_cl_miner.h
│   │   └── ethash_cl_miner_kernel.h
│   ├── ethashseal
│   │   ├── EthashAux.h
│   │   ├── EthashClient.h
│   │   ├── EthashCPUMiner.h
│   │   ├── EthashGPUMiner.h
│   │   ├── Ethash.h
│   │   ├── EthashProofOfWork.h
│   │   └── GenesisInfo.h
│   ├── ethcore
│   │   ├── ABI.h
│   │   ├── BasicAuthority.h
│   │   ├── BlockHeader.h
│   │   ├── ChainOperationParams.h
│   │   ├── Common.h
│   │   ├── CommonJS.h
│   │   ├── Exceptions.h
│   │   ├── ICAP.h
│   │   ├── KeyManager.h
│   │   ├── Precompiled.h
│   │   ├── SealEngine.h
│   │   └── Transaction.h
│   ├── ethereum
│   │   ├── AccountDiff.h
│   │   ├── Account.h
│   │   ├── All.h
│   │   ├── BasicGasPricer.h
│   │   ├── BlockChain.h
│   │   ├── BlockChainSync.h
│   │   ├── BlockDetails.h
│   │   ├── Block.h
│   │   ├── BlockQueue.h
│   │   ├── CachedAddressState.h
│   │   ├── ChainParams.h
│   │   ├── ClientBase.h
│   │   ├── Client.h
│   │   ├── CommonNet.h
│   │   ├── Defaults.h
│   │   ├── EthereumHost.h
│   │   ├── EthereumPeer.h
│   │   ├── Executive.h
│   │   ├── ExtVM.h
│   │   ├── GasPricer.h
│   │   ├── GenericFarm.h
│   │   ├── GenericMiner.h
│   │   ├── GenesisInfo.h
│   │   ├── Interface.h
│   │   ├── LogFilter.h
│   │   ├── MiningClient.h
│   │   ├── State.h
│   │   ├── Transaction.h
│   │   ├── TransactionQueue.h
│   │   ├── TransactionReceipt.h
│   │   ├── Utility.h
│   │   └── VerifiedBlock.h
│   ├── evmasm
│   │   ├── Assembly.h
│   │   ├── AssemblyItem.h
│   │   ├── BlockDeduplicator.h
│   │   ├── CommonSubexpressionEliminator.h
│   │   ├── ConstantOptimiser.h
│   │   ├── ControlFlowGraph.h
│   │   ├── Exceptions.h
│   │   ├── ExpressionClasses.h
│   │   ├── GasMeter.h
│   │   ├── Instruction.h
│   │   ├── KnownState.h
│   │   ├── LinkerObject.h
│   │   ├── PathGasMeter.h
│   │   ├── SemanticInformation.h
│   │   └── SourceLocation.h
│   ├── evmcore
│   │   ├── EVMSchedule.h
│   │   ├── Exceptions.h
│   │   └── Instruction.h
│   ├── include
│   │   └── evmjit
│   │       ├── JIT-c.h
│   │       └── JIT.h
│   ├── libethereum
│   │   └── libevm
│   │       ├── All.h
│   │       ├── ExtVMFace.h
│   │       ├── JitUtils.h
│   │       ├── JitVM.h
│   │       ├── SmartVM.h
│   │       ├── VMFace.h
│   │       ├── VMFactory.h
│   │       └── VM.h
│   ├── lll
│   │   ├── All.h
│   │   ├── CodeFragment.h
│   │   ├── Compiler.h
│   │   ├── CompilerState.h
│   │   ├── Exceptions.h
│   │   └── Parser.h
│   ├── natspec
│   │   └── NatspecExpressionEvaluator.h
│   ├── p2p
│   │   ├── All.h
│   │   ├── Capability.h
│   │   ├── Common.h
│   │   ├── HostCapability.h
│   │   ├── Host.h
│   │   ├── Network.h
│   │   ├── NodeTable.h
│   │   ├── Peer.h
│   │   ├── RLPXFrameCoder.h
│   │   ├── RLPXFrameReader.h
│   │   ├── RLPXFrameWriter.h
│   │   ├── RLPxHandshake.h
│   │   ├── RLPXPacket.h
│   │   ├── RLPXSocket.h
│   │   ├── RLPXSocketIO.h
│   │   ├── Session.h
│   │   ├── UDP.h
│   │   └── UPnP.h
│   ├── scrypt
│   │   ├── b64.h
│   │   ├── crypto_scrypt-hexconvert.h
│   │   ├── libscrypt.h
│   │   ├── sha256.h
│   │   ├── slowequals.h
│   │   └── sysendian.h
│   ├── solidity
│   │   ├── ArrayUtils.h
│   │   ├── AsmCodeGen.h
│   │   ├── AsmData.h
│   │   ├── AsmParser.h
│   │   ├── AsmStack.h
│   │   ├── AST_accept.h
│   │   ├── ASTAnnotations.h
│   │   ├── ASTForward.h
│   │   ├── AST.h
│   │   ├── ASTJsonConverter.h
│   │   ├── ASTPrinter.h
│   │   ├── ASTUtils.h
│   │   ├── ASTVisitor.h
│   │   ├── CompilerContext.h
│   │   ├── Compiler.h
│   │   ├── CompilerStack.h
│   │   ├── CompilerUtils.h
│   │   ├── ConstantEvaluator.h
│   │   ├── ContractCompiler.h
│   │   ├── DeclarationContainer.h
│   │   ├── DocStringAnalyser.h
│   │   ├── DocStringParser.h
│   │   ├── Exceptions.h
│   │   ├── ExpressionCompiler.h
│   │   ├── GasEstimator.h
│   │   ├── GlobalContext.h
│   │   ├── InterfaceHandler.h
│   │   ├── LValue.h
│   │   ├── NameAndTypeResolver.h
│   │   ├── ParserBase.h
│   │   ├── Parser.h
│   │   ├── ReferencesResolver.h
│   │   ├── Scanner.h
│   │   ├── SourceReferenceFormatter.h
│   │   ├── SyntaxChecker.h
│   │   ├── Token.h
│   │   ├── TypeChecker.h
│   │   ├── Types.h
│   │   ├── Utils.h
│   │   ├── Version.h
│   │   └── Why3Translator.h
│   ├── testutils
│   │   ├── BlockChainLoader.h
│   │   ├── Common.h
│   │   ├── FixedClient.h
│   │   └── StateLoader.h
│   ├── web3jsonrpc
│   │   ├── AccountHolder.h
│   │   ├── AdminEthFace.h
│   │   ├── AdminEth.h
│   │   ├── AdminNetFace.h
│   │   ├── AdminNet.h
│   │   ├── AdminUtilsFace.h
│   │   ├── AdminUtils.h
│   │   ├── BzzFace.h
│   │   ├── Bzz.h
│   │   ├── DBFace.h
│   │   ├── DebugFace.h
│   │   ├── Debug.h
│   │   ├── EthFace.h
│   │   ├── Eth.h
│   │   ├── IpcServerBase.h
│   │   ├── IpcServer.h
│   │   ├── JsonHelper.h
│   │   ├── LevelDB.h
│   │   ├── MemoryDB.h
│   │   ├── ModularServer.h
│   │   ├── NetFace.h
│   │   ├── Net.h
│   │   ├── PersonalFace.h
│   │   ├── Personal.h
│   │   ├── SafeHttpServer.h
│   │   ├── SessionManager.h
│   │   ├── UnixSocketServer.h
│   │   ├── Web3Face.h
│   │   ├── Web3.h
│   │   ├── WhisperFace.h
│   │   ├── Whisper.h
│   │   └── WinPipeServer.h
│   ├── webthree
│   │   ├── IPFS.h
│   │   ├── Support.h
│   │   ├── Swarm.h
│   │   ├── SystemManager.h
│   │   └── WebThree.h
│   └── whisper
│       ├── BloomFilter.h
│       ├── Common.h
│       ├── Interface.h
│       ├── Message.h
│       ├── WhisperDB.h
│       ├── WhisperHost.h
│       └── WhisperPeer.h
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

## Example usage

- Start Ethereum node on the mainnet:

```bash
/opt/bin/eth
```

- Start Ethereum node on the morden testnet:

```bash
/opt/bin/eth --morden
```


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
