# Maintainer: Solomon Fosuhene <your.email@example.com>
# Originally based on Archinstall by Anton Hvornum and the Arch Linux team

pkgname=soloinstall
pkgver=1.0.0
pkgrel=1
pkgdesc="SoloLinux graphical and guided installer (rebranded from Archinstall)"
arch=(any)
url="https://github.com/sololinux/soloinstall"
license=(GPL-3.0-or-later)

depends=(
  'arch-install-scripts'
  'btrfs-progs'
  'coreutils'
  'cryptsetup'
  'dosfstools'
  'e2fsprogs'
  'glibc'
  'kbd'
  'libcrypt.so'
  'libxcrypt'
  'pciutils'
  'procps-ng'
  'python'
  'python-cryptography'
  'python-pydantic'
  'python-pyparted'
  'python-textual'
  'systemd'
  'util-linux'
  'xfsprogs'
  'lvm2'
  'f2fs-tools'
  'ntfs-3g'
)
makedepends=(
  'python-build'
  'python-installer'
  'python-setuptools'
  'python-sphinx'
  'python-wheel'
  'python-sphinx_rtd_theme'
  'python-pylint'
  'ruff'
)
optdepends=(
  'python-systemd: Adds journald logging'
)

provides=(soloinstall)
conflicts=(archinstall python-archinstall)
replaces=(archinstall python-archinstall)

# source=("soloinstall")
# noextract=("soloinstall")

# sha512sums=('SKIP')
# b2sums=('SKIP')

check() {
  cd "$srcdir"
  ruff check || true
}

# pkgver() {
#   awk '$1 ~ /^__version__/ {gsub("\"", ""); print $3}' soloinstall/__init__.py
# }

build() {
  cd "$srcdir"
  python -m build --wheel --no-isolation
  PYTHONDONTWRITEBYTECODE=1 make -C docs man || true
}

package() {
  cd "$srcdir"
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -vDm 644 docs/_build/man/soloinstall.1 "$pkgdir/usr/share/man/man1/soloinstall.1" || true
}
