# P4_env
学习搭建P4环境
# P4环境配置

## 1、主机配置

```
本人配置：
#系统：Windows11
#内存：16G
虚拟机：
VMware17:可以关注；'软件安装家园'公众号
Ubuntu20.4:https://cn.ubuntu.com/download/alternative-downloads

虚拟机配置：
内存8GB（不然有些make check可能会不通过）
硬盘：至少40G
CPU：2核2线程
安装好VMware Tools方便拖拽文件：https://blog.csdn.net/qq_36393978/article/details/128624330
```

## 2、配置P4环境

参考文档：[poohdang/p4-env - 码云 - 开源中国 (gitee.com)](https://gitee.com/poohdang/p4-env/tree/advanced)
(给博主点个👍，因为之前弄了好久，各种错误，这个一次就弄好了)

### 1、VPN

**#安装前最好能有个能在Linux上跑的VPN**

VPN：

```http
（1）https://suying999.net/user/tutorial?os=linux&client=clash
（2）https://github.com/wanhebin/clash-for-linux
```

**或者VM下的Ubuntu虚拟机共享主机的VPN**：
```html
https://arctee.cn/686.html
```




### 2、开始配置P4

#### 1、安装git  

```shell
$ sudo apt-get update
$ sudo apt install git
```
**确保python3指令指向期望的解释器**
```shell
$ sudo apt install python3 python3-pip
$ python3 -V
$ python3 -m pip -V
```

#### 2、设置工作目录并克隆本仓库

```shell
#当前目录为Home
# 以下工作目录可自定义，此处以/Workspace/P4为示例
$ mkdir -p ~/Workspace/P4 && echo "export P4_HOME=~/Workspace/P4" >> ~/.bashrc  
$ source ~/.bashrc
$ cd $P4_HOME # 这一句命令一定要跳到~/Workspace/P4 ，否则前面的重新配置
$ git clone https://gitee.com/poohdang/p4-env.git
$ cd p4-env
```

#### 3、安装必要的依赖和编译工具

```shell
$ sudo chmod 755 p4*.sh
$ ./p4-deps.sh
```

#### 4、下载源码

2种方法

##### 方法一

```shell
#直接从github上下载，需要挂VPN，若出现aborting停止了，则说明可能网络波动，把刚刚下的文件夹（只留下p4-env）全删了再次执行下面命令
#（或者注释掉脚本已经成功clone的部分）。
$ ./p4-git.sh
```

##### 方法二

需要能与虚拟机拖拽文件

```
链接：https://pan.baidu.com/s/1jDwfEc1wkDQARgGorho5kA?pwd=9bpt

提取码：9bpt
```

下好后拖进去就行，改一下名字，把版本号啥的都删了（mininet/protobuf/grpc/bmv2_deps/pi/bmv2/p4c），全都放到和p4-env同一目录下

#### 5、编译安装

```shell
#以mininet为例子，按照以下顺序一个个执行就行(mininet/protobuf/grpc/bmv2_deps/pi/bmv2/p4c)
$ ./p4-install.sh mininet 
```

##### 6、 检查python搜索路径

```shell
$ echo "/home/$USER/.local/lib/python3.8/site-packages" >> p4-env.pth
$ sudo cp -f p4-env.pth /usr/local/lib/python3.8/dist-packages/
```



至此，Ubuntu20.4配置p4环境结束，具体联系可以参考文档：

[p4lang/tutorials: P4 language tutorials (github.com)](https://github.com/p4lang/tutorials/tree/master)

[nsg-ethz/p4-learning: Compilation of P4 exercises, examples, documentation, slides for learning or teaching (github.com)](https://github.com/nsg-ethz/p4-learning)
