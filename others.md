- Wechat

将 https://github.com/zq1997/deepin-wine 压缩包下载至本地，然后解压终端打开，运行`install.sh`，完成wine的安装

继续上面的网站，往下拉找到微信并手动下载`.deb`安装包，建议下可以解决依赖错误的那个

1. 微信字无法显示：

```bash
sudo vim /opt/deepinwine/tools/run.sh
 
# 找到WINE_CMD="deepin-wine"行，将其改为
 
WINE_CMD="LC_ALL=zh_CN.UTF-8 deepin-wine"
```
2. 图片无法显示：

```bash
sudo apt install libjpeg62:i386
```

- 向日葵

https://sunlogin.oray.com/download/ 下载

如果连接一瞬间就断开，被控机是ubuntu，可以从以下两点解决：

1. 终端输入`xhost+`确定连接没有被限制
2. 切换桌面显示器
```bash
sudo apt-get install lightdm
```

- Anaconda

若出现CondaHTTPError: HTTP 000 CONNECTION FAILED for url ＜https://mirrors.tuna.tsinghua.edu.cn/anaconda/

或者是下载速度过慢，添加中科大源

```bash
conda config --add channels https://mirrors.ustc.edu.cn/anaconda/pkgs/free/
conda config --set show_channel_urls yes
```

将其他以及default删去
```bash
vim ~/.condarc
```
