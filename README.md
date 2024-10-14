# Tibia for Arch Linux (PKGBUILD)

This is a PKGBUILD for installing Tibia on Arch Linux with the latest QT6 and Wayland update. Follow the instructions below to set it up, including steps to fix potential font rendering issues.

## Installation

Clone the repository and use `makepkg` to install:

```bash
git clone https://github.com/dev-rfc/tibia-arch-linux
cd tibia-arch-linux
makepkg -si
```


## Fixing Font Rendering Issues
If you experience poor font rendering, you can adjust the font configuration to improve clarity.

Open the file ``~/.config/fontconfig/fonts.conf`` in a text editor. If the file does not exist, you can create it by running:

```bash
mkdir -p ~/.config/fontconfig
touch ~/.config/fontconfig/fonts.conf
```

Copy and paste the following content into ``fonts.conf``. This configuration will enhance the hinting style specifically for the Verdana font, which can improve font rendering:

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <match target="font">
    <test name="family" compare="contains">
      <string>Verdana</string>
    </test>
    <edit name="hintstyle" mode="assign">
      <const>hintfull</const>
    </edit>
  </match>
</fontconfig>
```

Ensure you have the [ttf-ms-fonts](https://aur.archlinux.org/packages/ttf-ms-fonts) package installed. This package provides the necessary Microsoft TrueType fonts, including Verdana. You can install it from the AUR.

After configuring the font settings, rebuild the font cache to apply the changes:

```bash
fc-cache -f
```

The font rendering in Tibia should be improved.


## Disclaimer

This repository is not affiliated, associated, authorized, endorsed by, or in any way officially connected with CipSoft GmbH, the creators of Tibia. Tibia is a trademark of CipSoft GmbH. All trademarks, logos, and brand names are the property of their respective owners.

This PKGBUILD is provided "as is" without warranty of any kind, express or implied. Use it at your own risk. The author of this project assumes no responsibility for any damages or issues that may arise from using this content.
