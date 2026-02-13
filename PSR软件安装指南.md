# ***目录***

**1.PSRCHIVE系列包的安装**

**2.DSPSR的安装**

*(待补充)*


# ***1.PSRCHIVE系列包的安装***

PSRCHIVE官网：[https://psrchive.sourceforge.net](https://psrchive.sourceforge.net)

PSRCHIVE只能在Linux系统或conda中以一个python标准库进行安装。
更多详细的安装说明、使用说明请以官网为准。


**Step 1.**
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
![enter image description here](https://i.ibb.co/gM96jXfn/WPS-1.png)


**Step 2.**
原则上可以cd进入到psrchive目录下运行其中的bootstrap和configure文件了。但是根据本人在安装PSRCHIVE经历来看，依然需要事先配置好psrchive的各个环境变量及其工作目录。不然容易报错。

如何配置环境变量可以详见官网说明：

[https://psrchive.sourceforge.net/installation.shtml](https://psrchive.sourceforge.net/installation.shtml)

假设你已经在系统的某处（以用户目录/home/<your_username>为例）下创建好的Pulsar目录:
```bash
mkdir -p /home/<your_username>/Pulsar
```
在用户个人目录 /home/<your_username>/.profile(或.bashrc) 文件中键入以下环境变量即可（以下PSRHOME变量的设置以用户个人目录下的Pulsar为例的）
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


**Step 3. GNU Tools 的安装或更新**

并非所有系统都安装好了GNU Tools系列工具包，而PSRCHIVE是基于这一开源工具包开发的系列数据处理包。在这里我将贴出安装和更新GNU Tools的指令：
```bash
sudo apt update
sudo apt install pkgconfig
sudo apt install -y autotools-dev autoconf libtool make
sudo apt install g++ gfortran
sudo apt install libfftw3-dev pgplot5 libcfitsio-dev
```


**Step 4.进入psrchive目录，进行启动配置和编译**
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


**补充：**
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


**Step 1. 下载DSPSR源码**

先确定自己想要在系统的哪个位置（目录）DSPSR

以 /home/<your_username> 用户个人目录为例
```bash
cd /home/<your_username>
```
运行以下指令,将会下载DSPSR的源代码至你运行cd指令后的工作路径
```bash
git clone --recursive git://git.code.sf.net/p/dspsr/code dspsr
```
下载完成之后，工作目录上会出现dspsr目录。


**Step 2. 进入dspsr目录，创建backends.list文件**
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
![enter image description here](https://i.ibb.co/j9mhVDPK/WPS-2.png)
![enter image description here](https://i.ibb.co/9MXsBzn/WPS-3.png)


**Step 3.在dspsr目录下配置、编译与安装**

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
sudo make install prefix="$HOME/Astro_sorfware"
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


**Step 4.在终端中输入dspsr --version，如果终端跳出版本信息即证明安装成功。**

![enter image description here](https://i.ibb.co/0p0NYWx2/WPS-4.png)

*（空白，待后续补充）*
