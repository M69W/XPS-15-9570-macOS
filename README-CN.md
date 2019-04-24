## XPS 9570黑苹果教程，更新中(2019-04-24)

### Window 下准备：
下载软件和镜像
制作U盘 软件TransMac：百度或官网 https://www.acutesystems.com/scrtm.htm

镜像(10.14.4): 选一，或自行官网下载  
黑苹果小兵https://blog.daliansky.net/  macOS-Mojave-10.14.4-18E226-official-version-with-Clover-4903-original-image.html  
远景论坛版主：  
1.【Len's DMG】macOS Mojave 10.14.4正式版 18E226  With Clover 4903原版镜像 http://bbs.pcbeta.com/viewthread-1809650-1-1.html  
2.【Len's DMG】macOS Mojave 10.14.4 18E2034  With Clover 4907 iMac2019九代特别版 http://bbs.pcbeta.com/viewthread-1809790-1-1.html  

### 制作U盘：  
步骤搜百度先，下次更新  
或看这个 http://www.xitongcheng.com/jiaocheng/xtazjc_article_41339.html  
或看apple官网教程，略  

### 设置BIOS：  
1.Xps 9570 默认硬盘是radio on模式，需改radio on 为achi: (为何要设置？因知识盲区，待完善)  
不重装系统改硬盘模式 RAID ON 改成AHCI：https://www.chiphell.com/thread-1678085-1-1.html  
2.设置Clover 启动  
F2进入BIOS设置：  
1.Secure Boot - Secure Boot Enable里改成Disabled  
![setting](./images/图2.png)  

2.设置U盘 启动 Clover  
![setting](./images/图2.png)  
![setting](./images/图2.png)  
![setting](./images/图2.png)  
选CLOVER  
![setting](./images/图2.png)  

选CLOVERX64.efi, OK  
![setting](./images/图2.png)  
![setting](./images/图2.png)  





macOS 安装过程，略  
视情况而定：  
特别注意的是小兵镜像：（在以往的安装过程中）  
第一安装选择默认第一项，安装中途会重启报错，  
第一次安装后的重启，选中你安装的那个硬盘名字重启，  
可能会有几次重启，复制此操作即可。  

安装后进入系统：  
默认先用安装的Clover 进入系统，  

Window下  
最终目的是硬盘启动，放Clover到ESP /EFI 下  
打开DiskGenius，  
![setting](./images/图2.png)  
教程中有多硬盘和多个EFI分区，是视情况而定，默认是第一个  
![setting](./images/图2.png)  
![setting](./images/图2.png)  
![setting](./images/图2.png)  
这样就完成了window下将Clover放入硬盘的操作。  

### macOS下
放Clover 到硬盘（非U盘），硬盘启动  
打开 Clover Configurator（下面有下载链接，官网已出中文版），  
找到Tools 的第一行【Mount EFI】，一般来说，有多少个EFI分区这里就显示多少个。  
一个硬盘就一个EFI，插入U盘时U盘的EFI分区也会在这里显示，（找到你的window 默认的那个，如果是多硬盘多系统，  
也可以放非window 默认的分区下。），题外，没有EFI分区，请自己百度。  
![setting](./images/图2.png)  
![setting](./images/图2.png)  

如果下载的CLVOER 不对应，需修改一个地方  
![setting](./images/图2.png)  
![setting](./images/图2.png)  

这里的补丁感兴趣看这里  
https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-hdmi-output-issue-public-testing-stage.275126/    

https://github.com/bavariancake/XPS9570-macOS/commit/64c16d9bd88620e54f5aa987fec829c90cb37a26    

https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-kernel-panic-due-to-divide-by-zero.261687/     

![setting](./images/图2.png)  
![setting](./images/图2.png)  



至此，就完成了macOS下替换Clover操作，重启一般就可以了。  

