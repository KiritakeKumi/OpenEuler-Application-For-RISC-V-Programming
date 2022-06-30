## 第一章 实训二  使用QEMU安装RISC-V openEuler

### 下载 QEMU 源代码并构建


`$ sudo apt install build-essential`

安装必要的构建工具

`$ wget https://download.qemu.org/qemu-7.0.0.tar.xz`

 下载最新 QEMU 源码包，**请将 `7.0.0` 替换为目前最新的 QEMU 版本 或保留原状**

`$ tar xvJf qemu-<latest>.tar.xz`

解压

`$ cd qemu-<latest>`


在进行下一步之前建议预防性安装一下依赖包

`sudo apt-get install libpixman-1-dev zlib1g-dev pkg-config libglib2.0-dev sudo apt-get install pkg-config ninja-build`



`./configure --target-list=riscv64-softmmu,riscv64-linux-user --prefix=/home/riscv/program/riscv64-qemu`


`riscv-64-linux-user`为用户模式，可以运行基于 RISC-V 指令集编译的程序文件

`softmmu`为镜像模拟器，可以运行基于 RISC-V 指令集编译的linux镜像，为了测试方便，可以两个都安装

`home/riscv/program/riscv64-qemu`为安装到的目录 可自行选择 如无特殊自定义要求可保留原样

`$ make`

`$ make install`


如果 `--prefix` 指定的目录位于根目录下，则需要在 `./configure` 前加入 `sudo`


### 配置环境变量并验证安装

`$ nano ~/.bashrc`

使用任意编辑器修改 ~/.bashrc 在文末添加：

````
export QEMU_HOME=/home/riscv/program/riscv64-qemu
export PATH=$QEMU_HOME/bin:$PATH
````
**注意一定要将 `QEMU_HOME` 路径替换为 `--prefix` 定义的路径 如果在QEMU配置过程中未修改此处保持原样即可**

`$ source ~/.bashrc`

`$ echo $PATH`

`$ qemu-system-riscv64 --version`

如出现类似如下输出表示 QEMU 工作正常
````
QEMU emulator version 5.0.0
Copyright (c) 2003-2020 Fabrice Bellard and the QEMU Project developers
````
PS：此处输出随您所安装的版本不同产生变化

### 下载 openEuler RISC-V 系统镜像
恭喜你已经成功编译安装了最新版的 QEMU，接下来我们需要下载 openEuler RISC-V 的系统镜像。

由于我们的目标是运行最新版的 openEuler RISC-V OS，我们采用最新的发行版 22.03：

注：  `20.03`的系统镜像安装移步至 [20.03系统镜像下载](https://gitee.com/openeuler/RISC-V/blob/dced224a78ff47e547d4d00fcf3023177c7f4a5f/doc/tutorials/vm-qemu-oErv.md#%E4%B8%8B%E8%BD%BD-openeuler-risc-v-%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F)


提供两种安装方式

#### 浏览器下载
下载地址： https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/development/2203/Image/

#### Linux命令行安装

```bash
mkdir oervimg
cd oervimg
wget https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/development/2203/Image/run.sh
wget https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/development/2203/Image/fw_payload_oe.elf
wget https://mirror.iscas.ac.cn/openeuler-sig-riscv/openEuler-RISC-V/development/2203/Image/openEuler-22.03.riscv64.qcow2
```
其中的三个文件说明如下：

* **fw_payload_oe.elf**
利用 openSBI 将 kernel-5.10 的 image 作为 payload 所制作的用于 QEMU 启动的 image。

* **openEuler-22.03.riscv64.qcow2**
openEuler RISC-V 移植版的 rootfs 镜像。

* **run.sh**
利用 `qemu-riscv64` 运行openEuler RISC-V 系统镜像的脚本

### 启动openEuler RISC-V

在上一步下载的文件所在的目录下执行`bash run.sh`

run.sh文件说明
```
#!/bin/bash

qemu-system-riscv64 \
  -nographic -machine virt \
  -smp 8 -m 2G \
  -bios fw_payload_oe.elf \
  -drive file=openEuler-22.03.riscv64.qcow2,format=qcow2,id=hd0 \
  -object rng-random,filename=/dev/urandom,id=rng0 \
  -device virtio-rng-device,rng=rng0 \
  -device virtio-blk-device,drive=hd0 \
  -device virtio-net-device,netdev=usernet \
  -netdev user,id=usernet,hostfwd=tcp::22222-:22
````
注意 `-smp` 选项为CPU核数，`-m` 为虚拟机内存大小 请根据宿主机配置酌情修改。

这里以主机端口转发的方式实现网络功能。为 SSH 转发的 22222 端口也可改为自己需要的端口号


## 欢迎使用

- 登录用户：`root`
- 默认密码：`openEuler12#$`

建议在登录成功之后立即修改 root 用户密码





