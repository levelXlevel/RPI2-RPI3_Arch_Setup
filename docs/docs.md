# Post install

## First Boot

### Objectives

1. Reset default passwords
2. Change hostname
3. Initialize package manager
4. Upgrade the system
5. Reboot

### Steps

1. Login as default user
   > ssh alarm@alarmpi
2. SU as root
   > su -
3. Change password for root & default user
   > passwd root
   > passwd alarm
4. Change hostname
   > hostnamectl hostname `new_hostname`
5. Init keys
   > pacman-key --init
   > pacman-key --populate archlinuxarm
6. Update the system
   > pacman -Syu --noconfirm
7. Reboot
   > reboot

## Second boot

### Objectives

1. Add new groups
2. Add new users
3. Install critical software
4. Add user/s to sudoer
5. Setup AUR
6. Configure Pi

### Steps

1. Add Groups
   1. Add system groups
      1. groupadd -r docker
      2. groupadd -r ansible
   2. Add regular groups
      1. groupadd pi
      2. groupadd `username`
2. Add new users
   1. useradd -m -g pi -G wheel,users,docker pi
   2. useradd -m -g ansible -G wheel,users,docker ansible
   3. useradd -m -g `username` -G wheel,users `username`
   4. Change shells if needed/desired
      1. usermod --shell /bin/bash `username`
3. Install software
   > pacman -S –noconfirm sudo vim base-devel git go
4. Add default user to sudoer
   > echo “alarm ALL=NOPASSWD: ALL” >/etc/sudoers.d/000-users
   1. Add any additional users to sudoer
5. Setup AUR as non-root user

   1. Exit `root` and return to regular user
   2. Install Yay

      > rm -rf /tmp/yay-bin

      > git clone https://aur.archlinux.org/yay-bin.git /tmp/yay-bin

      > cd /tmp/yay-bin

      > makepkg -si

   3. Install packages (Replaces previously installed vi package)

      > yay -S --noconfirm vi-vim-symlink usbutils lshw

      [OPTIONAL]

      - ansible
      - docker docker-compose
      - hwinfo

6. Configure Pi
   1. Install some useful packages
      > yay -S --noconfirm raspi-config-git i2c-tools lm_sensors
   2. Use raspi-config to adjust pi
      1. Locale
      2. Timezone
      3. Interfacing
      4. SPI
      5. I2C
      6. Advance
      7. Expand Filesystem
      8. Memory Split = 16
7. Configure Bash
   1. Install a few tools/utilities
      > yay -S --noconfirm find-the-command fzf fastfetch
   2. Add stuff to bash_profile
      > vi ~/.bash_profile
      ```
      fastfetch
      source /usr/share/doc/find-the-command/ftc.bash
      ```

## How To

### Docker

```
yay -S --noconfirm docker docker-compose
sudo systemctl enable –now docker
```

### Grafana

```
yay -S --noconfirm grafana-bin
sudo systemctl enable --now grafana
```

### Prometheus Exporters

#### Install

```
yay -S --noconfirm prometheus prometheus-node-exporter
sudo systemctl enable --now prometheus prometheus-node-exporter
```

#### Additional Exporters

```
yay -S --noconfirm prometheus-blackbox-exporter
sudo systemctl enable --now prometheus-blackbox-exporter
yay -S --noconfirm prometheus-speedtest-exporter
yay -S --noconfirm prometheus-ping-exporter
sudo systemctl enable --now prometheus-ping-exporter
```

#### Enable Admin

TBD

## Disable package compression

> sudo vi /etc/makepkg.conf

Change _PKGEXT_ to just `tar` without compressing package.

```
#PKGEXT='.pkg.tar.zst'
#PKGEXT='.pkg.tar.xz”'
PKGEXT='.pkg.tar'
```

### Additional packages

> yay -S --noconfirm pacman-updatedb-hook
