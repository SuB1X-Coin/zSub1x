
Debian
====================
This directory contains files used to package zsub1xd/zsub1x-qt
for Debian-based Linux systems. If you compile zsub1xd/zsub1x-qt yourself, there are some useful files here.

## zsub1x: URI support ##


zsub1x-qt.desktop  (Gnome / Open Desktop)
To install:

	sudo desktop-file-install zsub1x-qt.desktop
	sudo update-desktop-database

If you build yourself, you will either need to modify the paths in
the .desktop file or copy or symlink your zsub1xqt binary to `/usr/bin`
and the `../../share/pixmaps/zsub1x128.png` to `/usr/share/pixmaps`

zsub1x-qt.protocol (KDE)

