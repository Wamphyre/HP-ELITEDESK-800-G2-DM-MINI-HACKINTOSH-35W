# HP EliteDesk 800 G2 Mini Hackintosh (OpenCore 1.0.5 / macOS Sequoia)

**Current Status**: Fully reconfigured from scratch to run macOS Sequoia on this machine instead of macOS Monterey  
**Last Updated**: July 2025  
**OpenCore**: 1.0.5  
**SMBIOS**: iMac19,1

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
| **Boot Options** | Startup Delay | **5** |
| | Fast Boot | **Disabled** |
| | CD-ROM Boot | **Disabled** |
| | USB Storage Boot | **Enabled** |
| | Network (PXE) Boot | **Disabled** |
| | After Power Loss | **Power Off** |
| | UEFI & Legacy Boot Order | **User Preference** |
| **Secure Boot Configuration** | Legacy Support | **Enabled** |
| | Secure Boot | **Disabled** |
| | All Other Options | **Unchecked** |
| **System Options** | Turbo-boost | **Enabled** |
| | Multi-processor | **Enabled** |
| | Virtualization Technology (VTx) | **Enabled** |
| | Virtualization Technology for Directed I/O (VTd) | **Disabled** |
| | M.2 WLAN/BT | **Enabled** |
| | M.2 SSD | **Enabled** |
| | Allow PCIe/PCI SERR# Interrupt | **Enabled** |
| | Power Button Override | **4 sec** |
| **Built-in Device Options** | Embedded LAN Controller | **Enabled** |
| | Wake on LAN | **Disabled** |
| | Dust Filter | **Disabled** |
| | Video Memory Size | **512MB** |
| | M.2 USB / Bluetooth | **Enabled** |
| | Audio Device | **Enabled** |
| | Internal Speakers | **Enabled** |
| | Increase Idle Fan Speed (%) | **0** |
| **Port Options** | All Ports | **Enabled** |
| | Restrict USB Devices | **Allow all USB Devices** |
| **Option ROM Launch Policy** | Configure Option ROM Launch Policy | **All UEFI** |
| **Power Management Options** | Runtime Power Management | **Enabled** |
| | Extended Idle Power States | **Enabled** |
| | S5 Maximum Power Savings | **Disabled** |
| | SATA Power Management | **Enabled** |
| | PCI Express Power Management | **Disabled** |
| | Power On from Keyboard Ports | **Disabled** |
| | Unique Sleep State Blink Rates | **Disabled** |
| **Remote Management Options** | All Settings | **Default Configuration** |

## ✅ What's Working
- **Most major components**:
  - Intel HD 530 Graphics (Full QE/CI acceleration)
  - ALC221 Audio (Internal speakers, microphone, DP output)
  - Intel I219-LM Ethernet
  - USB 3.0 (Complete port mapping)
  - Power Management (basic CPU PM)
  - iServices (iMessage, FaceTime)

## ⚠️ Known Issues (macOS Sequoia)
- ❌ **DRM** does not work (e.g., Apple TV+, Safari Netflix)
- ❌ **Native Intel WiFi** is non-functional — use a supported external USB WiFi dongle
- ⚠️ **Sleep** is unstable and may fail to resume properly

## ⚡️ Power Management
- Functional CPU power states via CPUFriend
- TSC sync enabled
- Hibernate disabled (HibernateMode = None)
- Sleep not reliable

## 🌐 Connectivity
| Component | Support | Notes |
|-----------|---------|-------|
| Ethernet | ✅ Native | IntelMausi.kext |
| WiFi 2.4/5GHz | ❌ Not working | Use supported USB dongle |
| Bluetooth | ✅ Native | IntelBluetoothFirmware.kext |
| AirDrop | ✅ Functional | Requires valid SMBIOS |
| Continuity | ⚠️ Partial | Handoff works, Universal Clipboard doesn't |

## 🎉 Credits
https://github.com/jparrack/HP-Elitedesk-800-G2-Mini-Hackintosh

## 🙏 Support
If this project helped you, consider supporting my work:  
https://ko-fi.com/wamphyre94078
