# fedora-kde-spin-customizations
My efforts to make Fedora KDE spin more usable for my needs

# Full system update
```bash
sudo dnf update --refresh
```

# NVIDIA drivers
```bash
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-nvidia.repo
sudo dnf install dkms-nvidia nvidia-driver nvidia-settings nvidia-driver-libs.i686
sudo dnf install nvidia-driver-cuda cuda-devel cuda-cudnn-devel cuda-gcc cuda-samples
sudo dnf update --refresh

sudo dnf copr enable zawertun/scrapyard
sudo dnf install kde-style-sierra-breeze-enhanced
```

- [Black Screen on Login Screen](https://github.com/negativo17/nvidia-driver/issues/74)
- [Crazy Progress Indicator Spinner](https://github.com/negativo17/nvidia-driver/issues/81)
- [Fedora'da Nvidia DKMS Sürücüleri](https://anilozbek.blogspot.com/2019/08/fedorada-nvidia-dkms-suruculeri.html)

```bash
sudo rm -rf /var/lib/dkms/nvidia/
sudo dkms install nvidia/440.64
```

# CPU tools

```bash
sudo dnf install thermald kernel-tools tlp powertop

git clone https://github.com/jsalatas/plasma-pstate
cd plasma-pstate
sudo ./install.sh
```

# Steam installation
```bash
sudo dnf config-manager --add-repo=https://negativo17.org/repos/fedora-steam.repo
sudo dnf -y install steam libnsl.i686 libnsl2.i686 kernel-modules-extra gamemode
```

# My favorite software
```bash
sudo dnf install blender inkscape okteta
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
sudo dnf install VirtualBox-6.0
sudo dnf remove virtualbox-guest-additions
sudo usermod -a -G vboxusers maidis
```

# Development tools
```bash
sudo dnf install SFML-devel love Box2D-devel glew-devel
sudo dnf install SDL2-devel SDL2_gfx-devel SDL2_net-devel SDL2_ttf-devel SDL2_image-devel SDL2_mixer-devel
sudo dnf install qt-creator* qt5-devel qt5 qt5*-devel
sudo dnf install fedora-packager astyle doxygen graphviz-devel
sudo dnf groupinstall 'C Development Tools and Libraries'
sudo dnf install kate git libstdc++-devel
sudo dnf install clang-analyzer clang clang-tools-extra cppcheck kcachegrind clazy uncrustify
sudo dnf install json-devel jsoncpp-devel curl-devel curlpp-devel gtest-devel tesseract-devel
sudo dnf install opencv-devel opencv-core opencv-contrib
sudo dnf install godot terminology gperftools
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

# Cutelyst
```bash
cd /etc/yum.repos.d/
sudo wget https://download.opensuse.org/repositories/home:/buschmann23:/Cutelyst:/devel/Fedora_$(rpm -E %fedora)/home:buschmann23:Cutelyst:devel.repo
sudo dnf check-update
sudo dnf install cutelyst2-devel grantlee-qt5-devel
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
sudo dnf update --refresh
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
ln -s ~/.dropbox-dist/dropboxd ~/.config/autostart-scripts/ 
~/.dropbox-dist/dropboxd

sudo dnf install dolphin-plugins
```

# Multimedia packages
```bash
sudo dnf -y install gstreamer-plugins-base gstreamer1-plugins-base gstreamer-plugins-bad gstreamer-plugins-ugly gstreamer1-plugins-ugly gstreamer-plugins-good-extras gstreamer1-plugins-good-extras gstreamer1-plugins-bad-freeworld ffmpeg gstreamer-ffmpeg gstreamer1-plugins-bad-free-extras mencoder youtube-dl elisa-player
```


# Set up DNF to use delta packages and fastest mirrors
```bash
#TODO: sudo is not enough here
sudo echo 'fastestmirror=true' >> /etc/dnf/dnf.conf
sudo echo 'deltarpm=true' >> /etc/dnf/dnf.conf
```

# Tools
```bash
sudo dnf install htop p7zip p7zip-plugins unrar xclip fatrace
```

# Audio/video software
```bash
sudo dnf install audacity lmms kdenlive vlc flowblade avidemux-qt mkvtoolnix-gui
sudo dnf install cinelerra --nogpgcheck --repofrompath cingg,https://cinelerra-gg.org/download/pkgs/fedora29
sudo dnf install https://www.ocenaudio.com/downloads/ocenaudio_centos7.rpm

mkdir ~/.cache/vlc
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

#  Document editing
```bash
sudo dnf install lyx texmaker
sudo dnf install texlive-sourcesanspro texlive-tcolorbox texlive-babel-turkish
sudo dnf install pandoc
sudo dnf install libreoffice-writer libreoffice-impress libreoffice-calc libreoffice-draw libreoffice-graphicfilter libreoffice-math libreoffice-langpack-tr
```

# Maths
```bash
sudo dnf install armadillo-devel octave scilab cantor gmp-devel glm-devel mpfr-devel
```

# Sublime Text
```bash
sudo rpm -v --import https://download.sublimetext.com/sublimehq-rpm-pub.gpg
sudo dnf config-manager --add-repo https://download.sublimetext.com/rpm/stable/x86_64/sublime-text.repo
sudo dnf install sublime-text
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

# Photo Editing
```bash
sudo dnf install gimp gmic-gimp gimp-lensfun gimp-resynthesizer gimp-wavelet-denoise-plugin gimp-wavelet-decompose gimp-luminosity-masks GREYCstoration-gimp ufraw-gimp gimp-elsamuko gimp-normalmap gimpfx-foundry gimp-lqr-plugin gimp-data-extras gimp-heif-plugin gimp-paint-studio gimp-fourier-plugin gimp-focusblur-plugin gimp-high-pass-filter gimp-layer-via-copy-cut

sudo dnf install krita luminance-hdr
```
