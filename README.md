# fedora-kde-spin-customizations
My efforts to make Fedora KDE spin more usable for my needs

# Full system update
```bash
sudo dnf update --refresh
```

# Nasty NVIDIA drivers
```bash
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf install nvidia-driver kernel-devel akmod-nvidia dkms acpi

sudo dnf copr enable chenxiaolong/bumblebee
sudo dnf install akmod-bbswitch bumblebee primus

sudo gpasswd -a $USER bumblebee

sudo systemctl enable bumblebeed
sudo systemctl disable nvidia-fallback

sudo dnf install nvidia-settings nvidia-driver-libs.i686

sudo yum -y install cuda nvidia-driver-cuda cuda-devel
sudo dnf update --refresh
```

# Steam installation
```bash
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-steam.repo
sudo dnf -y install steam
sudo dnf install libnsl.i686 libnsl2.i686

sudo dnf install meson systemd-devel pkg-config git
sudo dnf copr enable gicmo/nursery
sudo dnf install gamemode
```

# Installation of some of my favorite software
```bash
#TODO: Install LibreOffice components individually
sudo dnf install gimp blender inkscape krita okteta libreoffice
```

# Enabling third-party repositories
```bash
sudo dnf install fedora-workstation-repositories
```

# Google Chrome installation
```bash
sudo dnf config-manager --set-enabled google-chrome
sudo dnf install google-chrome-stable
```

# VirtualBox installation
```bash
cd /etc/yum.repos.d/
sudo wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo
sudo dnf update --refresh
sudo dnf install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms
sudo dnf install VirtualBox-5.2
sudo usermod -a -G vboxusers maidis
```

# Installation of some development tools
```bash
sudo dnf install SFML-devel
sudo dnf install qt-creator* qt5-devel qt5 qt5*-devel
sudo dnf install fedora-packager
sudo dnf install kate
sudo dnf install clang-analyzer clang
```

# Removal of some unused pre-installed software
```bash
#TODO: some package names may be incorrect, they may not be removed (due to dependencies)
sudo dnf remove kwrite akregator dragon konqueror korganizer kpat kmahjongg kmines kmag kontact kmail knode kf5-ktnef 

sudo dnf remove ktp*
sudo dnf remove calligra*
sudo dnf remove dnfdragora

sudo dnf remove pim-data-exporter akonadi-import-wizard kwalletmanager5

sudo dnf remove abrt

sudo dnf remove dnfdragora dnfdragora-updater
```

# Enabling RPM Fusion repositories
```bash
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

# Turn off unneeded system services
```bash
sudo systemctl disable initial-setup.service
```

# Cutelyst installation
```bash
cd /etc/yum.repos.d/
sudo wget https://download.opensuse.org/repositories/home:/buschmann23:/Cutelyst:/devel/Fedora_28/home:buschmann23:Cutelyst:devel.repo
sudo dnf check-update
sudo dnf install cutelyst2-devel
```

# Visual Studio Code installation
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf check-update
sudo dnf install code
```

# .NET Core installation
```bash
sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
sudo dnf update
sudo dnf install libunwind libicu compat-openssl10
sudo dnf install dotnet-sdk-2.1.200
```

# OBS installation
```bash
sudo dnf install obs-studio
sudo dnf install gstreamer1-plugins-good gstreamer-ffmpeg gstreamer1-libav
sudo dnf config-manager --set-enabled fedora-cisco-openh264
sudo dnf upgrade
sudo dnf install gstreamer1-plugin-openh264
```

# KDE Connect port configuration
```bash
sudo firewall-cmd --zone=public --permanent --add-port=1714-1764/tcp
sudo firewall-cmd --zone=public --permanent --add-port=1714-1764/udp
sudo systemctl restart firewalld.service
```

# Installation of HP printer drivers
```bash
sudo dnf install hplip hplip-libs hplip-gui hplip-common
sudo dnf install skanlite
```

# E-book tools
```bash
sudo dnf install sigil calibre
```

# Dropbox installation
```bash
#TODO: check auto start
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
~/.dropbox-dist/dropboxd
```

# Installation of some multimedia packages
```bash
sudo dnf -y install gstreamer-plugins-base gstreamer1-plugins-base gstreamer-plugins-bad gstreamer-plugins-ugly gstreamer1-plugins-ugly gstreamer-plugins-good-extras gstreamer1-plugins-good-extras gstreamer1-plugins-bad-freeworld ffmpeg gstreamer-ffmpeg
```


# Set up DNF to use delta packages and fastest mirrors
```bash
#TODO: sudo is not enough here
sudo echo 'fastestmirror=true' >> /etc/dnf/dnf.conf
sudo echo 'deltarpm=true' >> /etc/dnf/dnf.conf
```

# Installation of some system performance monitoring tools
```bash
sudo dnf install htop
```

# Installation of some audio/video software
```bash
sudo dnf install audacity lmms kdenlive vlc
```

# Terminal enhancements
```bash
sudo dnf install powerline powerline-fonts

cat >> ~/.bashrc <<EOL
if [ -f `which powerline-daemon` ]; then
  powerline-daemon -q
  POWERLINE_BASH_CONTINUATION=1
  POWERLINE_BASH_SELECT=1
  . /usr/share/powerline/bash/powerline.sh
fi
EOL
```

# Using GRUB theme
```bash
#TODO sudo is not enough here
sudo dnf install grub2-breeze-theme
sudo echo 'GRUB_THEME="/boot/grub2/themes/breeze/theme.txt"' >> /etc/default/grub
sed -i 's/GRUB_TERMINAL_OUTPUT="console"/#GRUB_TERMINAL_OUTPUT="console"/g' /etc/default/grub
grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```

# Password-free local partition mount
```bash
#TODO sudo is not enough here
sudo cat >> /etc/polkit-1/rules.d/99-mount-partitions.rules <<EOL
// Password-less mounting of local partitions
polkit.addRule(function(action, subject) {
    if (action.id == "org.freedesktop.udisks2.filesystem-mount-system" && subject.isInGroup("wheel")) {
       return polkit.Result.YES;
    }
});
EOL
```

# Setting SELinux to permissive mode
```bash
#TODO: sudo is not enough here, do i need that?
sed -i -e 's/SELINUX=enforcing/SELINUX=permissive/g' /etc/selinux/config
setenforce 0
```

# Screen temperature control
```bash
sudo dnf install redshift plasma-applet-redshift-control
```
