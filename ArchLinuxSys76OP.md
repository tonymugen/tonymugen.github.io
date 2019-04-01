
# Installing Arch Linux on the System76 Oryx Pro

The `lspci -k` output, run from the Pop! OS installation, is

	00:00.0 Host bridge: Intel Corporation 8th Gen Core Processor Host Bridge/DRAM Registers (rev 07)
		Subsystem: CLEVO/KAPOK Computer 8th Gen Core Processor Host Bridge/DRAM Registers
	00:01.0 PCI bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor PCIe Controller (x16) (rev 07)
		Kernel driver in use: pcieport
	00:02.0 VGA compatible controller: Intel Corporation Device 3e9b
		Subsystem: CLEVO/KAPOK Computer Device 95e1
		Kernel driver in use: i915
		Kernel modules: i915
	00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
		Subsystem: CLEVO/KAPOK Computer Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
	00:12.0 Signal processing controller: Intel Corporation Cannon Lake PCH Thermal Controller (rev 10)
		Subsystem: CLEVO/KAPOK Computer Cannon Lake PCH Thermal Controller
		Kernel driver in use: intel_pch_thermal
		Kernel modules: intel_pch_thermal
	00:14.0 USB controller: Intel Corporation Cannon Lake PCH USB 3.1 xHCI Host Controller (rev 10)
		Subsystem: CLEVO/KAPOK Computer Cannon Lake PCH USB 3.1 xHCI Host Controller
		Kernel driver in use: xhci_hcd
	00:14.2 RAM memory: Intel Corporation Cannon Lake PCH Shared SRAM (rev 10)
		Subsystem: Intel Corporation Cannon Lake PCH Shared SRAM
	00:16.0 Communication controller: Intel Corporation Cannon Lake PCH HECI Controller (rev 10)
		Subsystem: CLEVO/KAPOK Computer Cannon Lake PCH HECI Controller
		Kernel driver in use: mei_me
		Kernel modules: mei_me
	00:17.0 SATA controller: Intel Corporation Device a353 (rev 10)
		Subsystem: CLEVO/KAPOK Computer Device 95e1
		Kernel driver in use: ahci
		Kernel modules: ahci
	00:1d.0 PCI bridge: Intel Corporation Cannon Lake PCH PCI Express Root Port 9 (rev f0)
		Kernel driver in use: pcieport
	00:1d.5 PCI bridge: Intel Corporation Device a335 (rev f0)
		Kernel driver in use: pcieport
	00:1d.6 PCI bridge: Intel Corporation Device a336 (rev f0)
		Kernel driver in use: pcieport
	00:1d.7 PCI bridge: Intel Corporation Device a337 (rev f0)
		Kernel driver in use: pcieport
	00:1f.0 ISA bridge: Intel Corporation Device a30d (rev 10)
		Subsystem: CLEVO/KAPOK Computer Device 95e1
	00:1f.3 Audio device: Intel Corporation Cannon Lake PCH cAVS (rev 10)
		Subsystem: CLEVO/KAPOK Computer Cannon Lake PCH cAVS
		Kernel driver in use: snd_hda_intel
		Kernel modules: snd_hda_intel
	00:1f.4 SMBus: Intel Corporation Cannon Lake PCH SMBus Controller (rev 10)
		Subsystem: CLEVO/KAPOK Computer Cannon Lake PCH SMBus Controller
		Kernel driver in use: i801_smbus
		Kernel modules: i2c_i801
	00:1f.5 Serial bus controller [0c80]: Intel Corporation Cannon Lake PCH SPI Controller (rev 10)
		Subsystem: CLEVO/KAPOK Computer Cannon Lake PCH SPI Controller
	01:00.0 VGA compatible controller: NVIDIA Corporation GP104M [GeForce GTX 1070 Mobile] (rev a1)
		Subsystem: CLEVO/KAPOK Computer GP104M [GeForce GTX 1070 Mobile]
		Kernel driver in use: nvidia
		Kernel modules: nvidiafb, nouveau, nvidia_drm, nvidia
	01:00.1 Audio device: NVIDIA Corporation GP104 High Definition Audio Controller (rev a1)
		Kernel driver in use: snd_hda_intel
		Kernel modules: snd_hda_intel
	02:00.0 Non-Volatile memory controller: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981
		Subsystem: Samsung Electronics Co Ltd NVMe SSD Controller SM981/PM981
		Kernel driver in use: nvme
		Kernel modules: nvme
	03:00.0 Network controller: Intel Corporation Wireless 8265 / 8275 (rev 78)
		Subsystem: Intel Corporation Dual Band Wireless-AC 8265
		Kernel driver in use: iwlwifi
		Kernel modules: iwlwifi
	04:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 0c)
		Subsystem: CLEVO/KAPOK Computer RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
		Kernel driver in use: r8169
		Kernel modules: r8169
	05:00.0 SD Host controller: Realtek Semiconductor Co., Ltd. RTS5250 PCI Express Card Reader (rev 01)
		Subsystem: CLEVO/KAPOK Computer RTS5250 PCI Express Card Reader
		Kernel driver in use: sdhci-pci
		Kernel modules: sdhci_pci
		00:00.0 Host bridge: Intel Corporation Xeon E3-1200 v5/E3-1500 v5/6th Gen Core Processor Host Bridge/DRAM Registers (rev 08)
		00:02.0 VGA compatible controller: Intel Corporation Skylake GT2 [HD Graphics 520] (rev 07)
		00:08.0 System peripheral: Intel Corporation Xeon E3-1200 v5/v6 / E3-1500 v5 / 6th/7th Gen Core Processor Gaussian Mixture Model
		00:13.0 Non-VGA unclassified device: Intel Corporation Sunrise Point-LP Integrated Sensor Hub (rev 21)
		00:14.0 USB controller: Intel Corporation Sunrise Point-LP USB 3.0 xHCI Controller (rev 21)
		00:14.2 Signal processing controller: Intel Corporation Sunrise Point-LP Thermal subsystem (rev 21)
		00:16.0 Communication controller: Intel Corporation Sunrise Point-LP CSME HECI #1 (rev 21)
		00:17.0 SATA controller: Intel Corporation Sunrise Point-LP SATA Controller [AHCI mode] (rev 21)
		00:1c.0 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #1 (rev f1)
		00:1c.2 PCI bridge: Intel Corporation Sunrise Point-LP PCI Express Root Port #3 (rev f1)
		00:1f.0 ISA bridge: Intel Corporation Sunrise Point-LP LPC Controller (rev 21)
		00:1f.2 Memory controller: Intel Corporation Sunrise Point-LP PMC (rev 21)
		00:1f.3 Audio device: Intel Corporation Sunrise Point-LP HD Audio (rev 21)
		00:1f.4 SMBus: Intel Corporation Sunrise Point-LP SMBus (rev 21)
		00:1f.6 Ethernet controller: Intel Corporation Ethernet Connection I219-LM (rev 21)
		02:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS525A PCI Express Card Reader (rev 01)

