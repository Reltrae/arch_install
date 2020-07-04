# arch_install

ping -c 3 archlinux.org
fdisk -l
cfdisk /dev/sda
mkfs.fat -F32 /dev/sda1
mkfs.ext4 /dev/sda2
mkfs.ext4 /dev/sda3
mount /dev/sda2 /mnt
mkdir /mnt/home
mount /dev/sda3 /mnt/home
pacstrap /mnt base linux linux-firmware nano
genfstab -U /mnt >> /mnt/etc/fstab
arch-chroot /mnt /bin/bash
ln -sf /usr/share/zoneinfo/Europe/Kiev /etc/localtime
hwclock --systohc --utc
echo username > /etc/hostname
nano /etc/hosts
127.0.0.1 localhost.localdomain username
pacman -S networkmanager
systemctl enable NetworkManager
passwd
pacman -S grub efibootmgr
mkdir /boot/efi
mount /dev/sda1 /boot/efi/
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB --removable
grub-mkconfig -o /boot/grub/grub.cfg
exit
umount -R /mnt
reboot
root
pass
useradd -m -g users -G wheel -s /bin/bash username
passwd username
pass
pacman -S sudo
EDITOR=nano visudo
exit
username
pass
sudo fallocate -l 3G /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
free -m
sudo nano /etc/fstab
/swapfile none swap sw 0 0
sudo pacman -S pulseaudio pulseaudio-alsa xfce4-pulseaudio-plugin xorg xorg-xinit xorg-server xfce4 lightdm lightdm-gtk-greeter
echo "exec startxfce4" > ~/.xinitrc
sudo systemctl enable lightdm
startx
===========================================================================================
РУСИФИКАЦИЯ

sudo nano /etc/vconsole.conf  (Правим настройки клавиатуры и шрифтов)
KEYMAP=ru
FONT=cyr-sun16

sudo nano /etc/locale.gen
Пишем en_US.UTF-8 и ru_RU.UTF-8 UTF-8
sudo locale-gen
===========================================================================================
РУСИФИКАЦИЯ

sudo nano /etc/locale.conf
Пишем: LANG=ru_RU.UTF-8 (Ctrl+X и Y и Enter) перезагрузка и система на русском.
===========================================================================================
УСТАНОВКА YAOURT

sudo pacman -S --needed base-devel git wget yajl
cd /tmp
git clone https://aur.archlinux.org/package-query.git
cd package-query/
makepkg -si
cd ..
git clone https://aur.archlinux.org/yaourt.git
cd yaourt/
makepkg -si
cd ..
sudo rm -dR yaourt/ package-query/
===========================================================================================
