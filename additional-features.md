# Additional features for Linux on Lenovo Yoga/IdeaPad Slim 7 Carbon AMD

This page contains additional optional features in Linux for Lenovo Yoga/IdeaPad Slim 7 Carbon AMD.

Tested on Ubuntu 21.10.

## Battery optimization

### [TLP](https://askubuntu.com/a/1309400/94215)

```
sudo apt install tlp tlp-rdw
sudo tlp start
```

### Battery Conservation Mode

Todo: test this:

On Lenovo Vantage (the Windows 10 app) there's "Battery Conservation Mode" feature which limit battery charge to around 60% to increase battery lifespan. To enable this feature on Linux, you can install a GNOME extention ([see below](#quick-access-to-additional-settings)) or you can use the following commands:

```
# Turn on
echo 1 > /sys/bus/platform/drivers/ideapad_acpi/VPC2004:00/conservation_mode
# Turn off
echo 0 > /sys/bus/platform/drivers/ideapad_acpi/VPC2004:00/conservation_mode
```

## Quick access to additional settings
Gnome extention with a quick access Lenovo features: https://extensions.gnome.org/extension/4331/ideapad-mode/

![image](https://user-images.githubusercontent.com/1665580/147859097-c610b60c-b6bd-4393-b570-857cfce6418f.png)
