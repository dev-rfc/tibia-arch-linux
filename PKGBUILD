# Based in the PKGBUILD of Ricardo Cabral <https://aur.archlinux.org/packages/tibia> 

pkgname=tibia
pkgver=14.0.0
pkgrel=1
pkgdesc="Fast-paced free MMORPG game"
arch=('x86_64')
url="https://www.tibia.com"
license=('custom')
depends=('glu' 'libgl' 'libice' 'libxext' 'pcre' 'qt6-base' 'ttf-ms-fonts')
makedepends=('gendesk' 'python-html2text')

DLAGENTS=("https::/usr/bin/curl --compressed  -fL --retry 3 --retry-delay 3 -e %u -o %o %u")

source=("${pkgname}.tar.gz::https://static.tibia.com/download/tibia.x64.tar.gz"
        "${pkgname}-agreement.php::https://www.tibia.com/support/agreement.php")

sha256sums=('SKIP'
            'SKIP') # Replace with actual checksum for agreement.php

prepare() {
  gendesk -f -n
  html2text "${srcdir}/${pkgname}-agreement.php" > LICENSE
}

package() {
  install -d "${pkgdir}/opt/tibia"
  cp -dr --no-preserve=ownership Tibia/* "${pkgdir}/opt/tibia/"
  chmod -R 775 "${pkgdir}/opt/tibia"

  # Set group to 'games'
  chgrp -R games "${pkgdir}/opt/tibia"

  # Install desktop entry and icon
  install -Dm644 "${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install -Dm644 Tibia/tibia.ico "${pkgdir}/usr/share/pixmaps/tibia.ico"

  # Install license
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  # Create symlink for executable
  install -d "${pkgdir}/usr/bin"
  ln -s "/opt/tibia/Tibia" "${pkgdir}/usr/bin/tibia"

}

