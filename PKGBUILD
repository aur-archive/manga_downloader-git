# Conributor: Gabriel Peixoto <gabrielrcp@gmail.com>
# Maintainer: Ben R <thebenj88 *AT* gmail *DOT* com>

pkgname=manga_downloader-git
pkgver=0.325.b614d2f
pkgrel=1
pkgdesc="Python script for downloading manga from various websites"
arch=('any')
url="https://github.com/jiaweihli/manga_downloader"
license=('GPL3')
depends=('python2')
optdepends=('python2-imaging: for kindle conversion'
            'python2-beautifulsoup4: for Batoto parser')
makedepends=('git')

provides=('manga_downloader')
conflicts=('manga_downloader')


source=('git+git://github.com/jiaweihli/manga_downloader.git'
        'start-location.patch')
md5sums=('SKIP'
        '68c92e229bde4c9cb6e3a5e08dfb572a')

pkgver() {
  cd "$srcdir/manga_downloader"
   echo "0.$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
}

prepare() {

  cd "$srcdir/manga_downloader"

  # stop the script from trying to save manga in the install folder
  patch -Np1 -i "$srcdir/start-location.patch"

  # python fix
  find -type f -exec sed -e 's,#!/usr/bin/env python,#!/usr/bin/env python2,g' -i {} \;
  find -type f -exec sed -e 's,#!/usr/bin/python,#!/usr/bin/python2,g' -i {} \;
}


package() {
  cd "$srcdir/manga_downloader/src"

  install -dm 755 "$pkgdir/usr/share/manga_downloader"
  cp -r . "$pkgdir/usr/share/manga_downloader"
  install -dm 755 "$pkgdir/usr/bin/"
  ln -s /usr/share/manga_downloader/manga.py "$pkgdir/usr/bin/manga_downloader"
}
