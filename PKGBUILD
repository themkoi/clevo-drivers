# Maintainer: Nick Dowsett <nick42d AT gmail DOT com>
# Contributor: Evert Vorster <superchief AT evertvorster DOT com>
# Contributor: Steven Seifried <gitlab@canox.net>

pkgname=clevo-drivers-dkms-git
_pkgname=clevo-drivers
pkgver=4.15.0
pkgrel=1
pkgdesc="Unofficial modification of TUXEDO Computers kernel module drivers for keyboard, keyboard backlight & general hardware I/O using the SysFS interface, to allow it to run on other Clevo hardware. Use at your own risk."
url="https://github.com/nick42d/clevo-drivers"
license=("GPL-2.0+")
arch=('x86_64')
depends=('dkms')
makedepends=('git')
optdepends=('linux-headers: build modules against Arch kernel'
            'linux-lts-headers: build modules against LTS kernel'
            'linux-zen-headers: build modules against ZEN kernel'
            'linux-hardened-headers: build modules against the HARDENED kernel')
# tuxedo-keyboard-ite = ite_8291, ite_8291_lb, ite_8297 and ite_829x
provides=('tuxedo-drivers-dkms'
	  'tuxedo-keyboard'
          'tuxedo-keyboard-ite'
          'tuxedo-io'
          'clevo-wmi'
          'clevo-acpi'
          'uniwill-wmi'
          'ite_8291'
          'ite_8291_lb'
          'ite_8297'
          'ite_829x')
conflicts=('tuxedo-drivers-dkms' 'tuxedo-keyboard-dkms' 'tuxedo-keyboard-ite-dkms')
#backup=(etc/modprobe.d/tuxedo_keyboard.conf)
source=($pkgname-$pkgver.tar.gz::https://gitlab.com/tuxedocomputers/development/packages/tuxedo-drivers/-/archive/v$pkgver/$_pkgname-v$pkgver.tar.gz)
sha256sums=('SKIP')

prepare(){
	echo "$(ls)"
	cd "${srcdir}/tuxedo-drivers-v${pkgver}"*
	echo "Current directory is: $(pwd)"
	echo "pkgver is "${pkgver}
	patch -Np1 -i ../../patch.diff
}

package() {
	echo "Package step"
	mkdir -p "${pkgdir}/usr/src/${_pkgname}-${pkgver}"
	ln -s ${srcdir}/tuxedo-drivers ${srcdir}/${_pkgname}-${pkgver}
	cd ../
	echo "Current directory is: $(pwd)"
	sed -i "s/#MODULE_VERSION#/${pkgver}/" dkms.conf
	install -Dm644 dkms.conf -t "$pkgdir/usr/src/${_pkgname%}-$pkgver/"
	cd "${srcdir}/tuxedo-drivers-v${pkgver}"*
	echo "Current directory is: $(pwd)"

	install -Dm644 ./Makefile -t "$pkgdir/usr/src/${_pkgname%}-$pkgver/"
	install -Dm644 ./tuxedo_keyboard.conf -t "$pkgdir/usr/lib/modprobe.d/"
	cd ../../
	install -Dm644 ./tuxedo_io.conf -t "$pkgdir/usr/lib/modules-load.d/"
	#cp -avr "${_pkgname%}-$pkgver"/* "$pkgdir/usr/src/${_pkgname%}-$pkgver/"
cp -avr "${srcdir}"/tuxedo-drivers-v${pkgver}*/src/* "$pkgdir/usr/src/${_pkgname}-$pkgver/"
}

