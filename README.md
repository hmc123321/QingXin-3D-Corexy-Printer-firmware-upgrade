# 清心3D 单z Corexy 3D打印机固件升级
将此类型的打印机升级到 Marlin 2.0.x。  
这是某国产品牌`清心3D`的早期Corexy型3D打印机。  
![清心3D corexy](https://gd4.alicdn.com/imgextra/i4/676124885/TB2gLLWf3vD8KJjSsplXXaIEFXa_!!676124885.jpg "本机器")  

该机器使用的固件为Marlin1.0，过于古老难以接受，于是下决心更新其固件。[这是该机器的描述，但不是该公司的官方店铺](https://item.taobao.com/item.htm?spm=a230r.1.14.78.40dd2a97vibLN0&id=544475394126&ns=1&abbucket=10#detail)。  
该机器平台为单z轴，仅有y轴为线轨，其他均为8mm光轴。  
该店铺自称机器为“自研主板”，而且看起来确实很“自研”，因为做工一言难尽，甚至有一大坨2mm直径的焊锡搭在某MOS管的引脚上，反面更是有撬开铜皮的飞线！所以一直没敢轻易更新固件，因为不知道是Marlin固件中的哪块主板。  
在经过对多个引脚的比对后，从`Marlin\src\pins`中搜索到一块名为`Mega Controller`的主板能对上引脚定义，于是[查找到这一块](https://reprap.org/wiki/Mega_controller)
![BOARD_MEGACONTROLLER](https://reprap.org/mediawiki/images/thumb/8/83/Mega_controller_MiniPanel.JPG/720px-Mega_controller_MiniPanel.JPG "BOARD_MEGACONTROLLER")  
此主板正是该机器使用的，只不过清心的工程师对其进行了部分删减，诸如删掉了限位开关部分的一排GND。  
确定主板后工作就简单多了，于是有了这一版固件。固件删除了机器原版自带的不够精准的舵机探针，改为压电效应器,热床的控制方式改为了PID，增加了自定义启动界面。  
![压电效应器](https://gd1.alicdn.com/imgextra/i2/833130887/TB241L2XTnI8KJjSszbXXb4KFXa_!!833130887.jpg "压电效应器")  
后面由于尝试增加TMC2208的串口驱动，操作不当损坏主板，于是换成了手头多余的AnyCubic Trigorilla主板。  
大家如果要更改此固件为原版主板，只需要修改
```C
#define MOTHERBOARD BOARD_MEGACONTROLLER
...
#define X_MIN_ENDSTOP_INVERTING false
#define Y_MIN_ENDSTOP_INVERTING false
#define Z_MIN_ENDSTOP_INVERTING true 
...
#define Z_MIN_PROBE_ENDSTOP_INVERTING Z_MIN_ENDSTOP_INVERTING
```
即可。
