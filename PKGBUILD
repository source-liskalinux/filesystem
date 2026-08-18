# PKGBUILD For Liska Linux Filesystem

# Contributor: Janorovic Volkov <janorovicvolkov@gmail.com>
# Maintainer: Janorovic Volkov <janorovicvolkov@gmail.com>

pkgname=filesystem
pkgver=2026.08
pkgrel=1
pkgdesc='Base filesystem layout and core configuration for Liska Linux'
arch=('x86_64')
url='https://github.com/source-liskalinux/filesystem'
license=('GPL-3.0-or-later')
depends=('iana-etc')
backup=(
  'etc/environment'
  'etc/fstab'
  'etc/group'
  'etc/gshadow'
  'etc/host.conf'
  'etc/hostname'
  'etc/hosts'
  'etc/issue'
  'etc/ld.so.conf'
  'etc/liska-release'
  'etc/locale.conf'
  'etc/nsswitch.conf'
  'etc/os-release'
  'etc/passwd'
  'etc/profile'
  'etc/resolv.conf'
  'etc/securetty'
  'etc/shadow'
  'etc/shells'
  'etc/subgid'
  'etc/subuid'
)

package() {
    local dir mode user group link
    declare -A directories
    declare -A symlinks
    directories=(
        ["boot"]="755:0:0"
        ["dev"]="755:0:0"
        ["etc"]="755:0:0"
        ["etc/ld.so.conf.d"]="755:0:0"
        ["etc/profile.d"]="755:0:0"
        ["etc/skel"]="755:0:0"
        ["home"]="755:0:0"
        ["mnt"]="755:0:0"
        ["opt"]="755:0:0"
        ["proc"]="555:0:0"
        ["root"]="0750:0:0"
        ["run"]="755:0:0"
        ["run/liska"]="755:0:0"
        ["run/liska/bootmnt"]="755:0:0"
        ["srv"]="755:0:0"
        ["sys"]="555:0:0"
        ["tmp"]="1777:0:0"
        ["usr"]="755:0:0"
        ["usr/bin"]="755:0:0"
        ["usr/include"]="755:0:0"
        ["usr/lib"]="755:0:0"
        ["usr/lib/ld.so.conf.d"]="755:0:0"
        ["usr/local/bin"]="755:0:0"
        ["usr/local/etc"]="755:0:0"
        ["usr/local/include"]="755:0:0"
        ["usr/local/lib"]="755:0:0"
        ["usr/local/man"]="755:0:0"
        ["usr/local/sbin"]="755:0:0"
        ["usr/local/share"]="755:0:0"
        ["usr/local/src"]="755:0:0"
        ["usr/share/man/man1"]="755:0:0"
        ["usr/share/man/man2"]="755:0:0"
        ["usr/share/man/man3"]="755:0:0"
        ["usr/share/man/man4"]="755:0:0"
        ["usr/share/man/man5"]="755:0:0"
        ["usr/share/man/man6"]="755:0:0"
        ["usr/share/man/man7"]="755:0:0"
        ["usr/share/man/man8"]="755:0:0"
        ["usr/share/misc"]="755:0:0"
        ["usr/share/pixmaps"]="755:0:0"
        ["usr/src"]="755:0:0"
        ["var"]="755:0:0"
        ["var/cache"]="755:0:0"
        ["var/empty"]="755:0:0"
        ["var/lib/misc"]="755:0:0"
        ["var/local"]="755:0:0"
        ["var/log"]="755:0:0"
        ["var/opt"]="755:0:0"
        ["var/spool/mail"]="1777:0:0"
        ["var/tmp"]="1777:0:0"
    )
    symlinks=(
        ["bin"]="usr/bin"
        ["etc/mtab"]="../proc/self/mounts"
        ["lib"]="usr/lib"
        ["sbin"]="usr/bin"
        ["usr/local/share/man"]="../man"
        ["usr/sbin"]="bin"
        ["var/lock"]="../run/lock"
        ["var/mail"]="spool/mail"
        ["var/run"]="../run"
        ["lib64"]="usr/lib"
        ["usr/lib64"]="lib"
    )
    cd "$pkgdir"
    for dir in "${!directories[@]}"; do
        IFS=':' read -r mode user group <<< "${directories[$dir]}"
        install -vdm "$mode" -o "$user" -g "$group" "$dir"
    done
    for link in "${!symlinks[@]}"; do
        ln -sv "${symlinks[$link]}" "$link"
    done
    if [ -d "$srcdir" ]; then
        cp -a "$srcdir/." "$pkgdir/etc/"
    fi
    chmod 600 "$pkgdir/etc/shadow" 2>/dev/null || true
    chmod 600 "$pkgdir/etc/gshadow" 2>/dev/null || true
    chmod 600 "$pkgdir/etc/securetty" 2>/dev/null || true
    chmod 644 "$pkgdir/etc/passwd" 2>/dev/null || true
    chmod 644 "$pkgdir/etc/group" 2>/dev/null || true
}
