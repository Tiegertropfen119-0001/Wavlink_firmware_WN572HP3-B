# Wavlink SPI Dumped Firmware with Working U-Boot

This repository contains the SPI-dumped firmware for Wavlink devices, including a functional U-Boot bootloader, useful for debugging, recovery, and firmware restoration.

## Links
[Wavlink Firmware (Offical)](https://docs.wavlink.xyz/Firmware/fm-572hp3-b)\
[Wavlink UBoot fix](https://github.com/Tiegertropfen119-0001/Wavlink_firmware_WN572HP3-B/blob/main/fm_dumps/wavlink_working.bin)\
[SPI Flash PDF](https://www.boyamicro.com/download/SPI_NOR_Flash/BY25Q128AS.pdf)\

SPI flash may vary as they are just using drop-in replacements
## Background

### Issue with Broken Device
A broken Wavlink device displayed the following error during boot:
LZMA uncompression error: %d U-Boot image! Entering emergency mode. Please transmit a valid U-Boot image through this serial console. The U-Boot image will be booted up directly, and not be written to flash. Accepted mode is Ymodem-1K. spl: ymodem

Serial flashing didn't work, rendering the device inaccessible.

### Recovery Steps
I had access to another Wavlink outdoor AP that was damaged in a thunderstorm. After debugging, I identified a shorted 2.4 GHz amplifier. Desoldering the amplifier allowed the device to boot successfully. From this device, I dumped the working firmware and U-Boot.
![the_spi_chip](https://github.com/Tiegertropfen119-0001/Wavlink_firmware_WN572HP3-B/blob/main/img/SPIFlashWorkingWavlink.jpg)
![reading_spi_chip](https://github.com/Tiegertropfen119-0001/Wavlink_firmware_WN572HP3-B/blob/main/img/SPIReading.png)
### Boot Log of Working Device
U-Boot 2018.09-g4066fd9-dirty (Oct 19 2022 - 11:00:39 +0800)

System Information: CPU: MediaTek MT7621AT ver 1, eco 3 Clocks: CPU: 880MHz DDR: 1200MHz Bus: 220MHz XTAL: 40MHz Model: MediaTek MT7621 reference board DRAM: 128 MiB

Flash Environment: SPI Flash: Detected BY25Q128AS Page size: 256 Bytes Erase size: 64 KiB Total: 16 MiB Warning: Bad CRC, using default environment

Input/Output Interfaces: Input: uartlite0@1e000c00 Output: uartlite0@1e000c00 Error: uartlite0@1e000c00

Network: Ethernet: Interface: eth@1e100000 (eth0) MAC Address: Random - 7e:68:0d:b7:1e:8b

Boot Sequence: Autoboot Countdown: 0 seconds

GPIO Status: 572HP3 GPIO Configuration: GPIO 16: 1 → 0 GPIO 17: 1 → 0 GPIO 3: 1 → 0 GPIO 4: 0

## EZP2019+ Setup
![image](https://github.com/user-attachments/assets/a3064dcd-5c17-4649-9f55-0da1e195848f)


## Flashing Instructions

1. Use the SPI dump to flash the firmware to the broken device.
2. The U-Boot bootloader provides a failsafe web GUI for firmware restoration. If the firmware is corrupted, upload Wavlink's official firmware through this interface.

### Accessing the Failsafe Web GUI
- Set your PC's IP to:
  - **IP Address:** 192.168.10.100
  - **Subnet Mask:** 255.255.255.0
- Access the device at **192.168.10.1** via a web browser. 

Alternatively, TFTP can also be used for recovery.

## Notes
- U-Boot logs may vary slightly across devices, but they remain relatively universal.
- Ensure you have the correct tools for SPI flashing and follow all safety precautions during hardware modifications.

## Disclaimer
This repository is for educational and research purposes only. Use it at your own risk. Ensure compliance with local laws and regulations.

