# Maintainer: Vlad <vlad@archlinux.net>
# Contributor: Sebastien Bariteau <numkem@gmail.com>

pkgname=atlassian-jira
pkgver=7.1.2
pkgrel=1
pkgdesc="Bug tracking, issue tracking and project management software"
url="https://www.atlassian.com/software/jira"
license=('custom')
arch=('i686' 'x86_64')
depends=('java-environment>=7')
optdepends=('mysql-connector-java: connect to MySQL'
            'libcups: used by bin/config.sh'
            'fontconfig: used by bin/config.sh')
backup=('etc/conf.d/jira'
        'opt/atlassian-jira/conf/server.xml'
        'opt/atlassian-jira/atlassian-jira/WEB-INF/classes/jira-application.properties')
install='jira.install'
source=("https://www.atlassian.com/software/jira/downloads/binary/atlassian-jira-software-${pkgver}-jira-${pkgver}.tar.gz"
        'jira.conf.d'
        'jira.service')
sha256sums=('4837de0425845966a4138e518da5325436bbc6c91bc78e7497bfc0384dfa411b'
            'd1ca27e15edb0032a37b1b0df302209e78d11671d44b6a239a017be9881708d0'
            'cff80b2a8f930ba3d1c11df809afa11ffe29b78d946689cb588b1ce2f4c01e5d')

package() {
  mkdir -p "$pkgdir/opt/atlassian-jira/"
  cp -r "$srcdir/atlassian-jira-software-${pkgver}-standalone/"* "$pkgdir/opt/atlassian-jira/"
  # remove unneeded *.bat files
  find "$pkgdir/opt/atlassian-jira/bin" -name '*.bat' -type f -exec rm "{}" \;

  # Setup systemd service
  install -dm755 "$pkgdir/usr/lib/systemd/system"
  install -Dm644 "$srcdir/jira.service" "$pkgdir/usr/lib/systemd/system"
  install -Dm644 "$srcdir/jira.conf.d" "$pkgdir/etc/conf.d/jira"
}
