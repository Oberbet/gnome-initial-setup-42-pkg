# Maintainer: Balló György <ballogyor+arch at gmail dot com>

pkgname=gnome-initial-setup
pkgver=42.0.1
pkgrel=1
pkgdesc='Simple, easy, and safe way to prepare a new system'
arch=('x86_64')
url='https://gitlab.gnome.org/GNOME/gnome-initial-setup'
license=('GPL')
depends=('cheese' 'gdm' 'gnome-online-accounts' 'libgnomekbd' 'malcontent')
makedepends=('meson')
source=("https://mirror.csclub.uwaterloo.ca/gnome/sources/gnome-initial-setup/42/gnome-initial-setup-42.0.1.tar.xz")
sha256sums=('fcf43f2fbe4dc04c3ac2ae505633feb1ef30da70ca95eabc61e2006b192e5e55')

build() {
  arch-meson $pkgname-$pkgver build
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  DESTDIR="$pkgdir" meson install -C build
  install -d -o root -g 102 -m 750 "$pkgdir/usr/share/polkit-1/rules.d"

  # Setup system user and group
  echo 'u gnome-initial-setup - "GNOME Initial Setup" /run/gnome-initial-setup' |
    install -Dm644 /dev/stdin "$pkgdir/usr/lib/sysusers.d/$pkgname.conf"
  echo 'd /run/gnome-initial-setup 0700 gnome-initial-setup gnome-initial-setup -' |
    install -Dm644 /dev/stdin "$pkgdir/usr/lib/tmpfiles.d/$pkgname.conf"
    }
