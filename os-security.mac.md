---
id: vxbi3i0e35z2g1ypdbm536b
title: Mac
desc: ''
updated: 1653130112988
created: 1653130096530
---

# macOS Security Overview

- [ ] Learn about where to find hardware and software specifications.
- [ ] Learn how to see all current activity
- [ ] Learn about where to collect log files.

- [ ] Learn about the various security settings within macOS.

- [ ] Learn about the recovery partition and what services it offers.

---

## macOS Auditing

### System Info

About my Mac menu setting is the quickest way to gather information any macOS operating system.

![OS](https://support.apple.com/library/content/dam/edam/applecare/images/en_US/macbookpro/macos-sierra-macbookpro-apple-menu-about-this-mac-system-info.jpg)

![System info](https://www.howtogeek.com/thumbcache/2/200/c3b95b0063665c7a2debaf5bb4e644d1/wp-content/uploads/2015/05/img_555e1ca7180ff.png)

- The Overview screen will provide overview of the hardware specifications, including the make and model, processor, memory, graphics, and the serial number of the device.
  - Display
  - Storage capacity
  - Support tab for useful links on Apple.com

### Activity Monitor

![Activity](https://www.intego.com/mac-security-blog/wp-content/uploads/2017/02/cpu.png)

Similar to Windows, Activity Monitor is the best way to get real-time information about everything that is happening.

- CPU
- Memory
- Active processes
- Disk space
- Network activity

### Console

Found in the Utilities folder in macOS's application for logging any and all information.

## macOS Security Settings

All of security settings found in System Preferences in Security and Privacy settings.

### General Settings & GateKeeper

- Change administrative password
- GateKeeper functionality to prevent unauthorized third-party apps from being installed.

### FileVault

- macOS disk encryption feature provides 128-bit AES encryption.
- Requires password on boot before the computer, data and files can be accessed.

### Privacy

- Allows to control permissions and access to computer features.
  - Webcam camera
  - Microphone
  - Input monitoring

### Startup Disk

- View any internal partition and network drives.

---

## macOS Recovery

### macOS Utilities

- Hidden partition on macOS recovery replaces the installation discs that come with new computers.
- Access by restarting Mac while holding down the R key.

![macOS Utilities](https://www.cisdem.com/resource/attach/file/images/macos-utilities.jpg)

### Disk Utility

- Offers a lot of functionality to managing storage on macOS.
- Allows to run first aid, partition or create more volumes on the storage, or erase the drive altogether.
  - Restore from Time Machine Backup
  - Reinstall macOS
  - Get Help Online via Safari browser
  - Access Disk Utility
- Requires administrator access to make any changes.
  - If the disk is encrypted with filevault, the key will be required to unlock the the drive to make any modifications.
- If the hidden partition is erased or reformatted, macOS has an internet recovery by booting while holding `option + R`.
  - Requires an internet connection to download macOS utilities.
