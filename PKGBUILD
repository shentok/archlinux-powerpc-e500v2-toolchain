# Maintainer:

pkgname=powerpc-e500v2-toolchain
pkgver=024.05.r380.g5777bfc0f7
pkgrel=1
pkgdesc='Static analysis tool for ELF libraries and executables'
arch=($CARCH)
url='https://invent.kde.org/sdk/elf-dissector'
license=(GPL)
#depends=(harfbuzz hicolor-icon-theme libdwarf qt5-base)
makedepends=('buildroot-meta')
#optdepends=('capstone: disassembler' 'gnuplot: performance plot')
source=("git+https://github.com/buildroot/buildroot.git")
options=(!strip)
sha256sums=('SKIP')

pkgver() {
  cd "buildroot"
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' | cut -c2-47
}

prepare() {
  cd "${srcdir}/buildroot/configs"
  echo "BR2_powerpc=y" > powerpc_e500v2_toolchain_defconfig
  echo "BR2_powerpc_8548=y" >> powerpc_e500v2_toolchain_defconfig
  echo "BR2_PACKAGE_HOST_GDB=y" >> powerpc_e500v2_toolchain_defconfig
}

build() {
  cd "${srcdir}/buildroot"
  make powerpc_e500v2_toolchain_defconfig
  make sdk
}

package() {
  mkdir -p "${pkgdir}/opt/"
  cd "${pkgdir}/opt/"
  tar zxf "${srcdir}/buildroot/output/images/powerpc-buildroot-linux-uclibcspe_sdk-buildroot.tar.gz"
  mv powerpc-buildroot-linux-uclibcspe_sdk-buildroot ${pkgname}
  cd ${pkgname}
  ./relocate-sdk.sh "/opt/${pkgname}"
}
