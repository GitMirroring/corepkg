# CorePKG build script for Core.
# Copyright David Egan Evans <sinuhe@gnu.org>
#
# This program is free software; you can redistribute it and/or modify it 
# under the terms of the GNU General Public License as published by the 
# Free Software Foundation; either version 2 of the License, or (at your 
# option) any later version.
#
# This program is distributed in the hope that it will be useful, but 
# WITHOUT ANY WARRANTY; without even the implied warranty of 
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU 
# General Public License for more details.
#
# You should have received a copy of the GNU General Public License along 
# with this program; if not, see <https://www.gnu.org/licenses/>.

DIST=Core
PKG=corepkg
VERSION=8

if test ! -w .
then echo 'Cannot write to this directory!' 1>&2; exit 2
fi

if test ! -f core.info
then echo "The core.info file is not present." 1>&2; exit 3
fi

if test -d /tmp/$DIST-$PKG/
then rm -rf /tmp/$DIST-$PKG/
fi

rm -rf $PKG
tar xjf $PKG-$VERSION.tar.bz2 || exit 4
cd $PKG || exit 5

mkdir -pm 755 /tmp/$DIST-$PKG/usr/bin
mkdir -pm 755 /tmp/$DIST-$PKG/usr/man/man8
cp man/corepkg.8 /tmp/$DIST-$PKG/usr/man/man8/
bzip2 -9 /tmp/$DIST-$PKG/usr/man/man8/corepkg.8
cp src/corepkg /tmp/$DIST-$PKG/usr/bin/ && chmod a+x /tmp/$DIST-$PKG/usr/bin/*

cd ..
cp core.info /tmp/$DIST-$PKG/
if test $(id -u) -ne 0
then echo $PKG has been installed to /tmp/$DIST-$PKG/ 1>&2
	echo Before packaging: chown -R root: /tmp/$DIST-$PKG/ 1>&2
else chown -R root: /tmp/$DIST-$PKG/
	corepkg -c /tmp/$DIST-$PKG/ && rm -rf /tmp/$DIST-$PKG/
fi
rm -rf $PKG
