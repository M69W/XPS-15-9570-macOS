 [中文](README_CN.md) |
 [中文教程](xps%209570黑苹果安装教程(更新中).docx)

 - `OC` from QQ群友 @毒舌のロリコン，here is a backup
 - `OC-0.5.6-MOD-UI-HDMI` base on [xxxzc's OC](https://github.com/xxxzc/xps15-9570-macos/releases/tag/200118-1) change a liittle for HDMI Output with [0.5.6 mod OC](http://bbs.pcbeta.com/viewthread-1838814-1-1.html) 
 - `clover`  too long time to forget base on what it is.


### More Information See  
### CLOVER  
https://github.com/bavariancake/XPS9570-macOS  
https://github.com/Xigtun/xps-9570-mojave  
https://github.com/LuletterSoul/Dell-XPS-15-9570-macOS-Mojave  
https://github.com/smallssnow/XPS9570-8570H-macos  
https://github.com/AnneviLL/xps15-9570-hackintosh-EFI  
### OC  
https://github.com/xxxzc/xps15-9570-macos  
https://github.com/OldDream/Dell-XPS-15-9570-macOS-Mojave  


[ Modify macOS CPU Performance](https://github.com/stevezhengshiqi/one-key-cpufriend) as needed.

Put Touchpad driver into L/E(or S/L/E) and rebuild the kext cache  
`sudo cp -R VoodooI2CHID.kext /Library/Extensions`  
`sudo cp -R VoodooPS2Controller.kext /Library/Extensions`  
`sudo cp -R VoodooI2C.kext /Library/Extensions`  
`sudo kextcache -i /`  



Thanks to:   
Austere.J(@FireWolf), @bavariancake @Xigtun @LuletterSoul @9570 4k and so on
  
https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-hdmi-output-issue-public-testing-stage.275126/  
https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-kernel-panic-due-to-divide-by-zero.261687/  
https://www.tonymacx86.com/threads/fix-coffee-lake-intel-uhd-graphics-630-on-macos-mojave-hdmi-output-issue-public-testing-stage.275126/
