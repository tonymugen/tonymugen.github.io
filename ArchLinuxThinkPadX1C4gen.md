
# Installing Arch Linux on the 4th generation ThinkPad X1 Carbon

The `lspci` output is

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
	04:00.0 Network controller: Intel Corporation Wireless 8260 (rev 3a)

The `lscpu` output is

	Architecture:        x86_64
	CPU op-mode(s):      32-bit, 64-bit
	Byte Order:          Little Endian
	Address sizes:       39 bits physical, 48 bits virtual
	CPU(s):              4
	On-line CPU(s) list: 0-3
	Thread(s) per core:  2
	Core(s) per socket:  2
	Socket(s):           1
	NUMA node(s):        1
	Vendor ID:           GenuineIntel
	CPU family:          6
	Model:               78
	Model name:          Intel(R) Core(TM) i7-6600U CPU @ 2.60GHz
	Stepping:            3
	CPU MHz:             2162.690
	CPU max MHz:         3400.0000
	CPU min MHz:         400.0000
	BogoMIPS:            5618.00
	Virtualization:      VT-x
	L1d cache:           32K
	L1i cache:           32K
	L2 cache:            256K
	L3 cache:            4096K
	NUMA node0 CPU(s):   0-3
	Flags:               fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm pbe syscall nx pdpe1gb rdtscp lm constant_tsc art arch_perfmon pebs bts rep_good nopl xtopology nonstop_tsc cpuid aperfmperf tsc_known_freq pni pclmulqdq dtes64 monitor ds_cpl vmx smx est tm2 ssse3 sdbg fma cx16 xtpr pdcm pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand lahf_lm abm 3dnowprefetch cpuid_fault epb invpcid_single pti ssbd ibrs ibpb stibp tpr_shadow vnmi flexpriority ept vpid ept_ad fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx rdseed adx smap clflushopt intel_pt xsaveopt xsavec xgetbv1 xsaves dtherm ida arat pln pts hwp hwp_notify hwp_act_window hwp_epp flush_l1d


## Requirements

I want to have full-disk encryption, with the exception of the boot partition and I am installing with WiFi.

## Preliminaries

I used the `archlinux-2019.01.01-x86_64.iso`, put it on a USB flash drive using `dd` (standard procedure).

Inserted the USB drive, booted while pressing `F12` on boot to enter the boot disk picker. The WiFi card has functional firmware, checked by running

	lspci -k
	dmseg | grep iwlwifi

List WiFi networks, pick the relevant and follow prompts to connect:

	wifi-menu

Set up time and date.

	timedatectl set-ntp true
	timedatectl set-timezone America/New_York

I want to use LVM on LUKS to get full-disk encryption, including the SWAP. `/boot` will be un-encrypted.

## Disk preparation

Partition the target disk (here, it is `/dev/sda`).

To list partitions:

	fdisk -l

Lenovo does not let you boot from a GPT partition with BIOS, and I could not get EFI to work either, so I am using MBR instead. I use `fdisk` to partition the main SSD.

	fdisk /dev/sda

`p` to list current partitions
`o` to delete them all and create an empty MBR partition table
`n` to create new

 - first (for boot): default start, end at +200M, otherwise defaults, erase ext4 signature if asked
 - second (`linux` default): the rest of the disk, all defaults

`p` to check if everything looks sane
`w` to write (THE DISK WILL BE ERASED AT THIS POINT)

Format the EFI boot partition (left unencrypted):

	mkfs.ext4 /dev/sda1

Create the non-boot file systems. The following will require coming up with a passphrase. I followed the instructions in [Encrypting an entire system](https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system).

Encrypt the future LVM container:

	cryptsetup luksFormat —-type luks2 /dev/sda2
	cryptsetup open /dev/sda2 cryptlvm

Prepare the logical volumes:

	pvcreate /dev/mapper/cryptlvm
	vgcreate MainVolGroup /dev/mapper/cryptlvm
	lvcreate -L 12G MainVolGroup -n swap
	lvcreate -l 100%FREE MainVolGroup -n root

	mkfs.ext4 /dev/MainVolGroup/root
	mkswap /dev/MainVolGroup/swap

	mount /dev/MainVolGroup/root /mnt
	swapon /dev/MainVolGroup/swap

Mount the BIOS boot partition:

	mkdir /mnt/boot
	mount /dev/sda1 /mnt/boot

## Installation

Install Arch:

	pacstrap /mnt base base-devel python gvim grub dhclient networkmanager gnome-keyring

