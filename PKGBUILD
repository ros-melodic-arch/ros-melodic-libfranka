pkgname="ros-melodic-libfranka"
pkgver="0.7.1"
pkgrel=1
pkgdesc="C++ library for Franka Emika research robots "
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h')
url="http://wiki.ros.org/libfranka"
license=('Apache')

ros_makedepends=(ros-melodic-roscpp ros-melodic-catkin)
makedepends=('cmake' 'ros-build-tools' ${ros_makedepends[@]})

ros_depends=()
depends=('eigen' 'poco' ${ros_depends[@]})

provides=($pkgname)
conflicts=($pkgname)
_dir="libfranka-release-release-melodic-libfranka"
source=("ros-melodic-libfranka-$pkgver.tar.gz::https://github.com/frankaemika/libfranka-release/archive/release/melodic/libfranka/$pkgver.tar.gz")
sha256sums=("508c192bfad0db8758f76bda1d6a6bc64164bbc747fb25372a55313cafd9a5b7")

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

