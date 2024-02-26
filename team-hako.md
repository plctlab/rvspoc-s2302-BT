# S2302《二进制翻译及优化》产出提交

## 参赛队伍信息

- 队伍名称：hako
- 组队情况：个人参赛

## 提交内容

- 代码仓库：https://github.com/ptitSeb/box64/tree/ff6cc844821439a8f50b68b27e6f1ac5264579c8 （已经合入上游）
- 测试平台：SG2042
- 操作系统：revyOS
- 运行环境：box64 (`ff6cc844821439a8f50b68b27e6f1ac5264579c8`), Wine 9.0

## 配置软件环境

### 获取 box64

安装依赖

```shell=
sudo apt install gcc cmake mold
```

获取源代码

```shell=
git clone https://github.com/ptitSeb/box64.git 
cd box64
git checkout ff6cc844821439a8f50b68b27e6f1ac5264579c8
```

编译

```shell=
mkdir build
cd build
cmake .. -DRV64=1 -DCMAKE_BUILD_TYPE=RelWithDebInfo -DWITH_MOLD=1
mold -run make -j`nproc`
```

安装

```shell=
sudo make install
sudo systemctl restart systemd-binfmt
```

测试是否安装成功：运行 `box64 --help` 应该可以看到类似的输出

```plain!
Dynarec for RISC-V With extension: I M A F D C XTheadBa XTheadBb XTheadBs XTheadCondMov XTheadMemIdx XTheadMemPair XTheadFMemIdx XTheadMac PageSize:4096 Running on unknown riscv64 cpu with 64 Cores
Params database has 59 entries
Params database has 71 entries
This is Box64, The Linux x86_64 emulator with a twist

Usage is 'box64 [options] path/to/software [args]' to launch x86_64 software.
 options are:
    '-v'|'--version' to print box64 version and quit
    '-h'|'--help' to print this and quit
    '-f'|'--flags' to print box64 flags and quit
```

### 获取 Wine

测试使用的 Wine 9.0 来自 Pi-Apps-Coders。

> - [下载链接](https://github.com/Pi-Apps-Coders/files/releases/download/large-files/wine-9.0.tar.gz)
> - sha256: 5b73630de811ab3d489e0a8bc120924e0208830a5746a0820fe73cede1ddb3c1

```shell=
wget https://github.com/Pi-Apps-Coders/files/releases/download/large-files/wine-9.0.tar.gz
tar -xf wine-9.0.tar.gz
# 将 wine 加入 $PATH 中
export PATH=$PATH:$(pwd)/wine-9.0/bin/
```

PE 文件（`.exe`）的运行方法

```shell=
# path/to/game.exe 替换为实际的 .exe 文件路径
wine path/to/game.exe
```

## 运行游戏

### 轩辕剑叁外传天之痕

> 游戏的压缩包
> 
> - sha256: 334922fbc8aa233277326132f5920a494395070302aa418b47bbf21ea07b5add

运行 `Setup.exe`，然后就能够运行游戏 `swd3eDvd.exe`。

### CS 1.6

> 游戏的安装包
> 
> - sha256: b2275e14444b3212c19b78cdf25f74851f4d4092f0e32ed4d35ddb6aee5a9c86

运行该 `.exe` 文件安装游戏，游戏的可执行文件为 `hl.exe`。

注：可以进行联机游戏，但启用 NPC 时游戏会卡死（原因不明，但似乎不是 box64 的问题）。如果开启本地服务器游戏，可以将 NPC 数量设置为 0。
