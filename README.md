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

WINEPREFIX="/home/{USERID}/.autodesk_fusion/wineprefixes/default" wine "C:\Program Files\Autodesk\webdeploy\production\{LONGID}\Autodesk Identity Manager\AdskIdentityManager.exe" "adskidmgr:/login?code={CODE}"
```

### XBOX Wireless Dongle

Install `xone-dkms` and `xone-dongle-firmware`