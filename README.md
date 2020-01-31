# Hackintosh_Asus-H110s1_QL2X_DW1820A_OC
Hackintosh for Asus-H110s1, QL2X, DW1820A, using Opencore and Support macOS 10.15.2 

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

### Not working:
- Sleep  

### Not tested yet:
- 3.5mm Audio Output  
- DP port  
- 4k display  
- Airdrop  
- AirPlay  
- Continuity  
  
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
- 0x59120000: Three ports (1 DP, 2 HDMI) on motherboard working, but two HDMI ports can't display well (appear purple in color). **Support HEVC**
- 0x591b0000: Two ports (1 DP, 1 HDMI close to DP) on motherboard working, but one HDMI port have no output. **Support HEVC.**

I still try to fix this problem.

---
# Performance
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/13EE6E89-9978-4196-BB65-22C892472BAA_1_105_c.jpeg?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/8CB768EC-7D4C-49EA-9FDE-12661C0B0B63_1_105_c.jpeg?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.12.45.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.40.26.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.58.51.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午4.54.32.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午5.00.46.png?raw=true)
![image](https://github.com/Road00/Hackintosh_Asus-H110s1_QL2X_DW1820A_OC/blob/master/Figure/截屏2020-01-27下午5.01.24.png?raw=true)
