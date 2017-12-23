# Notes on installing Arch from existing Arch

* 500GB SSD  with GPT
* UEFI boot
* NVIDIA graphics

### Partitions

| # | type | mount |
|---|------|-------|
| 1 | vfat | /boot |
| 2 | swap | |
| 3 | ext4 | / |

```bash
mkdir /mnt/newssd/
mount /dev/sde3 /mnt/newssd/
mkdir /mnt/newssd/boot
mount /dev/sde1 /mnt/newssd/boot/
```

### Strapping the system
```bash
pacstrap -c /mnt/newssd/ alsa-utils ark base base-devel bash-completion bmon btrfs-progs calibre certbot cfv clementine cuda curl dolphin dolphin-plugins dstat exfat-utils exiv2 firefox flac gimp git glances gmic gparted gsmartcontrol gst-libav gst-plugins-base gst-plugins-good gst-plugins-ugly gstreamer gwenview htop kalgebra kate kcharselect kcolorchooser kdeconnect kdegraphics-thumbnailers kdiff3 keepassx2 kfind kid3-qt kio-extras kipi-plugins kmplot kompare konversation krename kruler kshutdown kwrite lame libvdpau linux-headers linux-tools lshw lsof mc mcomix mlocate most mp3gain ncdu noto-fonts-cjk noto-fonts-emoji noto-fonts-extra ntfs-3g nvidia-dkms nvidia-settings nvidia-utils okular opencl-nvidia opera optipng p7zip pamixer pavucontrol-qt plasma-pa python python-beautifulsoup4 python-future python2-beautifulsoup4 python2-exiv2 qbittorrent quota-tools raw-thumbnailer redshift reflector rsync soundkonverter sox spectacle subdl subdownloader sysstat systemsettings tmux tree ttf-droid ttf-linux-libertine unrar unzip vim  vlc wavpack wget xsane yakuake zip zsh zsh-syntax-highlighting

genfstab -U /mnt/newssd/ >> /mnt/newssd/etc/fstab
rsync -avz --progress /var/cache/pacman/ /mnt/newssd/var/cache/pacman/
```

**[** REMEMBER to add extra disks to fstab **]**

### chroot to the environment

```bash
arch-chroot /mnt/newssd/
```

## Once inside

```bash
ln -sf /usr/share/zoneinfo/America/Argentina/Buenos_Aires /etc/localtime
hwclock --systohc
systemctl enable dhcpcd.service
```
##### `/etc/locale.gen`
```
en_GB.UTF-8 UTF-8  
en_GB ISO-8859-1  
en_US.UTF-8 UTF-8  
en_US ISO-8859-1  
es_AR.UTF-8 UTF-8  
es_AR ISO-8859-1  
```
Then run `locale-gen`

##### `/etc/locale.conf`
```
LANG=en_US.UTF-8
LC_TIME="en_GB.UTF-8"
```
##### `/etc/vconsole.conf`
```
KEYMAP=es
```
##### `/etc/hostname`
```
ry42
```
##### `/etc/hosts`
```
# Static table lookup for hostnames.
# See hosts(5) for details.
#<ip-address>   <hostname.domain.org>   <hostname>
127.0.0.1       localhost.localdomain   localhost       phen42
::1             localhost.localdomain   localhost       phen42
```
##### `/etc/mkinitcpio.conf`
```
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
HOOKS=(base udev autodetect modconf block filesystems keyboard fsck keymap)
```
run `mkinitcpio -p linux`
