# Maintainer: bemxio <bemxiov at protonmail dot com>

pkgname="sklauncher-bin"
pkgdesc="Secure and modern Minecraft Launcher"

pkgver=3.2.12
pkgrel=4

arch=(any)

url="https://skmedix.pl"
license=("Apache-2.0" "LicenseRef-SKlauncher")

depends=("java-runtime>=17")
makedepends=(unzip gendesk)
provides=(sklauncher)

install="${pkgname}.install"

source=("https://skmedix.pl/binaries/skl/${pkgver}/SKlauncher-${pkgver}.jar" "sklauncher" "LICENSE.sklauncher")
md5sums=("5b67c472ea94d09f540d598fcbd18f73" "3fbda136409cd254ce125839e59ae1c1" "edd0f7efa3df3a5cadaa2ecebf9eb57d")

noextract=("SKlauncher-${pkgver}.jar")

prepare() {
	# extract the logo out of the JAR file
	unzip -o -j "SKlauncher-${pkgver}.jar" logo.png -d .

	# generate a .desktop file
	gendesk -f -n \
		--pkgname SKlauncher \
		--pkgdesc "${pkgdesc}" \
		--exec sklauncher \
		--icon sklauncher \
		--categories "Game;Simulation"
}

package() {
	# copy the JAR file
	install -Dm755 "SKlauncher-${pkgver}.jar" "${pkgdir}/usr/share/java/sklauncher/SKlauncher.jar"

	# copy the executable script
	install -Dm755 sklauncher "${pkgdir}/usr/bin/sklauncher"

	# copy the extracted icon and the generated .desktop file
	install -Dm644 logo.png "${pkgdir}/usr/share/pixmaps/sklauncher.png"
	install -Dm644 SKlauncher.desktop "${pkgdir}/usr/share/applications/sklauncher.desktop"

	# copy the terms of service
	install -Dm644 LICENSE.sklauncher "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
