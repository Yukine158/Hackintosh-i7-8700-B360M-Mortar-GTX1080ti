记录一个初心者的黑苹果安装历程

# 我的配置

| 硬件     | HARDWARE     | 型号                            |
| -------- | ------------ | ------------------------------- |
| 主板     | Motherboard  | MSI B360M Mortar (BIOS 7B23v16) |
| CPU      | CPU          | Intel i7-8700                   |
| 内存     | RAM          | Adata DDR4 2666MHz 8G*2         |
| 显卡     | Graphic Card | Gigabyte Aorus GTX1080Ti 11g    |
| 硬盘     | Storage1     | WD SN550 M.2 NVME 512G          |
| 硬盘     | Storage2     | HGST HTS721010A9E630 1T         |
| 硬盘     | Storage3     | TOSHIBA Q200EX M.2 SATA 256G    |
| 板载网卡 | Onboard LAN  | Intel I219-V                    |
| 显示器   | Monitor      | Acer KG241YU                    |
| 拓展坞   | USB Hub      | Belkin Type-C Hub F4U092btSGY   |
| 键盘     | Keyboard     | FILCO Minila with wire          |
| 鼠标     | Mouse        | Razer Lancehead                 |

# 功能实现

主板及CPU

板载网卡

显卡

iTunes/ App Store/ iCloud

# 待实现

板载声卡 Realtek ALC892

iMessage/ Facetime

# EFI说明

## Config.plist

DSDT FIX 适用BIOS版本高于7B23v16

HDAS to HDEF 用于模拟Nvram

Product Name选择iMac18,2

Board Serial Number, S/N, SmUUID待使用者自行生成

## Clover

使用Clover时，勾选-verbose（用于确定问题）Set Nvidia to VESA

 # 显卡驱动

Mac OS High Sierra 10.13.6 (17G66)无原生Nvidia Webdriver

1.下载WebDriver-387.10.10.10.40.133并打开

2.记录错误页面的BuildNumber (17G10021等)

3.打开终端

4.输入sudo nano -w /System/Library/CoreServices/SystemVersion.plist

5.修改本机BuildNumber为Webdriver BuildNumber

6.保存plist

7.安装Webdriver

8.修改回原BuildNumber

9.开EFI的config.plist

10.引导参数栏添加nvda_drv=1

11.重新启动

# iTunes/ App Store

需更新iTunes版本至12.8.2

# Annex 黑苹果安装指南

1.Windows系统下事前准备

2.Mac OS High Sierra 10.13.6 (17G66)系统安装文件 （检查md5）

3.Diskgenius （用于windows下操作EFI分区）

4.ProperTree （修改plist）

5.Etcher （制作启动u盘）

6.EFI和BOOT文件夹 （替换EFI分区同名文件夹）

## BIOS设置

SETTINGS\高级\PCI子系统设置\Above 4G memory/Crypto Currency mining [允许]

SETTINGS\高级\内建显示配置\设置第一显卡 [PEG]（仅同时拥有核显及独显需要手动设置） SETTINGS\高级\内建显示配置\集显共享内存 [64M]（如果使用拥有核显的处理器） SETTINGS\高级\内建显示配置\集成显卡多显示器 [允许]（如果使用拥有核显的处理器）

SETTINGS\高级\ACPI设置\电源 LED 灯 [双色]（如果选择 [闪烁]，睡眠时电源灯将不断闪烁）

SETTINGS\高级\整合周边设备\SATA设置\SATA模式 [AHCI模式]（如果选择 Optane 模式则无法识别硬盘）

SETTINGS\高级\USB设置\XHCI Hand-off [允许] SETTINGS\高级\USB设置\传统USB支持 [允许]

SETTINGS\高级\电源管理设置\ErP Ready [允许]

SETTINGS\高级\Windows操作系统的配置\Windows 10 WHQL支持 [允许]（开启为「纯」UEFI 模式，否则为「兼容」UEFI 模式，推荐设置为允许） SETTINGS\高级\Windows操作系统的配置\MSI 快速开机 [禁止] SETTINGS\高级\Windows操作系统的配置\快速开机 [禁止]

SETTINGS\高级\唤醒事件设置\唤醒事件管理 [BIOS] SETTINGS\高级\唤醒事件设置\USB设备从S3/S4/S5唤醒 [允许]

SETTINGS\启动\启动NumLock状态 [关]（macOS 默认可使用数字键盘，只有 macOS 的话推荐关闭） SETTINGS\启动\启动模式选择 [UEFI]

OC(Overclocking)\CPU 特征\Intel 虚拟化技术 [允许]（必须） OC(Overclocking)\CPU 特征\Intel VT-D 技术 [禁止]（必须） OC(Overclocking)\CPU 特征\CFG锁定 [禁止]（必须）

## etcher

使用etcher写入系统安装文件

## Diskgenius

打开Diskgenius，分配驱动器号给EFI分区，备份并删除原EFI及BOOT文件夹，粘贴EFI及BOOT文件夹。

## 引导

使用U盘进入Clover，选择从U盘安装mac OS，按空格选择-verbose及Set Nvidia to VESA。

## 安装

进入mac OS安装界面，抹除磁盘为mac扩展日志式，返回安装mac os。如遇到“提示应用程序副本已损坏”，进入终端，输入命令date 110713212015.30，即可返回安装。

自动重启，再次进入Clover，选择boot mac os from [disk name]，按空格选择-verbose及Set Nvidia to VESA，安装自动继续进行。

再次重启，选择boot mac os from [disk name]，按空格选择-verbose及Set Nvidia to VESA，安装自动继续进行，随后可设置管理员账户及密码。

安装Nvidia Webdriver，并重启。

# 大体为以上步骤，待更新20210215









