<p align="center">
  <img src="https://raw.githubusercontent.com/Silence1017/EtherWatchdog_Dapp/main/images/card.png" align="middle"  width="500" />
</p>

------------------------------------------------------------------------------------------

<p align="center">
  <b>让🐶来帮助你解决最棘手的安全问题😄😏😆</b>
</p>


<center>[背景](#1) | [环境需求](#2) | [前端界面](#3) | [框架流程](#4) | [使用文档](#5) | [About Us](#6)</center>


EtherWatchdog是一款通过**交易**的操作码序列**实时**检测智能合约漏洞的安全平台，我们全面的智能合约漏洞检测服务可以帮助从初创公司到企业的每个人维护他们的以太坊区块链应用程序。EtherWatchdog的**未来**绝不仅仅是一个普通的智能合约漏洞检测平台，它有能力成为像**Etherscan**一样优秀的**区块链搜索**、**API**和**分析平台**。

[Dapp源码](https://github.com/Silence1017/EtherWatchdog_Dapp)  [Server源码](https://github.com/Silence1017/Lingnan-EthDarkness-Server)

<p id="1"></p> 

## 🌎 背景

以太坊的问世将区块链技术的发展推入以智能合约为标志的2.0时代。智能合约利用区块链去中心化的特性，将传统合同转变为代码的形式部署在区块链平台上，极大地降低了交易的成本。然而随着应用场景的丰富，智能合约控制的金融资产不可避免地成为黑客攻击的目标，其公开透明、不可篡改的特性以及与日俱增的复杂性更加剧了恶意攻击事件的发生。目前由智能合约安全漏洞引发的大规模安全案例不在少数，不仅造成了巨大的经济损失，而且严重破坏了基于区块链的信用体系，影响了用户对区块链技术的信任度和满意度。

<p id="2"></p> 

## 📃 环境需求

1. [MetaMask](https://metamask.io/)
2. [Node](https://nodejs.org/) v16.20.0
3. [Ganache](https://www.trufflesuite.com/ganache) v7.7.7
4. [Truffle](https://trufflesuite.com/truffle/) v5.8.1 (npm install -g truffle)
5. [Solidity](https://soliditylang.org/) v0.5.16
6. [Web3.js](https://web3js.org/) v1.8.2

<p id="3"></p> 

## 💻 前端界面

前端界面展示EtherWatchdog的三个部分————数据集、模型与检测。

1. 数据集：展示Geth插桩获取的部分交易信息。
2. 模型：展示用于检测合约漏洞的CNN-BiLSTM多分类模型。
3. 检测：展示合约漏洞检测流程，用户输入待检测的交易Hash并提交，后端返回检测结果并上链。

<p id="4"></p> 

## 🎉 框架流程

### 🎙️ 数据集获取

我们结合Geth插桩和深度学习技术实现了一个简易的智能合约漏洞检测框架。Geth插桩是指在以太坊客户端Geth源码中插入可以输出交易数据的代码段，交易操作码序列是由EVM操作码和操作数组成的序列。我们通过Geth插桩拿到每笔调用合约的交易的信息，而交易信息便包括了每笔交易的操作码序列，这些序列组成了训练数据集。

### ⚡ 漏洞检测

我们搭建了基于CNN-BiLSTM的深度学习多分类模型，将交易操作码序列向量化并传入模型，最终检测出合约是否存在漏洞，若存在则输出哪种漏洞。目前模型能检测5种漏洞，包括错误的权限检查（Incorrect Check for Authorization）、错误处理的异常（No Check after Contract Invocation）、缺少标准事件（Missing the Transfer Event）、严格余额检查（Strict Check for Balance）和时间戳/区块号依赖（Timestamp Dependency & Block Number Dependency）。

<p id="5"></p> 

## 📜 使用文档

### 🙈 初始化

```
truffle init
npm init
```
![img](https://raw.githubusercontent.com/Silence1017/EtherWatchdog_Dapp/main/images/5.png)

### 😾 启动私链

> 打开Ganache，启动本地私链，默认生成10个有100个ETH的账户

> 查看配置端口，默认7545，可以依照需求自行更改

> 修改truffle-config.js里面的配置端口
```
development: {
     host: "127.0.0.1",     // Localhost (default: none)
     port: 7545,            // Standard Ethereum port (default: none)
     network_id: "*",       // Any network (default: none)
 }
```

### 🔖 truffle部署合约

> 进入truffle控制台
```
truffle console
```
显示truffle(development)连接上了development环境

> 部署合约
```
migrate
migrate --reset    // 如果合约修改了需要重新部署，则需要添加reset参数
```
成功后控制台和Canache分别有如下输出
![img](https://raw.githubusercontent.com/Silence1017/EtherWatchdog_Dapp/main/images/1.png)

![img](https://raw.githubusercontent.com/Silence1017/EtherWatchdog_Dapp/main/images/2.png)

可以在打开的Ganache中看到执行成功的交易, 默认花费第一个帐户的ETH

### 🎩 检测合约漏洞

> 点击检测界面，输入查询交易Hash并提交，得到如下结果

![img](https://raw.githubusercontent.com/Silence1017/EtherWatchdog_Dapp/main/images/3.png)

![img](https://raw.githubusercontent.com/Silence1017/EtherWatchdog_Dapp/main/images/4.png)

## 🔔展望

畅想一下未来，EtherWatchdog的未来绝不仅仅是一个普通的智能合约漏洞检测平台，它有能力成为像**Etherscan**一样优秀的**区块链搜索**、**API**和**分析平台**。未来🐶想做到：
```text
1、像Etherscan一样实时检测并展示最新区块中的含漏洞交易，并提供免费的API供开发者使用。
2、制作一个包含以太坊所有交易的漏洞数据集供开发者使用，有效地避免社区成员调用含有漏洞的合约。
3、🐶有能力做到像Etherscan一样获取以太坊相关信息，包括合约、交易、区块、账户等信息并提供相关API，因为🐶对EVM进行了修改。
```

## 🔔Citation

如果EtherWatchdog对您的研究有帮助，欢迎引用

```
@inproceedings{gu2023detecting,
  title={Detecting Unknown Vulnerabilities in Smart Contracts with Multi-Label Classification Model Using CNN-BiLSTM},
  author={Gu, Wanyi and Wang, Guojun and Li, Peiqiang and Li, Xubin and Zhai, Guangxin and Li, Xiangbin and Chen, Mingfei},
  booktitle={Ubiquitous Security: Second International Conference, UbiSec 2022, Zhangjiajie, China, December 28--31, 2022, Revised Selected Papers},
  pages={52--63},
  year={2023},
  organization={Springer}
}
```
<p id="6"></p> 

## 👦👧About Us

**Lingnan Ethereum Darkness Agent**

✉️: 1257311626@qq.com

✉️: ouzhsh@126.com

✉️: 835837078@qq.com

✉️: 963544587@qq.com

✉️: cswygu@qq.com

最最感谢我们的博士师兄李培强以及**老王**❤️