但，目前，触摸板驱动(截至2019/04/06, 请下载群里最新的)还需大家进一步完善。  
可能会导致开机进不了系统，重启几次也是可以的。  
这里的解决方法是在进入macOS下将触摸板驱动放L/E 下，（也可以放S/L/E下）  
此处为终端操作，主要是考虑到没有联网，内置软件操作会方便点。  
可以借助软件操作，软件操作略(待完善)。  
找到并打开【启动台】(logo是小火箭)，【其他】，【终端】  
下面只是示范，·目的是使用终端和命令，把触摸板驱动放到指定目录下，重建缓存·。 
![setting](./images/图2.png)   

驱动在xps9570-Touchpad 目录下，鼠标拖这个文件夹到终端，如下：  
![setting](./images/图2.png)  

然后方向键定位到最前，如下：  
![setting](./images/图2.png)  
输入cd 空格,即：   
![setting](./images/图2.png)  
回车后显示：表示当前目录是这个文件夹下。  
![setting](./images/图2.png)  
看下是不是有三个驱动,命令ls,回车，显示如下  
![setting](./images/图2.png)  
然后执行下面的命令（每次一条，第一次需输入密码，最后一条是重建缓存的命令）  
把三个触摸屏驱动放在了L/E，（也可以放S/L/E下）  
`sudo cp -R VoodooI2C.kext /Library/Extensions`  
`sudo cp -R VoodooI2CHID.kext /Library/Extensions`    
`sudo cp -R VoodooPS2Controller.kext /Library/Extensions`    
`sudo kextcache -i /`  
至此，操作驱动到L/E的操作结束。  
可以将config.plist里去掉-v(啰嗦模式)，不操作此步骤也可以  
最后，重启即可  

### 题外：  
S/L/E或L/E的驱动替换变动，请记得一定要重建缓存  
找到并打开【启动台】(logo是小火箭)，【其他】，【终端】，输入  
`sudo kextcache -i /`  
回车，需输入安装时设置的密码。此步骤也可以使用软件Kext Utility或其他软件要执行，只要达到重建缓存的目的就好。  

如果使用Clover Configurator 打开的，记得卸载EFI分区。  
不卸载有什么问题吗，请自测，但不建议，此处为知识盲区，不解释。  

### 网络：
XPS 9570目前需换内置网卡，如DW1560，DW1830等  
群里有官网的拆机教程  

不换网卡可以用安卓热点（USB联网）连接上网，  
需要HoRNDIS.kext（下面有链接），可以放CLOVER/kexts/Other下重启生效，  
记得手机开USB 联网。  
下载安装，如下  
Android USB tethering driver for Mac OS X  
https://github.com/jwise/HoRNDIS/releases   
https://www.joshuawise.com/horndis  (offical website how to use  
https://www.waerfa.com/horndis   

题外，如果是用安装包安装后想直接提取HoRNDIS.kext驱动的方法  
终端，输入`open /Library/Extensions`,回车。打开的目录下找到HoRNDIS.kext。  

外设有线网卡需要下载对应的驱动才能使用！  
OS X driver for Intel onboard LAN   
https://github.com/RehabMan/OS-X-Intel-Network   
https://bitbucket.org/RehabMan/os-x-intel-network/downloads/  



下面可能有需要？    

Clover  
stable release  
https://sourceforge.net/projects/cloverefiboot/files/Installer/   

unofficial(last issue)  
https://github.com/Dids/clover-builder/releases   
更新Clover，更新这个CLOVERX64.efi即可  


Download Clover Configurator  
https://mackie100projects.altervista.org/download-clover-configurator/   

Lilu  
https://github.com/acidanthera/Lilu/releases   

Existing Lilu plugins  
https://github.com/acidanthera/Lilu/blob/master/KnownPlugins.md   

AppleALC  
https://github.com/acidanthera/AppleALC/releases   

WhateverGreen  
https://github.com/acidanthera/WhateverGreen/releases   

kextupdater  
https://bitbucket.org/profdrluigi/kextupdater/downloads/   

