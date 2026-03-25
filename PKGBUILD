# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2017, 2018, 2019, 2020, 2021,
#                2022, 2023, 2024, 2025, 2026
#                Jesus Alonso
#    Copyright © 2022, 2023, 2024, 2025, 2026
#                Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as
#    published by the Free Software Foundation, either version 3 of
#    the License, or (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.
#    If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
#   Jesus Alonso
#     <doragasu at hotmail dot com>

# NOTE: As I want these packages for Genesis/Megadrive development, they do
# only support the m68000 CPU. If you want to support other m68k variants,
# either modify _target_cpu to suit your needs, or go wild, remove the
# --with-cpu switches and change --disable-multilib with --enable-multilib.
# Be warned that multilib packages will take a lot more time to build, and
# will also require more disk space.

_os="$(
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _libc="ndk-sysroot-gcc-compact"
  _compiler="clang"
  _libcompiler="libllvm"
  _sh="dash"
elif [[ "${_os}" == "GNU/Linux" ]]; then
  _libc="glibc"
  _compiler="gcc"
  _libcompiler="libgcc"
  _sh="sh"
elif [[ "${_os}" == "Msys" ]]; then
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
else
  _msg=(
    "Unknown os '${_os}'."
  )
  msg \
    "${_msg[*]}"
  _libc="msys2-w32api-runtime"
  _libc_headers="msys2-w32api-headers"
  _compiler="gcc"
  _libcompiler="gcc-libs"
  _sh="sh"
fi
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  _git="false"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_git_service" ]]; then
  _git_service="github"
fi
_archive_format="tar.xz"
_target=m68k-elf
_target_cpu=m68000
_pkg=gcc
pkgbase="${_target}-${_pkg}"
pkgname=(
  "${pkgbase}"
)
pkgver=15.2.0
_mpfrver=4.2.2
_mpcver=1.3.1
_gmpver=6.3.0
pkgrel=24
_pkgdesc=(
  "The GNU Compiler Collection."
  "(${_target})"
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  "aarch64"
  "armv8l"
  "armv7l"
  'i686'
  "mips"
  "pentium4"
  "powerpc"
  "x86_64"
)
license=(
  'GPL'
  'LGPL'
  'FDL'
  'custom'
)
url="http://${_pkg}.gnu.org"
depends=(
  "${_target}-binutils>=2.29-1"
  'zlib'
)
makedepends=(
  "${_target}-newlib"
)
if [[ "${_os}" == "Android" ]]; then
  makedepends+=(
    # This may be why it doesnt build.
    # Maybe it wants m68k-elf-mpc.
    "libmpc"
  )
fi
optdepends=(
  "${_target}-newlib"
)
options=(
  '!emptydirs'
  '!distcc'
  '!strip'
)
conflicts=(
  "${_target}-gcc-bootstrap=${pkgver}"
)
replaces=(
  "${_target}-gcc-bootstrap"
)
source=()
sha256sums=()
PKGEXT="pkg.tar.xz"
_tarname="${_pkg}-${pkgver}"
_tarfile="${_tarname}.${_archive_format}"
_sum="438fd996826b0c82485a29da03a72d71d6e3541a83ec702df4271f6fe025d24e"
_sig_sum="df837ba60ef8045d818b0bce190c00a9aac87e3b3e6dba9f04cf6d2f061ba239"
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
_uri="https://ftp.gnu.org/gnu/${_pkg}/${_tarname}/${_tarfile}"
if [[ "${_evmfs}" == "false" ]]; then
  true
elif [[ "${_evmfs}" == "true" ]]; then
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
fi
_src="${_tarfile}::${_uri}"
source+=(
  "${_src}"
  "https://ftp.gnu.org/gnu/${_pkg}/${_tarname}/${_tarfile}.sig"
  "https://ftp.gnu.org/gnu/mpfr/mpfr-${_mpfrver}.${_archive_format}"
  "https://ftp.gnu.org/gnu/mpfr/mpfr-${_mpfrver}.${_archive_format}.sig"
  "https://ftp.gnu.org/gnu/mpc/mpc-${_mpcver}.${_archive_format}"
  "https://ftp.gnu.org/gnu/mpc/mpc-${_mpcver}.${_archive_format}.sig"
  "https://ftp.gnu.org/gnu/gmp/gmp-${_gmpver}.${_archive_format}"
  "https://ftp.gnu.org/gnu/gmp/gmp-${_gmpver}.${_archive_format}.sig"
)
sha256sums+=(
  "${_sum}"
  "SKIP"
  "SKIP"
  "SKIP"
  "SKIP"
  "SKIP"
  "SKIP"
  "SKIP"
)
validpgpkeys=(
  "13975A70E63C361C73AE69EF6EEB81F8981C74C7"
  "A534BE3F83E241D918280AEB5831D11A0D4DB02A"
  "AD17A21EF8AED8F1CC02DBD9F7D5C9BF765C61E3"
  "343C2FF0FBEE5EC2EDBEF399F3599FF828C67298"
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

prepare() {
  cd \
    "${srcdir}/${_tarname}"

  # symlinks for in-tree build
  ln \
    -s \
    "../mpfr-${_mpfrver}"
  ln \
    -s \
    "../mpc-${_mpcver}"
  ln \
    -s \
    "../gmp-${_gmpver}"
  # hack! - some configure tests for
  # header files using "$CPP $CPPFLAGS"
  sed \
    -i \
    "/ac_cpp=/s/\$CPPFLAGS/\$CPPFLAGS -O2/" \
    {"libiberty","gcc","mpfr-${_mpfrver}","mpc-${_mpcver}","gmp-${_gmpver}"}"/configure"
  mkdir \
    "${srcdir}/${_pkg}-build"
}

build() {
  local \
    _configure_opts=()
  export \
    CFLAGS="${CFLAGS} -Wno-unknown-warning-option"
  _configure_opts+=(
    --prefix="/usr"
    --target="${_target}"
    --enable-languages="c,c++"
    --disable-multilib
    --with-cpu="${_target_cpu}"
    --with-system-zlib
    --with-newlib
    --with-libgloss
    --disable-shared
    --disable-nls
  )
  # GCC cannot be built with -Werror=format-security
  export \
    CFLAGS=${CFLAGS//-Werror=format-security/}
  export \
    CXXFLAGS=${CXXFLAGS//-Werror=format-security/}
  cd \
    "${srcdir}/${_pkg}-build"
  "../${_tarname}/configure" \
    "${_configure_opts[@]}"
  make
}

package_m68k-elf-gcc() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "${srcdir}/${_pkg}-build"
  make \
    "${_make_opts[@]}" \
    install
  # Remove unwanted files
  rm \
    -rf \
    "${pkgdir}/usr/share"
  rm \
    "${pkgdir}/usr/lib/libcc1.so" \
    "${pkgdir}/usr/lib/libcc1.so.0"
    "${pkgdir}/usr/lib/libcc1.so.0.0.0"
  # Strip it manually
  strip \
    "${pkgdir}/usr/bin/"* \
    2>/dev/null || \
    true
  find \
    "${pkgdir}/usr/lib" \
    -type \
      "f" \
    -exec \
      "/usr/bin/${_target}-strip" \
        --strip-unneeded \
        {} \; \
        2>"/dev/null" || \
    true
}
