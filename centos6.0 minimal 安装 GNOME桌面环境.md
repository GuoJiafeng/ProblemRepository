<https://blog.csdn.net/hotday_kevin/article/details/8310054>

****#yum groupinstall "X Window System"

**** yum  groupinstall "Desktop"



~~~~
4.安装KDE桌面环境

yum groupinstall "KDE (K Desktop Environment)"

yum groupinstall "KDE Desktop"

5.卸载GNOME桌面

yum groupremove "GNOME Desktop Environment"

6.卸载KDE桌面环境

yum groupremove "KDE (K Desktop Environment)"

开机为文本界面，由文本界面切换到图形界面：

方法1：运行命令

#startx ， 需要先配置图形界面信息

方法2：修改/etc/inittab文件中的

id:3:initdefault ， 将3改为5 ，重新启动系统；

方法3：进入图形界面： init 5

从图形界面进入文本界面： init 3

重启： init 6

关机： init 3

真机环境中，在图形界面和文本界面间快捷键切换：

Ctrl+Alt+F(n) , 其中F(n)为F1-F6 ，为6个控制台；

Ctrl+ALT+F7 ；

eg:CTRL+ALT+F1是进入文本界面，CTRL+ALT+F7才是图形
~~~~

