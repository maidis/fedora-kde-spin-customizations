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

# My favorite software
```bash
sudo dnf install gimp blender inkscape krita okteta
sudo dnf install libreoffice-writer libreoffice-impress libreoffice-calc libreoffice-draw libreoffice-graphicfilter libreoffice-math
```

# Third-party repositories
```bash
sudo dnf install fedora-workstation-repositories
```

# Google Chrome
```bash
sudo dnf config-manager --set-enabled google-chrome
sudo dnf install google-chrome-stable
```

# VirtualBox
```bash
cd /etc/yum.repos.d/
sudo wget http://download.virtualbox.org/virtualbox/rpm/fedora/virtualbox.repo
sudo dnf update --refresh
sudo dnf install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms
sudo dnf install VirtualBox-5.2
sudo usermod -a -G vboxusers maidis
```

# Development tools
```bash
sudo dnf install SFML-devel love Box2D-devel glew-devel
sudo dnf install SDL2-devel SDL2_gfx-devel SDL2_net-devel SDL2_ttf-devel SDL2_image-devel SDL2_mixer-devel
sudo dnf install qt-creator* qt5-devel qt5 qt5*-devel
sudo dnf install fedora-packager astyle doxygen
sudo dnf groupinstall 'C Development Tools and Libraries'
sudo dnf install kate
sudo dnf install clang-analyzer clang clang-tools-extra
sudo dnf install json-devel jsoncpp-devel curl-devel curlpp-devel gtest-devel tesseract-devel
```

# Removal of some unused pre-installed software
```bash
#TODO: some package names may be incorrect, they may not be removed (due to dependencies)
sudo dnf remove kwrite akregator dragon konqueror korganizer kpat kmahjongg kmines kmag kontact kmail knode kf5-ktnef 

sudo dnf remove kget ktp* calligra* dnfdragora

sudo dnf remove pim-data-exporter akonadi-import-wizard kwalletmanager5

sudo dnf remove abrt dnfdragora dnfdragora-updater
```

# RPM Fusion
```bash
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

# Unneeded system services
```bash
sudo systemctl disable initial-setup.service
```

# Cutelyst
```bash
cd /etc/yum.repos.d/
sudo wget https://download.opensuse.org/repositories/home:/buschmann23:/Cutelyst:/devel/Fedora_28/home:buschmann23:Cutelyst:devel.repo
sudo dnf check-update
sudo dnf install cutelyst2-devel
```

# Visual Studio Code
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
sudo dnf check-update
sudo dnf install code
```

# .NET Core
```bash
sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
sudo dnf update
sudo dnf install libunwind libicu compat-openssl10
sudo dnf install dotnet-sdk-2.1.200
sudo dnf install https://rpms.remirepo.net/fedora/remi-release-28.rpm
sudo dnf --enablerepo=remi install libui-devel
```

# OBS
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

# HP printer drivers
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

sudo dnf install dolphin-plugins
```

# Multimedia packages
```bash
sudo dnf -y install gstreamer-plugins-base gstreamer1-plugins-base gstreamer-plugins-bad gstreamer-plugins-ugly gstreamer1-plugins-ugly gstreamer-plugins-good-extras gstreamer1-plugins-good-extras gstreamer1-plugins-bad-freeworld ffmpeg gstreamer-ffmpeg gstreamer1-plugins-bad-free-extras mencoder
```


# Set up DNF to use delta packages and fastest mirrors
```bash
#TODO: sudo is not enough here
sudo echo 'fastestmirror=true' >> /etc/dnf/dnf.conf
sudo echo 'deltarpm=true' >> /etc/dnf/dnf.conf
```

# Tools
```bash
sudo dnf install htop p7zip p7zip-plugins unrar xclip
```

# Audio/video software
```bash
sudo dnf install audacity lmms kdenlive vlc flowblade avidemux-qt
cat >> /etc/yum.repos.d/cincv.repo <<EOL
[cincv]
name=cincv
baseurl=https://cinelerra-cv.org/five/pkgs/fedora/
gpgcheck=0
# end of cincv
EOL
sudo dnf install cinelerra
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

# GRUB themes
```bash
#TODO sudo is not enough here
sudo dnf install grub2-breeze-theme
sudo echo 'GRUB_THEME="/boot/grub2/themes/breeze/theme.txt"' >> /etc/default/grub
sed -i 's/GRUB_TERMINAL_OUTPUT="console"/#GRUB_TERMINAL_OUTPUT="console"/g' /etc/default/grub
grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```

# Restore Windows 10 entry in Grub
#grub> search -f /EFI/Microsoft/Boot/bootmgfw.efi

#hd1,gpt2
```bash
sudo cat >> /etc/grub.d/40_custom <<EOL
menuentry 'Microsoft Windows 10' {
set root='hd1,gpt2'
chainloader /EFI/Microsoft/Boot/bootmgfw.efi
boot
}
EOL

sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
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

# Fonts
```bash
sudo dnf install impallari-raleway-fonts google-roboto-fonts google-roboto-mono-fonts google-noto-mono-fonts google-noto-sans-fonts google-noto-serif-fonts lato-fonts
sudo dnf install cabextract
sudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm
```

#  LaTeX editors
```bash
sudo dnf install lyx texmaker
```

# Maths
```bash
sudo dnf install armadillo-devel octave scilab cantor gmp-devel glm-devel mpfr-devel
```

