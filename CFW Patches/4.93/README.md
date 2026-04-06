# xai_plugin Installer
XAI Plugin - Original Source by mysis [https://www.psx-place.com/threads/custom-xai_plugin-source.12455/]

You can check and download the latest xai_plugin update package

If you want to install a PKG manually, make sure it is the one for your version, otherwise it will not work:

- **CFW 4.93 PEX/D-PEX:** xai_updater.pkg
- **CFW 4.81-4.89/4.93:** xai_updater_cex.pkg
- **CFW 4.84 REBUG DECR LE:** xai_updater_rebug_decr.pkg


The application uses beeps to let the user know if the update has been completed successfully or not, this is the list of beeps:

- **SINGLE BEEP:** Update completed successfully
- **DOUBLE BEEP:** Firmware not supported
- **TRIPLE BEEP:** Error when updating


## Updater package version: 1.25 :package: :new:
- [XAI] Added support for CFW 4.93
- [XAI] Added option to set custom/dynamic temp/speed in PS2 games (need latest EMUs from kozarovv)
- [XAI] Added 'Toggle Demo Unlocker' option
- [XAI] Added 'Toggle Epilepsy Warning' option
- [XAI] Updated Trophy Unlocker code and XAI menu
- [XAI] Improved CBOMB fix
- [XAI] Code improved

## Updater package version: 1.24 :package:
- [XAI] Added [Toggle XMB Waves] option for FW 2.70 waves (Only PEX/D-PEX/CEX)

## Updater package version: 1.23 :package:
- [XAI] Updated overclock code (Thanks to Chattrapat Sangmanee [@chattrapat_s])
- [XAI] Added more core/memory frequencies (300MHz - 1050MHz)

## Updater package version: 1.22 :package:
- [XAI] Added [Overclock Tools] menu

## Updater package version: 1.21 :package:
- [XAI] Merged options [Resize VFLASH/NAND Regions] and [Install Petitboot] in [Install OtherOS]
- [XAI] Added [CFW 4.92 Fixes] in xai_plugin
	* download_plugin.sprx: Fixed error while downloading to internal HDD

## Updater package version: 1.20
- [XAI] Added support for CFW 4.92

## Updater package version: 1.19
- [XAI] Improved metldr dump
- [XAI] Fixed [Dump ERK] option not working on some PS3s
- [XAI] Added support for dumping decrypted metldr (Thanks to **Mathieulh**, **flatz**, **CMX**, **zecoxao** and **M4j0r**)
- Added xai_plugin update PKG for Rebug 4.84 DECR

## Updater package version: 1.18
- [XAI] Firmware independant while patching LV1 for options:
     + Enable/Disable QA Flags
	 + Dump Token Seed
	 + Rebug Toolbox options
- [XAI] Added support for CFW 4.84 DECR
- [XAI] Merged options [Enable/Disable TrophyUnlocker] in [Toggle TrophyUnlocker]
- [XAI] Merged options [Enable/Disable PSN Protection] in [Toggle PSN Protection]
- [XAI] Updated Import Licenses to rap.bin option
- [XAI] Updated Export Licenses to rap.bin option

## Updater package version: 1.16
- Fixed minor bug wrongly detecting that CFW syscalls were disabled while using [Dump RAM] option

## Updater package version: 1.13
- Now Cobra shows the correct disc image for PS2 (blue disc icon)
- Added option to export RAP license of RIF licenses in current user account
- Fixed [Check GPU/VRAM clock speed] option
- Added option to download latest version webMAN MOD through xai_plugin
- Updated FTP server (Experimental)
- Fixed libCrypt for PSX games (thanks to aldostools)
- Enabled [Install All Packages] in non QA flagged PS3
- Added german language in xai_plugin (thanks to FadedHD3)
- Updated french language in xai_plugin (thanks to EimGdt and Chronoss09)
- Updated OtherOS and PSN icon (thanks to HackZy01)

## Updater package version: 1.12
 - Updated Cobra version to 8.4
 - Use PS2 FAN Modes on PS2 Classic games (make sure webMAN MOD FAN Control is disabled)

## Updater package version: 1.11
 - Initial release

## Updater package version: 1.0
- Test package
