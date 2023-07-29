# Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx

![Sonoma](https://cdn.jsdelivr.net/gh/ianchen0713/PicGo@master/202307291018414.png)

## 什么是 CFG LOCK

CFG-Lock 是 BIOS 中的一项设置，允许写入特定的寄存器（在本例中为 MSR 0xE2）。默认情况下，大多数主板会锁定此变量，其中许多厂商甚至将选项直接隐藏在 GUI 中。而且，我们关心它的原因是 macOS 实际上要写入此变量，而不仅仅是 macOS 的一部分。包括内核和 AppleIntelPowerManagement。它定义了 CPU 的电源状态（C-States），这就是为什么它对于 macOS 必不可少的原因。如果没有写入 MSR 0xE2 的能力，则将丢失所有或大部分 CPU 电源管理，并且系统无法启动。

## 使用 RU 解锁 CFG LOCK & 设置 DVMT

准备一个 U 盘，格式化为 FAT32

> tips:U 盘分区表**必须**为 MBR (不能是 GUID) ，否则容易出现进不去 RU 的情况

解压 RU.zip，新建一个 EFI 文件夹，把 RU.zip 解压出来的 BOOT 文件夹放入 EFI 文件夹中，重启进入 RU

![RU.EFI](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/c383046db44e9e8e2744970924c0a585.png)

按 `ESC` - `ALT + '='` - 按 `↓` 一直找到 "CpuSetup" 回车进入

![CPUSetup](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/f1e6d84634287718d298705c866b2132.png)

我们需要修改的值，以下数值只使用于 HP PAVILION GAMING LAPTOP 15-dk0xxx

|        功能        | 位置  | 值  |     含义     |
| :----------------: | :---: | :-: | :----------: |
|     CFG UNLOCK     | 0x3E  |  0  |   Disable    |
| DVMT Pre-Allocated | 0x107 | 0x2 |  设置为 64M  |
| DVMT Total Gfx Mem | 0x108 | 0x3 | 设置为无上限 |

按 `Ctrl + W` 保存该值

![0x3E](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/0x3E.png)

按 `Ctrl+PGDN` 翻到下一页

![0x107](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/0x107.png)

每个位置的值都要修改，修改完成后出现下图弹窗即为修改成功

![CTRL+W](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/def7c28ba48597f5876c6e61821f33dd.png)

重启查看 CFG LOCK 是否解锁

打开 Hackintool，点击工具

![打开Hackintool](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/1.png)

查询结果 CFG Lock 为 0 即为解锁成功

![查询结果](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/2.png)

## 感谢

特别感谢群内两位大佬的热情指导
![感谢](https://cdn.jsdelivr.net/gh/ianchen0713/Hackintosh-HP-PAVILION-GAMING-LAPTOP-15-dk0xxx@main/images/7d52858eb83551ce6dced25ad8eb6134.png)

## 引用

-   [什么是 CFG LOCK](https://blog.daliansky.net/undefined.html)
-   [RU.EXE + RU.EFI](http://ruexe.blogspot.com/)
-   [【黑苹果】无法解锁的 CFG LOCK | 新技能 get !](https://www.bilibili.com/video/BV1LV4y1N7jF)
