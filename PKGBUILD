#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.8.1
pkgrel=80
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses' 'git')
source=('git://git.suckless.org/st'
  '1.diff'
  '2.diff'
  '3.diff'
  '4.diff'
  '5.diff')
sha1sums=('SKIP'
          '72bc03bb16a29fd996761f6216717eec67f50a0e'
          '623f474b62fb08e0b470673bf8ea947747e1af8b'
          '46e92d9d3f6fd1e4f08ed99bda16b232a1687407'
          'd3329413998c5f3feaa7764db36269bf7b3d1334'
          'aad7fb654ab36b122a36c3e8a87a7135d50ef749')

pkgver() {
  cd "${srcdir}/${pkgname}"
  git describe --tag | tr '-' '.'
}

prepare() {
  local file
  cd "${srcdir}/${pkgname}"
  for file in "${source[@]}"; do
    if [[ "${file}" == *.diff ]]; then
      msg "Applying ${file}..."
      patch -Np1 <"${srcdir}/${file}"
    fi
  done
  mv config.def.h config.h
  #Remove terminfo stuff (per Arch's official package PKGBUILD)
  #sed '/@tic/d' -i Makefile
}

build() {
  cd "${srcdir}/${pkgname}"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "${srcdir}/${pkgname}"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README "${pkgdir}/usr/share/doc/${pkgname}/README"
}
