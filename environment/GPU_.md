### GPU环境配置

***tensorflow-gpu==1.14+cuda10.0+cudnn7.4***

接下来所需要的文件都在[网盘](https://pan.baidu.com/s/1zWy4wufAOOEUD5vZ6PUrHQ)，密码是 l5ft

给官网下载不方便的读者提供

**A.硬件确定**

这个大家可以上网查自己电脑的硬件，这里不再赘述。
****
**B.驱动程序**

首先，打开**软件和更新**（点击左下角，里面找），打开之后，当前页面有 **下载自**，这里切换到阿里的镜像*http://mirrors.aliyun.com/ubuntu*，因为接下来需要下载很多东西，切换国内的镜像就像你用pip的道理是一样的，会提升速度

![](https://github.com/sherlcok314159/Ubuntu/blob/main/Images/software_and_update.jpg)

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

把上述内容插入（按i）到最后，然后按Esc，打":wq!"，**注意":"一定一定不能忘记**

该操作的意思是强制保存并退出

```bash
sudo source ~/.bashrc #进行更新
sudo reboot #重启
```

重启好输入

```bash
sudo nvcc -V
```



应该出现像上面一样反映出你CUDA的版本号