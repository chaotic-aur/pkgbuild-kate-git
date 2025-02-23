# Maintainer: dr460nf1r3 <dr460nf1r3@garudalinux.org>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: Antonio Rojas <arojas@archlinux.org>
# Contributor: Andrea Scarpino <andrea@archlinux.org>

pkgname=kate-git
pkgver=21.07.70_r17988.g3d0d58325
pkgrel=1
pkgdesc="Advanced Text Editor"
groups=(kde-applications-git kde-utilities-git)
url="https://www.kde.org/applications/utilities/kate/"
depends=(knewstuff-git ktexteditor-git kactivities-git kuserfeedback-git hicolor-icon-theme)
optdepends=('konsole-git: open a terminal in Kate'
            'clang: C and C++ LSP support'
            'python-language-server: Python LSP support'
            'texlab: LaTeX LSP support'
            'rust: Rust LSP support')
arch=(x86_64)
license=(GPL LGPL FDL)
makedepends=(extra-cmake-modules-git kdoctools-git plasma-framework-git knewstuff-git kitemmodels-git ktexteditor-git kactivities-git kuserfeedback-git git)
provides=(${pkgname%-git} kwrite)
conflicts=(${pkgname%-git} kdesdk-kate kdebase-kwrite kwrite)
source=(git+https://invent.kde.org/utilities/${pkgname%-git}.git)
md5sums=('SKIP')

pkgver() {
  cd ${pkgname%-git}
  _major_ver="$(grep -m1 'set *(RELEASE_SERVICE_VERSION_MAJOR' CMakeLists.txt | cut -d '"' -f2)"
  _minor_ver="$(grep -m1 'set *(RELEASE_SERVICE_VERSION_MINOR' CMakeLists.txt | cut -d '"' -f2)"
  _micro_ver="$(grep -m1 'set *(RELEASE_SERVICE_VERSION_MICRO' CMakeLists.txt | cut -d '"' -f2)"
  echo "${_major_ver}.${_minor_ver}.${_micro_ver}_r$(git rev-list --count HEAD).g$(git rev-parse --short HEAD)"
}

prepare() {
  mkdir -p build
}

build() {
  cd build
  cmake -B build -S ../kate \
    -DBUILD_TESTING=OFF
  cmake --build build
}

package() {
  cd build
  DESTDIR="$pkgdir" cmake --install build
}
