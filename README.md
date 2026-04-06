Tools and steps
~~~
### fsarchiver:
#   backup/savefs yoursysFS eg /dev/sda1
#   restore/restfs new/different eg /dev/sdc7

### grub:
# working linux OS installation eg on /dev/sdc1
#   grub on external drive eg sdc

# boot in the helper sys OS on /dev/sdc1
# remove grub.cfg on restored sys eg /dev/sdc7
   mount /dev/sdc7 /mnt
   rm /mnt/boot/grub/grub.cfg
# change "/" dev (most likely some UUID is there, which is from the orig sys) in fstab to /dev/sdc7
   vi /mnt/etc/fstab
   umount /mnt
   # as the grub.cfg was removed in /dev/sdc7 grub-update will now work correctly, means it will not take the old UUID info from that grub.cfg , which causes chaos...
   grub-update
   reboot

### recreate grub.cfg on external /dev/sdc from  helper sys OS on /dev/sdc1
# you can now boot from /dev/sdc7 and
# update OS
# on every kernel update where grub.cfg will be recreated you will have to remove /boot/grub.cfg again, like described above:
# boot in the helper sys OS on /dev/sdc1
# remove grub.cfg on restored sys eg /dev/sdc7
   mount /dev/sdc7 /mnt
   rm /mn/boot/grub/grub.cfg
   grub-update
   reboot

# then you can fearlessly boot /dev/sdc7 again and upgrade again if needed ... until everything is working as you like it

### update
# this was done eg from linux mint 20.3 to upgrade to 22.3 on /dev/sdc7:
sudo -h mintupgrade
# mint 21
# upgrade to 21.3
sudo -h mintupgrade
# mint 22
# upgrade to 22.3


~~~
