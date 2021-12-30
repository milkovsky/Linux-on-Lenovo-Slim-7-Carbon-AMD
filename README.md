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
| Processor | Processor: AMD Ryzen™ 7 5800U-Prozessor | ✔ Yes | All 16 cores work out of the box |
| Graphics | Integrated AMD Radeon | ✔ Yes | via standard kernel driver |
| RAM | 16 GB LPDDR4X 4266MHz | ✔ Yes | 13,5G were recognized |
| Display | 14.0" 2.8K (2880x1800) OLED, Multitouch | ✔ Yes | Resolution is correctly detected by `xrandr`, 200% scaling was activated by default and looks good. Automatic brightness adjustment works out of the box. Multitouch works out of the box. |
| Storage | 1 TB M.2 2280 SSD | ✔ Yes | Via standard kernel driver |
| Wifi | Realtek | ✔ Yes | Works out of the box on Ubuntu. Did not work on `POP!_OS` |
| Bluetooth | Bluetooth 5.0| ✔ Yes | Works as expected |
| Speakers  | Dolby | ❌ NO | Only 2 speakers out of 4 work. [See details below](#speakers) |
| Microphone | | ✔ Yes | out of the box |
| Webcam | Infrared 720p-HD-Camera | ❌ NO | Only vertical lines are shown in "Cheese" |

## Speakers

Only 2 speakers out of 4 work. THis was also mentioned here: https://www.reddit.com/r/linuxhardware/comments/qxtson/comment/hmae1dy/?utm_source=share&utm_medium=web2x&context=3

Problem research:

- https://www.reddit.com/r/linuxaudio/comments/g1c1jo/2_out_of_4_speakers_dont_play_in_linux_on_my/
- https://github.com/hg8/arch-matebook-x-pro-2019/blob/master/guide-fix-matebook-x-pro-speakers-linux.md
- https://imgur.com/a/v86hHVn

WIP....
