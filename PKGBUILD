# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
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

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_offline="false"
_git="false"
_pkgname="retroarch"
_pkg="com.${_pkgname}"
_Pkg="${_pkgname}"
pkgname="${_pkgname}-bin"
pkgver=1.20.0
# _commit="e117ccae32d5a7d75479b61f034000122fe9fa24"
pkgrel=1597175263
_pkgdesc=(
  "Cross-platform videogame emulator"
  "with support for many gaming platforms."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'arm'
  'aarch64'
  'i686'
  'x86_64'
)
url="${_pkgname}.com"
license=(
  'GPL3'
)
depends=(
)
_os="$( \
  uname \
    -o)"
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  depends+=(
    'inteppacman'
  )
optdepends=(
)
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  optdepends+=(
  )
makedepends=(
  'coreutils'
)
checkdepends=(
)
provides=(
  "${_pkgname}=${pkgver}"
)
conflicts=(
  "${_pkgname}"
)
source=()
sha256sums=()
_url="https://f-droid.org/repo"
_tag="${pkgrel}"
_tag_name="pkgrel"
_tarname="${_pkgname}-${pkgver}-${pkgrel}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  source+=(
    "${_tarname}::git+${_url}#${_tag_name}=${_tag}"
  )
  sha256sums+=(
    SKIP
  )
elif [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == 'pkgrel' ]]; then
    _tar="${_tarname}.apk::${_url}/${_pkg}_${pkgrel}.apk"
    _sig="${_tarname}.apk.sig::${_url}/${_pkg}_${pkgrel}.apk.asc"
    _sum="16c6f49781b2cbbb980650764edc5b7f937e9eef8c4e8da6e2a743b93f9f8271"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _tar="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum="dacf4a05e8dab38c49034e5d58deb477c36d005fe81324cf7973ba5487d87eb7"
  fi
  source+=(
    "${_tar}"
    "${_sig}"
  )
  sha256sums+=(
    "${_sum}"
    "SKIP"
  )
fi
validgpgkeys=(
  # F-droid binary releases
  "37D2C98789D8311948394E3E41E7044E1DBA2E89"
)

package() {
  local \
    _dest_dir \
    _dest
  _dest_dir="/usr/bin"
  _dest="${_pkgname}.apk"
  if [[ "${_os}" == "Android" ]]; then
    _dest_dir="/system/app/${_Pkg}"
    _dest="base.apk"
  fi
  install \
    -dm755 \
    "${pkgdir}${_dest_dir}"
  install \
    -Dm644 \
    "${srcdir}/${_tarname}.apk" \
    "${pkgdir}/${_dest_dir}/${_dest}"
}

# vim: ft=sh syn=sh et
