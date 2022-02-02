# Developer's Guide
## Setting up a Full Development Environment
TODO

Quick notes:
* Install vsCode.
* Install PlatformIO.
  * Install the Arduino platform
  * Install the Teensy boards
  * (Unfortunately) Modify Teensy files for USB_Serial_Audio_MTP support
* Get the `SOAR-Code` source code from GitHub (currently (2022-01-17) a private repo, but this might change.)
* Get several Halibut Electronics maintained branches of libraries from GitHub, then link them into `SOAR-Code`.
* Open source code in PlatformIO.
* Build, Upload, Profit!

## Flashing a pre-built `.hex` file.
### Install `TeensyLoader` (Do this once)
Download and install the Teensy Loader for your OS of choice: https://www.pjrc.com/teensy/loader.html

**NOTE FOR LINUX USERS** Make sure you follow all the instructions on that page, especially the part about putting a file in `/etc/udev/rules.d/`.  Without this, your user account won't have permissions to talk to the USB sub-system.

Plug in your SOAR to a USB port on your computer, and start the `TeensyLoader`.  (It doesn't matter what order this is done in.)  If `TeensyLoader` can see the SOAR, the two arrow buttons (the "swooping down" arrow for `Program`, and the "right pointing arrow" for `Reboot`) will be green.  If it can't see the SOAR, then they will be gray'd out.

If the SOAR is totally bricked (so that the boot loader isn't even running), the arrows will be gray'd out too.  That (probably) ok, we can fix this.

### Downloading New Firmware
New releases of firmware are available here: https://electronics.halibut.com/releases/SOAR/

Files are date stamped. Download the latest release.  This will give you a file that ends with `.hex`.  This is the firmware file.  Note this filename and location.

### Flash the Firmware
Click on the Document icon, `Open HEX File`.  Load the `.hex` file you just downloaded.

* **If the `Program` button works**, then press it.
* **If the `Program` button is gray'd out or does not work**, then use [a long plastic tool of some kind](https://www.ifixit.com/Store/Tools/Spudger/IF145-002?o=4) and press the (physical) `Program` button on the Microcontroller in the middle of the middle board. 
  * "Golly, Mark, could you make that any harder to get to?"  Sorry about that...  I don't have to do this when programming from PlatformIO, it just programs the Teensy directly and automatically. I haven't yet figured out what PlatformIO is doing that makes this work automatically. I'll update this document if I figure it out. (I also accept pull requests! ;-)

### Getting At The SD Card (Version v2.1 only)
**Note:** This section only applies to the v2.1 Prototype hardware.  This will probably be replaced when v2.2 Production hardware is available.

**Note:** This is (hopefully) no longer necessary, since the 2022-02-01 build, which adds MTP access to the SD card over USB.

There's an SD Card on the buried end of the Teensy. This stores all configuration, audio recordings, etc.  It is presented to your computer over USB as an MTP device (like a camera or phone).  If you can't get MTP working, or otherwise want direct access to this SD card, you'll need to remove the UI board on top to access the SD card:
* Remove all power (including USB cable) from SOAR
* Remove the four screws holing the UI Deck (the top board) from the stack.
  * Note: The UI Deck is the green board, not just the display on the red board. The display is part of the UI Deck, and is hard soldered down. Don't try to remove it.
* Carefully remove the UI Deck board from the stack.  Note that there are three different headers connecting the UI Deck to the DA Deck (the middle board).  Be careful not to bend these pins.
* **ONLY REMOVE OR INSERT THE SD CARD WHEN THE MICROCONTROLLER IS NOT POWERED**

The physical `Program` Button is also much easier to access with the UI Deck removed.  It is safe to flash SOAR with the UI Deck removed.

**Be very careful when replacing the UI Deck!**  The tall header pins between the UI Deck and DA Deck are very bendy.  It may take a bit of "Insert the long strip of pins first, just a little bit, then kinda force the UI Deck to the side a bit while getting the middle pins to go in, then forcing it a different way to get the last three pins in" or something like this. It's a little fiddly.