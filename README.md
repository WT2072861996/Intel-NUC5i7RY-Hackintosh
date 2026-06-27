# 🖥️ Intel NUC5i7RY · OpenCore Hackintosh

**Intel Core i7-5557U · Iris Graphics 6100 · Broadwell · OpenCore 1.0.x**

<div align="center">

![CPU](https://img.shields.io/badge/CPU-i7_5557U_Broadwell-0071C5?style=flat-square)
![GPU](https://img.shields.io/badge/GPU-Iris_6100-0071C5?style=flat-square)
![RAM](https://img.shields.io/badge/RAM-16_GB_DDR3L-8B5CF6?style=flat-square)
![OpenCore](https://img.shields.io/badge/OpenCore-1.0.x-9cf?style=flat-square)
![Chipset](https://img.shields.io/badge/Chipset-Wildcat_Point_LP-00A3E0?style=flat-square)
![Status](https://img.shields.io/badge/Status-Working-brightgreen?style=flat-square)

**[🖥️ 硬件配置](#-硬件配置) · [⚙️ BIOS 设置](#%EF%B8%8F-bios-设置) · [✅ 驱动状态](#-驱动状态) · [📦 EFI 配置](#-efi-配置) · [🚀 快速开始](#-快速开始) · [📸 截图](#-截图)**

</div>

---

## 🖥️ 硬件配置

| 组件 | 型号 | 规格 | 驱动情况 |
|:-----|:-----|:-----|:--------:|
| **型号** | Intel NUC5i7RY | NUC 迷你主机 | ✅ |
| **主板** | INTEL NUC5I7RY | Wildcat Point-LP (Broadwell) | ✅ |
| **CPU** | Intel Core i7-5557U | 2C/4T @ 3.10-3.40 GHz | ✅ 睿频正常 |
| **核显** | Intel Iris Graphics 6100 | 8086:162B, 48EU | ✅ 硬件加速 |
| **内存** | 双通道 DDR3L SO-DIMM | 16 GB @ 1600 MHz (8 GB × 2) | ✅ |
| **存储** | Samsung SSD 860 EVO | 250 GB SATA SSD | ✅ |
| **声卡** | Realtek ALC283 | HDA: 10EC-0283 | ✅ |
| **有线网卡** | Intel I218-V | 1 Gbps | ✅ |
| **Wi-Fi** | Intel Dual Band Wireless-AC 7265 | 8086-095A | ⚠️ 需 AirportItlwm |
| **蓝牙** | Intel 无线 Bluetooth | 8087-0A2A | ⚠️ 需 IntelBluetoothFirmware |
| **USB 3.0** | Intel xHCI | 8086-9CB1 | ✅ |
| **USB 2.0** | Intel EHCI | 8086-9CA6 | ✅ |

---

## ✅ 驱动状态

| 功能 | 状态 | 功能 | 状态 |
|:-----|:---:|:-----|:---:|
| **Iris 6100 核显** | ✅ | **GPU 硬件加速** | ✅ |
| **Intel I218-V 有线网卡** | ✅ | **Realtek ALC283 声卡** | ✅ |
| **USB 2.0/3.0** | ✅ | **SATA SSD** | ✅ (TRIM 支持) |
| **CPU 睿频** | ✅ | **XCPM 电源管理** | ✅ |
| **HDMI 视频输出** | ✅ | **MiniDP 视频输出** | ✅ |
| **睡眠/唤醒** | ✅ | **NVRAM** | ✅ |
| **Wi-Fi (Intel 7265)** | ⚠️ | **蓝牙 (Intel)** | ⚠️ |

---

## ⚙️ BIOS 设置

| 设置 | 值 | 说明 |
|:-----|:---:|:-----|
| **Secure Boot** | Disabled | macOS 不支持 |
| **Fast Boot** | Disabled | 避免启动问题 |
| **VT-x** | Enabled | 虚拟机支持 |
| **VT-d** | Disabled | 或添加 `dart=0` |
| **UEFI Boot** | Enabled | |
| **SATA Mode** | AHCI | SSD 最优性能 |

> 进入 NUC BIOS 方法：开机按 F2

---

## 📦 EFI 配置

### Kexts 清单

```
EFI/OC/Kexts/
├── Lilu.kext                   ✅ 内核补丁框架
├── VirtualSMC.kext             ✅ SMC 模拟
├── WhateverGreen.kext          ✅ GPU 补丁
├── AppleALC.kext               ✅ 声卡驱动
├── IntelMausiEthernet.kext     ✅ 有线网卡驱动
├── USBPorts.kext               ✅ USB 定制映射
├── SMCBatteryManager.kext      ✅ 电池传感器
├── SMCProcessor.kext           ✅ CPU 传感器
├── SMCSuperIO.kext             ✅ 风扇/温度
├── SMCLightSensor.kext         ✅ 环境光传感器
├── BrightnessKeys.kext         ✅ 亮度按键
├── ECEnabler.kext              ✅ 嵌入式控制器
└── RestrictEvents.kext         ✅ 事件限制
```

### SSDT 热补丁

```
EFI/OC/ACPI/
├── SSDT-PLUG.aml       ✅ CPU 电源管理 (XCPM)
├── SSDT-EC.aml         ✅ EC 仿冒 (Broadwell 必需)
├── SSDT-PNLF.aml       ✅ 背光控制
├── SSDT-USBX.aml       ✅ USB 电源属性
├── SSDT-SBUS.aml       ✅ SMBus 支持
├── SSDT-MCHC.aml       ✅ MCHC 仿冒
├── SSDT-HPET.aml       ✅ HPET IRQ 修复
├── SSDT-RTC0.aml       ✅ RTC 兼容性
└── SSDT-DMAC.aml       ✅ DMA 控制器修复
```

### Drivers

| Driver | 说明 |
|:-------|:----:|
| HfsPlus.efi | HFS+ 文件系统支持 |
| OpenRuntime.efi | OpenCore 运行时环境 |
| OpenCanopy.efi | 图形引导界面 |
| ResetNvramEntry.efi | NVRAM 重置入口 |

---

## 🚀 快速开始

### 1️⃣ BIOS 配置

1. 开机按 F2 进入 BIOS
2. 按上述表格配置
3. 按 F10 保存退出

### 2️⃣ EFI 部署

```bash
# 挂载 USB 的 EFI 分区
diskutil list
sudo diskutil mount diskXs1

# 复制 EFI 文件夹
cp -R EFI /Volumes/EFI/
```

### 3️⃣ 生成三码（重要！）

使用 GenSMBIOS 或 OCAT 生成自己的 SMBIOS 序列号，不要直接使用本仓库的三码。

### 4️⃣ 安装 macOS

1. 制作 macOS 安装 U 盘
2. 替换 U 盘 EFI 分区中的 EFI 文件夹
3. 从 USB 启动 → 选择「Install macOS」
4. 按提示完成安装（约 2-3 次重启）
5. 安装完成后将 EFI 复制到硬盘 EFI 分区

---

## 📸 截图

| 系统信息 |
|:--------:|
| ![系统信息](https://cdn.jsdelivr.net/gh/WT2072861996/Intel-NUC5i7RY-Hackintosh@main/Screenshots/screenshot.png) |

---

## 🔧 注意事项

- **Intel NUC5i7RY** 是 Broadwell 平台 NUC 迷你主机，支持 Iris Graphics 6100（48EU）
- Intel AC 7265 Wi-Fi 使用 **AirportItlwm**（需 ContinuousIntegration 构建版本）
- Realtek ALC283 声卡 layout-id 已配置，如无声可尝试其他 layout-id
- 本机支持 HDMI + MiniDP 双显示输出
- ⚠️ **自行生成三码后再使用，不要直接使用本仓库的序列号**

---

## 📄 许可证

MIT License — 仅供学习和研究

> ⚠️ 在非 Apple 硬件上安装 macOS 可能违反 EULA

---

<p align="center">
  <b>为 Hackintosh 社区贡献 ❤️</b><br/>
  <sub>Intel NUC5i7RY · OpenCore 1.0.x · 2026年</sub>
</p>
