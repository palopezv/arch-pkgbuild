# Maintainer: Phoenixlzx < phoenixlzx@xblue.tk >

pkgname=vuze
pkgver=4.7.1.2
pkgrel=1
pkgdesc='One of the most powerful bitTorrent client with GUI in the world, written in Java.'
arch=('i686' 'x86_64')
url='http://www.vuze.com/'
license=('GPL')
depends=('java-runtime' 'libgnomeui')
optdepends=('xulrunner192: install if vuze crashes.')
source=("http://sourceforge.net/projects/azureus/files/vuze/Vuze_4712/Vuze_4712_linux.tar.bz2/download")
md5sums=('0a946df1eccb8d4e23b5aa8b40ab8747')
#[[ $CARCH == 'x86_64' ]] && source[0]="http://sourceforge.net/projects/azureus/files/vuze/Vuze_4702/Vuze_4702_linux-x86_64.tar.bz2/download" && md5sums[0]='c6230f17d383410476fc807c37a1daad'

package() {
  install -d ${pkgdir}/usr/share
  cp -r vuze ${pkgdir}/usr/share
  install -Dm755 vuze/vuze ${pkgdir}/usr/bin/vuze
  sed -i 's%#PROGRAM_DIR="/home/username/apps/azureus"%PROGRAM_DIR="/usr/share/vuze"%' ${pkgdir}/usr/bin/vuze
  install -Dm644 vuze/vuze.png ${pkgdir}/usr/share/pixmaps/vuze.png
  install -Dm644 vuze/vuze.desktop  ${pkgdir}/usr/share/applications/vuze.desktop
}
