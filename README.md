# Hackintosh_Asus-H110s1_QL2X_DW1820A_OC
Hackintosh for Asus-H110s1, QL2X, DW1820A, using Opencore and Support macOS Catalina    

**使用EFI前请务必修改三码(SSN,UUID,ROM)**    
**Please change three system codes (SSN,UUID,ROM) before using this EFI**   

---

I'm so sorry, it's the lastest time to update this EFI for this Hardware(QL2X).    
Because I alreadly change to use I3-8100.     
But I found some ways to fix the display problem like appear purple in color:    

1. Try to Display Injector using Hackintosh.
2. Try to force RGB mode.

Reference linking:

- [MacOS強制外接螢幕輸出RGB](https://blog.driftking.tw/2018/10/MacOS%E5%BC%B7%E5%88%B6%E5%A4%96%E6%8E%A5%E8%9E%A2%E5%B9%95%E8%BC%B8%E5%87%BARGB/)
- [Force RGB mode in Mac OS X to fix the picture quality of an external monitor](https://www.mathewinkson.com/2013/03/force-rgb-mode-in-mac-os-x-to-fix-the-picture-quality-of-an-external-monitor)
- [Dell U2713H on Mac: forcing RGB mode instead of YCbCr](https://embdev.net/topic/284710)

---

2020-04-17 更新：

- Update LiLu to 1.4.3    
- Update Whatevergreen to 1.3.9     
- Update AppleALC to 1.4.8     
- Update CPUFriend to 1.2.0    
- Update NVMeFix to 1.0.2
- Update VirtualSMC to 1.1.2

---

2020-04-01 更新：

- Already support to Catalina 10.15.4    
- Update Whatevergreen to 1.3.8-DEBUG-t3 (Fix HDMI bug)     
- Update Opencore to 0.5.6     

---

Already upgrade to Catalina 10.15.3

---

2020-02-20 更新：

- 修复USB3.0接口， 现在USB-C和两个USB3.0速率正常了。

---

2020-02-18 更新：  

- 显卡ID改为 0x193b0005 ｜ MacBookPro13,1 ｜ Intel HD Graphics 530/4K  

	牺牲HEVC硬解，但是所有视频输出接口工作正常  

- 增加 **LogoutHook** 文件用于模拟NVRAM，请在安装完系统后将该文件夹放置在任意位置。并且在终端输入 ```sudo defaults write com.apple.loginwindow LogoutHook /path/to/LogoutHook.command```

	比如你放在**下载**文件夹内： ```sudo defaults write com.apple.loginwindow LogoutHook /Users/xjn/Documents/LogoutHook/LogoutHook.command```

	重启后，你会在/EFI/下看到nvram.plist，代表已经成功模拟了。

	**！运行后不要删除补丁包 ！**

- 如果认为支持HEVC硬解更重要，可以下载 [EFI-630.zip](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/raw/master/EFI-630.zip)。 此EFI显卡ID设置为 0x59120000 ｜iMac18,2 ｜	Intel HD Graphics HD630  

	**！ 此EFI仅中间的HDMI接口可以使用 ！**
	
- 定制USB接口，修复USB-C接口（现在可以正反插），修复USB充电（现支持苹果快充）   

- 地区代码从```HK```改为```#a```, 修复Wi-Fi只能到300m的bug  

---

# Hardware/硬件
|  | Specifications / 型号 | Note / 备注 |
|-------------------------|:---------------------------------:|:-------------------------------:|
| Motherboard/主板: | Asus H110s1 | (mini STX) |
| CPU/处理器: | QL2X | (7820HK modify from BGA to LGA) |
| CPU Cooler/散热器: | NOCTUA NH-L9i |  |
| Hard Drive/硬盘: | Hikvision C2000pro 512gb |  |
| RAM/内存: | JUHOR 16G DDR4 2666MHz X2 |  |
| Wireless Card/无线网卡: | BCM94350ZAE | (DW1820A) |
| Tower Case/机箱: | SilverStone VT02 |  |
| Power/电源: | 55/25mm 19v 120w DC power adapter |  |
  
---
# Functions/功能
### Work：
- 1080p display support one HDMI port (close to DP port)  
- Audio output on HDMI  
- All USB ports  
- Wi-Fi & Bluetooth  
- 3.5mm Audio Output & Mic Input
- Airdrop  
- AirPlay  
- Continuity  

### Not working:
- Sleep  

### Not tested yet:
- DP port  
- 4k display  
  
---

# BIOS setting/BIOS设定：

### Disable：
- Fast Boot  
- CFG Lock   
- VT-d  
- CSM  
- Intel SGX  

### Enable：
- VT-x  
- Above 4G decoding  
- Hyper Threading  
  
---
  
# More Detail for QL2X

QL2X is a **Engineering Sample(ES)** version CPU for 7820HK with HD630, 7820HK is a laptop processor, it be modified from BGA socket to LGA socket and make 7820HK can use into desktop platform. So it buring some problem to drive the graphics card in hackintosh.

7820HK was using in Macbook pro 14,3 (15 inch,2017).

I try three ig-platform-id for QL2X: 
 
- 0x19120000 (skylake HD530 with 3 DP ports)  
- 0x59120000 (kabylake HD630 with 3 DP ports, use in iMac18,2)  
- 0x591b0000 (kabylake HD630 with 1 LVDS port and 2 DP ports, use in MacBookPro14,3)    

Result: 

- 0x19120000: Three ports (1 DP, 2 HDMI) on motherboard working. **Unsupport HEVC**
- 0x59120000: Two ports (2 HDMI) on motherboard working, but two HDMI ports can't display well (appear purple in color). **Support HEVC**
- 0x591b0000: One ports (1 HDMI close to DP) on motherboard working, another HDMI port have no output. **Support HEVC**

**!!More importantly!!**

To using QL2X into desktop platform, we need to close the **ME** in BIOS. It make MacOS cannot wake up graphics card after sleep. So this platform can't sleep.

Because ME was closed in BIOS, we need to add ```-disablegfxfirmware``` in ```boot-arg```

I still try to fix this problem later.

---
# 关于QL2X的更多细节

QL2X 是 7820HK 的ES版本CPU， 核显为HD630。 7820HK是个笔记本平台的CPU，大佬通过魔改接口让它可以工作在桌面平台。这很自然会带来一些问题在黑苹果的时候。

首先，7820HK 曾经被用在 Macbook pro 14,3 (15 inch,2017) 平台上。

为了驱动这块 QL2X 的核显，我尝试了3个ig-platform-id：  
- 0x19120000 (skylake平台 核显为HD530  原生驱动3个DP接口)  
- 0x59120000 (kabylake 平台 核显为HD630 原生驱动3个DP接口, 用于iMac18,2)  
- 0x591b0000 (kabylake 平台 核显为HD630 原生驱动 1个LVDS接口 和 2个DP接口, 用于MacBookPro14,3)    

对应了3个结果：

- 0x19120000: 主板上的3个接口 (1 DP, 2 HDMI) 都正常工作，但是**不支持HEVC硬解**
- 0x59120000: 主板上的2个接口 (2 HDMI) 都工作, 可是2个HDMI接口输出都有问题(紫屏)。不过**支持HEVC硬解**
- 0x591b0000: 主板上的1个接口(1 HDMI 靠近DP那个) 工作正常, 剩下那个HDMI接口无输出。**支持HEVC硬解**

**另外很重要的是：**

为了让QL2X可以在桌面平台上使用，我们需要关闭BIOS中的ME。这会导致macOS系统无法在睡眠后唤醒显卡。导致这套系统无法睡眠。

同时，因为 BIOS 中的 ME 被关掉了, 我们需要在 ```boot-arg``` 中添加 ```-disablegfxfirmware``` 

我以后会尝试解决这些问题。

---
# Performance/展示

![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/13EE6E89-9978-4196-BB65-22C892472BAA_1_105_c.jpeg?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/8CB768EC-7D4C-49EA-9FDE-12661C0B0B63_1_105_c.jpeg?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.12.45.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.40.26.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/%E6%88%AA%E5%B1%8F2020-02-18%E4%B8%8B%E5%8D%886.58.19.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.58.51.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.54.32.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午5.00.46.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午5.01.24.png?raw=true)

---
# Reference/参考

[精解OpenCore](https://blog.daliansky.net/OpenCore-BootLoader.html) - [黑果小兵的部落阁 ](https://blog.daliansky.net/)

[使用OpenCore引导黑苹果](https://blog.xjn819.com/?p=543) - [XJN](https://blog.xjn819.com/) 

[Asrock deskmini 310-com hackintosh 10.14-10.15 EFI](https://blog.xjn819.com/?p=7) - [XJN](https://blog.xjn819.com/)

[分享EFI 华硕H110S1 STX主板 i3-8100 UHD630](http://bbs.pcbeta.com/viewthread-1801615-1-1.html) - [mike20080924](http://i.pcbeta.com/space-uid-3336274.html)

[DW1820A/BCM94350ZAE/BCM94356ZEPA50DX插入的正确姿势](https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html) - [黑果小兵的部落阁](https://blog.daliansky.net/)
