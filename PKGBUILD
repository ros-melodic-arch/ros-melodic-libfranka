# Maintainer: Libor Wagner <libor.wagner@cvut.cz>

pkgname=libfranka
pkgver=0.8.0
pkgrel=1
pkgdesc='C++ library for Franka Emika research robots'
arch=('x86_64')
license=('Apache')
depends=(cmake git poco eigen)
url=https://github.com/frankaemika/libfranka
source=(git://github.com/frankaemika/libfranka)
md5sums=(SKIP)

_dir=$pkgname

prepare() {
    cd $_dir
    git submodule init
    git checkout $pkgver
    git submodule update
}

build() {

    # Create build directory
  	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  	cd ${srcdir}/build

    # build
    cmake -DCMAKE_BUILD_TYPE=Release $srcdir/$_dir
    cmake --build .
}

package() {
    cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
