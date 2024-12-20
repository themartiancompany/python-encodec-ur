# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Yauheni Kirylau <actionless dot loveless AT gmail MF com>
# shellcheck disable=SC2034,SC2154

_py="python"
_pkg="encodec"
_pkgname="${_py}-${_pkg}"
pkgname="${_pkgname}"
pkgver=0.1.1.r21.g0e2d0ae
_commit="0e2d0aed29362c8e8f52494baf3e6f99056b214f"
pkgrel=1
pkgdesc="EnCodec: High Fidelity Neural Audio Compression by Facebook"
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
  "${_py}-numpy"
  "${_py}-pytorch"
  "${_py}-torchaudio"
  "${_py}-einops"
)
makedepends=(
  "${_py}-wheel"
  "${_py}-hatchling"
  "${_py}-build"
  "${_py}-installer"
  "${_py}-setuptools"
)
optdepends=(
)
_branch="main"
_tag_name="commit"
_tag="${_commit}"
source=(
  "${pkgname}::git+${url}.git#${_tag_name}=${_tag}"
)
md5sums=(
  'SKIP'
)

pkgver() {
  cd \
    "${srcdir}/${pkgname}" || \
    exit \
      2
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
    "${srcdir}/${pkgname}" || \
  exit \
    2
  "${_py}" \
    -m \
      build \
      --wheel \
      --no-isolation
}

package() {
  cd \
    "${srcdir}/${pkgname}" || \
  exit 2
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