FakeSMC  
https://github.com/RehabMan/OS-X-FakeSMC-kozlek   
https://bitbucket.org/RehabMan/os-x-fakesmc-kozlek/downloads/   

VirtualSMC  
https://github.com/acidanthera/VirtualSMC/releases   
https://github.com/acidanthera/VirtualSMC/blob/master/Docs/FAQ.md   
Virtual SMC on MOJAVE
https://www.tonymacx86.com/threads/virtual-smc-on-mojave.262360/   

CPUFriend  
https://github.com/acidanthera/CPUFriend/releases   

NoTouchID
https://github.com/al3xtjames/NoTouchID/releases 

OS X driver for Intel onboard LAN   
https://github.com/RehabMan/OS-X-Intel-Network   
https://bitbucket.org/RehabMan/os-x-intel-network/downloads/  


SmartTouchpad()  
https://osxlatitude.com/forums/topic/1948-elan-focaltech-and-synaptics-smart-touchpad-driver-mac-os-x/ 

Android USB tethering driver for Mac OS X  
https://github.com/jwise/HoRNDIS/releases   
https://www.joshuawise.com/horndis  (offical website how to use  
https://www.waerfa.com/horndis   
How to get the kexts  
`brew cask install horndis`  
`sudo kextload /Library/Extensions/HoRNDIS.kext`  
can find HoRNDIS.kext in /Library/Extensions/HoRNDIS.kext  

awesome-mac  
https://github.com/jaywcjlove/awesome-mac/blob/master/README-zh.md   

CPU 查看变频(intel-power-gadget)  
https://software.intel.com/en-us/articles/intel-power-gadget-20   

调整 macOS CPU性能  
https://github.com/stevezhengshiqi/one-key-cpufriend  


PlistEdit Pro  
https://www.fatcatsoftware.com/plisteditpro/   
https://www.icopybot.com/download.htm  (for window  

videoproc  
https://www.videoproc.com/download/videoproc.dmg   

Clover Configurator
https://mackie100projects.altervista.org/download-clover-configurator/ 

Hackintool formerly Intel FB-Patcher  
Download Hackintool  
http://headsoft.com.au/download/mac/Hackintool.zip   
http://headsoft.com.au/download/mac/FBPatcher.zip  (formerly Intel FB-Patcher  
https://www.insanelymac.com/forum/topic/335018-hackintool-v174/   
https://blog.daliansky.net/Intel-FB-Patcher-tutorial-and-insertion-pose.html   

MaciASL  
https://github.com/RehabMan/OS-X-MaciASL-patchmatic   
https://github.com/acidanthera/MaciASL   

Kext Utility  
http://cvad-mac.narod.ru/index/0-4   
http://cvad-mac.narod.ru/files/Kext_Utility.app.v2.6.6.zip   


触摸板  
https://www.tonymacx86.com/threads/voodooi2c-help-and-support.243378/  

VoodooI2C编译教程  
https://www.penghubingzhou.cn/2019/01/24/VoodooI2C%20Build/  


[GUIDE] Installing 3rd Party Kexts - El Capitan, Sierra, High Sierra, Mojave +
https://www.tonymacx86.com/threads/guide-installing-3rd-party-kexts-el-capitan-sierra-high-sierra-mojave.268964/   
例如触摸板驱动放`L/E`  
在other的上一级文件夹下（打开 terminal ，把驱动所在的文件夹拖进 terminal，方向键定位到最左，输入cd,输入空格，回车）  
`sudo cp -R VoodooI2C.kext /Library/Extensions`  
`sudo cp -R VoodooI2CHID.kext /Library/Extensions`  
`sudo cp -R VoodooPS2Controller.kext /Library/Extensions`  
`sudo kextcache -i /`  
至此，config.plist可以去掉-v(啰嗦模式)  

An iDiot's Guide To Lilu and its Plug-ins  
https://www.tonymacx86.com/threads/an-idiots-guide-to-lilu-and-its-plug-ins.260063/ 

