# vim:set ft=sh:
# Maintainer: Devin Christensen <quixoten at gmail dot com>
pkgname=powerline-fonts-git
_gitname=powerline-fonts
pkgver=20171013.d70b156
pkgrel=1
pkgdesc="Powerline fonts for X11 and the console"
arch=('any')
url='https://github.com/Lokaltog/powerline-fonts'
license=('CPL')
depends=('fontconfig' 'xorg-font-utils')
makedepends=('git')
conflicts=('powerline-fonts')
provides=('ttf-hack')
install=$pkgname.install
source=('git://github.com/Lokaltog/powerline-fonts.git'
	'git://github.com/Lokaltog/powerline.git')
md5sums=('SKIP' 'SKIP')

pkgver() {
	cd $_gitname
	# Use the tag of the last commit
	echo $(git log -1 --format="%ci" | sed 's/.*\([0-9]\{4\}\)-\([0-9]\{2\}\)-\([0-9]\{2\}\).*/\1\2\3/').$(git rev-parse --short HEAD)
}

package() {
	cp="cp -dpr --no-preserve=ownership"
	install -d "$pkgdir/usr/share/fonts/TTF"
	install -d "$pkgdir/usr/share/fonts/OTF"
	install -d "$pkgdir/usr/share/fonts/misc"
	install -d "$pkgdir/usr/share/kbd/consolefonts"
	install -d "$pkgdir/etc/fonts/conf.avail"

	cd $_gitname
	find . -iname "*.ttf" -exec install -m644 {} $pkgdir/usr/share/fonts/TTF \;
	find . -iname "*.otf" -exec install -m644 {} $pkgdir/usr/share/fonts/OTF \;
	find . -iname "*.pcf.gz" -exec install -m644 {} $pkgdir/usr/share/fonts/misc \;
	find . -iname "*.psf.gz" -exec install -m644 {} $pkgdir/usr/share/kbd/consolefonts \;

	install -m644 $srcdir/powerline/font/PowerlineSymbols.otf $pkgdir/usr/share/fonts/OTF
	install -m644 $srcdir/powerline/font/10-powerline-symbols.conf $pkgdir/etc/fonts/conf.avail
}
