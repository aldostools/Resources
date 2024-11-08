# PS1 & PS2 emulators modifications by kozarovv

## PS2 Netemu Features:

* `FPS Counter`
  * First one or two reads after enabling menu are bugged and show wrong value. That's because code to reset counter works only when menu is active. At some point this will be fixed.
  * Counter is measuring GS Display/Dispfb registers write count per second. It's independent of PS3 framerate; it shows PS2 internal framerate.
* `Activate menu combo` for gamepads where the PS button is not working.
  * Press Left DPAD + `SQUARE` + `L1` + `R1` for 5-6 seconds in-game to open the menu.
* `EE Overclocking/Undeclocking`
* `Partial Antiblur`
* `2 new config commands` for the above features
  * 0x4F for No Blur (no param)
  * 0x4E for Cycles manipulation parameter: 1 = -50%, 2 = -25%, 3 = +25%, 4 = +50%
  New config commands are ignored on unpatched emulators, so it's safe to add them even for HEN setups (they will just do nothing there).
* `Modified BIOS` with added X modules for increased PS2 homebrew compatibility.
  * Added: XMCMAN, XSIO2MAN, XPADMAN, XMCSERV, XMTAPMAN, LIBSD

Features not implemented in this release:
* `Displaying a R5900 PC/RA` it's useful only for fixing games. Patches are available on the wiki.
* `Fastboot (skip PS2 logo)` it's a BIOS patch, and I didn't had time to create a config for it; hardcoding wasn't an option.

Both manipulating EE cycles and enabling No Blur are much less effective than what I expected them to be.
For now the only game that is known to profit from No Blur is Kingdom Hearts 2, no games affected by cycle manipulations for now (but that was tested before fps counter was a thing).
New configuration features are accessible through the Debug Menu and replace Vsync Delay and XOR CSR options. Configs for those options are still working fine.
Code quality is terrible, many features were thrown onto existing code that sometimes has been modified earlier. So it matches original Netemu code quality at least. :D

-----------------------------------------------------------------------------------------------

