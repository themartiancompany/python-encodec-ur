# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2022, 2023, 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
# Maintainer:
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Maintainer:
#   Yauheni Kirylau
#     <actionless dot loveless AT gmail MF com>

# shellcheck disable=SC2034,SC2154
if [[ ! -v "_git" ]]; then
  _git="true"
fi
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg="encodec"
_pkgname="${_py}-${_pkg}"
pkgname="${_pkgname}"
pkgver="0.1.1.r21.g0e2d0ae"
_commit="0e2d0aed29362c8e8f52494baf3e6f99056b214f"
pkgrel=1
_pkgdesc=(
  "EnCodec: High Fidelity"
  "Neural Audio Compression by Facebook"
)
arch=(
  'any'
)
_http="https://github.com"
_ns="facebookresearch"
url="${_http}/${_ns}/${_pkg}"
license=(
  'MIT'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-soundfile"
  "${_py}-numpy"
  "${_py}-pytorch"
  "${_py}-torchaudio"
  "${_py}-einops"
)
makedepends=(
  "${_py}"
  "${_py}-wheel"
  "${_py}-hatchling"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
)
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
optdepends=(
)
_branch="main"
_tag_name="commit"
_tag="${_commit}"
_tarname="${_pkg}-${_tag}"
if [[ "${_git}" == "true" ]]; then
  _src="${_tarname}::git+${url}.git#${_tag_name}=${_tag}"
fi
source=(
  "${_src}"
)
md5sums=(
  'SKIP'
)

pkgver() {
  cd \
    "${srcdir}/${_tarname}"
  set \
    -o \
    pipefail
  git \
    describe \
      --tags \
      --long | \
    sed \
      's/\([^-]*-g\)/r\1/;s/-/./g;s/^v//' || \
    echo \
      0.0.1
}

build() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    -m \
      build \
      --wheel \
      --no-isolation
}

package() {
  cd \
    "${srcdir}/${_tarname}"
  "${_py}" \
    -m \
      installer \
      --destdir="${pkgdir}" \
      "dist/"*".whl"
  install \
    -Dm644 \
    "LICENSE" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
