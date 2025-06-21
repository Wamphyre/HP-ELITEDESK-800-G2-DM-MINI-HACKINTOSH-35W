# HP EliteDesk 800 G2 Mini Hackintosh (OpenCore 1.0.4 / macOS Monterey)

**Current Status**: macOS Monterey 12.x with full hardware support  
**Last Updated**: June 2025  
**OpenCore**: 1.0.4  
**SMBIOS**: iMac17,1

## 📋 Hardware Specifications
| Component        | Model                           |
|------------------|---------------------------------|
| CPU              | Intel Skylake (i5-6500T) |
| Graphics         | Intel HD Graphics 530          |
| Audio            | Realtek ALC221 (layout-id 88)   |
| Ethernet         | Intel I219-LM                  |
| WiFi/Bluetooth   | Intel Dual Band Wireless-AC    |
| Ports            | 6x USB 3.0, 2x DisplayPort, VGA |

## ⚙️ BIOS Setup Configuration

> **Important**: Upgrade to the latest BIOS (2024) using HP Network utility for automated installation.

| BIOS Section | Setting | Configuration |
|--------------|---------|---------------|
| **Security** | TPM Embedded Security | **Hidden** |
| | Intel Software Guard Extension (SGX) | **Disabled** |
| | Secure Boot Configuration | Legacy Support: **Enabled**<br>Secure Boot: **Disabled** |
| **Boot Options** | USB Storage Boot | **Enabled** |
| | PXE Boot | **Disabled** |
| | Fast Boot | **Disabled** |
| | CD-ROM Boot | **Disabled** |
| **System Options** | Turbo-boost | **Enabled** |
| | Multi-processor | **Enabled** |
| | Virtualization Technology (VT-x) | **Enabled** |
| | M.2 SSD | **Enabled** |
| | Allow PCIe/PCI SERR# Interrupt | **Enabled** |
| **Built-in Devices** | Embedded LAN Controller | **Enabled** |
| | Audio Device | **Enabled** |
| | Internal Speakers | **Enabled** |
| | Video Memory Size | **512MB** |
| **Port Options** | All Ports | **Enabled** |
| **Optional ROM Policy** | Legacy Support | **All Legacy** |
| **Power Management** | All Options | **Enabled** |
| | Unique Sleep State Blink Rates | **Disabled** |
| **Remote Management** | All Options | **Disabled** |

## ✅ What's Working
- **All major components**:
  - Intel HD 530 Graphics (Full QE/CI acceleration)
  - ALC221 Audio (Internal speakers, microphone, DP output)
  - Intel I219-LM Ethernet
  - Intel WiFi/Bluetooth (Handoff/AirDrop)
  - USB 3.0 (Complete port mapping)
  - Power Management (Sleep/Wake, CPU PM)
  - iServices (iMessage, FaceTime)

## 🛠️ Detailed Technical Configuration

### 1. Essential ACPI Patches
```xml
<!-- Injected SSDTs -->
SSDT-EC-USBX.aml    # Embedded controller emulation
SSDT-HPET.aml       # System timer correction
SSDT-SBUS-MCHC.aml  # SMBus enablement

<!-- Binary Patches -->
HPET _CRS to XCRS Rename   # Prevents IRQ conflicts
Fix C-states for Skylake   # 0x0D000000 → 0x0D00000D
RTC IRQ 8 Patch            # Fixes random wake issues
```

### 2. Device Properties
**HD 530 Graphics:**
```xml
<key>AAPL,ig-platform-id</key>
<data>AAASGQ==</data>          # 00001619 (headless mode)
<key>framebuffer-con1-alldata</key>
<data>AAQAAAQAAAACAAAA</data>  # HDMI configuration
<key>enable-gpu-idle</key>
<data>AQ==</data>              # Enable GPU idle states
```

**ALC221 Audio:**
```xml
<key>layout-id</key>
<integer>88</integer>          # HP G2 specific layout
<key>hda-idle-support</key>
<string>1</string>             # Audio idle support
```

### 3. Critical Kexts
| Kext | Function |
|------|----------|
| VirtualSMC | Apple SMC emulation |
| WhateverGreen | Intel graphics patches |
| AppleALC | Audio with layout-id 88 |
| IntelMausi | I219-LM Ethernet support |
| AirportItlwm | Native WiFi support |
| CPUFriend+Provider | Optimized power profile for 35W CPUs |
| RTCMemoryFixup | Fixes CMOS resets |

### 4. Boot Arguments
```bash
-v alcid=88 -igfxidle -igfxnohdmi -igfxrpsc=0 -igfxmpc=0 gfxrst=1
```
- `gfxrst=1`: Fixes graphics artifacts on wake
- `-igfxidle`: Enables low-power GPU states
- `alcid=88`: Forces audio layout for ALC221

## ⚡️ Power Management
- **CPUFriend**: Custom profile for low-power CPUs
- **CpuTscSync**: TSC counter synchronization
- **PowerTimeoutKernelPanic**: Prevents timeout panics
- **Hibernation**: Disabled (HibernateMode = None)

### BIOS Settings:
1. Reset BIOS to defaults
2. Apply recommended settings above
3. Disable Secure Boot

## 🌐 Connectivity
| Component | Support | Notes |
|-----------|---------|-------|
| Ethernet | ✅ Native | IntelMausi.kext |
| WiFi 2.4/5GHz | ✅ Native | AirportItlwm.kext |
| Bluetooth | ✅ Native | IntelBluetoothFirmware.kext |
| AirDrop | ✅ Functional | Requires valid SMBIOS |
| Continuity | ⚠️ Partial | Handoff works, Universal Clipboard doesn't |

## 🎉 Credits
https://github.com/jparrack/HP-Elitedesk-800-G2-Mini-Hackintosh

## 🙏 Support
If this project helped you, consider supporting my work:
https://ko-fi.com/wamphyre94078
