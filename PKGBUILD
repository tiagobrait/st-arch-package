#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.8.4
pkgrel=99
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses' 'git')
source=('git://git.suckless.org/st'
'st-custom-tiagobrait.diff'
'st-scrollback-20210507-4536f46.diff'
'st-scrollback-mouse-20191024-a2c479c.diff'
'st-scrollback-mouse-altscreen-20200416-5703aa0.diff'
'st-hidecursor-0.8.2.diff'
'st-clipboard-20180309-c5ba9c0.diff'
'st-bold-is-not-bright-0.8.2.diff'
'st-base16-0.8.2.diff'
'st-anysize-0.8.2.diff'
'st-vertcenter-20180320-6ac8c8a.diff'
'st-boxdraw_v2-0.8.3.diff'
)


sha1sums=('SKIP'
          '2022825f74dc66cd3ab0827822bfe30c45a9c42b'
          '04ffc556dcc7b40f490ef6a2bea48787bdd47b7b'
          'e457b4819f5233999e21d6df8438931160cd9181'
          '49ffb0dd6cce1cbfeb12e8599e21b7157b85b1d4'
          'b020afee7209a55014dbc317606c7443461a1c03'
          'ef12fb41f1405b7236755eb1ca320b39ed03fe58'
          'bef42114952e4fead262bb1b491112014ac7bc39'
          'fbd757314885a7c229f8db67b129f2f48289bbd1'
          'a75f5eaee7b05b1cd960ef133a34d3aeb69d8f27'
          'aad7fb654ab36b122a36c3e8a87a7135d50ef749'
          'e8761bf9e0b4f8c056c6e9b4c88261d78b205620')


prepare() {
  local file
  cd "${srcdir}/${pkgname}"
  for file in "${source[@]}"; do
    if [[ "${file}" == *.diff ]]; then
      msg "Applying ${file} patch..."
      patch -Np1 <"${srcdir}/${file}"
    fi
  done
  mv config.def.h config.h
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