The `lscpu` output is

	Architecture:        x86_64
	CPU op-mode(s):      32-bit, 64-bit
	Byte Order:          Little Endian
	CPU(s):              12
	On-line CPU(s) list: 0-11
	Thread(s) per core:  2
	Core(s) per socket:  6
	Socket(s):           1
	NUMA node(s):        1
	Vendor ID:           GenuineIntel
	CPU family:          6
	Model:               158
	Model name:          Intel(R) Core(TM) i7-8750H CPU @ 2.20GHz
	Stepping:            10
	CPU MHz:             897.328
	CPU max MHz:         4100.0000
	CPU min MHz:         800.0000
	BogoMIPS:            4416.00
	Virtualization:      VT-x
	L1d cache:           32K
	L1i cache:           32K
	L2 cache:            256K
	L3 cache:            9216K
	NUMA node0 CPU(s):   0-11
	Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid fsgsbase tsc_adjust bmi1 avx2 smep bmi2 erms invpcid mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp flush_l1d


## Requirements

I want to have full-disk encryption, with the exception of the boot partition and I am installing with WiFi. There is a discrete NVIDIA graphics card. I would like to use it for OpenCL/CUDA and for an external monitor.

## Preliminaries

I used the `archlinux-2019.01.01-x86_64.iso`, put it on a USB flash drive using `dd` (standard procedure).

