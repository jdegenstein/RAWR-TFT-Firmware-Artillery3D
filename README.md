<!-- omit in toc -->
# RAWR TFT Firmware for the Artillery 3D Printer
![GitHub](https://img.shields.io/github/license/wgcv/RAWR-TFT-Firmware-Artillery3D)
![GitHub Release Date](https://img.shields.io/github/release/wgcv/RAWR-TFT-Firmware-Artillery3D)
<p align="center">
<img width=1080 src="https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-banner.jpeg" />
The most powerful TFT firmware for the Artillery X1 and Genius, keeping the vanilla essence but with incredible tools.
</p>
 
## Table of Contents
- [Features](#features)
- [Screens](#screens)
- [How to update TFT Firmware](#how-to-setup-the-tft-firmware)
- [Customization](#customization)
  - [Configuration](#editing-configuration)
  - [Themes](#themes)
  - [Reset](#reset)
  - [Deployment](#deployment)
- [Contribute](#contribute)

## Features
- M600 from USB and MicroSD (Pause, Change Filament, and Resume, without changing Marlin)
- Pre-Heat
- PID for ABS and PLA
- Extruder Calibration (E-Steps)
- Filament Change
- Baby Steps
- Change configuration without rebuilding (config.ini file)
- Auto Leveling and Manual Leveling (5 points).
- Gcode Console

  
 ⚠️ **You don't need to modify or open the printer** to use the firmware and the M600. 
 
 📐 For auto-leveling, you might need to make some changes in Marlin firmware and add additional hardware.

🐙 If you want to use M600 with **octoprint** check [RewriteM600](https://github.com/wgcv/RewriteM600)

🖨 ✅ Working on **Artillery Sidewinder X1** and **Artillery Genius**

👷🏽‍♀️ If you try it on another 3D printer with TFT28, please add it to the readme file.
  
## Screens
| Status page with flow and speed |  Status page clasic |
|:--------------------------:|:-------------------------:|
|![](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-statusscreen1.jpg) | ![](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-statusscreen2.jpg)
| Main menu |  Settings menu |
|![](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-mainmenu.jpg) | ![](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-settings.jpg)
| Printing menu | M600 |
![](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-printing.jpg) <img width=1080/>| ![](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-M600.jpg)<img width=1080/>

## How to setup the TFT firmware

1. Download the latest release from https://github.com/wgcv/RAWR-TFT-Firmware-Artillery3D/releases
2. Unzip the downloaded file.
3. Copy the files `mkstft28.bin`, `config.ini`, and the folders `bmp` and `font` to the root of a blank SD card (<8GB and formatted as FAT32).
4. Insert the SD card in the TFT's SD card slot and restart the TFT by pressing the reset button or disconnecting and connecting the power cable.
5. Wait for the firmware, configuration, font, and icons to update.
![image](https://raw.githubusercontent.com/wgcv/RAWR-TFT-Firmware-Artillery3D/docs/img/readme-copysd.jpg)
<p align=center>Failing to update your icons &amp; fonts will result in missing icons and/or unreadable text</p>

⚠️ If you get the error message: "NO PRINTER ATTACHED," go to settings -> BaudRate -> 250000 (or try it with the baud rate of your Marlin, normally 115200 or default Artillery firmware 250000).

## Customization
### Editing Configuration
The firmware can be configured using the **config.ini** file.
- To edit the preheat values, check lines `224` to `231`. The `T` is the extruder temperature and `B` the bed temperature.
- To edit the bed size, modify line `155`. For the X1, the default value is `size_max:X300 Y300 Z400` and for the Genius, `size_max:X220 Y220 Z250`.
- To show the flow and speed on the status screen, change line `308` to `show_status_speed_flow:1`.

#### Updating Firmware Configuration
To update the firmware configuration:
1. Edit the settings in **config.ini**.
2. Copy the **config.ini** file to the root of the SD card (the SD card capacity should be less than or equal to 8GB and formatted as FAT32).
3. Insert the SD card in the TFT's SD card slot and restart the TFT by pressing the reset button or disconnecting and reconnecting the power cable.
4. The TFT will update and store the configuration from the **config.ini** file.


### Themes
You can create your own themes by changing the BMP images and sharing the link by opening a PR.

### Reset
To reset the TFT's touch screen calibration, create a blank file named `reset.txt` and place it in the root folder of the SD card. Insert the SD card into the TFT's SD card reader and power cycle your printer to start the reset process.

### Deployment
<ol>
<li>Set up Visual Studio Code with PlatformIO following these <a href="https://github.com/bigtreetech/Document/blob/master/How%20to%20install%20VScode+Platformio.md">instructions</a></li>
<li>Click on the PlatformIO icon (1) and then click on Open Project (2):
 
   <img src="https://user-images.githubusercontent.com/25599056/56637513-6b258e00-669e-11e9-9fad-d0571e57499e.png"></li>
<li>Find the firmware source directory, then click Open:
 
   <img src="https://user-images.githubusercontent.com/25599056/56637532-77115000-669e-11e9-809b-f6bc25412f75.png"></li>
  <li>After opening the project, edit <a href="platformio.ini"><code>platformio.ini</code></a> and set the <code>default_envs</code> to one that matches your TFT model and version. For the Artillery, it is:
   <pre>
[platformio]
src_dir      = TFT
boards_dir   = buildroot/boards
default_envs = MKS_28_Clone_V1_0
</pre></li>
  <li>Click the check mark (✓) at the bottom of VSCode or press <code>Ctrl</code>+<code>Alt</code>+<code>B</code> (Windows) / <code>Ctrl</code>+<code>Option</code>+<code>B</code> (macOS) to compile.

<img src="https://user-images.githubusercontent.com/25599056/56637550-809ab800-669e-11e9-99d3-6b502e294688.png"></li>
<li>A <code>mkstft28.xx.xbin</code> file will be generated in the <em>hidden</em> <code>.pio\build\MKS_28_Clone_V1_0</code> folder. Follow the update process outlined in the <a href="#how-to-setup-the-tft-firmware">How to setup the TFT Firmware</a> section above to update your TFT to the latest version.</li>

## Contribute
You can report issues, create themes, implement new features with PR or **Sponsor it on [PayPal](https://paypal.me/wgcv)**. 

### Thanks to:
- @usua69
