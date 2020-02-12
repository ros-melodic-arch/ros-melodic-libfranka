# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: Your Name <youremail@domain.com>
pkgname="ros-melodic-libfranka"
pkgver="0.7.1"
_pkgver_patch=1
pkgrel=1
pkgdesc="C++ library for Franka Emika research robots "
arch=(x86_64)
url="https://github.com/frankaemika/libfranka"
license=('Apache')

ros_makedepends=(ros-melodic-roscpp ros-melodic-catkin)
makedepends=('cmake' 'ros-build-tools' ${ros_makedepends[@]})

depends=('eigen' 'poco' ${ros_depends[@]})

provides=($pkgname)
conflicts=($pkgname)
_dir="libfranka-release-release-melodic-libfranka-$pkgver-$_pkgver_patch"
source=("ros-melodic-libfranka-$pkgver-$_pkgver_patch.tar.gz::https://github.com/frankaemika/libfranka-release/archive/release/melodic/libfranka/$pkgver-$_pkgver_patch.tar.gz")
md5sums=('86f1aacc71666f7c2357e87445967ba6')

build() {
	# Use ROS environment variables
  	source /usr/share/ros-build-tools/clear-ros-env.sh
  	[ -f /opt/ros/melodic/setup.bash ] && source /opt/ros/melodic/setup.bash

	# Create build directory
  	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  	cd ${srcdir}/build

	# Build project
	cmake ${srcdir}/${_dir} \
	      -DCMAKE_BUILD_TYPE=Release \
	      -DCATKIN_BUILD_BINARY_PACKAGE=ON \
	      -DCMAKE_INSTALL_PREFIX=/opt/ros/melodic \
	      -DPYTHON_EXECUTABLE=/usr/bin/python3 \
	      -DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}

