#2016 tiagobrait
#Based on the orignal Arch SLACKBUILD at
#'https://git.archlinux.org/svntogit/community.git/tree/trunk/PKGBUILD?h=packages/st'

pkgname=st
pkgver=0.9
pkgrel=1
pkgdesc='Simple virtual terminal emulator for X'
url='http://git.suckless.org/st/'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
source=("https://dl.suckless.org/st/st-${pkgver}.tar.gz"
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
        'font2.diff'
)

sha1sums=('c93587f7021b524dcbb712013c5a7bd92d4f47f2'
          'cd593374f6f978b5741bbc34b2d09cdf34905081'
          'cad68e6a3e39a78c5bf35d4a31cdefc911a020b5'
          '0022448c825d42d7260351db5f40ca361a17a2a8'
          '376b25261a0fc9d05417b7d8404170984dd86da5'
          'fe14277f8c0a9c27f9a23c4b09450e57c7c1a3d0'
          '06dcc2964004a23eff9e4c70c2b9124718aa1a37'
          '4c1630fb75b479d4dc691b8dcd715cdb75c3a4e1'
          'd7cc074555cd556beed7ba3fc8775ec3b9dfe247'
          '6a1ee1ef9b010ca85789531fa0e05fb83eee046f'
          '42897cbf46a5d88985feb42b2e909ca6e41abf0b'
          '0476165ef3e2a9a84e0fac9c20c9957d4d1676cf'
          'f76d19edc1d8d7d9adbe17b01ea2a15f51df57c5')


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
