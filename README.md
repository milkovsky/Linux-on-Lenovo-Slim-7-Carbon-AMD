# Linux on Lenovo Yoga Slim 7 Carbon Gen 6 (14" AMD)

US name: Lenovo Yoga IdeaPad 7 Carbon Gen 6 (14" AMD)

> Inspired by [similar researches for other laptops](https://github.com/milkovsky/Linux-on-Lenovo-Slim-7-Carbon-AMD/blob/main/links.md).

![Lenovo Yoga IdeaPad 7 Carbon Gen 6 (14" AMD)](https://user-images.githubusercontent.com/1665580/147853477-aecb6d4a-220d-4d68-ab83-a40508e09da4.png)

> © lenovo.com

The laptop was released in Nevember 2021. Full name in Europe "[Lenovo Yoga Slim 7 Carbon Gen 6 (14" AMD)](https://www.lenovo.com/de/de/laptops/yoga/yoga-slim-series/Yoga-Slim-7-Carbon-Gen-6-14-inch-AMD/p/LEN101Y0006)", "Lenovo IdeaPad Slim 7 Carbon Gen 6 (14" AMD)".

psref: https://psref.lenovo.com/Detail/Yoga/Yoga_Slim_7_Carbon_14ACN6?M=82L0005RMX

Tested specifications:

- Processor: AMD Ryzen™ 7 5800U-Prozessor
- RAM: 16 GB LPDDR4X 4266MHz
- 1 TB M.2 2280 SSD
- Screen: 14.0" 2.8K (2880x1800) OLED, Multitouch
- Graffic card: integrated AMD

Tested disctributions, kernel versions:

- Ubuntu 21.10
- Ubuntu 22.04
- POP_OS 22.04
- Fedora 35
- Kernel: 5.13.0.22, 5.15, 5.16

## Linux support

| Function | Details | Status | Notes |
| --- | --- |  :---: | --- |
| Processor | Processor: AMD Ryzen™ 7 5800U-Prozessor | ✔ Yes | All 16 cores were detected in `htop` |
| Graphics | Integrated AMD Radeon | ✔ Yes | via standard kernel driver |
| RAM | 16 GB LPDDR4X 4266MHz | ✔ Yes | 13,5G were recognized in `htop` due to reserved GPU RAM. Can be changed in UEFI. |
| Display | 14.0" 2.8K (2880x1800) OLED, Multitouch | ✔ Yes | see [display details](#display) below. |
| Storage | 1 TB M.2 2280 SSD | ✔ Yes | Via standard kernel driver |
| Wifi | Realtek | ✔ Yes | Requires additional setup for some kernel versions. See [wifi details](#wifi) below. |
| Bluetooth | Bluetooth 5.0| ✔ Yes | Works as expected. Bluetooth mouse is recognized and works as expected. |
| Speakers  | Dolby Vision Atmos Speaker System | ❌ only 2 speakers | Only 2 speakers out of 4 work out of the box. [See details about Speakers](#speakers) below. |
| Microphone | | ✔ Yes | Out of the box. todo: test if all mics work |
| Webcam | Infrared 720p-HD-Camera | ✔ Yes | Works out of the box. Note: Sometimes only vertical lines are shown. To fix it turn the camera off and on with the killswitch. |
| Webcam killswitch | | ✔ Yes | Works out of the box. |
| Ports | 3 × USB-C, Mini-jack | ✔ Yes | All the ports work. Charging works only via left port. |
| Graphic Dongle | USB-Typ-C to USB-Typ-A-/HDMI-/VGA | ✔ Yes | Works. HDMI monitor works, USB keyboard works. |
| Keyboard |  | ⚠️ Minor issues | see [Keyboard details](#keyboard) below |
| Touchpad | | ⚠️ Only the US version | EU/Yoga variant has no touchpad. Otherwise, all features work on the US variant. |
| Power button |  | ✔ Yes |  |
| Battery | 4 Cell, 61 Wh | ✔ Yes | Battery life is approximately 5 hours during a regular usaage in ballanced mode. See [more details about bettery](#battery) below. |
| Power management | | ✔ Yes | Works, see [more details about power management](#power-management) below. |
| Lid | ACPI-compliant |  ✔ Yes | Works as expected, todo: check ACPI logs |
| Suspend |  | ✔ Yes | Works stable in ubuntu 22.04 LTS (5.15.0-25-generic). In supendend mode laptop lost 10% battery in 1,5 days. |
| Hibernate |  | ✔ Yes | Works in NixOS |
| Face recognition |  | ✔ Requires additional setup | See [details about face recognition](#face-recognition) below. |
| AMD P-State | | ✔ Is default since kernel 6.3 | See [details about AMD P-State](#amd-p-state) below. |

## Display

Colors look nice. GNOME night mode works fine as well.

### Brightness

Brightness adjustment keys work fine with kernel 5.13. Kernel 5.15 has issues with adjustment keys, see [keyboard details](#keyboard) below.

### Touchscreen

Multitouch works out of the box even in BIOS.
This is only a feature in the US version, not the European one. 

### Resolution & Scaling

Resolution is correctly detected by `xrandr`, 200% scaling was activated by default and looks good.

Some apps require custom adjustments for proper scaling. A few examples:

#### Spotify

- sudo vim /var/lib/snapd/desktop/applications/spotify_spotify.desktop
- And then you change the Exec directive to include the option:
  Exec=env BAMF_DESKTOP_FILE_HINT=/var/lib/snapd/desktop/applications/spotify_spotify.desktop /snap/bin/spotify --force-device-scale-factor=2 %U

#### Steam

Create a scaled launcher:

- `vim .local/share/applications/SteamScaled.desktop`
- Paste next text:

```
[Desktop Entry]
Name=Steam Scaled
Exec=env GDK_SCALE=2 steam
Type=Application
StartupNotify=true
Icon=steam
StartupWMClass=steam
Name[en_US]=Steam Scaled
```

#### GRUB

-	Make a backup: sudo cp -a /etc/default/grub /etc/default/grub.bak
-	Open the configuration: sudo $EDITOR /etc/default/grub
-	Edit GRUB_GFXMODE entry to suit your resolution e.g. 1024x768
-	sudo update-grub
-	Reboot; GRUB will display in the mode you set.

## Wifi

Works as expected in Ubuntu 22.04, POP_OS 22.04. Works with 5 Ghz networks. For other versions some setup manipulations were required.

**kernel 5.13**

Works out of the box on Ubuntu 21.10 with kernel 5.13, as it already contains the required API changes.

**kernel 5.15**

Does not work with 5.15 kernel out of the box. Follow carefully the [additional setup instructions](https://github.com/lwfinger/rtw89) to fix the wifi module.

## Speakers

Only 2 speakers out of 4 work. Open issue: https://github.com/milkovsky/Linux-on-Lenovo-Slim-7-Carbon-AMD/issues/2

Problem research:

`alsa-info` output: http://alsa-project.org/db/?f=045c0b1e6b2f41b44c1a3bc145617ce60a6f756a

Kernel bug reports:
- https://bugzilla.kernel.org/show_bug.cgi?id=215632
- https://bugzilla.kernel.org/show_bug.cgi?id=208555

Other links:
- https://www.reddit.com/r/linuxaudio/comments/g1c1jo/2_out_of_4_speakers_dont_play_in_linux_on_my/
- https://github.com/hg8/arch-matebook-x-pro-2019/blob/master/guide-fix-matebook-x-pro-speakers-linux.md
- https://imgur.com/a/v86hHVn
- https://bugzilla.kernel.org/show_bug.cgi?id=208555#c547
- https://www.reddit.com/r/linuxhardware/comments/qxtson/comment/hmae1dy/?utm_source=share&utm_medium=web2x&context=3

## Keyboard

Some function buttons do not work: F9 (settings), Star S. Print Screen works only while Fn button is pressed. All the other functions including Fn lock, home, end, pg up, pg down work out of the box. 3 levels of keyboard light work as well.

## Battery

Tested balanced mode for now. Battery life is approximately 5 hours.

You can find a separate [page with additional tools for battery performance improvements](https://github.com/milkovsky/Linux-on-Lenovo-Slim-7-Carbon-AMD/blob/main/additional-features.md#battery-optimization).

## Power management

All the 3 power modes in GNOME do change BIOS power modes settings.

todo: test power modes

## Face recognition

It works with [Howdy](https://github.com/boltgolt/howdy) after enabling the IR-sensor with this: https://github.com/EmixamPP/linux-enable-ir-emitter

[Setup instructions](https://rcarrillo.dev/enabling-face-authentication-on-linux-with-howdy/):

Install https://github.com/EmixamPP/linux-enable-ir-emitter:

```
git clone https://github.com/EmixamPP/linux-enable-ir-emitter.git
cd linux-enable-ir-emitter
sudo bash installer.sh install
```
`sudo linux-enable-ir-emitter` configure look at the ir emitter and answer no on the 1st question and yes on the 2nd question.

Install howdy:

```
sudo add-apt-repository ppa:boltgolt/howdy
sudo apt update
sudo apt install howdy
```

`sudo howdy config`, set `device_path` to `/dev/video0`.
`sudo howdy add` follow the instructions
Reboot.

## AMD P-State

AMD P-State is enabled by default for all Linux kernels starting with version 6.3 and you can manually enable it with kernel 5.17+, as it is written in this [ArchWiki page (about a similar model)](https://wiki.archlinux.org/title/Lenovo_IdeaPad_5_Pro_14ACN6#AMD_P-State).

NOTE:
OEM kernel in Ubuntu has enabled driver by default.
```
sudo apt install linux-image-5.17.0-1012-oem 
```

---

## Contribution

In case you have some additional information about various Linux-related topics on this laptop, feel free to [open an issue](https://github.com/milkovsky/Linux-on-Lenovo-Slim-7-Carbon-AMD/issues/new) and/or [create a Pull-request](https://github.com/milkovsky/Linux-on-Lenovo-Slim-7-Carbon-AMD/pulls).
