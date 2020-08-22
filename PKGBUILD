# Maintainer Tyler Kaminski <durcor at disroot dot org>

# Based on comgr PKGBUILD by acxz <akashpatel2008 at yahoo dot com>

pkgname=comgr-git
_pkgname="${pkgname%-git}"
pkgver=r193.c6ae0cf
pkgrel=1
pkgdesc='Radeon Open Compute - compiler support'
arch=('x86_64')
url='https://github.com/RadeonOpenCompute/ROCm-CompilerSupport'
license=('custom:NCSAOSL')
depends=(zlib llvm-amdgpu rocm-device-libs)
makedepends=(cmake rocm-cmake)
provides=("$_pkgname")
conflicts=("$_pkgname")
source=("$pkgname::git+$url")
sha256sums=('SKIP')

pkgver() {
  cd "$pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  cmake -B build -Wno-dev \
        -DCMAKE_INSTALL_PREFIX=/opt/rocm \
        -DCMAKE_PREFIX_PATH="/opt/rocm/llvm;/opt/rocm" \
        "$pkgname/lib/comgr"

  make -C build
}

package() {
  DESTDIR="$pkgdir" make -C build install
  install -Dm644 "$pkgname/LICENSE.txt" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