Generate `fstab`:

	genfstab -U /mnt >> /mnt/etc/fstab

Edit `/mnt/etc/crypttab` to add a line

	cryptlvm	UUID=_/dev/sda2 UUID_	none	luks,discard,timeout=5

An easy way to transfer the UUID without typing it is to do

	blkid | grep sda2 >> /mnt/etc/crypttab

and edit the `crypttab` file to make it correct.

There is an issue with GRUB and LVM which causes grub-mkconfig to hang and grub-install to keep probing LVM devices. For the [workaround](https://bbs.archlinux.org/viewtopic.php?id=242594), prepare the following:

	mkdir /mnt/hostlvm
	mount --bind /run/lvm /mnt/hostlvm

## Configuration

Move into the fresh Arch installation on the main disk. Not that the paths will no longer require `/mnt` in front.

	arch-chroot /mnt

To deal with the GRUB/LVM problem, run

	ln -s /hostlvm /run/lvm

Edit `/etc/mkinitcpio.conf` (this is now on the target drive):

	HOOKS=(base udev autodetect **keyboard** **keymap** modconf block **lvm2** **encrypt** **resume** filesystems fsck) # resume is included for suspend to disk support

	mkinitcpio -p linux

Install GRUB on BIOS:

	grub-install --target=i386-pc

Use `blkid` to list UUIDs of devices. Edit `/etc/default/grub` to modify variables. Append "lvm" to `GRUB_PRELOAD_MODULES`. Then append `resume=/dev/MainVolGroup/swap cryptdevice=UUID=UUID-of-/dev/sda2:cryptlvm` to `GRUB_CMDLINE_LINUX_DEFAULT`. The `resume=...` part is for suspend to disk support.

Make the GRUB config.

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

Create `/etc/hostname` and write *sidonia* there. Edit `/etc/hosts` to add

	127.0.0.1	localhost
	::1			localhost
	127.0.0.1	sidonia.localdomain sidonia

To make a root password and add a non-root user:

	passwd
	useradd -m -g wheel tonyg
	passwd tonyg

Finally, to enable `sudo` for the user, uncomment the `%wheel ALL=(ALL) ALL` line in `/etc/sudoers`. I like to reboot etc without entering a password, so I also add `%wheel ALL=(ALL) NOPASSWD: REBOOT`. I add `/sbin/shutdown` to the `REBOOT` alias.

## Environment set-up

### Basic connectivity

I start with installing `htop` to test that everything is working. Then

 - `git` version control
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

	pacman -S xf86-video-intel mesa xorg xorg-xinit xorg-xrdb xorg-xlsfonts xorg-xfontsel pango

Add a version of the i3 window manager along with some needed add-ons.

	pacman -S i3-gaps i3status i3blocks i3lock termite termite-terminfo dmenu network-manager-applet feh compton arandr

Copy fonts that I have in the `add_fonts` directory in this repository to `$HOME/.local/share/fonts` (a.k.a `$XDG_CONFIG_HOME/share/fonts`), then run

	fc-cache -v

for `fontconfig` to recognize them (check with `fc-list`). To make extra sure that other applications can use the fonts,

	cd .local/share/fonts
	mkfontscale
	mkfontdir

To set up a good-looking environment, I need to install

	pacman -S arc-gtk-theme lxappearance pulseaudio pavucontrol lm_sensors psensor acpi scrot sysstat

For a graphical login, I use `lightDM`.

	pacman -S lightdm lightdm-gtk-greeter

I included the modified config files in the `systemwide_config` directory in this repository. Move `lightdm.conf` and `lightdm-gtk-greeter.conf` to `/etc/lightdm`. Add any images you want for background to `/usr/share/backgrounds`.

### Vim

Next, I set up my vim environment. I move the `.vimrc` and `.vim` from this repository to the home directory. For `YouCompleteMe` to work, I need to install `cmake`:

	pacman -S cmake clang python2 boost

Change to the `.vim/bundle` directory and clone the [VundleVim](https://github.com/VundleVim/Vundle.vim) repository to it. Start `vim` and run

	:PluginInstall

After that, change to `YouCompleteMe` and run

	./install.sh --clang-completer --system-libclang

### Miscellaneous software

Next I install various pieces of software for general operation.

	pacman -S firefox ranger file w3m highlight atool sxiv zathura zathura-pdf-poppler zathura-ps zathura-djvu vlc

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


