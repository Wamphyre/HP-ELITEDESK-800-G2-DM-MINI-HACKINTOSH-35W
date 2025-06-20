# Optimized for OpenCore 1.0.4 and macOS Monterey

# BIOS Setup

- I recommend you to upgrade to the latest BIOS (2024) from the same BIOS HP Network utility, easy and automated.
- TPM Embedded Security - Set to hidden
- Intel Software Guard Extension (SGX) - Disabled
- In boot options - USB Storage boot is enabled but PXE, Fast and CD-ROM boot are disabled. It's down to you and your drives for the boot order.
- Secure boot configuration - Set to Legacy Support Enable and Secure Boot Disable
- System Options - Turbo-boost, Multi-processor, VT (VTx), M.2 SSD and Allow PCIe/PCI SERR# Interrupt are left enabled.
- Virtualization options are secure and stable to use
- Built in device options - Embedded LAN controller, audio device and internal speakers are enabled. Increase video memory size to 512mb.
- Port options - enable them all
- Optional ROM policy - All legacy
- Power management options - enable all apart from unqiue sleep state blink rates
- Remote management options - disable all options here

# Thanks to:

- https://github.com/jparrack/HP-Elitedesk-800-G2-Mini-Hackintosh

# What works?

- Everything
- 100% Super performant hardware and astonishing compatbility

## Don't forget to buy me a beer!
https://ko-fi.com/wamphyre94078
