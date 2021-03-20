# HP 840 G6 Big Sur 11.2.3

Based on work done by:
- https://github.com/kecinzer/hpelitebook850g5-opencore
- https://github.com/Joaotcs/Hackintosh-Elitebook-8x0-g5
- reddit posts by forgotten hero that helped me with my iGPU :)
- forums, etc..

**Upgrade your BIOS to latest version!**. \
**Set iGPU to 64MB in BIOS**. \
**Generate your own serial etc. https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#generate-a-new-serial**. 

Using itlwm Airport version for integrated Intel AX200, working perfectly for me:
- 802.11n only for now. 
- Bluetooth working great.
- I prefer this option much more then Broadcom bcm94352z and BCM94360NG (Plug and Play) since they often have problems with Power management enabled/freezing. Especially if using multi-boot with Windows or Linux like I am.

Almost everything works expect:
- integrated microphone :(
- Fibocom WWAN

Buggy:
- sometimes after upgrading to Big Sur and/or installing newer VoodooI2c I encountered some weird trackpad behavior while trying to mark text or drag-and-drop using touchpad and two fingers. For example I would click(mark) on the begining of the text with 1 finger on the bottom left, and hold it..while using another finger to mark a text or drag-and-drop, but as soon as I lift the other finger (but still holding first finger bottom left (aka virtual left mouse press area)) the text gets unmarked (or drag and drop gets - dropped) as If I moved my first finger from bottom left. IDK why or when it started to happen but It annoys me alot :/. If anybody figures it out, please let me know!
