# Maintainer: Pedro Alejandro López-Valencia <palopezv at gmail.com>
#
# This file is provided under the BSD 2-clause license.
# <http://opensource.org/licenses/BSD-2-Clause>
#
# Patches welcome. Send pull requests to
# https://github.com/vorbote/vuze-plugin-i2p

pkgname=vuze-plugin-i2p
pkgver=0.3.0
pkgrel=2
pkgdesc="Vuze plugin for the I2P darknet network. When you need to go underground."
arch=('any')
url=http://azureus.sourceforge.net/plugin_details.php?plugin=azneti2p
license=('GPL2')
depends=('vuze')
options=(!strip)
source=("http://azureus.sourceforge.net/plugins/azneti2p_${pkgver}.jar")
noextract=("azneti2p_${pkgver}.jar")
md5sums=('154f1460b337c3f878cff769253d91e3')

build () {
	cd "$srcdir"
	install -Dm644 azneti2p_${pkgver}.jar "${pkgdir}/usr/share/vuze/plugins/I2P/azneti2p_${pkgver}.jar"
}
