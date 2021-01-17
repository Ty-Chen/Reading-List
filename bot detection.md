# 服务端工作室脚本检测综述



## 一. 简介

&emsp;&emsp;目前常用的服务端工作室脚本检测技术主要通过分析游戏数据提取关键特征。其特征可以分为两类：充分条件和必要条件。二者皆有其优缺点，下文会逐一进行分析。

## 二. 充分条件

&emsp;&emsp;充分条件指的是可能来自于工作室脚本的一系列特征性行为。通常我们可以将这一系列行为标记为疑似工作室脚本，从而进行进一步判断。常见的利用充分条件进行工作室脚本检测的包括以下两种：

- 动作行为检测
- 社交行为检测

&emsp;&emsp;充分条件由于缺少必要性，只能作为“疑似”工作室脚本的检测。同时，这里存在一个缺陷：工作室脚本开发者可以很容易的修改工作室脚本的行为，因此针对特定行为的判断需要随之更新。更有甚者，随着工作室脚本的升级，已经有些可以模拟对话或者玩家随机行为的脚本出现，这导致了检测日益困难。

### 2.1 动作行为检测

&emsp;&emsp;动作行为检测着眼于移动、技能释放等行为，通过大数据分析平台分析整个动作行为序列。通过**标记特定行为序列**来检测是否是工作室脚本[2]，常见算法有`Simple Scoring Algorithm`及`Naive Bayesian Algorithm`。除此之外还可以通过**获取大量相似行为序列**的方式来判断是否是脚本[3]，常见算法为`Logistic Regression Algorithm with Self-Similarity of Characters`。

### 2.2 社交行为检测

&emsp;&emsp;社交是MMORPG的核心玩法之一，聊天、组队、团队、好友、帮派、势力等组成了错综复杂的社交行为网络。对于工作室脚本来说，其社交行为无疑和真实玩家有着巨大的区别。例如可以通过机器学习算法拉取并分析聊天记录，判断其**聊天内容的相似性**（机器人个体聊天语句的大量重复以及机器人之间的重复）[4]。除此之外，还可以分析玩家参与PVP/PVE玩法的组队、帮派、攻防等记录，由于MMORPG本身特性，决定了其PVE/PVP等多人玩法均有着短时间内的强交互特性，而工作室并不具有该特点，由此衍生出了一些日志统计分析的检测方法[5]。

## 三. 必要条件

&emsp;&emsp;必要条件指的是必然来自于工作室脚本的一系列特征性行为。工作室脚本的目的在于通过大量获取虚拟货币并转化为现金而获利，无论工作室脚本开发者如何修改脚本行为，毫无疑问的依然存在相同的虚拟货币特征：

- 大量积攒虚拟货币（通常是每次获取极少，来自于怪物掉落等）
- 分批交易或大额度转出

&emsp;&emsp;在[6]中，开发者采取了交易链追踪的方式构成大型的图，通过`Density-Based Spatial Clustering of Applications with Noise (DBSCAN) algorithm`算法分离脚本和真实玩家的经济行为。另外[7]一文分析了脚本机器人的资金链，由此作为特征来区分脚本和玩家。

&emsp;&emsp;通过经济行为作为必要条件检测机器人可以从宏观角度分析出大批的工作室脚本，但是也存在着一些缺陷。

- 首先，脚本工作室脚本的升级也会针对这些检测做一些措施，比如增加交易中间人或者更改交易方式（如邮件、拍卖行上架等）
- 其次，宏观检测难以快速定位单个工作室脚本，检测速度较慢，不够迅速
- 另外建立拓扑网络图需要大量的资源、建立庞大的结构，训练和更新代价更大。

## 参考文献

[1] Show Me Your Account: Detecting MMORPG Game Bot Leveraging Financial Analysis with LSTM

[2] In-game action sequence analysis for game bot detection on the big data analysis platform

[3] You are a game bot!: Uncovering game bots in mmorpgs via self-similarity in the wild

[4] Chatting pattern based game bot detection: do they talk like us?

[5] Online game bot detection based on party-play log analysis

[6] Game-bot detection based on clustering of asset-varied location coordinates

[7] No silk road for online gamers!: Using social network analysis to unveil black markets in online games