## PS2 Gxemu Features:
* `Extended Config Table` using trick from [psdevwiki.com/Talk:PS2_Emulation](https://www.psdevwiki.com/ps3/Talk:PS2_Emulation#Extend_config_table_by_50%_in_ps2_gxemu)
  * Added a few configurations as an example: Way of the Samurai 1 and 2 (SLUS_204.07/SSLUS_208.93) Darkwatch SLUS_210.42 (stuttering audio fix only).
* `Modified BIOS with added X modules` for increased homebrew compatibility.
  * Added: XMCMAN, XSIO2MAN, XPADMAN, XMCSERV, XMTAPMAN, LIBSD
* `Temperature Display`, credits to 3141card for original Netemu implementation.
* `FPS counter`
  * Temperature display and FPS counter can be accessed in two ways. By `SQUARE` + `SELECT` combo ingame, this refresh temps/fps when combo is pushed. Second way is to open menu and push and keep pressed `SQUARE` . This refresh data every second.
* `Custom config file loading` Config need to have exact game executable name (ie SLES_123.45), emu search for configs in `/dev_hdd0/vm/gx/`

* Now temperatures are hidden in menu, hold `SQUARE` button to see them.
* Implemented ingame `SQUARE` + `SELECT` combo to show temperatures popup.

***Changes 23102024:***
* Change how emulator read custom config. Due to broken configs in gxemu database we need to load our data before internal database is parsed.
  * This is required for games like Crash Twinsanity SLUS version, and True Crime Streets of Ney York, in both $ony left unfinished config in database.
  * Internal database is still fully working and custom is used only if exist and if hash and id is correct.
* Now config file can have up to 2064 bytes (0x810). There is no need to fill shorter configs with zero bytes anymore.
* Now temperatures/fps are hidden in menu, hold square button to see them.
* Improved ingame (square + select combo) popup size.
* Fixed screen corruption when select + square combo is hold for longer time. 
* Since menu string is sorted out, there is now only 1 version of emu with all new functions inside. 
* Added many new configs.
* Remove DEV9 blacklist. This is old but I forgot to mention it earlier.

<details>
<summary>Games which are originally blacklisted from accessing DEV9</summary>
<pre>
    SLES_540.13	0x0CD1298155	World Snooker Championship 2007
    SLES_518.40	0x12C93199A5	NHL Hitz Pro
    SLES_549.13	0x15C93199AD	Pro Evolution Soccer 2008
    SLUS_211.86	0x24D92589A5	NBA Ballers - Phenom
    SLUS_212.35	0x2CD12D8125	MLB 2k6
    SLUS_211.38	0x34C9359935	X-Men Legends II - Rise of Apocalypse
    SLUS_211.28	0x34C93599E5	Blitz - The League
    SLUS_211.28	0x34C93599E5	Blitz - The League
    SLES_542.10	0x449961C9E5	NBA 2K7
    SLES_542.46	0x4C9169C1CD	FIFA '07
    SLES_542.45	0x4C9169C1D5	NHL '07
    SLES_542.44	0x4C9169C1DD	FIFA '07
    SLES_542.43	0x4C9169C1E5	FIFA '07
    SLES_542.41	0x4C9169C1F5	FIFA '07
    SLES_542.40	0x4C9169C1FD	FIFA '07
    SLUS_213.74	0x4CB14DE12D	Marvel - Ultimate Alliance
    SLUS_212.74	0x54A955F915	Outrun 2006 - Coast 2 Coast
    SLUS_213.01	0x5CA15DF165	World Series of Poker
    SLUS_212.86	0x5CA15DF1FD	WWE SmackDown! vs RAW 2006
    SLUS_212.86	0x5CA15DF1FD	WWE SmackDown! vs RAW 2006
    SLUS_214.63	0x649965C94D	Tom Clancy's Ghost Recon 2
    SLUS_214.60	0x649965C955	NBA Live '07
    SLUS_214.61	0x649965C95D	NASCAR '07
    SLUS_214.58	0x649965C965	NHL '07
    SLUS_214.59	0x649965C96D	NCAA Football '07
    SLES_531.04	0x6BB149E15D	Tom Clancy's Rainbow Six - Lockdown
    SLUS_214.91	0x6C916DC165	World Series of Poker - Tournament of Champions
    SLUS_214.83	0x6C916DC1A5	Tiger Woods PGA Tour '07
    SLUS_214.82	0x6C916DC1AD	NFL Street 3
    SLUS_214.81	0x6C916DC1B5	NCAA March Madness '07
    SLUS_214.77	0x6C916DC1D5	Madden NFL '07 [Hall of Fame Edition]
    SLUS_214.76	0x6C916DC1DD	Madden NFL '07
    SLUS_213.83	0x748975D9DD	Fight Night - Round 3
    SLUS_214.33	0x7C817DD125	FIFA Soccer '07
    SLUS_214.25	0x7C817DD165	NHL 2K7
    SLUS_214.24	0x7C817DD16D	NBA 2K7
    SLUS_214.27	0x7C817DD175	WWE SmackDown! vs RAW 2007
    SLUS_214.12	0x7C817DD1CD	World Championship Poker featuring Howard Lederer - All-In
    SLUS_205.65	0x84798529BD	Champions of Norrath
    UNKNOWN     0x8559A109AD	UNKNOWN
    SLUS_215.68	0x8579852915	Arena Football - Road to Glory
    SLUS_215.82	0x8579852965	MVP '07 - NCAA Baseball
    SLES_545.11	0x8D51A90145	UEFA Champions League
    SLES_545.13	0x8D51A901B5	UEFA Champions League
    SLES_545.12	0x8D51A901BD	UEFA Champions League
    SLUS_216.20	0x8D718D21BD	NCAA Football '08
    SLUS_205.41	0x9C619D31E5	NBA Ballers
    SLES_544.48	0x9D41B911AD	World Series of Poker - Tournament of Champions
    SLUS_215.61	0x9D619D31C5	Major League Baseball 2K7
    SCUS_975.44	0x9F29357805	NBA '07 featuring The Life Vol.2
    SCUS_975.56	0x9F293578E5	MLB '07 - The Show
    SLUS_216.38	0xB549B51915	Madden NFL '08
    SLUS_216.32	0xB549B51925	NHL 2K8
    SLUS_216.47	0xB549B5195D	NHL '08
    SLUS_216.48	0xB549B519A5	FIFA Soccer '08
    SLUS_216.49	0xB549B519AD	NBA Live '08
    SCES_532.85	0xBC61793025	Ratchet - Gladiator
    SLUS_216.69	0xBD41BD1105	NBA 2K8
    SLUS_208.20	0xC439C569F5	Tom Clancy's Ghost Recon - Jungle Storm
    SCUS_974.01	0xC7716D20D5	Hot Shots Golf FORE!
    SCUS_974.01	0xC7716D20D5	Hot Shots Golf FORE!
    SLES_516.97	0xCA11E941F5	SSX 3
    SCUS_973.53	0xCF7965285D	Ratchet and Clank - Up Your Arsenal
    SCUS_973.53	0xCF7965285D	Ratchet and Clank - Up Your Arsenal
    SCES_515.93	0xD20911582D	Hardware Online Arena [Beta, Promo & Full Release]
    SCUS_973.28	0xD7617D308D	Gran Turismo 4
    SLES_525.45	0xE339C1695D	Star Wars Battlefront
    PCPX_980.42	0xE794CCB06D	Minna no Tennis
    SCES_515.78	0xEA3129608D	Network Access Disc [Original, v4.02 & v4.03]
    SLUS_209.73	0xEC11ED4115	Champions - Return to Arms
    SCUS_975.00	0xEF594508D5	MLB '06 - The Show
    SLUS_208.89	0xF409F559AD	MLB Slugfest - Loaded
    SCUS_974.65	0xF7415D10E5	Ratchet - Deadlocked
    SCUS_974.65	0xF7415D10E5	Ratchet - Deadlocked
<br>
Repeated entries are really in emu... I can only guess that's because games have different versions released under the same ID, and some kind of automatic parser were used to create that list.
</pre></details>

More features, more messy code inside. Shame on me. :P
-----------------------------------------------------------------------------------------------

## PS2 Emu Features:
* `Temperature Display`
  * Temperature display can be accessed in two ways. By `SQUARE` + `SELECT` combo ingame, this refresh temps when combo is pushed. Second way is to open menu and push and keep pressed `SQUARE`. This refresh data every second.
  * Under the hood, this was the most demanding port of the old implementation. Ps2_emu misses basics like s(n)printf; there is also no vuart bug that the old implementation relies on; additionally, there is also less space that is known to be unused.
  * Due to the above, supported temperatures are in the range of 00-99 °C. Temperatures above 99 °C will be shown without the first character (e.g., 123 will be 23). But if you are hitting +100c on PS3, then you have more problems than that.

* Now temperatures are hidden in menu, hold `SQUARE` button to see them.
* Implemented ingame `SQUARE` + `SELECT` combo to show temperatures popup.

## Known bugs
* ps2_emu/ps2_gxemu have micro stutter when it starts to display popup. Collecting 3x temperatures data takes too long.
  I'm looking into different solutions, but in next version South Bridge temperature probably will be available only in menu.
-----------------------------------------------------------------------------------------------

## PS1 Netemu Features:

* `Automatic GTE Widescreen Patch` - Patched Geometry Transformation Engine for automatic Widescreen
  * Work only on 3D elements. Compatibility differs per game but should be on par with Duckstation "Widescreen Rendering".
  * You need to select the `Full Screen Display` option to enable.
  * Compatible with `ISO`, real `discs`, `EBOOTS`, and `Official Classics`.
  * While fully working, code under the hood is a little bit janky due to lack of space in elf. Sorry!

Features not implemented in this release:
* `Dithering removal patch`. Because many people prefer it enabled as on the original PS1.
* `Forced bilinear filtering removal`. Because many people prefer it enabled, and I had no good way to make a menu separator for that.

-----------------------------------------------------------------------------------------------

## PS1 Emu Features: COMPLETELY UNTESTED!!!

* `Automatic GTE Widescreen Patch` - Patched Geometry Transformation Engine for automatic Widescreen
  * Work only on 3D elements. Compatibility differs per game.
  * You need to select the `Full Screen Display` option to enable.
  * Compatible with `ISO` and real `discs`.
  * While fully working, code under the hood is a little bit janky due to lack of space in elf. Sorry!

Features not implemented in this release:
* `Dithering removal patch`. Because many people prefer it enabled as on the original PS1.

### Nearest + no dither mods - ps1_netemu.self

This just a fun stuff that I made back in the day at request of Haker120.
There is no plan to update any emu from this pack for now.
While they are safe to use, there is a bug where filtering is not set to nearest when upscaler is set to normal with disabled smoothing.
Every other combination of settings should work fine. All 3 emus have implemented widescreen hack when full screen is selected.

-----------------------------------------------------------------------------------------------

* All files should be compatible with `4.75+ firmwares`. Some features were tested more, some less.
* All patches were written in pure PPE and SPE assembly; code portability is not existing if Sony updates emulators (shouldn't happen, really).
* BIG THANKS to people who helped with testing all of that! mrjaredbeta, kamilb880, Jabu, A youkai of love. Thanks to them I was able to create all those mods without PS3 hardware!
* I hope that I didn't mess up files; if something is not working as expected, then I probably packed the wrong self.
