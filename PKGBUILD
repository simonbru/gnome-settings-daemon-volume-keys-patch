# Maintainer:  Robin Visser  <rxvisser@gmail.com>
# Contributor: Filip Hendrik <stoatally@gmail.com>
# Contributor: Rowan Lewis   <rl@nbsp.io>

pkgname=gnome-settings-daemon-volume-step-patch
pkgver=3.26.1
pkgrel=1
pkgdesc="GNOME Settings daemon with an additional patch to allow configuration of volume steps"
url="http://www.gnome.org"
arch=(x86_64)
license=('GPL')
depends=(dconf gnome-desktop gsettings-desktop-schemas libcanberra-pulse libnotify libsystemd
         libwacom pulseaudio pulseaudio-alsa upower librsvg libgweather geocode-glib geoclue2 nss
         libgudev gtk3-print-backends libnm)
makedepends=(intltool xf86-input-wacom libxslt docbook-xsl python git gnome-common)
provides=('gnome-settings-daemon')
conflicts=('gnome-settings-daemon')
options=('!emptydirs')
install=gnome-settings-daemon.install
groups=('gnome')
source=(https://download.gnome.org/sources/${pkgname:0:21}/${pkgver:0:4}/${pkgname:0:21}-$pkgver.tar.xz
        volume-step.patch)
sha256sums=('711ac9bad06f6a4225f5eb2f4796474662f81f7077e16a4b7ee7ab974b65d893'
            'b4c47bc172fdf37365b5a0d547e7415419b994e566b6b730f0ed4429583a96fb')

prepare() {
  cd ${pkgname:0:21}-$pkgver

  # https://bugzilla.gnome.org/show_bug.cgi?id=650371
  patch -p1 -i ../volume-step.patch
}

build() {
  cd ${pkgname:0:21}-$pkgver

  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
      --libexecdir=/usr/lib/${pkgname:0:21} --disable-static

  # https://bugzilla.gnome.org/show_bug.cgi?id=656231
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

  make
}

package() {
  cd ${pkgname:0:21}-$pkgver
  make DESTDIR="$pkgdir" install
}
