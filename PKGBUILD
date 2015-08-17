pkgdesc="ROS - driver_base"
url='http://www.ros.org/'

pkgname='ros-groovy-driver-base'
pkgver='1.6.6'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('ros-build-tools')

depends=(ros-groovy-message-generation
  ros-groovy-message-runtime
  ros-groovy-roscpp
  ros-groovy-self-test
  ros-groovy-diagnostic-updater
  ros-groovy-dynamic-reconfigure
  ros-groovy-std-msgs
)

build() {
  [ -f /opt/ros/groovy/setup.bash ] && source /opt/ros/groovy/setup.bash
  if [ -d ${srcdir}/driver_base ]; then
    cd ${srcdir}/driver_base
    git fetch origin --tags
    git reset --hard release/groovy/driver_base/${pkgver}-0
  else
    git clone -b release/groovy/driver_base/${pkgver}-0 git://github.com/ros-gbp/driver_common-release.git ${srcdir}/driver_base
  fi
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/driver_base
  cmake ${srcdir}/driver_base -DCATKIN_BUILD_BINARY_PACKAGE=ON -DCMAKE_INSTALL_PREFIX=/opt/ros/groovy -DPYTHON_EXECUTABLE=/usr/bin/python2 -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
