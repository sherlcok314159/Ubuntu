### GPU环境配置

***tensorflow-gpu==1.14+cuda10.0+cudnn7.4***

接下来所需要的文件都在[网盘](https://pan.baidu.com/s/1zWy4wufAOOEUD5vZ6PUrHQ)，密码是 l5ft

给官网下载不方便的读者提供

**A.硬件确定**

这个大家可以上网查自己电脑的硬件，这里不再赘述。
****
**B.驱动程序**

首先，打开**软件和更新**（点击左下角，里面找），打开之后，当前页面有 **下载自**，这里切换到阿里的镜像*http://mirrors.aliyun.com/ubuntu*，因为接下来需要下载很多东西，切换国内的镜像就像你用pip的道理是一样的，会提升速度

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/software_and_update.png)

接下来Ctrl+Alt+T打开终端输入以下命令
```bash
sudo apt-get update
sudo apt-get upgrade #更新源，否则接下来找不到驱动程序
sudo apt-get install gcc make cmake #安装装环境时需要的编辑器
'''
若你已经root了（sudo -i），以上命令的sudo都不用打
'''
```
安装驱动程序网上流传较广的教程是禁用nouveau，即ubuntu自带的驱动程序，然后关闭图形界面，执行驱动程序的run文件等等。本教程采用与上述方案不一样的操作，因为这些操作跟机型不同，有很多坑，如run文件跑不起来等等。

打开软件和更新，打开驱动程序，选择系统推荐的驱动程序，我的是Win10 联想拯救者LegionY7000，GTX1650，官网上查驱动程序其实是不支持nvidia-driver-460，但我装了之后跑没问题。你选择上面推荐的驱动程序，然后**点击应用更改**，大概需要1，2分钟的样子。

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/driver.png)

然后命令行打开输入reboot，进行重启，在终端输入nvidia-smi，如果你的驱动装好了，应该是以下的样子


**C.CUDA安装**

装这个之前需要确定好版本，注意与tensorflow,cuda,cudnn这三者之间的对应关系，如下图

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/version.png)


我选择的是run文件

下载好之后，你打开终端，找到文件的位置

```bash
sudo -i #root
chmod a+x 文件路径 #可通过拖拽文件至终端解决

#该命令为赋予执行该文件的超级用户权限，否则等会执行不了

执行完上面之后，输入run文件路径，同样可拖拽解决

```
安装时一定要注意如果里面有如果问你是否安装Graphics Driver的时候，大概一开始就会问，你要输入n(o)，因为驱动程序刚刚已经有了。

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/cuda.jpg)

其他的全部yes就完了

结束之后，安装vim编辑器，这是Ubuntu系统上的文本编辑器，十分方便

```bash
sudo apt-get install -f vim

#当然，上述命令等价为
sudo apt-get install vim

#只是第一个命令可以一定程度解决依赖缺失问题
```

然后继续终端输入

```bash

sudo vim ~/.bashrc
#修改cuda路径
~指的是root文件夹下的
```
export CUDA_HOME=/usr/local/cuda
export PATH=$PATH:$CUDA_HOME/bin
export LD_LIBRARY_PATH=/usr/local/cuda-10.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

把上述内容插入（按i）到最后，然后按Esc，打":wq!"（该操作的意思是强制保存并退出），**注意":"一定一定不能忘记**。另外，**不同版本cuda不一样**，不能照抄，还有**路径之间不要留空格**


```bash
sudo source ~/.bashrc #进行更新
sudo reboot #重启
```

重启好输入

```bash
sudo nvcc -V
```

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/nvcc.png)

应该出现像上面一样反映出你CUDA的版本号


**D.cudnn安装**

按照**对应**的版本去官网下载，注意，需要下**3个deb**文件。

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/cudnn.png)

下载好之后，举例来讲

```bash
dpkg -i 文件路径

#按照上图的顺序来安装，不要搞乱，第二个应该是文件名里带dev的，第三个文件名带doc
```

检验

```bash
cp -r /usr/src/cudnn_samples_v8/home/cudnntest
cd /home/cudnntest/cudnn_samples_v8/mnistCUDNN
make make
/.mnistCUDNN
```
注意，不同版本不同，会导致cudnn_samples_v后面的数字不同，建议仔细查看一下

如果没问题的话，最后一行应该是如下所示：

>Test Passed!

然后接下来安装anaconda，dpkg命令即可，只是**别忘了添加到系统变量**

按照pip

```bash
sudo apt-get install python3-pip
#注意，如果只是python，会是python2的pip
```

到root文件下创立“.pip”文件夹，然后把pip.conf放进去，里面设置pip从清华的镜像站下载第三方包

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/root.png)

点击其他位置，点击计算机，里面有root。

另外，Ubuntu是可以访问Windows系统的文件的，但是**没有更改的权限**。

打开终端，输入

```bash
若为tensorflow2.x版本
pip3 install tensorflow==2.x
若为tensorflow1.x版本，可能找不到，需要提前下好轮子
pip3 install 轮子文件
```

我强烈建议安装Vscode，宇宙最强编辑器，里面打开拓展，安装python扩展和中文包，dpkg开头为code的deb文件即可

若你不喜欢，那就打开终端

```bash
source activate #激活anaconda基本环境
python #唤醒python
接下来跟你打开python自带的IDLE一个模样
conda list #查看该环境包的版本
source deactivate #退出环境
```
当然，日后不同的环境不能混起来，可以用conda创建虚拟环境

```python
conda create -n learn python=3.8
#创建了一个名为learn的python3.8包
```

在终端里面输入，一般环境激活即可，不用上面那样

```python
import tensorflow as tf
sess=tf.Session(config=tf.ConfigProto(log_device_placement=True))
```

你可以看终端，应该是可以看到发现GPU设备的

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/GPU_DEVICE.png)

截取部分如上