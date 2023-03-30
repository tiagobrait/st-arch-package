#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.9.1
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
source=("https://github.com/tiagobrait/st/releases/download/${pkgver}/${pkgname}-${pkgver}.tar.gz")
sha1sums=('12c95829c57a8355ce1d494fa4b822c06050ecfb')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
