# HP EliteBook 840 G6 Hackintosh 
**Big Sur 11.3 & OpenCore 0.6.8**

* My config: Intel i5 8265U (UHD 620)
https://www.notebookcheck.net/HP-EliteBook-840-G6-6XD76EA.441613.0.html
* BigSur/Windows10/Ubuntu multiboot with OpenCanopy GUI using this theme (https://github.com/tekteq/opencanopy-minimal-theme)
* FileVault/BitLocker/LUKS compatible and working

**Based on the work done by:**
- https://github.com/kecinzer/hpelitebook850g5-opencore
- https://github.com/Joaotcs/Hackintosh-Elitebook-8x0-g5
- r/hackintosh reddit post by @LGariv
- Dortania's Guide of all guides
- forums, trial and error, etc..

I didn't fork @kecinzer or @Joaotcs repo's since I didnt keep track of all the changes I made from the beginning, but most of the heavy lifting was done by them.

**Changes made from kecinzer repo:**
- SMBIOS changed to MacBookPro 15,2 since my CPU is the most similar to this series
- Since SMBIOS changed - CPU also changed from CP00 to PR00, so had to modify SSDT-PLUG for PR00 
- Fixed sound - ALC215 layout-id 18 for HP 830 G6 thanks to 965987400abc
- Fixed display backlight control with SSDT-PNLF-CFL.aml
- iGPU patching for Whiskey Lake UHD620 with the help from a reddit/hackintosh post by @LGariv (https://www.reddit.com/r/hackintosh/comments/hu46xm/fix_hdmi_port_and_possibly_others_not_working_on/), added some more device atributes that fixed external HDMI and DP output from HP UltraSlim dock and wake from sleep issues
- Created new USBPorts.kext (since different SMBIOS changed USB mappings) using Hackintool. Works great with HP UltraSlim dock USB's and doesn't break sleep
- Created custom CPUFriend based on Fewt's fork of CPUFriendFriend, using MacBook Air values for better battery life
- Added SSDT-XOSI for trackpad fix (not using @Joaotcs/kecinzer patches since it didn't work for this trackpad)
- Configured OpenCanopy with custom theme - opencanopy-minimal-theme
- New OpenCore secure boot options not used (https://github.com/kecinzer/hpelitebook850g5-opencore/tree/master/secureboot)
- Using alpha Airportitlwm.kext for stock Intel Wifi https://github.com/OpenIntelWireless/itlwm
- SMBIOS config options to support Windows 10 (multi-)booting using Opencore loader with no issues (working great so far, no issues with major version updates/licence/devices not working..)
- Removed @kecinzer's SSDT-INPUT.aml to fix brightness up/down special keys, since his custom remapping wasn't valid for this laptop (if brightness keys still dont work just hold power button for 30 sec - thanks to @borygo77 - https://github.com/kecinzer/hpelitebook850g5-opencore/issues/22)

**BIOS/UEFI:**
- **Upgrade your BIOS to latest version!**
- **Set iGPU to 64MB in BIOS**
- **Generate your own serial, UUID, etc.** 
https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial
- **Disable Secure Boot**

**After Install:**
- run one-key-hdpi script to enable hidpi resolution with 1,3,1 options when asked (https://github.com/xzhih/one-key-hidpi) 
- set hidpi resolution using RDM tool (https://github.com/usr-sse2/RDM), for me 1680x945 seems the best
- disable Force Click in System Pref -> Trackad -> Point and Click (and enable Secondary Click aka Right click if you wish) 


**Almost everything works except:**
* Internal microphone and 3.5mm microphone input(only sound output works)
* Bluetooth microphone with integrated Intel Wifi/Bluetooth (worked on BCM94360NG with Galaxy Buds)
note: Mic works but only after soft rebooting from Windows, after sleep stops working. Hopefully they can fix this issue in IntelBluetoothFirmware kext
https://github.com/OpenIntelWireless/IntelBluetoothFirmware/issues/262
* Fibocom WWAN
* Hibernate (Sleep working great!)
* Keyboard nipple and buttons  

**Buggy:**
Sometime after upgrading to Big Sur and/or installing newer VoodooI2c I encountered some weird trackpad behavior while trying to mark text or drag-and-drop using touchpad and two fingers. For example I would click(mark) on the begining of the text with 1st finger press on the bottom left trackpad(virtual left mouseclick), and hold it..while using 2nd finger to mark text (or drag-and-drop), but as soon as I lift the 2nd finger (but still holding first finger bottom left) the text gets unmarked (or drag and drop gets - dropped) as if I removed my 1st finger from bottom left(I didnt :). IDK why or when it started to happen but it annoys me alot :/. Worked perfectly on Catalina before(or older OpenCore/VoodooI2C). If anybody figures it out, please let me know!!!

**Color Banding:**
If you are lucky as I am and decided to upgrade your screen from stock 200nits to 400nits one (CMN14E0/N140HCA-GA3), or live outside central/eastern EU where you get decent lcd panel OOB.. you are out of luck if you are sensitive to screen banding like I am :) Your Launchpad and many apps will display banding artefacts since this screen is 6bits (262K colors) and not 8bit (16M colors). Not that your eyes will see the difference (in Windows :) but in MacOS every iGPU after Skylake will expect a minimum of 8bit screen and will not allow dithering to show correct color on 6bit screen. Only option is to spoof Skylake iGPU but that breaks sleep and breaks backlight control (stuck at 100% backlight). There is no fix for this as of now. If you want to try this config open an issue and I will send you updated EFI, but breaks sleep, no output after sleep (you have to manually restart -> hold power button), and no backlight control. But the color issue is fixed though :) 
![20210411_154013 (1)](https://user-images.githubusercontent.com/69514506/115157322-ea30df80-a088-11eb-83d3-f42e02507671.jpg)
Screenshot is from here -> Gradients test https://www.eizo.be/monitor-test/
