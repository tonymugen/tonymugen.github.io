# Installing Arch Linux on the ThinkPad P73

The `lspci` output is

```sh
00:00.0 Host bridge: Intel Corporation Device 3e20 (rev 0d)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 0d)
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics 630 (Mobile) (rev 02)
00:04.0 Signal processing controller: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Thermal Subsystem (rev 0d)
00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th/8th Gen Core Processor Gaussian Mixture Model
00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10)
00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10)
00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
00:15.0 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH Serial IO I2C Controller #0 (rev 10)
00:15.1 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH Serial IO I2C Controller #1 (rev 10)
00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10)
00:16.3 Serial controller: Intel Corporation Cannon Lake PCH Active Management Technology - SOL (rev 10)
00:17.0 SATA controller: Intel Corporation Cannon Lake Mobile PCH SATA AHCI Controller (rev 10)
00:1b.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #17 (rev f0)
00:1c.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #1 (rev f0)
00:1c.5 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #6 (rev f0)
00:1c.7 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #8 (rev f0)
00:1d.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port #9 (rev f0)
00:1e.0 Communication controller: Intel Corporation Cannon Lake PCH Serial IO UART Host Controller (rev 10)
00:1f.0 ISA bridge: Intel Corporation Device a30e (rev 10)
00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection (7) I219-LM (rev 10)
01:00.0 VGA compatible controller: NVIDIA Corporation TU104GLM [Quadro RTX 4000 Mobile / Max-Q] (rev a1)
01:00.1 Audio device: NVIDIA Corporation TU104 HD Audio Controller (rev a1)
01:00.2 USB controller: NVIDIA Corporation TU104 USB 3.1 Host Controller (rev a1)
01:00.3 Serial bus controller [0c80]: NVIDIA Corporation TU104 USB Type-C UCSI Controller (rev a1)
02:00.0 Non-Volatile memory controller: Sandisk Corp Device 5006
04:00.0 PCI bridge: Intel Corporation JHL7540 Thunderbolt 3 Bridge [Titan Ridge 4C 2018] (rev 06)
05:00.0 PCI bridge: Intel Corporation JHL7540 Thunderbolt 3 Bridge [Titan Ridge 4C 2018] (rev 06)
05:01.0 PCI bridge: Intel Corporation JHL7540 Thunderbolt 3 Bridge [Titan Ridge 4C 2018] (rev 06)
05:02.0 PCI bridge: Intel Corporation JHL7540 Thunderbolt 3 Bridge [Titan Ridge 4C 2018] (rev 06)
05:04.0 PCI bridge: Intel Corporation JHL7540 Thunderbolt 3 Bridge [Titan Ridge 4C 2018] (rev 06)
06:00.0 System peripheral: Intel Corporation JHL7540 Thunderbolt 3 NHI [Titan Ridge 4C 2018] (rev 06)
2c:00.0 USB controller: Intel Corporation JHL7540 Thunderbolt 3 USB Controller [Titan Ridge 4C 2018] (rev 06)
52:00.0 Network controller: Intel Corporation Wi-Fi 6 AX200 (rev 1a)
54:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)
55:00.0 Non-Volatile memory controller: Sandisk Corp Device 5006
```

The `lscpu` output is

```sh
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
Address sizes:                   39 bits physical, 48 bits virtual
CPU(s):                          16
On-line CPU(s) list:             0-15
Thread(s) per core:              2
Core(s) per socket:              8
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       GenuineIntel
CPU family:                      6
Model:                           158
Model name:                      Intel(R) Core(TM) i9-9880H CPU @ 2.30GHz
Stepping:                        13
CPU MHz:                         4511.756
CPU max MHz:                     4800.0000
CPU min MHz:                     800.0000
BogoMIPS:                        4601.60
Virtualization:                  VT-x
L1d cache:                       256 KiB
L1i cache:                       256 KiB
L2 cache:                        2 MiB
L3 cache:                        16 MiB
NUMA node0 CPU(s):               0-15
Vulnerability Itlb multihit:     KVM: Mitigation: Split huge pages
Vulnerability L1tf:              Not affected
Vulnerability Mds:               Not affected
Vulnerability Meltdown:          Not affected
Vulnerability Spec store bypass: Mitigation; Speculative Store Bypass disabled via prctl and seccomp
Vulnerability Spectre v1:        Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:        Mitigation; Enhanced IBRS, IBPB conditional, RSB filling
Vulnerability Srbds:             Mitigation; TSX disabled
Vulnerability Tsx async abort:   Mitigation; TSX disabled
Flags:                           fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single ssbd ibrs ibpb stibp ibrs_enhanced tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp md_clear flush_l1d arch_capabilities
```

Disable secure boot in the BIOS by pressing `F1` (no need to also press `Fn`) after the Lenovo splash screen. Insert the Arch install media, reboot and press `F12` after the Lenovo splash screen to get to boot disk menu and select the USB Arch boot media. I used the 2020.07.01 release ISO for this installation.

## Requirements

I want full-disk encryption. The laptop came with a 1 TB NVMe drive. I added another 1 TB NVMe drive to the available extra port. I want to mirror them in RAID1. The `boot` partition is on one of the drives only (no RAID) and not encrypted. I am installing with WiFi.

The machine has a discrete NVIDIA GPU. I want it to be always on, with modesetting from the Intel card.

## Starting the process

Once at the Arch install boot screen, press `e` to enter kernel command line options. Add `video=1920x1080` to enlarge the console fonts (I have the 4K screen version of the P73 and the default resolution makes the letters tiny). It is not necessary to blacklist the nouveau driver anymore (at least with this combination of hardware and Arch media), unlike the [Pryx Pro](/ArchLinuxSys76OP.md) I did last year. The command should be separated by space from the rest of the options on the line but can be at the beginning or end. The WiFi card has functional firmware, checked by running

```sh
lspci -k
dmseg | grep iwlwifi
```

Use `iwctl` to connect to a network, the old `wifi-menu` is no longer included. I followed the instructions [here](https://wiki.archlinux.org/index.php/Iwd#iwctl).

```sh
iwctl
 > device list                  # the device is wlan0 on my machine
 > station wlan0 scan
 > station wlan0 get-networks
 > station wlan0 connect *SSID* # enter password
 > exit
```

Set up time and date.

```sh
timedatectl set-ntp true
timedatectl set-timezone America/New_York
```

## Disk preparation

Partition the target disks (here, they are `/dev/nvme0n1` and `/dev/nvme1n1`).

To list partitions:

```sh
fdisk -l
```

Start with the disk where the boot partition will reside:

```sh
gdisk /dev/nvme1n1
```

`p` to list current partitions
`o` to delete them all and create an empty GPT partition table
`n` to create new

- first (for EFI, code EF00): default start, end at +500M, otherwise defaults, erase ext4 signature if asked
- second (Linux RAID, code FD00): the rest of the disk

`p` to check if everything looks sane
`w` to write (THE DISK WILL BE ERASED AT THIS POINT)

Repeat with the `/dev/nvme0n1`, but only create a RAID partition. Format the EFI boot partition (left unencrypted):

```sh
mkfs.fat -F32 /dev/nvme1n1p1
```

Create the RAID1 array with the two RAID partitions.

```sh
mdadm --create --verbose --level=1 --metadata=1.2 --raid-devices=2 /dev/md/root /dev/nvme0n1p1 /dev/nvme1n1p2
watch -1n /proc/mdstat # to watch progress; takes ~1 hr for 1 TB
```

Encrypt the future LVM container:

```sh
cryptsetup luksFormat —-type luks1 /dev/md/md127
cryptsetup open /dev/md/md127 cryptlvm
```

I have to use `luks1` because GRUB does not support `luks2` as of this writing. Prepare the logical volumes:

```sh
pvcreate /dev/mapper/cryptlvm
vgcreate MainVolGroup /dev/mapper/cryptlvm
lvcreate -L 16G MainVolGroup -n swap
lvcreate -l 100%FREE MainVolGroup -n root

mkfs.ext4 /dev/MainVolGroup/root
mkswap /dev/MainVolGroup/swap

mount /dev/MainVolGroup/root /mnt
swapon /dev/MainVolGroup/swap
```

I am using 16G of space for SWAP. I want to be able to suspend to disk, but although I have 64G of RAM I found from previous experience that 16G is sufficient for that.

Mount the EFI boot partition:

```sh
mkdir /mnt/boot
mount /dev/nvme1n1p1 /mnt/boot
```

## Installation

Install Arch:

```sh
pacstrap /mnt mdadm lvm2 linux linux-firmware base base-devel python gvim git grub dhclient networkmanager gnome-keyring efibootmgr nvidia nvidia-utils nvidia-settings
```

Generate `fstab`:

```sh
genfstab -U /mnt >> /mnt/etc/fstab
```

Edit `/mnt/etc/crypttab` to add a line

```sh
cryptlvm UUID=_/dev/md/md127 UUID_ none luks,discard,timeout=5
```

The `discard` option enables [TRIM](https://wiki.archlinux.org/index.php/Solid_state_drive) support. There are security implications, but not serious enough for my use case. Read the linked documentation to decide for yourself. An easy way to transfer the UUID without typing it is to do

```sh
blkid -pi /dev/md/md127 | cut -d' ' -f3 >> /mnt/etc/crypttab
```

and edit the `crypttab` file to make it correct, or use `:read` in vim.

There used to be an issue with GRUB and LVM which caused grub-mkconfig to hang and grub-install to keep probing LVM devices. That no longer seems to be a problem. If it is for you, use this [workaround](https://bbs.archlinux.org/viewtopic.php?id=242594). I also have it in my [Oryx Pro](/ArchLinuxSys76OP.md) instructions.

## Configuration

Move into the fresh Arch installation on the main disk. Note that the paths will no longer require `/mnt` in front.

```sh
arch-chroot /mnt
```

Edit `/etc/mkinitcpio.conf` (this is now on the target drive):

```sh
HOOKS=(base udev autodetect **keyboard** **keymap** modconf block **mdadm_udev** **encrypt** **lvm2** **resume** filesystems fsck)
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)

mkinitcpio -p linux
```

Use `blkid` to list UUIDs of devices. Edit `/etc/default/grub` to modify variables. Append "lvm" to `GRUB_PRELOAD_MODULES`. Uncomment the `GRUB_ENABLE_CRYPTDISK=y` line. Append `cryptdevice=UUID=UUID-of-/dev/md/md127:cryptlvm root=/dev/MainVolGroup/root resume=/dev/MainVolGroup/swap ec_sys.write_support=1 nvidia-drm.modeset=1 video=1920x1080 module_blacklist=nouveau` to `GRUB_CMDLINE_LINUX_DEFAULT`. The `resume=...` part is for suspend to disk support. Install GRUB on EFI and make the config:

```sh
grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=ArchLinuxGRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

Activate NetworkManager:

```sh
systemctl enable NetworkManager
```

Time zone and locale specification (I am in New York, yours may be different).

```sh
ln -sf /usr/share/zoneinfo/America/New_York /etc/localtime
hwclock --systohc
```

Uncomment all `en_US` entries in `/etc/locale.gen`.

```sh
locale-gen
```

Set `LANG=en_US.UTF-8` in newly created `/etc/locale.conf`.

Network settings:

Create `/etc/hostname` and write *nerv* there (that is the name I gave the laptop; substitute what you like). Edit `/etc/hosts` to add

```sh
127.0.0.1  localhost
::1        localhost
127.0.0.1  nerv.localdomain nerv
```

Add root password and at least one non-root user before exiting `chroot`. Exit `chroot`, optionally `unmount -R /mnt`, and shut down the computer. Remove the USB drive and start the laptop again.

## Finish up

Once booted into the new system, install connect to WiFi again, now using `nmcli`.

```sh
nmcli device wifi list
nmcli device wifi connect *SSID* --ask
```

and enter the WiFi password (if any) at the prompt.

I install all the basic things I need, like Xorg etc, and pull down my git bare repository of dot files. Instructions for that are [here](https://www.atlassian.com/git/tutorials/dotfiles). I use `lightDM` to manage login. To get the [NVIDIA Optimus](https://wiki.archlinux.org/index.php/NVIDIA_Optimus) in the NVIDIA graphics only mode to work, two files are necessary: `10-nvidia-drm-outputclass.conf` (I have an example [here](https://github.com/tonymugen/dotfiles/blob/master/systemConf/10-nvidia-drm-outputclass.conf)) goes into the `/usr/share/X11/xorg.conf.d` directory. You also need to run `xrandr` on startup. I have a [script](https://github.com/tonymugen/dotfiles/blob/master/systemConf/displaySetup.sh) I put in the `/etc/lightdm` directory. Not having this file while activating modesetting with `10-nvidia-drm-outputclass.conf` will result in a black screen. If that happens, open another `TTY` (e.g., `Fn+Ctrl+Alt+F5`) and delete `10-nvidia-drm-outputclass.conf` from `/usr/share/X11/xorg.conf.d` I also put the `nvidia.hook` file (example [here](https://github.com/tonymugen/dotfiles/blob/master/systemConf/nvidia.hook)) into `/etc/pacman.d/hooks` to make sure `mkinitcpio` is run after updates involving `linux` or `nvidia` packages.
