---
title: Fedora - настройка после установки
categories:
- blog
---

Примерные действия, которые можно сделать после установки Fedora на десктопе.

* Обновление:

  ```bash
  dnf update
  reboot
  ```

* Virtualbox guest additions, если необходимо

  ```bash
  dnf install gcc kernel-devel kernel-headers dkms make bzip2 perl
  export KERN_DIR=/usr/src/kernels/`uname -r`
  cd /run/media/user/VBOX*
  ./VboxLinuxAdditions.run
  reboot
  ```

* Включить репозиторий [RPM Fusion free][1] и nonfree:

  ```bash
  dnf install --nogpgcheck \
    http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-22.noarch.rpm
  dnf install --nogpgcheck \
    http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-22.noarch.rpm
  ```

* Установить драйвер [nvidia][2], если необходимо:

  ```bash
  dnf install akmod-nvidia "kernel-devel-uname-r == $(uname -r)"
  ```

* Установить кодеки для звука и браузера (html5):

  ```bash
  dnf install -y gstreamer1-libav gstreamer1-plugins-bad-free \
    gstreamer1-plugins-bad-freeworld gstreamer1-plugins-good \
    gstreamer1-plugins-good-extras gstreamer1-plugins-ugly gstreamer1-vaapi
  ```

* Настроить сглаживание шрифтов, как в Ubuntu:

  ```bash
  dnf install -y freetype-freeworld
  ```

  ```xml
  <!-- /etc/fonts/local.conf -->
  <?xml version='1.0'?>
  <!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>
  <fontconfig>
   <match target="font">
    <edit mode="assign" name="rgba">
     <const>rgb</const>
    </edit>
   </match>
   <match target="font">
    <edit mode="assign" name="hinting">
     <bool>true</bool>
    </edit>
   </match>
   <match target="font">
    <edit mode="assign" name="hintstyle">
     <const>hintslight</const>
    </edit>
   </match>
   <match target="font">
    <edit mode="assign" name="lcdfilter">
     <const>lcddefault</const>
    </edit>
   </match>
   <match target="font">
    <edit mode="assign" name="autohint">
     <bool>false</bool>
    </edit>
   </match>
   <dir>~/.fonts</dir>
  </fontconfig>
  ```

* Настроить отображение русского шрифта в tty:

  ```bash
  cat /etc/vconsole.conf
  KEYMAP="us"
  FONT="UniCyr_8x16"
  ```

* Установить google chrome можно с официального сайта или из fedy.

* Можно установить gnome-tweak-tool, fedy.


[1]: http://rpmfusion.org/Configuration
[2]: http://rpmfusion.org/Howto/nVidia
