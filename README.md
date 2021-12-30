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
| Display | 14.0" 2.8K (2880x1800) OLED, Multitouch | ✔ Yes | Resolution is correctly detected by `xrandr`, 200% scaling was activated by default and looks good. Automatic brightness adjustment works out of the box. Multitouch works out of the box. |
| Storage | 1 TB M.2 2280 SSD | ✔ Yes | Via standard kernel driver |
| Wifi | Realtek | ✔ Yes | Works out of the box on Ubuntu. Works with 5 Ghz networks. Might require some additional setup in other distros (E.g. it did not work on `POP!_OS` from the box) |
| Bluetooth | Bluetooth 5.0| ✔ Yes | Works as expected |
| Speakers  | Dolby Vision Atmos Speaker System | ❌ Weak | Only 2 speakers out of 4 work. [See details below](#speakers) |
| Microphone | | ✔ Yes | Out of the box. todo: test if all mics work |
| Webcam | Infrared 720p-HD-Camera | ✔ Yes | Works out of the box. Note: Sometimes only vertical lines are shown. To fix it turn the camera off and on with the killswitch. |
| Webcam killswitch | | ✔ Yes | Works out of the box. |
| Ports | 3 × USB-C, Mini-jack | ✔ Yes | Charging works over all the ports. Charging "flash" symbol appears in a few minutes after plugging in. Todo: charging ports, display, docking. Charging works only via left port, external display only via right one, but it is a known hardware limitation of the laptop |
| Graphic Dongle | USB-Typ-C to USB-Typ-A-/HDMI-/VGA | ✔ Yes | Works |
| Keyboard |  | ✔ Almost | [see below](#keyboard) for details |
| Touchpad | | ✔ Yes | touchpad is detected and works in GNOME. Left, right clicks, 2-finger scrolling, 2-finger zooming, 3-finger workspaces switching work. |
| Power button |  | ✔ Yes |  |
| Battery | 4 Cell, 61 Wh | ✔ Yes | Todo: test battery life |
| Power management | | ✔ Yes | works, see [below](#power-management) for details |
| Lid | ACPI-compliant |  ✔ Yes | works as expected, todo: check ACPI logs |
| Suspend |  | ❌ NO | Suspend works. But keyboard does not work after waking up |
| Hibernate |  | Unknown | todo: test |
| Windows hello |  | ❌ NO | Does not work out of the box. Todo: research |

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
