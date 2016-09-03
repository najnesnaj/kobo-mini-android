# kobo-mini-android
These files are modifications so android works on the kobo mini.




https://github.com/marek-g/kobo-kernel-2.6.35.3-marek
arch/arm/mach-mx5/mx50_rdp.c
The Kobo Mini uses a different port on the SoC for the internal uSDHC to other readers from in i.MX507 family... SD3


kobo u-boot-2009.08 sources
include/configs/mx50_rdp.h
The Android uses partition 2 instead of partition 1, other command line parameters have been added
/mmcblk0p2 rootfstype=ext4 rootwait rw noinitrd init=/init video=mxc_elcdif_fbff


--------------------------I used the android image for the kobo touch Marek Gibek prepared----------
get hardware config from original kobo mini (sd card is mmcblk1)
dd if=/dev/mmcblk1 of=kobo_mini_hw_config.img skip=524272 bs=1 count=67

write hw-config
dd if=kobo_mini_hw_config.img of=/dev/mmcblk1 seek=524272 bs=1


write U-boot
dd if=u-boot_mddr_256-E50610-K4X2G323PC.bin skip=2 of=/dev/mmcblk1 bs=512 seek=2

write kernel
dd if=uImage of=/dev/mmcblk1 bs=512 seek=2048
------------------------------
