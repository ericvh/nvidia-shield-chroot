Eric's NVIDIA Shield TV Chroot Hack

This is a quick and dirty hack on top of the TWRP recovery stuff
which chroots into ubuntu on an sdcard versus starting the recovery
GUI.  There are essentially a few steps:
* update your device to 1.2.  Earlier firmware have some issues with booting without HDMI connected and may have other instabilities  Later versions may have different problems.
* enable debug mode on your device and oem unlock fastboot 
  http://forum.xda-developers.com/android-tv/nvidia-shield-android-tv/shield-android-tv-rooted-t3123197
* grab bootimg_tools
  http://forum.xda-developers.com/showthread.php?t=2319018
* grab recovery images 
* grab an ubuntu aarch64 tarball and unpack it on an sdcard formated ext4
* (OPTIONAL) just use ericvh/arch64-ubuntu-dev from docker if you like
* use bootimg tools to unpack recovery boot.img
* update the ramdisk with init.rc and add/update /sbin/ubuntu
* repack ramdisk
* mkbootimg with new kernel (optional?) and new ramdisk
* use: fastboot boot newboot.img
* if that works, fastboot flash boot newboot.img
* for the last step to work you may have to cut down ramdisk, I deleted a bunch of the recovery stuff to make it fit in mine and built my kernel without a bunch of debug.

NOTES:
* probably should fix to use pivot_root or switch_root - haven't gotten this to work
* there's probably a multirom path here as well, but I haven't really tried
* happy to pull updates to any of this if folks have better methods...