### 双系统时间  
Windows将这个时钟作为本地时间来看待，也就是CMOS时间就是北京时间。  
MacOSX将这个时钟作为Coordinated Universal Time (UTC) 世界标准时间看待，也就是Greenwich Mean Time (GMT) 格林威志时间。  
所以如果你在MacOSX和Windows都选北京时间作为本地时区是，  
一旦连到互联网上，同步过时间后，就会造成时间的不一致。  

windows10 管理员身份运行 cmd (搜索‘cmd’，右键管理员运行)  
`Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1`

### 调整 macOS CPU性能	调整 macOS CPU性能   
https://github.com/daliansky/XiaoMi-Pro/blob/master/one-key-cpufriend/README_CN.md  

### 字体发虚  
一键开启 macOS HiDPI    
https://github.com/xzhih/one-key-hidpi/blob/master/README-zh.md   
https://comsysto.github.io/Display-Override-PropertyList-File-Parser-and-Generator-with-HiDPI-Support-For-Scaled-Resolutions/   

macOS Mojave 字体渲染由默认的灰度抗锯齿改回之前的次像素抗锯齿   
https://lvii.github.io/system/2018-09-26-setting-macos-mojave-font-rendering-from-grayscale-to-subpixel-antialiasing/  

### 任何来源  
1.打开「终端」：应用程序->实用工具->终端；   
2.粘贴下面的命令:  
`sudo spctl --master-disable`     
回车，输入你的系统密码:  
3.再次打开安全设置选项，就会发现「任何来源」选项回来了  

### Mac os 10.14.x 取消4位数密码限制  
默认至少4位数密码  
打开终端输入：  
`pwpolicy -clearaccountpolicies`  
然后  
`passwd`  
便可以自由更改密码啦  

XPS 9570黑苹果例子  
https://github.com/bavariancake/XPS9570-macOS   
https://github.com/Xigtun/xps-9570-mojave   
https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave  (以上二者的集合)  
FireWolf OS X PE 9，火狼 macOS PE 系列的第九个版本，  
是基于 macOS 原版镜像制作的增强型维护系统。  
PE 提供原生的 HFS 以及 APFS 文件系统的读写操作。  
内置的实用工具以及维护套件可帮助你在无法启动主系统时访问转移个人文件、恢复系统备份、修复系统磁盘权限、编辑 ACPI 表等。  
https://pe.firewolf.app/cn/   
https://pe.firewolf.app/manual  (简体中文版使用手册)    

可能会用到的网站  
https://www.insanelymac.com   
https://www.tonymacx86.com   
https://www.osx86.net/   
http://bbs.pcbeta.com/forum.php?gid=86   
https://clover-wiki.zetam.org/zh-CN/zh-CN.home   
https://clover-wiki.zetam.org/zh-CN/FAQ   
https://www.osx86.net/files/file/49-clover-configurator   
https://github.com/RehabMan   
https://sourceforge.net/projects/voodoohda/files   
以上都是来自网上。  

为了快速定位到问题源头，  
不要只说问题！！！  
不要只说问题！！！  
不要只说问题！！！  
不然请随时接受被忽视吧，因为可能别人真不知道你在说什么！  

一般情况下：  
1.你的预期目的；  
2.你的操作过程;  
3.你遇到的问题。  

例如  
我的配置：  
截图配置或配置单(CPU，SSD，显卡，网卡，声卡，显示屏等)；如xps 9570 1080P  
我的操作：  
比如说用的是哪个系统或镜像、哪份Clover、在什么系统下怎么操作 BIOS 的、U盘 制作的步骤、Clover 引导的操作、config 的修改参数等等，  
越详细越好，最好就是能提供截图或贴下代码或相关的文件或链接，这样能更好的定位问题。  
我遇到的问题：  
描述问题现象，比如说显示报错的代码，能复制出来的或打印的 log 日志或者截图，以便他人定位问题。  


### 黑苹果有风险，请对自己的行为负责！  