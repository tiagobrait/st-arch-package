#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.8.5
pkgrel=99
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
source=('https://dl.suckless.org/st/st-0.8.5.tar.gz'
        'custom-tiagobrait.diff'
        'hidecursor.diff'
        'vertcenter.diff'
        'clipboard.diff'
        'scrollback.diff'
        'scrollback-mouse.diff'
        'scrollback-mouse-altscreen.diff'
        'bold-is-not-bright.diff'
        'anysize.diff'
        'boxdraw.diff'
        'base16-default-dark-theme.diff'
)

sha1sums=('774b4a687a54a7c91d25dceefa791c221f804308'
          '597db5f28cdf39fc6aa9b036fe26424005c9588e'
          '8a2cc5ee42819ebd34fc07aa0e6483479fcee5c9'
          'f3e4887a04f9500128eeceeb768249cf876db0d6'
          '7946bafaddc96546b67496ccf5f68302e1125657'
          'a36e58a39d695c957299e4d00fe762d4c618ee07'
          '06dcc2964004a23eff9e4c70c2b9124718aa1a37'
          '88e49f7c776d2cc3498c877daca39a4c77319484'
          'f9026995402369fbe72e2629c788d21f2574c3bf'
          'd14fc3d809e66eedf54a12fb120fffc0662e60c8'
          '78d3e0b34cd795018abae3c296e953aa888c7a3f'
          '0476165ef3e2a9a84e0fac9c20c9957d4d1676cf')


prepare() {
  local file
  cd "${srcdir}/${pkgname}-${pkgver}"
  for file in "${source[@]}"; do
    if [[ "${file}" == *.diff ]]; then
      msg "Applying [35m${file/.diff/}[0m patch..."
      patch -p1 <"${srcdir}/${file}"
    fi
  done
  mv config.def.h config.h
}

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 README "${pkgdir}/usr/share/doc/${pkgname}/README"
}
