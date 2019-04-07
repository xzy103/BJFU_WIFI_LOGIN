# BJFU_WIFI_LOGIN
自动登录BJFU校园网：连接WiFi、登录账户、获取账户信息，三大功能一站式搞定。  
更新时间：2019.4.7

## 代码主要结构
1.获取bjfu-wifi连接状态，False则进行连接。  
2.获取bjfu-wifi登录状态，False则进行登录。  
3.获取用户账户信息，例如剩余流量值。  

## 详细介绍
- 获取账户信息部分参考[Koonchung编写的BJFU_login项目](https://github.com/Koonchung/BJFU_login)

&#8195;&#8195;程序先判断当前目录下是否存在`userinfo`的文件（没有后缀），如果不存在，则创建，并获取用户输入的校园网账号和密码，写入文件，文件会被设置成`隐藏`。如果存在该文件，则从中读取账号和密码。  
&#8195;&#8195;将程序打包为`.exe`文件后放入开始菜单的启动文件夹中，程序会开机自动运行。每次运行时，检测设备是否连上了`bjfu-wifi`，如果没有连上，则会自动连接，并检测是否连接成功。  
&#8195;&#8195;如果`bjfu-wifi`处于连接状态，则检测校园网是否处于登录状态，如果没有登陆，则进行自动登录的操作。这是这个脚本的核心部分，登录的方法是获取登陆界面跳转后的url，取得其中的相关参数，将参数连同账号和密码提交到一个地址。提交方法是`requests.post(url, dict)`。提交后检测是否可以上网，即检测是否登录成功。  
&#8195;&#8195;如果设备处于联网并登录状态，则获取用户账户信息，例如剩余流量、包月类型等。这部分代码包含在`BJFUINFO`这个Class(类)里，由[Koonchung贡献](https://github.com/Koonchung/)，可以参考他的项目[BJFU_login](https://github.com/Koonchung/BJFU_login)。在其轮子的基础上，我做了一个显示`流量剩余百分比`的小改进。  
&#8195;&#8195;`PyColor`这个Class(类)用于程序运行时输出彩色的提示信息，可输出红黄绿三种颜色，例如`pcolor.printGreen(">>>>>开始运行...")`将在屏幕上输出绿色的文字。程序还加入了计时功能。  

## 打包成可执行的exe文件
使用[PyInstaller库](https://github.com/pyinstaller/pyinstaller)进行打包。  
安装方法  `pip install pyinstaller`  
打包方法：使用命令行，cd到.py脚本所在目录，`pyinstaller -F test.py`即可。`pyinstaller -i imag.ico -F test.py`可设置图标。  

## 依赖的第三方库
[requests](https://github.com/pyinstaller/pyinstaller)  
[pywifi](https://github.com/awkman/pywifi)  
[beautifulsoup4](https://pypi.org/project/beautifulsoup4/)  

## 关于作者
BJFU非计算机专业的一只野生猿，欢迎与我交流Python。(๑¯∀¯๑)


