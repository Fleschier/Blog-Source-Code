---
layout:     post
title:      "以太坊(ethereum)开发"
date:       2018-05-23 05:59:00
categories: Computer
tags:   ๑BlockChain
description: "学习记录"
---

> 不适合人类阅读的学习笔记

- **[以太坊社区](https://ethfans.org/)**

## 安装Truffle
---
### Node.js安装

- 先要进行node.js环境的安装，见上一篇博客。

### 命令行安装truffle

- 执行命令 ` npm install -g truffle`

## 创建工程
---

-  执行命令 `truffle init`

- truffle init会默认创建一个构建在以太坊内的代币demo应用。我们可以使用这个工程来进行快速的学习。

- `init` 之后目录下就会有若干文件和文件夹。结构如下：
![](images/block_chain/structure.png)

- contracts目录中包含Solidity合约代码，其中Migrations.sol是必须有的，其他就是你自己写的合约代码了。

- migrations目录中包含合约部署脚本，其中1_initial_migration.js就是用来部署Migrations.sol的，其他的脚本会按照顺序依次执行。

- test目录保存用来测试应用和合约的测试文件

- truffle.js - Truffle的配置文件

- 官方文档(命令行指令，前面要加truffle)：

```
Commands:
  init      //Initialize new and empty Ethereum project
  compile   //Compile contract source files
  migrate   //Run migrations to deploy contracts
  deploy    //(alias for migrate)
  build     //Execute build pipeline (if configuration present)
  test      //Run JavaScript and Solidity tests
  debug     //Interactively debug any transaction on the blockchain (experimental)
  opcode    //Print the compiled opcodes for a given contract
  console   //Run a console with contract abstractions and commands available
  develop   //Open a console with a local development blockchain
  create    //Helper to create new contracts, migrations and tests
  install   //Install a package from the Ethereum Package Registry
  publish   //Publish a package to the Ethereum Package Registry
  networks  //Show addresses for deployed contracts on each network
  watch     //Watch filesystem for changes and rebuild the project automatically
  serve     //Serve the build directory on localhost and watch for changes
  exec      //Execute a JS module within this Truffle environment
  unbox     //Download a Truffle Box, a pre-built Truffle project
  version   //Show version number and exit
```
终端输入`truffle`即可查看上述命令

## 安装以太坊客户端
---

- 这里我们选择了Ganache——[github项目](https://github.com/trufflesuite/ganache-cli)

- [图形版本下载地址](https://github.com/trufflesuite/ganache/releases)(linux下载 XX.AppImage文件格式的)

- 命令行版本（ganache-cli）下载 `npm install -g ganache-cli`

- Ganache的前身是testRPC

## 编译和部署合约
---

- Ganache默认运行在7545端口，可以在界面右上方的“设置”里进行更改。运行后默认创建10个账号，每个账号里有100ETH的余额。
要部署到链上，需要把IP、端口、网络ID告诉truffle。

- 若要修改，则修改truffle.js：
```
module.exports = {  
    networks: {  
        development: {  
            host: 'localhost',  
            port: '7545',  
            network_id: '*' // Match any network id  
        }  
    }  
};  
```

### 编译合约

#### 合约位置

- 所有你的合约应该位于`./contracts`目录。默认我们提供了一个合约文件，一个库文件，均以.sol结尾作为示例。尽管库文件有一定的特殊性，但为简单起见，当前均称之为合约。

- `truffle cmpile` 仅默认编译自上次编译后被修改过的文件，来减少不必要的编译。如果你想编译全部文件，可以使用--compile-all选项。

#### 约定

- Truffle需要定义的合约名称和文件名准确匹配。例如，如果文件名为 `MyContract.sol`，那么合约文件须为如下两者之一(并且匹配 **区分大小写**)：
```
contract MyContract {
  ...
}
// or
library MyContract {
  ...
}
```

- 编译目录:编译的输出位于`./build/contracts` 目录。如果目录不存在会自动创建。这些编译文件对于Truffle框架能否正常工作至关重要。你不应该在正常的编译或发布以外手动修改这些文件。

### 移植

- 命令 `truffle migrate`

- 这个命令会执行所有的位于 `migrations` 目录内的移植脚本。如果你之前的移植是成功执行的。`truffle migrate` 仅会执行新创建的移植。如果没有新的移植脚本，这个命令不同执行任何操作。可以使用选项 `--reset`来从头执行移植脚本。

### 修改配置

- Ganache默认运行在7545端口，可以在界面右上方的“设置”里进行更改。运行后默认创建10个账号，每个账号里有100ETH的余额。
要部署到链上，需要把IP、端口、网络ID告诉truffle。修改truffle.js：
```
module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*" // Match any network id
    }
  }
};
```

- 详见[官方文档](http://truffleframework.com/docs/advanced/configuration)




## 测试合约
---

- 直接执行命令：`truffle unbox metacoin `,创建这个项目。

- 由于metacoin的示例代码里已经把测试代码写好了，按照上面的修改完truffle.js之后，**我们就可以编译部署测试我们的代码了：**
```
truffle compile
truffle migrate
truffle test
```

- 结果如下:
![](/images/block_chain/metacion_test_result.png)

- 然后打开 ganache查看区块链的变化。 Accounts标签：第一个账户里ETH略有减少，因为交易消耗了gas；Blocks标签：Ganache是自动挖矿，生成了6个新区块，每个区块里有一个交易；Transactions标签：有6笔新交易，可以点开看交易详情；Logs标签：显示交易和挖矿日志



<br>
> 最后更新于2018.5.23
