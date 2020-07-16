# Installing Arch Linux on the ThinkPad P73

`F1` after Lenovo splash screen to get into BIOS. `F12` to get to boot disk menu. No need for the `Fn` key.

blacklisting nouveau no longer necessary

Use `iwctl` instead of wifi-menu.

```sh
iwctl
device list    # the device is wlan0
 station wlan0 scan
 station wlan0 get-networks
 station wlan0 connect *SSID* # enter password
 exit
```

For RAID1: `gdisk` partition FD00. Then

```bash
mdadm --create --verbose --level=1 --metadata=1.2 --raid-devices=2 /dev/md/root /dev/nvme0n1p1 /dev/nvme1n1p2
watch -1n /proc/mdstat # to watch progress; takes ~1 hr for 1 TB
```

Then proceed with LVM on LUKS (--type luks1) as before, using /dev/md/md127.

mdadm lvm2 efibootmgr linux and linux-firmware has to be added explicitly in pacstrap

add root pwd and user before exiting chroot
