#Contributor: Daenyth <Daenyth+arch [AT] gmail [dot] com>

pkgname=tremulous-updated
pkgver=1.1.0
pkgrel=7
pkgdesc="A free team based FPS/RTS hybrid built on the ioq3 engine. Includes community updates."
url="http://tremulous.net"
arch=('i686' 'x86_64')
license=('GPL')
depends=('sdl' 'openal>=1.7.411' 'libgl' "tremulous-data=$pkgver")
makedepends=(mesa)
provides=("tremulous=$pkgver-$pkgrel")
conflicts=('tremulous')
replaces=('trem-backport')
source=(http://releases.mercenariesguild.net/client/mg-client-manual.txt
        http://releases.mercenariesguild.net/client/mgclient_source_Release_1.011.tar.gz
        http://releases.mercenariesguild.net/tremded/mg_tremded_source_1.01.tar.gz
        http://projects.mercenariesguild.net/attachments/download/109/game.qvm
        http://projects.mercenariesguild.net/attachments/download/111/lakitu7_qvm.txt
        tremdedrc
        tremulous.desktop
        tremded.sh
        tremulous.sh
        tremulous.xpm)

backup=('etc/tremdedrc')
noextract=(mg_tremded_source_1.01.tar.gz)

md5sums=('e0e1b6e03e7596da00a77fe638560402'
         '95e526b961f875ba66b6fdd4842c913b'
         '938bdf944dff667b74e2132a87a49780'
         '90343619d140557d0c481a61ffa5756c'
         'a0b8970b33a27798c125f9152049013c'
         'f0056120d0192a0d4d591d1114439c52'
         'aef37632a2edcf74a53503a49530bad2'
         'b755d7c022cddc449ca2de508dfeee30'
         '8e89473f9fdb481ad44e5cea5f6f681e'
         '7e3a881608f1c7c0ccece1e07fcf92d8')

build() {
  local _arch=${CARCH/i686/x86}

  # Build and install the server
  mkdir -p $srcdir/tremded
  bsdtar -x -C $srcdir/tremded -f $srcdir/mg_tremded_source_1.01.tar.gz
  cd $srcdir/tremded
  make || return 1
  install -D -m755 build/release-linux-$_arch/tremded.$_arch $pkgdir/opt/tremulous/tremded.$_arch
  install -D -m644 $srcdir/tremdedrc                         $pkgdir/etc/tremdedrc
  install -D -m644 $srcdir/game.qvm                          $pkgdir/opt/tremulous/game.qvm
  install -D -m755 $srcdir/tremded.sh                        $pkgdir/usr/bin/tremded

  # Build and install the client
  cd $srcdir/Release_1.011
  make || return 1
  install -Dm755 build/release-linux-$_arch/tremulous.$_arch $pkgdir/opt/tremulous/tremulous.$_arch
  install -D -m755 $srcdir/tremulous.sh                      $pkgdir/usr/bin/tremulous

  # Install the documentation
  install -Dm644 $srcdir/mg-client-manual.txt $pkgdir/usr/share/tremulous/mg-client-manual.txt
  install -Dm644 $srcdir/lakitu7_qvm.txt      $pkgdir/usr/share/tremulous/lakitu7_qvm.txt

  # Install the .desktop and icon files
  install -D -m644 $srcdir/tremulous.xpm     $pkgdir/usr/share/pixmaps/tremulous.xpm
  install -D -m644 $srcdir/tremulous.desktop $pkgdir/usr/share/applications/tremulous.desktop

}

# vim:set ts=2 sw=2 et:
