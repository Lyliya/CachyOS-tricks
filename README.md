# Cachy OS Tricks

This repository is a collection of tweaks I had to do to make things work on Cachy OS


### G502 Hi-res scroll

```sh
sudo nano /etc/libinput/local-overrides.quirks
```

```
[Logitech G502]
MatchName=*Logitech G502*
AttrEventCode=-REL_WHEEL_HI_RES;-REL_HWHEEL_HI_RES;
```

### Connect to Fusion 360

Install Fusion 360 from [here](https://codeberg.org/cryinkfly/Autodesk-Fusion-360-on-Linux)

[link from issue](https://github.com/cryinkfly/Autodesk-Fusion-360-for-Linux/issues/460#issuecomment-2436702373)

```sh
ls ~/.autodesk_fusion/wineprefixes/default/drive_c/Program\ Files/Autodesk/webdeploy/production/

WINEPREFIX="/home/{USERID}/.autodesk_fusion/wineprefixes/default" wine "C:\Program Files\Autodesk\webdeploy\production\{LONSGID}\Autodesk Identity Manager\AdskIdentityManager.exe" "adskidmgr:/login?code={CODE}"
```

### XBOX Wireless Dongle

Install `xone-dkms` and `xone-dongle-firmware`

### UMC202HD not waking up from sleep

```sh
# Reset the usb (lsusb)
sudo usbreset 1397:0507
```

Prevent from going to sleep
```sh
sudo nano /usr/local/bin/umc-reset.sh
```

```sh
#!/bin/bash
/usr/bin/usbreset 1397:0507
```

```sh
sudo nano /etc/systemd/system/umc-wake-reset.service
```

```
[Unit]
Description=Reset Behringer UMC after system resume
After=suspend.target hibernate.target hybrid-sleep.target suspend-then-hibernate.target

[Service]
Type=oneshot
ExecStart=/usr/local/bin/umc-reset.sh
# Adding a slight delay can help if the USB bus is still re-initializing
ExecStartPre=/usr/bin/sleep 2

[Install]
WantedBy=suspend.target hibernate.target hybrid-sleep.target suspend-then-hibernate.target
```

```sh
sudo chmod +x /usr/local/bin/umc-reset.sh
sudo systemctl enable umc-wake-reset.service
sudo systemctl daemon-reload
```

### Discord no sound / mic only on call
```sh
sudo pacman -Syu pipewire pipewire-pulse pipewire-alsa pipewire-audio wireplumber alsa-utils sof-firmware alsa-ucm-conf
```