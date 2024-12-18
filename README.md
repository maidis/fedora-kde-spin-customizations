# fedora-kde-spin-customizations
My efforts to make Fedora KDE spin more usable for my needs

# Full system update
```bash
sudo dnf upgrade --refresh
```

# Firmware update
```bash
sudo fwupdmgr get-devices
sudo fwupdmgr refresh --force
sudo fwupdmgr get-updates
sudo fwupdmgr update
```

# NVIDIA drivers
```bash
sudo dnf config-manager addrepo --from-repofile=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf install dkms-nvidia nvidia-driver nvidia-settings nvidia-driver-libs.i686
sudo dnf install nvidia-driver-cuda cuda-devel cuda-cudnn-devel cuda-gcc
sudo dnf install mangohud
sudo dnf upgrade --refresh

sudo dnf copr enable zawertun/scrapyard
sudo dnf install kde-style-sierra-breeze-enhanced
sudo dnf install kvantum
```

- [Layan](https://store.kde.org/p/1325246/)
- [Black Screen on Login Screen](https://github.com/negativo17/nvidia-driver/issues/74)
- [Crazy Progress Indicator Spinner](https://github.com/negativo17/nvidia-driver/issues/81)
- [Fedora'da Nvidia DKMS Sürücüleri](https://anilozbek.blogspot.com/2019/08/fedorada-nvidia-dkms-suruculeri.html)

```bash
sudo rm -rf /var/lib/dkms/nvidia/
sudo dkms install nvidia/440.64
```

# CPU tools

```bash
sudo dnf install thermald kernel-tools tlp tlp-rdw powertop lm_sensors xset

sudo sensors-detect

#sudo systemctl mask power-profiles-daemon

sudo powertop --calibrate
sudo powertop --auto-tune

#git clone https://github.com/frankenfruity/plasma-pstate
#cd plasma-pstate
#sudo ./install.sh

sudo dnf copr enable angstr0m/plasma-pstate
sudo dnf in plasma-pstate
```
- [Fedora 36 Post Install Guide - Battery Life](https://github.com/devangshekhawat/Fedora-36-Post-Install-Guide#battery-life)
- [tlp actively breaks power-profiles-daemon when installed](https://bugzilla.redhat.com/show_bug.cgi?id=2028701)

# Steam installation
```bash
sudo dnf config-manager addrepo --from-repofile=https://negativo17.org/repos/fedora-steam.repo
sudo dnf -y install steam libnsl.i686 libnsl2.i686 kernel-modules-extra gamemode
```

# My favorite software
```bash
sudo dnf install blender inkscape okteta ktorrent
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

# RPM Fusion
```bash
sudo dnf install https://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm https://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
```

# VirtualBox
```bash
sudo dnf install VirtualBox
sudo dnf install binutils gcc make patch libgomp glibc-headers glibc-devel kernel-headers kernel-devel dkms
sudo dnf remove virtualbox-guest-additions
sudo usermod -a -G vboxusers maidis
```

# Development tools
```bash
sudo dnf install SFML-devel love Box2D-devel glew-devel
sudo dnf install SDL2-devel SDL2_gfx-devel SDL2_net-devel SDL2_ttf-devel SDL2_image-devel SDL2_mixer-devel
#sudo dnf install qt-creator* qt5-devel qt5 qt5*-devel
sudo dnf install fedora-packager astyle doxygen graphviz-devel
sudo dnf group install c-development
sudo dnf install kate git libstdc++-devel
sudo dnf install clang-analyzer clang clang-tools-extra cppcheck kcachegrind clazy uncrustify
sudo dnf install json-devel jsoncpp-devel curl-devel curlpp-devel gtest-devel tesseract-devel
sudo dnf install opencv-devel opencv-core opencv-contrib
sudo dnf install godot gperftools
```

# Removal of some unused pre-installed software
```bash
#TODO: some package names may be incorrect, they may not be removed (due to dependencies)
sudo dnf remove akregator dragon korganizer kpat kmahjongg kmines kmag kontact kmail kf5-ktnef kwrite

sudo dnf remove abrt dnfdragora dnfdragora-updater kget
```

# Cutelyst
```bash
sudo dnf config-manager addrepo --from-repofile=https://download.opensuse.org/repositories/home:/buschmann23:/Cutelyst:/devel/Fedora_39/home:buschmann23:Cutelyst:devel.repo
sudo dnf install cutelyst4-qt6-devel cutelyst4-qt6-docs*
```

# Visual Studio Code
```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
cat <<EOF | sudo tee /etc/yum.repos.d/vscode.repo
[code]
name=Visual Studio Code
baseurl=https://packages.microsoft.com/yumrepos/vscode
enabled=1
gpgcheck=1
gpgkey=https://packages.microsoft.com/keys/microsoft.asc
EOF
sudo dnf install code
```

# .NET Core
```bash
sudo dnf install dotnet
```

# OBS
```bash
sudo dnf install obs-studio
sudo dnf install gstreamer1-plugins-good gstreamer-ffmpeg gstreamer1-libav
sudo dnf config-manager --set-enabled fedora-cisco-openh264
sudo dnf upgrade --refresh
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
cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -
mkdir -p ~/.config/autostart/
cat >> ~/.config/autostart/dropbox.desktop <<EOL
[Desktop Entry]
Version=1.0
Name=Dropbox
GenericName=File Sharing
Exec=~/.dropbox-dist/dropboxd
StartupNotify=true
Terminal=false
Icon=dropbox
Type=Application
Categories=Network
EOL
sudo chmod +x ~/.config/autostart/dropbox.desktop
~/.dropbox-dist/dropboxd

sudo dnf install dolphin-plugins
```

# Multimedia packages
```bash
sudo dnf install -y gstreamer1-plugins-{bad-*,good-*,ugly-*,base} gstreamer1-libav --exclude=gstreamer1-plugins-bad-free-devel ffmpeg gstreamer-ffmpeg
sudo dnf install -y lame* --exclude=lame-devel
sudo dnf install -y mencoder yt-dlp elisa-player krecorder
```

# Tools
```bash
sudo dnf install htop p7zip p7zip-plugins unrar xclip fatrace
```

# Audio/video software
```bash
sudo dnf install audacity lmms kdenlive vlc flowblade avidemux-qt mkvtoolnix-gui shotcut HandBrake-gui
sudo dnf install cinelerra-gg
sudo dnf install https://www.ocenaudio.com/downloads/index.php/ocenaudio_fedora35.rpm
```
- [Unable to save subtitles on Linux](https://github.com/exebetche/vlsub/issues/213)

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
sudo dnf install grub2-breeze-theme
sudo echo 'GRUB_THEME="/boot/grub2/themes/breeze/theme.txt"' >> /etc/default/grub
sudo sed -i 's/GRUB_TERMINAL_OUTPUT="console"/#GRUB_TERMINAL_OUTPUT="console"/g' /etc/default/grub
sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
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
sudo sed -i -e 's/SELINUX=enforcing/SELINUX=permissive/g' /etc/selinux/config
sudo setenforce 0
getenforce
```

# Fonts
```bash
sudo dnf install -y fira-code-fonts impallari-raleway-fonts lato-fonts 'mozilla-fira*' 'google-roboto*'
sudo dnf install cabextract xorg-x11-font-utils
sudo rpm -i https://downloads.sourceforge.net/project/mscorefonts2/rpms/msttcore-fonts-installer-2.6-1.noarch.rpm

#sudo -s dnf copr enable dawid/better_fonts
#sudo -s dnf install fontconfig-font-replacements
#sudo -s dnf install fontconfig-enhanced-defaults
```

#  Document editing
```bash
sudo dnf install lyx texmaker
sudo dnf install texlive-sourcesanspro texlive-tcolorbox texlive-babel-turkish
sudo dnf install pandoc
sudo dnf install libreoffice-writer libreoffice-impress libreoffice-calc libreoffice-draw libreoffice-graphicfilter libreoffice-math libreoffice-langpack-tr
```

# Maths
```bash
sudo dnf install armadillo-devel octave cantor gmp-devel glm-devel mpfr-devel
```

# Icon Themes
```bash
sudo dnf install kfaenza-icon-theme papirus-icon-theme
```

# GTK Themes
```bash
sudo dnf install breeze-gtk
```
# GitHub
```bash
git config --global user.name "maidis"
git config --global user.email "ozbekanil@gmail.com"

ssh-keygen -t rsa -b 4096 -C "ozbekanil@gmail.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
xclip -sel clip < ~/.ssh/id_rsa.pub
```

- [Setting your username in Git](https://help.github.com/en/articles/setting-your-username-in-git)
- [Setting your commit email address](https://help.github.com/en/articles/setting-your-commit-email-address)
- [Generating a new SSH key and adding it to the ssh-agent](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
- [Adding a new SSH key to your GitHub account](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account)
- [GitHub Desktop](https://github.com/shiftkey/desktop/releases)

# Photo Editing
```bash
sudo dnf install gimp gmic-gimp gimp-lensfun gimp-resynthesizer gimp-wavelet-denoise-plugin gimp-wavelet-decompose gimp-luminosity-masks ufraw-gimp gimp-elsamuko gimpfx-foundry gimp-lqr-plugin gimp-data-extras gimp-heif-plugin gimp-paint-studio gimp-fourier-plugin gimp-focusblur-plugin gimp-high-pass-filter gimp-layer-via-copy-cut

sudo dnf install krita luminance-hdr rawtherapee darktable darktable-tools-noise 

sudo dnf install libheif qt-heif-image-plugin
```

# Zoom
```
sudo dnf install https://zoom.us/client/latest/zoom_x86_64.rpm
```
