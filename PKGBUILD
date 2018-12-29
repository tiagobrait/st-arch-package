#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.8.1
pkgrel=81
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses' 'git')
source=('git://git.suckless.org/st'
'1_font_shell_utmp.diff'
'st-clipboard-0.8.1.diff'
'st-hidecursor-0.8.1.diff'
'st-scrollback-0.8_1.diff'
'st-scrollback-0.8_2.diff'
'st-scrollback-0.8_3.diff'
'st-vertcenter-20180320-6ac8c8a.diff'
)


sha1sums=('SKIP'
'a101155f8480c7a61af932f377613f1bbafa365f'
'26e946870fa7ab3907cd6b8972ebbbd6a3aa0fe5'
'a5db64611e0dcf163eed3810c525addad3403718'
'8db2dd42eea766e632cf881b1800a03a32aa0dc7'
'46e92d9d3f6fd1e4f08ed99bda16b232a1687407'
'd3329413998c5f3feaa7764db36269bf7b3d1334'
'aad7fb654ab36b122a36c3e8a87a7135d50ef749'
)


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