Inserted the USB drive, booted while pressing `F7` on boot to enter the boot disk picker. Once there, press `e` to enter kernel command line options. Add `video=1920x1080` to enlarge the console fonts (the machine I have the 4K screen and the default resolution makes the letters tiny) and `module_blacklist=nouveau` to switch off the NVIDIA GPU for now. The commands should be separated by space and entered at the end of the line. Switching off the `nouveau` driver is necessary, otherwise any hardware listing (such as `lspci`) will hang with fans blazing. The WiFi card has functional firmware, checked by running

	lspci -k
	dmseg | grep iwlwifi

List WiFi networks, pick the relevant and follow prompts to connect:

	wifi-menu

Set up time and date.

	timedatectl set-ntp true
	timedatectl set-timezone America/New_York

I want to use LVM on LUKS to get full-disk encryption, including the SWAP. `/boot` will be unencrypted.

## Disk preparation

Partition the target disk (here, it is `/dev/sda`).

To list partitions:

	fdisk -l

System76 requires the EFI partition to be in `/boot` so that it can do firmware updates. I leave the secondary disk alone. It is already formatted and has data on it. I use `gdisk` to set up GPT.

	gdisk /dev/nvme0n1

`p` to list current partitions
`o` to delete them all and create an empty GPT partition table
`n` to create new

 - first (for EFI, code EF00): default start, end at +500M, otherwise defaults, erase ext4 signature if asked
 - second (LVM, code 8E00): the rest of the disk

`p` to check if everything looks sane
`w` to write (THE DISK WILL BE ERASED AT THIS POINT)

Format the EFI boot partition (left unencrypted):

	mkfs.fat -F32 /dev/nvme0n1p1

Create the non-boot file systems. The following will require coming up with a passphrase. I followed the instructions in [Encrypting an entire system](https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system).

Encrypt the future LVM container:

	cryptsetup luksFormat —-type luks1 /dev/nvme0n1p2
	cryptsetup open /dev/nvme0n1p2 cryptlvm

I have to use `luks1` because GRUB does not support `luks2` as of this writing. That is not an issue in the [ThinkPad](/ArchLinuxThinkPadX1C4gen.md) set-up, as far as I can tell because I am booting from BIOS there rather than EFI. Prepare the logical volumes:

	pvcreate /dev/mapper/cryptlvm
	vgcreate MainVolGroup /dev/mapper/cryptlvm
	lvcreate -L 16G MainVolGroup -n swap
	lvcreate -l 100%FREE MainVolGroup -n root

	mkfs.ext4 /dev/MainVolGroup/root
	mkswap /dev/MainVolGroup/swap

	mount /dev/MainVolGroup/root /mnt
	swapon /dev/MainVolGroup/swap

Mount the EFI boot partition:

	mkdir /mnt/boot
	mkdir /mnt/boot/efi
	mount /dev/nvme0n1p1 /mnt/boot/efi

## Installation

Install Arch:

	pacstrap /mnt base base-devel python gvim git grub dhclient networkmanager gnome-keyring efibootmgr

Generate `fstab`:

	genfstab -U /mnt >> /mnt/etc/fstab

Edit `/mnt/etc/crypttab` to add a line

	cryptlvm	UUID=_/dev/nvme0n1p2 UUID_	none	luks,discard,timeout=5

