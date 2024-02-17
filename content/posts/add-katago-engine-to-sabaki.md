+++
title = "Sabaki 安装 katago 引擎"
date = "2024-02-17T12:16:50+08:00"
tags = ["go"]
+++


在 Mac 系统中安装 AI 机器人展开围棋大战

![SCR-20240207-lnqm](https://cloud.synclue.com/2024/02/17/1708151084.png)

### 安装 Sabaki

在 Sabaki [官网](https://sabaki.yichuanshen.de/) 下载最新版本，支持 Windows，Mac，Linux 三个系统

### 安装 katago 

先在终端中安装katago，以下仅介绍如何在 Mac 中安装，~~Windows 或 Linux 的详见[官方指引](https://github.com/lightvector/KataGo?tab=readme-ov-file#windows-and-linux)~~

```
$ brew install katago
```

安装完成后校验是否可用，在终端中输入 katago

```
Usage: katago SUBCOMMAND

---Common subcommands------------------

gtp : Runs GTP engine that can be plugged into any standard Go GUI for play/analysis.
```

### Sabaki 中添加 katago 引擎

1. 打开 sabaki 首选项（顶部菜单）
2. 选择引擎
3. 点击左下角新增

有四项内容待填写：名称，路径，运行参数，启动参数，我们来依次填写

#### 名称

此处输入引擎名称，建议填写 `Katago` 

#### 路径

此处需要填写 katago 的安装路径，运行以下命令来获取：

```
$ which katago
```

复制输出的katago 路径，并将其粘贴到路径中

```
/opt/homebrew/bin/katago
```

#### 运行参数

要想 katago 正常运行，仅需 gtp 相关的命令即可，需要注意两个变量 A&B

```
gtp -config A -model B
```

此处采用最简单办法，使用 katago 自带的 A 和 B，来看一下如何获取 A&B 的文件路径

A 配置文件 `/path/to/gtp_example.cfg` ，直接使用 katago 默认 cfg 配置文件

```
$ brew list --verbose katago | grep .cfg | grep gtp
```

```
/opt/homebrew/Cellar/katago/1.14.0/share/katago/configs/gtp_example.cfg
```

B 模型文件 `/path/to/model.txt.gz`，直接使用 katago 默认已安装的模型文件

```
$ brew list --verbose katago | grep .gz
```

在返回的三个结果中任选一个，对于配置较低的 GPU，请尝试 g170e-b20***

```
/opt/homebrew/Cellar/katago/1.14.0/share/katago/g170-b30c320x2-s4824661760-d1229536699.bin.gz
/opt/homebrew/Cellar/katago/1.14.0/share/katago/g170-b40c256x2-s5095420928-d1229425124.bin.gz
/opt/homebrew/Cellar/katago/1.14.0/share/katago/g170e-b20c256x2-s5303129600-d1228401921.bin.gz
```

那么最终的运行参数可能是这样的，将其粘贴到运行参数字段中

```
gtp -config /opt/homebrew/Cellar/katago/1.14.0/share/katago/configs/gtp_example.cfg -model /opt/homebrew/Cellar/katago/1.14.0/share/katago/g170-b40c256x2-s5095420928-d1229425124.bin.gz
```

当然您也可以自行下载配置文件和模型文件，将相应的文件路径进行替换即可

#### 启动参数

将如下命令复制粘贴到启动参数字段中

```
time_settings 0 5 1
```

具体各个值的含义如下

```
0 = main time
10= time period
1 = stones per period
```

最终配置完成后，看且来就像下图所示

![SCR-20240207-lnqm](https://cloud.synclue.com/2024/02/17/1708151077.png)

### 试玩一局

1. 新对局
2. 对局信息中加载katago引擎（文件-对局信息 或 棋盘右下角点击找到对局信息）

![SCR-20240217-kcfa](https://cloud.synclue.com/2024/02/17/1708151056.jpg)

想要安装更多引擎，可以参考 sabaki 的 [WIKI 介绍](https://github.com/SabakiHQ/Sabaki/blob/master/docs/guides/engines.md)

### 常见问题

1. 未能奏效，主要检查引擎的路径是否在前面或者后面多了空格，把它删掉就可以了
2. 如果黑棋加载了 katago 引擎，需要在引擎中点击生成一手棋才可让对局进行
3. 如果对以上的内容完全看不懂，建议直接安装 [KaTrain](http://github.com/sanderland/katrain/releases)

### 附录

1. [别人的教程（johnriselvato）](http://johnriselvato.com/installing-katago-in-sabaki-2-for-macos/) 
2. [Katago WIKI](https://github.com/lightvector/KataGo#how-to-use)
3. [空格键导致无法运行的出处](https://github.com/SabakiHQ/Sabaki/issues/612)
4. [围棋AI及GUI的使用简介](https://zhuanlan.zhihu.com/p/267139001)
