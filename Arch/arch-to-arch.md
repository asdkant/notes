# Notes on installing Arch from existing Arch
## 1. Preparations and checklist
* 500GB SSD  with GPT
* UEFI boot
* NVIDIA graphics

### Partitions

| # | type | mount |
|---|------|-------|
| 1 | vfat | /boot |
| 2 | swap | |
| 3 | ext4 | / |

### Pacstrap
```
pacstrap -c /mnt/newssd/ alsa-utils ark base base-devel bash-completion bmon btrfs-progs calibre certbot cfv clementine cuda curl dolphin dolphin-plugins dstat exfat-utils exiv2 firefox flac gimp git glances gmic gparted gsmartcontrol gst-libav gst-plugins-base gst-plugins-good gst-plugins-ugly gstreamer gwenview htop kalgebra kate kcharselect kcolorchooser kdeconnect kdegraphics-thumbnailers kdiff3 keepassx2 kfind kid3-qt kio-extras kipi-plugins kmplot kompare konversation krename kruler kshutdown kwrite lame libvdpau linux-tools lshw lsof mc mcomix mlocate most mp3gain ncdu noto-fonts-cjk noto-fonts-emoji noto-fonts-extra ntfs-3g nvidia-dkms nvidia-settings nvidia-utils okular opencl-nvidia opera optipng p7zip pamixer pavucontrol-qt plasma-pa python python-beautifulsoup4 python-future python2-beautifulsoup4 python2-exiv2 qbittorrent quota-tools raw-thumbnailer redshift reflector rsync soundkonverter sox spectacle subdl subdownloader sysstat systemsettings tmux tree ttf-droid ttf-linux-libertine unrar unzip vim  vlc wavpack wget xsane yakuake zip zsh zsh-syntax-highlighting
```
