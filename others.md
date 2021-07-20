- Wechat

将https://github.com/zq1997/deepin-wine 压缩包下载至本地，然后解压终端打开，运行`install.sh`，完成wine的安装

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
