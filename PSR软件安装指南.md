# ***目录***

**1. PSRCHIVE系列包的安装** 

**2. DSPSR的安装**

**重要补充: 新版TEMPO2编译安装**

**重要补充: CUDA加速**

*(待补充)*


# ***1.PSRCHIVE系列包的安装***

PSRCHIVE官网：[https://psrchive.sourceforge.net](https://psrchive.sourceforge.net)

PSRCHIVE只能在Linux系统或conda中以一个python标准库进行安装。
更多详细的安装说明、使用说明请以官网为准。


## **Step 1. 下载PSRCHIVE源码**


**选择1: git clone**

先确定自己想要在系统的哪个位置（目录）安装PSRCHIVE

以 /home/<your_username> 用户个人目录为例
```bash
cd /home/<your_username>
```
运行以下指令,将会下载PSRCHIVE的源代码至你运行cd指令后的工作路径
```bash
git clone git://git.code.sf.net/p/psrchive/code psrchive
```
下载完毕后，工作路径下会有psrchive目录
![Downloaded git of PSRCHIVE](https://i.ibb.co/gM96jXfn/WPS-1.png)

**选择2: SourceForge**

进入到SourceForge项目页 https://sourceforge.net/projects/psrchive 点击"Files"然后再点击方框内的文件夹"psrchive", 即可看到多个版本的 PSRCHIVE 源码压缩文件。

![SourceForge: PSRCHIVE](https://i.ibb.co/FkLqYc9d/PSRCHIVE-SF-Project-Download.png)

点击任意一个下载即可。

下载成功后, 切记要把源码压缩包用
```bash
# 假设你按照psrchive的版本是xxxx-yy-zz:
tar -zxf psrchive-xxxx-yy-zz.tar.gz
```
指令进行解压。解压后会出现目录 ```psrchive-xxxx-yy-zz.tar.gz```, 这便是你下载下来的psrchive源码目录

## **Step 2.**

原则上可以cd进入到psrchive目录下运行其中的bootstrap和configure文件了。但是根据本人在安装PSRCHIVE经历来看，依然需要事先配置好psrchive的各个环境变量及其工作目录。不然容易报错。

如何配置环境变量可以详见官网说明：

[https://psrchive.sourceforge.net/installation.shtml](https://psrchive.sourceforge.net/installation.shtml)

假设你已经在系统的某处（以用户目录/home/<your_username>为例）下创建好的Pulsar目录:
```bash
mkdir -p /home/<your_username>/Pulsar
```
在用户个人目录 /home/<your_username>/.profile(或.bashrc) 文件中键入以下环境变量即可（以下PSRHOME变量的设置**以用户个人目录下的Pulsar**为例的）
```Bash
export PSRHOME=$HOME/Pulsar
export PATH=${PATH}:$PSRHOME/bin
export PGPLOT_DIR=$PSRHOME/pgplot
export PGPLOT_FONT=$PGPLOT_DIR/grfont.dat
export TEMPO2=$PSRHOME/tempo2
export PSRCAT_FILE=$PSRHOME/psrcat/psrcat.db
```
这一Pulsar目录你也可以创建在系统的其他位置。

记得将PSRHOME设置为Pulsar所在的目录！
```bash
export PSRHOME="/path/you/want/Pulsar"
```


## **Step 3. GNU Tools 的安装或更新**

并非所有系统都安装好了GNU Tools系列工具包，而PSRCHIVE是基于这一开源工具包开发的系列数据处理包。在这里我将贴出安装和更新GNU Tools的指令：
```bash
sudo apt update
sudo apt install pkgconfig
sudo apt install -y autotools-dev autoconf libtool make
sudo apt install g++ gfortran
sudo apt install libfftw3-dev pgplot5 libcfitsio-dev
```
如果是在**没有给用户root权限的多用户环境/服务器集群**里, 你也可以将上述GNU Tools源码的压缩包下载至你的用户目录中，利用相应的解压缩指令解压源码后编译。

## **Step 4.进入psrchive目录，进行启动配置和编译**
```bash
cd /path/you/download/psrchive
./bootstrap
./configure
```
中间还可能会遇到部分library包的缺失。解决方法是：直接cd到psrchive下的packages运行相应的文件：
```bash
sudo ./XXXX.csh
```
在configure成功以后,分别运行以下指令：
```bash
make
make check
sudo make install
```
运行上述make指令的时间会比较长，请耐心等待。

新开一个终端，输出psrchive后如果有命令提示，就证明安装已经成功。


## **补充：**
按照官网的提示：
[https://psrchive.sourceforge.net/third/install.shtml](https://psrchive.sourceforge.net/third/install.shtml)

PSRCHIVE软件自带的目录packages下有大量自动安装脚本，可以自动安装PSRCHIVE的其他依赖环境。请按照你自身的需求，在安装完PSRCHIVE所有必要的包以及设置好必要的环境变量以后，使用如下列出的指令自动安装：

（假设你已经cd到psrchive目录）
```bash
./configure
./packages/fftw.csh
./packages/cditsio.csh
./packages/pgplot.csh
./packages/tempo2.csh
./packages/psrcat.csh
./configure
```
*（空白，待后续补充）*

# ***2. DSPSR的安装***

DSPSR软件的官网：
[https://dspsr.sourceforge.net](https://dspsr.sourceforge.net)

更多详细的安装说明、使用说明请以官网为准。


## **Step 1. 下载DSPSR源码**

先确定自己想要在系统的哪个位置（目录）DSPSR

**选择1: git clone** 

以 /home/<your_username> 用户个人目录为例
```bash
cd /home/<your_username>
```
运行以下指令,将会下载DSPSR的源代码至你运行cd指令后的工作路径
```bash
git clone --recursive git://git.code.sf.net/p/dspsr/code dspsr
```
下载完成之后，工作目录上会出现dspsr目录。 

**选择2: SourceForge下载源码压缩文件**

进入到SourceForge项目页 https://sourceforge.net/projects/dspsr/, 点击"Files"然后再点击方框内的文件夹"dspsr", 即可看到多个版本的 DSPSR 源码压缩文件。

![SourceForge: DSPSR](https://i.ibb.co/j94V0X52/DSPSR-SF-Project-Download.png)

点击任意一个下载即可。

下载成功后, 同理
```bash
# 假设你按照dspsr的版本是aaaa-bb-cc:
tar -zxf dspsr-aaaa-bb-cc.tar.gz
```
解压后会出现目录 ```dspsr-aaaa-bb-cc.tar.gz```, 这便是你下载下来的dspsr源码目录

## **Step 2. 进入dspsr目录，创建backends.list文件**
```bash
sudo gedit backends.list
```
或者 
```bash
touch backends.list
```

backends文件是用于列出所有你需要的后端名称，防止各后端代码冲突。创建backends.list后，输入以下内容（举例）：
```
bpsr caspsr fits sigproc
```
示例如下：

![example](https://i.ibb.co/j9mhVDPK/WPS-2.png)\
![example](https://i.ibb.co/9MXsBzn/WPS-3.png)


## **Step 3.在dspsr目录下配置、编译与安装**

分别运行以下指令：
```bash
./bootstrap
./configure
make
make check
sudo make install
```
这一步可以不用太快开始。根据官网的提示，你可以把DSPSR安装到默认目录以外的地方，只需要在make install上指定--prefix参数即可，例如：
```bash
# 如果指定的位置没有权限写入, 需要sudo
make install prefix="$HOME/Astro_sorfware"
```
请确定好DSPSR的安装目录！

DSPSR的默认安装目录：如果你如上“PSRCHIVE系列包的安装”中设置了```$PSRHOME```这一环境变量，那么在你键入```make install```以后DSPSR将分别把它的系统文件(build products)安装至```$PSRHOME```的如下目录：
```bash
	$PSRHOME/bin
	$PSRHOME/lib
	$PSRHOME/include
	$PSRHOME/share
```
如果没有设置```$PSRHOME```，那么DSPSR会在```make install```指令执行时把它的build products安装到``/usr/local``目录下。

这一点请详见官网[https://dspsr.sourceforge.net/devel/install.shtml](https://dspsr.sourceforge.net/devel/install.shtml)


## **Step 4.在终端中输入dspsr --version，如果终端跳出版本信息即证明安装成功。**

![version status of DSPSR](https://i.ibb.co/0p0NYWx2/WPS-4.png)

# ***重要补充：新版TEMPO2编译安装***

TEMPO2 编译安装详情参考 https://bitbucket.org/psrsoft/tempo2/src/master/

假设你需要在服务器/集群环境里安装 TEMPO2。

由于国内众所周知的原因，sourceforge、git等一众开源码库在国内互联网环境下难以链接。您需要采取一定的技术手段将Tempo2源码或git库下载到您的工作环境下，后面利用诸如
```bash
rsync
```
的指令将 Tempo2 的源码/git库上传至服务器/集群下的用户目录。

以下是具体安装步骤。假设您的用户目录是/home/rainvent:
```bash

# PSRHOME 环境变量设置
export $PSRHOME="/home/rainvent/Pulsar" # 写入至~/.bashrc可永久设置
# TEMPO2 环境变量设置
export $TEMPO2="${PSRHOME}/tempo2" # 写入至~/.bashrc可永久设置
export PATH="$TEMPO2/bin:${PATH}"

# 路径至tempo2的源码目录
cd path/to/the/tempo2
# 将路径下的T2runtime所有内容复制到 $TEMPO2 下
cp -r ./T2runtime/* $TEMPO2

# 正式编译安装
./configure --prefix="$TEMPO2" # ./configure --help 可以查看其他参数
make
make install

# (可选) 编译安装tempo2插件, 不过笔者从未安装成功过, 不知为何 (π.π)
make plugins
make plugins-install
```

随后可以检测 TEMPO2 是否安装成功
```
which tempo2
tempo2 -v
```

# ***重要补充：CUDA加速***

**DSPSR支持使用CUDA加速其有关消色散、FFT的计算。**

相关的信息可以详见官网https://dspsr.sourceforge.net/manuals/dspsr/gpu.shtml

DSPSR使用CUDA相关功能之前需要预先设置PACKAGES变量的同时，也需要在编译时(./configure)输入相关的参数。

如下教程是**假定你已经完成过DSPSR的安装，现需要重新编译DSPSR。**
```bash
# setenv 设置环境变量
setenv PACKAGES /usr/local/cuda
# 或：export 设置环境变量
export PACKAGES="/usr/local/cuda"
# 以上cuda的所在路径以 /usr/local/cuda 为例，到make步骤时需要 sudo。请以你的机器 cuda 所在的实际路径为准

# 路径到 DSPSR 的源码目录
cd /the/path/to/dspsr
# 清除原先编译的dspsr后再./configure
make clean
# 重新 configure 并编译
# 注意输入参数 --with-cuda-dir；为保险起见尽可能将所有 --with-cuda 参数硬编码至 ./configure
./configure --with-cuda-dir=... \ # CUDA安装目录
			--with-cuda-include-dir=... \ # CUDA目录下的include
			--with-cuda-lib-dir=... \ # CUDA目录下的lib
			--prefix=$PSRHOME \ # 编译安装目录，这里选择为本教程常使用的$PSRHOME
			--LD_LIBRARY_PATH=... \ # 库目录
			PSRHOME=$PSRHOME \ # PSRHOME变量
			CUDA_NVCC_FLAGS="-arch=sm_75" \ # 一般不需要设置-arch。除非CUDA版本高于显卡所能支持的最大版本。
# 切记！必须根据机器/服务器集群所用的显卡(或GPU节点的显卡)设置-arch参数。
# 如20系显卡的计算能力是7.5，这里的参数便设置为 sm_75
...
...
...
# 完成configure后输入 make && make install 即可进行编译安装；如果有报错，按照报错的提示来解决问题
# 在这之前可以输入 grep CUDA Makefile 查看makefile是否有相关的参数被写入。
# 如果没有请检查上一步 ./configure 是否有缺漏并重新操作
make
make check
make install

```
## **Q: 如果我选择安装DSPSR的一开始就设置好启用CUDA加速选项呢 ?**

您可以选择在安装DSPSR的一开始就设置好CUDA加速选项。只需要
```bash
./configure
```
的时候设置好
```bash
--with-cuda-dir, --with-cuda-include-dir, --with-cuda-lib-dir
```
即可


## **Q: 如何安装CUDA ?**

从CUDA-toolkit文档官网 https://developer.nvidia.com/cuda-toolkit-archive 下载对应版本的CUDA安装即可。在这里不赘述。

## **Q: DSPSR运行过程中如何启用CUDA加速 ?**

只需要设置好```-cuda devices```选项即可。相关的信息详见官网https://dspsr.sourceforge.net/manuals/dspsr/gpu.shtml。

如下所示

```bash
dspsr -cuda 0 # 启动显卡0的一个进程
dspsr -cuda 0,1 # 启动显卡0, 1，两个显卡分别启动1个进程
dspsr -cuda 0,0,1,1 # 启动显卡0, 1，两个显卡分别启动2个进程
```
以此类推......

# **FFT性能优化**
具体详见官网https://dspsr.sourceforge.net/manuals/dspsr/optimize.shtml


### PSRCHIVE：Producing FFT Benchmarks for Central Processing Units

```bash
# PSRCHIVE FFT Optimizing (CPU)

# 路径到 PSRCHIVE 的源码目录
cd /the/path/to/psrchive
cd Util/fft
make bench # make bench 后需要经历相当长的时间, 请耐心等待其完成

```

### DSPSR: Producing FFT Benchmarks for Graphics Processing Units

```bash
# DSPSR FFT Optimizing (GPU)

# 路径到 DSPSR 的源码目录
cd /the/path/to/dspsr
cd Benchmark # 如果没有 Benchmark， 可以自行 git clone 相应版本的 DSPSR ，然后复制进DSPSR源码目录即可

# 运行 benchmark 程序，需要经历相当长的时间, 请耐心等待其完成（注意其报错）
./filterbank_bench.csh

# 复制 filterbank_bench.csh 产生的 filterbank_bench.out 至DSPSR的安装目录share中,
# 并更名为 filterbank_bench_CUDA.dat
cd filterbank_bench.out dspsr_prefix/share/filterbank_bench_CUDA.dat

```


