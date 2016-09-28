#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.7.5.gf739843
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses' 'git')
source=('git://git.suckless.org/st'
  '1.diff'
  '3.diff'
  '4.diff'
  '5.diff'
  '6.diff'
  '7.diff'
  '8.diff')
sha1sums=('SKIP'
          'e15232da0d5d5e9c4c80ab001f350fd7bb75bfe7'
          'ace82e8b5a878157b913e0f309452b7fb3eebc7e'
          '9827a5f22efc8d0b30d0ff81ec18f68a72bc9f7b'
          '0576ea2ab9f39a43ec5aec5005eb35e4c2cac219'
          '26648577ae77ba0b83d47385cae4f5b9a386a9ad'
          '52ffb09af39d3581dbfc21cdbe9c0e11d062d71d'
          'fae38d1bea0a538184472662a7a87f6643f662d0')

pkgver() {
  cd "${srcdir}/${pkgname}"
  git describe --tag | tr '-' '.'
}

prepare() {
  local file
  cd "${srcdir}/${pkgname}"
  mv config.def.h config.h
  sed 's/CPPFLAGS =/CPPFLAGS +=/g' -i config.mk
  #Remove terminfo stuff (per Arch's official package PKGBUILD)
  sed '/@tic/d' -i Makefile
  for file in "${source[@]}"; do
    if [[ "${file}" == *.diff ]]; then
      msg "Applying ${file}..."
      patch -Np1 <"${srcdir}/${file}"
    fi
  done
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
