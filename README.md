# Linux on Lenovo Yoga/IdeaPad Slim 7 Carbon (AMD)

> Inspired by https://github.com/nekr0z/linux-on-huawei-matebook-13-2019

The laptop was released in Nevember 2021. Full name in Europe "[Lenovo Yoga Slim 7 Carbon Gen 6 (14" AMD)](https://www.lenovo.com/de/de/laptops/yoga/yoga-slim-series/Yoga-Slim-7-Carbon-Gen-6-14-inch-AMD/p/LEN101Y0006)", "Lenovo IdeaPad Slim 7 Carbon Gen 6 (14" AMD)".

Tested specifications:

- Processor: AMD Ryzen™ 7 5800U-Prozessor
- RAM: 16 GB LPDDR4X 4266MHz
- 1 TB M.2 2280 SSD
- Screen: 14.0" 2.8K (2880x1800) OLED, Multitouch
- Graffic card: integrated AMD

Tested disctribution:

- Ubuntu 21.10
- Kernel: 5.13.0.22

## Linux support

| Function | Details | Status | Notes |
| --- | --- |  :---: | --- |
| Processor | Processor: AMD Ryzen™ 7 5800U-Prozessor | ✔ Yes | All 16 cores were detected in `htop` |
| Graphics | Integrated AMD Radeon | ✔ Yes | via standard kernel driver |
| RAM | 16 GB LPDDR4X 4266MHz | ✔ Yes | 13,5G were recognized in `htop` |
| Display | 14.0" 2.8K (2880x1800) OLED, Multitouch | ✔ Yes | see [below](#display) for details |
| Storage | 1 TB M.2 2280 SSD | ✔ Yes | Via standard kernel driver |
| Wifi | Realtek | ✔ Requires fixes | See details [below](#wifi) |
| Bluetooth | Bluetooth 5.0| ✔ Yes | Works as expected. Bluetooth mouse is recognized and works as expected. |
| Speakers  | Dolby Vision Atmos Speaker System | ❌ Weak | Only 2 speakers out of 4 work. [See details below](#speakers) |
| Microphone | | ✔ Yes | Out of the box. todo: test if all mics work |
| Webcam | Infrared 720p-HD-Camera | ✔ Yes | Works out of the box. Note: Sometimes only vertical lines are shown. To fix it turn the camera off and on with the killswitch. |
| Webcam killswitch | | ✔ Yes | Works out of the box. |
| Ports | 3 × USB-C, Mini-jack | ✔ Yes | Charging works over all the ports. Charging "flash" symbol appears in a few minutes after plugging in. Todo: charging ports, display, docking. Charging works only via left port, external display only via right one, but it is a known hardware limitation of the laptop |
| Graphic Dongle | USB-Typ-C to USB-Typ-A-/HDMI-/VGA | ✔ Yes | Works. HDMI monitor works, USB keyboard works. |
| Keyboard |  | ✔ Almost | [see below](#keyboard) for details |
| Touchpad | | ✔ Yes | Touchpad is detected and works good in GNOME. Left, right clicks, 2-finger scrolling, 2-finger zooming, 3-finger workspaces switching work. |
| Power button |  | ✔ Yes |  |
| Battery | 4 Cell, 61 Wh | ✔ Yes | Todo: test battery life |
| Power management | | ✔ Yes | Works, see [below](#power-management) for details |
| Lid | ACPI-compliant |  ✔ Yes | Works as expected, todo: check ACPI logs |
| Suspend |  | ✔ Requires kernel ^5.15 | See details [below](#suspend) |
| Hibernate |  | Unknown | todo: test |
| Windows hello |  | ❌ NO | Does not work out of the box. Todo: research |

## Display

Colors look nice. GNOME night mode works fine as well.

### Brightness

Brightness adjustment keys work fine.

Automatic brightness adjustment works out of the box.

### Touchscreen

Multitouch works out of the box even in BIOS.

### Resolution & Scaling

Resolution is correctly detected by `xrandr`, 200% scaling was activated by default and looks good.

Some apps require custom adjustments for proper scaling. A few examples:

Spotify:

- sudo vim /var/lib/snapd/desktop/applications/spotify_spotify.desktop
- And then you change the Exec directive to include the option:
  Exec=env BAMF_DESKTOP_FILE_HINT=/var/lib/snapd/desktop/applications/spotify_spotify.desktop /snap/bin/spotify --force-device-scale-factor=2 %U

GRUB:

-	Make a backup: sudo cp -a /etc/default/grub /etc/default/grub.bak
-	Open the configuration: sudo $EDITOR /etc/default/grub
-	Edit GRUB_GFXMODE entry to suit your resolution e.g. 1024x768
-	sudo update-grub
-	Reboot; GRUB will display in the mode you set.

## Wifi

Works out of the box on Ubuntu with kernel 5.13. Works with 5 Ghz networks. Does not work with 5.15 kernel out of the box.

Might require some [additional setup](https://github.com/lwfinger/rtw89) in other distros (E.g. it did not work on `POP!_OS` from the box).

## Speakers

Only 2 speakers out of 4 work. This problem was also mentioned here: https://www.reddit.com/r/linuxhardware/comments/qxtson/comment/hmae1dy/?utm_source=share&utm_medium=web2x&context=3

Problem research:

- https://www.reddit.com/r/linuxaudio/comments/g1c1jo/2_out_of_4_speakers_dont_play_in_linux_on_my/
- https://github.com/hg8/arch-matebook-x-pro-2019/blob/master/guide-fix-matebook-x-pro-speakers-linux.md
- https://imgur.com/a/v86hHVn

## Keyboard

Mostly works. Some function buttons do not work: F9 (settings), F11, Star S. All the other functions including Fn lock, home, end, pg up, pg down work out of the box. 3 levels of keyboard light work as well.

## Power management

All the 3 power modes in GNOME do change BIOS power modes settings.

todo: test power modes

todo: check this: Suspend to S3 state works out of the box. For hibernation to work `Secure boot` must be disabled in BIOS. Laptop seems to wake up without any issues.

## Suspend

Suspend works. Requires [kernel 5.15 update](#kernel-update-to-515) for stable work, as it contains an important laptop suspend/resume fix for various AMD models.
5.13 kernel issues: the laptop keyboard does not work after waking up, Although both USB keyboard, mouse and touchpad wake up fine.

### Kernel update to 5.15

```
cd /tmp/

wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.15/amd64/linux-headers-5.15.0-051500_5.15.0-051500.202110312130_all.deb

wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.15/amd64/linux-headers-5.15.0-051500-generic_5.15.0-051500.202110312130_amd64.deb

wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.15/amd64/linux-image-unsigned-5.15.0-051500-generic_5.15.0-051500.202110312130_amd64.deb

wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.15/amd64/linux-modules-5.15.0-051500-generic_5.15.0-051500.202110312130_amd64.deb

sudo dpkg -i *.deb
```

Source: https://ubuntuhandbook.org/index.php/2021/11/linux-kernel-5-15-out/)

YOu might want to [sign the core for secure boot](https://ubuntu.com/blog/how-to-sign-things-for-secure-boot) afterwards.
