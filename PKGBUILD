# Maintainer:

pkgname=powerpc-e500v2-toolchain
pkgver=024.05.r378.g916f9bb1a3
pkgrel=1
pkgdesc='Static analysis tool for ELF libraries and executables'
arch=($CARCH)
url='https://invent.kde.org/sdk/elf-dissector'
license=(GPL)
#depends=(harfbuzz hicolor-icon-theme libdwarf qt5-base)
makedepends=('buildroot-meta')
#optdepends=('capstone: disassembler' 'gnuplot: performance plot')
source=("git+https://github.com/buildroot/buildroot.git")
sha256sums=('SKIP')

pkgver() {
  cd "buildroot"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' | cut -c2-47
}

prepare() {
  cd "${srcdir}/buildroot/configs"
  echo "BR2_powerpc=y" > powerpc_e500v2_toolchain_defconfig
  echo "BR2_powerpc_8548=y" >> powerpc_e500v2_toolchain_defconfig
}

build() {
  cd "${srcdir}/buildroot"
  make powerpc_e500v2_toolchain_defconfig
  make sdk
}

package() {
  DESTDIR="$pkgdir" cmake --install build
}
