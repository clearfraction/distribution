[![Slack](https://img.shields.io/badge/Community-Slack-orange.svg)](https://join.slack.com/t/linuxgangclub/shared_invite/enQtODYyNDMzNTIzMzYzLWJjYWYxNjBiNGZmYzc1MWIyYmIxZGQxNzRkOGUzNTdkY2NmZTJmOGQ3OWI0YTkzMDU2NGNlMGRmNTA2YWNjMzk)

# Clear Fraction - unofficial repository for [Clear Linux](https://clearlinux.org/)
## FFmpeg, Mpv, Gstreamer, Brave, VSCodium and more applications
## x264, x265(HEVC) and AV1 support


## [TODO](https://github.com/clearfraction/distribution/projects/1)

### How to enable the repository

* `swupd 3rd-party add clearfraction https://clearfraction.gitlab.io/updates`

Optional steps:

* `cp -r /opt/3rd-party/bundles/clearfraction/usr/share/applications/* ~/.local/share/applications/` if you don't see launchers of installed applications (not needed for `codecs` bundle)

* `glib-compile-schemas /opt/3rd-party/bundles/clearfraction/usr/share/glib-2.0/schemas/` if gsettings schema error

* `rm -rvf ~/.cache/gstreamer-1.0/` fix for troubles with gstreamer audio playback

### Install software

`swupd 3rd-party bundle-list -a` will show all availanle bundles
`swupd 3rd-party install codecs` will install ffmpeg & gstreamer-libav

### Get updates

`swupd 3rd-party update`



#### Environment variables

Very helpful for better system integration, for example any application can use ffmpeg&gstreamer without issues

* For GNOME users: add to the end of line `/usr/share/gdm/env.d/flatpak.env`: `XDG_DATA_DIRS=...:/opt/3rd-party/bundles/clearfraction/usr/share/`

* For all:

`echo 'FONTCONFIG_PATH=/usr/share/defaults/fonts' >> ~/.config/environment.d/envvars.conf`

`echo 'XDG_DATA_DIRS=$XDG_DATA_DIRS:/opt/3rd-party/bundles/clearfraction/usr/share/' >> ~/.config/environment.d/envvars.conf`

`echo 'GST_PLUGIN_PATH_1_0=/opt/3rd-party/bundles/clearfraction/usr/lib64/gstreamer-1.0:/usr/lib64/gstreamer-1.0' >> ~/.config/environment.d/envvars.conf`

`echo 'PATH=/opt/3rd-party/bundles/clearfraction/bin:/opt/3rd-party/bundles/clearfraction/usr/bin:/opt/3rd-party/bundles/clearfraction/usr/local/bin:$PATH' >> ~/.config/environment.d/envvars.conf`

`echo 'LD_LIBRARY_PATH=/opt/3rd-party/bundles/clearfraction/usr/lib64:/opt/3rd-party/bundles/clearfraction/usr/local/lib64:$LD_LIBRARY_PATH'  >> ~/.config/environment.d/envvars.conf`

Copying icons is neccessary 'cause this [bug](https://github.com/clearlinux/swupd-client/issues/1420).

### How to repair

* `sudo swupd 3rd-party repair`

