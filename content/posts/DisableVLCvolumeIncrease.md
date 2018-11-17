+++
title = "Disabling VLC volume increase"
date = 2018-10-28T10:24:50+05:30
tags = [""]
categories = [""]
draft = false
+++

If you use the VLC player, it is suggested that you do not increase the volume higher than 100% in order to avoid potential damage to speakers. 

### Why is it needed?
Increasing volume above 100% in VLC can damage your speakers. [Dell](https://www.dell.com/community/Laptops-General-Read-Only/VLC-Media-Player-WARNING/td-p/4082242) and HP do not cover this damage under warranty.

### Why does it happen?
The VLC player can allow large power output through speaker than the original sound output. So the speaker might not be able to handle this output power. (In recent BIOSes and Drivers, Dell has limited the speaker power output)

### What is the Solution?
 Disable all the possible options which can lead to an accidental increase in sound.

1. Disable mouse wheel control
    * Go to  Tools -> Preferences 
    * Select "Hotkeys" Tab
    * Now at the bottom of the screen you will see "Mouse wheel vertical axis control"
    * select "Ignore option"
    * Save the settings and restart the VLC. 
2. Remove CTRL+ UP and CTRL + Down hotkeys
   * Go to  Tools -> Preferences 
   * Select "Hotkeys" Tab
   * In the search bar search "volume"
   * There you will see two results "Volume up" and "Volume down"
   * Double-click on each of them and click Unset
   * Save the settings and restart the VLC. 
3. Limit the volume display to 100%
   * Go to  Tools -> Preferences 
   * Now at the bottom of the screen you will see "Show settings"
   * select "All"
   * Now go to Interface -> Main interfaces -> Qt
   * Scroll down to the very bottom, you will see "Maximum Volume Displayed"
   * Limit it "100"
   * Save the settings and restart the VLC. 

Please let me know if you are not able to do it.