The `discard` option enables [TRIM](https://wiki.archlinux.org/index.php/Solid_state_drive) support. There are security implications, but not serious enough for my use case. Read the linked documentation to decide for yourself. An easy way to transfer the UUID without typing it is to do

	blkid -pi /dev/nvme0n1p2 | cut -d' ' -f3 >> /mnt/etc/crypttab

and edit the `crypttab` file to make it correct, or use `:read` in vim.

There is an issue with GRUB and LVM which causes grub-mkconfig to hang and grub-install to keep probing LVM devices. For the [workaround](https://bbs.archlinux.org/viewtopic.php?id=242594), prepare the following:

	mkdir /mnt/hostlvm
	mount --bind /run/lvm /mnt/hostlvm

## Configuration

Move into the fresh Arch installation on the main disk. Note that the paths will no longer require `/mnt` in front.

	arch-chroot /mnt

To deal with the GRUB/LVM problem, run

	ln -s /hostlvm /run/lvm

Edit `/etc/mkinitcpio.conf` (this is now on the target drive):

	HOOKS=(base udev autodetect **keyboard** **keymap** modconf block **encrypt** **lvm2** **resume** filesystems fsck) # resume is included for suspend to disk support

	mkinitcpio -p linux

Use `blkid` to list UUIDs of devices. Edit `/etc/default/grub` to modify variables. Append "lvm" to `GRUB_PRELOAD_MODULES`. Uncomment the `GRUB_ENABLE_CRYOTDISK=y` line. Append `cryptdevice=UUID=UUID-of-/dev/nvme0n1p2:cryptlvm root=/dev/MainVolGroup/root resume=/dev/MainVolGroup/swap ec_sys.write_support=1 video=1920x1080 module_blacklist=nouveau` to `GRUB_CMDLINE_LINUX_DEFAULT`. The `resume=...` part is for suspend to disk support. Install GRUB on EFI:

	grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=ArchLinuxGRUB 

Make the GRUB config:

	grub-mkconfig -o /boot/grub/grub.cfg

Activate NetworkManager:

	systemctl enable NetworkManager

Time zone and locale specification (I am in New York, yours may be different).

	ln -sf /usr/share/zoneinfo/America/New_York /etc/localtime
	hwclock --systohc

Uncomment all `en_US` entries in `/etc/locale.gen`.

	locale-gen

Set `LANG=en_US.UTF-8` in newly created `/etc/locale.conf`.

Network settings:

Create `/etc/hostname` and write *nerv* there (that is the name I gave the laptop; substitute what you like). Edit `/etc/hosts` to add

	127.0.0.1	localhost
	::1			localhost
	127.0.0.1	nerv.localdomain nerv

Exit `chroot`, optionally `unmount -R /mnt`, and shut down the computer. Remove the USB drive and start the laptop again.

## Driver installation

Start by connecting to WiFi

	nmcli device wifi list
	nmcli device wifi connect *SSID* --ask

and enter the WiFi password (if any) at the prompt.

Start by installing the NVIDIA drivers:

	pacman -S nvidia nvidia-utils nvidia-settings

The System76 drivers are available from AUR. Cannot install these using root, so I generate my root password and add a regular user first.

	passwd
	useradd -m -g wheel *username*
	passwd tonyg

To enable `sudo` for the user, uncomment the `%wheel ALL=(ALL) ALL` line in `/etc/sudoers`. I like to reboot etc without entering a password, so I also add `%wheel ALL=(ALL) NOPASSWD: REBOOT`. I add `/sbin/shutdown` to the `REBOOT` alias. Reboot the laptop. Login as the regular user and proceed with driver installation. First install kernel headers:

	pacman -S linux-headers

Now install the kernel modules (mostly following the instructions [here](https://ebobby.org/2018/07/15/archlinux-on-oryp4/)):

	git clone https://aur.archlinux.org/system76-dkms.git
	cd system76-dkms
	makepkg -sci
	modprobe system76
	cd
	rm -rvf system76-dkms

	git clone https://aur.archlinux.org/system76-firmware-daemon.git
	cd system76-firmware-daemon
	makepkg -sci
	systemctl enable --now system76-firmware-daemon.service
	cd
	rm -rvf system76-firmware-service

	git clone https://aur.archlinux.org/system76-io-dkms.git
	cd system76-io-dkms
	makepkg -sci
	modprobe system76-io
	cd
	rm -rvf system76-io-dkms

	git clone https://aur.archlinux.org/system76-driver.git
	cd system76-driver
	makepkg -sci
	cd
	rm -rvf system76-driver

	git clone https://aur.archlinux.org/system76-power.git
	cd system76-power
	makepkg -sci
	systemctl enable --now system76-power.service
	cd
	rm -rvf system76-power

## Environment set-up

### Basic connectivity

I start with installing `htop` to test that everything is working. Then

 - `ethtool` to manage the internet card
 - `iptables` firewall
 - `openvpn` VPN
 - `networkmanager-openvpn` VPN plugin for `NetworkManager`

 To set up the [firewall](https://wiki.archlinux.org/index.php/Simple_stateful_firewall), write the following (with `sudo`):

	iptables -N TCP
	iptables -N UDP
	iptables -P FORWARD DROP
	iptables -P OUTPUT ACCEPT
	iptables -P INPUT DROP
	iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
	iptables -A INPUT -i lo -j ACCEPT
	iptables -A INPUT -m conntrack --ctstate INVALID -j DROP
	iptables -A INPUT -p icmp --icmp-type 8 -m conntrack --ctstate NEW -j ACCEPT
	iptables -A INPUT -p udp -m conntrack --ctstate NEW -j UDP
	iptables -A INPUT -p tcp --syn -m conntrack --ctstate NEW -j TCP
	iptables -A INPUT -p udp -j REJECT --reject-with icmp-port-unreachable
	iptables -A INPUT -p tcp -j REJECT --reject-with tcp-reset
	iptables -A INPUT -j REJECT --reject-with icmp-proto-unreachable

Save the rules to a file. I retain a copy for re-use on other systems.

	iptables-save | sudo tee /etc/iptables/iptables.rules
	systemctl enable iptables

### X windows

Next, I set up X windows. I want the whole thing, including the fonts, so I go with the `xorg` group.

	pacman -S --needed xf86-video-intel mesa xorg xorg-xinit xorg-xrdb xorg-xlsfonts xorg-xfontsel pango

Add a version of the i3 window manager along with some needed add-ons.

	pacman -S --needed i3-gaps i3status i3blocks i3lock termite termite-terminfo dmenu network-manager-applet feh compton

Copy fonts that I have in the `add_fonts` directory in this repository to the freshly created `/usr/share/fonts/added`, then run

	fc-cache -v

for `fontconfig` to recognize them (check with `fc-list`). Copy the `local.conf` file from the `systemwide_conf` directory to `/etc/fonts`. Copy the `60-fonts.conf` to `/etc/X11/xorg.conf.d`.

To set up a good-looking environment, I need to install

	pacman -S arc-gtk-theme lxappearance pulseaudio pavucontrol lm_sensors psensor acpi scrot sysstat

For a graphical login, I use `lightDM`.

	pacman -S lightdm lightdm-gtk-greeter

I included the modified config files in the `systemwide_config` directory in this repository. Move `lightdm.conf` and `lightdm-gtk-greeter.conf` to `/etc/lightdm`. Add any images you want for background to `/usr/share/pixmap`.

### Vim

Next, I set up my vim environment. I move the `.vimrc` and `.vim` from this repository to the home directory. For `YouCompleteMe` to work, I need to install `cmake`:

	pacman -S cmake clang python2 boost

Change to the `.vim/bundle` directory and clone the [VundleVim](https://github.com/VundleVim/Vundle.vim) repository to it. Start `vim` and run

	:PluginInstall

After that, change to `YouCompleteMe` and run

	./install.sh --clang-completer --system-libclang

### Miscellaneous software

Next I install various pieces of software for general operation.

	pacman -S firefox ranger file w3m highlight atool sxiv zathura zathura-pdf-poppler zathura-ps zathura-djvu mpv lsd

### LaTeX

I use a close to maximal TeX Live. Install it with

	pacman -S texlive-core texlive-bibtexextra texlive-fontsextra texlive-formatsextra texlive-humanities texlive-latexextra texlive-pictures texlive-publishers texlive-science ghostscript

### R compilation

I compile R from source because I want a bast BLAS/LAPACK implementation. I currently like Intel's [math kernel library](https://software.intel.com/en-us/mkl). Download the archive from Intel's website (you have to sign in but it's free) and unzip it. Get into the unpacked directory. Before installation, make sure you have `cpio` already installed. Then type (possibly with `sudo`)

	./install.sh

and follow prompts. It will complain that the OS is unsupported, but ignore that and everything seems to proceed normally. Download R dependencies (except `blas` and `lapack` that will be provided by MKL).

	pacman -S --needed $( pacman -Si r | grep Depends | cut -d' ' -f12- )

Install some optional dependencies.

	pacman -S tk gcc-fortran jdk-openjdk

Unzip the R download tarball and change to the directory. Run the MKL script that establishes some needed shell variables.

	source /opt/intel/mkl/bin/mklvars.sh intel64

While I am at it, I add `$MKLROOT` to `.bashrc`. It helps to have it for any other compilations that require BLAS. Then run configuration and installation.

	MKL="-L${MKLROOT}/lib/intel64 -Wl,--no-as-needed -lmkl_gf_lp64 -Wl,--start-group \
		-lmkl_gnu_thread  -lmkl_core  -Wl,--end-group -fopenmp  -ldl -lpthread -lm"
	./configure --with-blas="$MKL" --with-lapack --with-tcltk
	make
	make info
	make install
	make install info

Check that the linking worked by running

	ldd bin/exec/R

(it is the `bin` directory in the current R download directory, not `/bin`)

I also need the GNU Scientific library for one of my projects.

	pacman -S gsl

### NVIDIA set-up

I mostly follow the instructions [here](https://ebobby.org/2018/08/06/archlinux-nvidia-on-oryp4/). I activate the NVIDIA card 

	sudo system76-power graphics nvidia

I add the file `10-nvidia-drm-outputclass.conf` to `/usr/share/X11/xorg.conf.d`. This file contains

	Section "OutputClass"
		Identifier "intel"
		MatchDriver "i915"
		Driver "modesetting"
	EndSection

	Section "OutputClass"
		Identifier "nvidia"
		MatchDriver "nvidia-drm"
		Driver "nvidia"
		Option "AllowEmptyInitialConfiguration"
		Option "PrimaryGPU" "yes"
		ModulePath "/usr/lib/nvidia/xorg"
		ModulePath "/usr/lib/xorg/modules"
	EndSection

I also put the following script in `/etc/lightdm` to check if the NVIDIA card is on at startup, and add an external monitor if it is connected.

	#!/bin/sh

	if system76-power graphics | grep -q 'nvidia'; then
		xrandr --setprovideroutputsource modesetting NVIDIA-0
		xrandr --output eDP-1-1 --auto --primary --dpi 144
		if [ $( xrandr | grep HDMI | cut -d ' ' -f2 ) == "connected" ]; then 
			output=$( xrandr | grep HDMI | cut -d ' ' -f1 )
			xrandr --output $output --auto --left-of eDP-1-1
		fi
	fi

I keep the screens (I have a 4K external monitor, and the HiDPI screen on the laptop) at the full resolution, but enlarge fonts and follow some suggestions on the [Arch HiDPI wiki page](https://wiki.archlinux.org/index.php/HiDPI). I am really happy with the text rendering with this set-up. Running the screens at 1080p made everything larger, but noticeably fuzzier.

