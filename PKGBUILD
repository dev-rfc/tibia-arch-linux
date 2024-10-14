# Based in the PKGBUILD of Ricardo Cabral <https://aur.archlinux.org/packages/tibia> 
pkgname=tibia
pkgver=14.0.0
pkgrel=1
pkgdesc="Fast-paced free MMORPG game"
arch=('x86_64')
url="https://www.tibia.com"
license=('custom')
depends=('glu' 'libgl' 'libice' 'libxext' 'pcre' 'qt6-base' 'ttf-ms-fonts')
optdepends=('vulkan-driver: for Vulkan rendering')
makedepends=('python-html2text')

DLAGENTS=("https::/usr/bin/curl --compressed  -fL --retry 3 --retry-delay 3 -e %u -o %o %u")

source=("${pkgname}.tar.gz::https://static.tibia.com/download/tibia.x64.tar.gz"
  "file://tibia.desktop"
  "file://tibia.png"
  "${pkgname}-agreement.php::https://www.tibia.com/support/agreement.php")

sha256sums=('b4a5cb31075bc2c228ea0ba2f1c66e53003b271094b5de4f8b3d9a0cb2282ce4'
  'f82c3abc72ec224ebae74f006864bdb790b95cfc83a1bc24baa1a974ec7d0537'
  '1c4e72a86a1f3245f1696d27e423ac9a198249b3698f610b00f4ae1b341e4454'
  'SKIP')
  
prepare() {
  html2text "${srcdir}/${pkgname}-agreement.php" > LICENSE
}

package() {
  install -d "${pkgdir}/opt/tibia"
  cp -dr --no-preserve=ownership Tibia/* "${pkgdir}/opt/tibia/"
  chmod -R 775 "${pkgdir}/opt/tibia"

  # Set group to 'games'
  chgrp -R games "${pkgdir}/opt/tibia"

  # Install desktop entry and icon
  install -Dm644 "tibia.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install -Dm644 "tibia.png" "${pkgdir}/usr/share/pixmaps/tibia.png"
  install -Dm644 "tibia.png" "${pkgdir}/usr/share/pixmaps/com.tibia.client.png"
  
  # Install license
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

  # Create symlink for executable
  install -d "${pkgdir}/usr/bin"
  ln -s "/opt/tibia/Tibia" "${pkgdir}/usr/bin/tibia"
}

