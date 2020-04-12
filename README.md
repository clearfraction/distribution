[![Slack](https://img.shields.io/badge/Community-Slack-orange.svg)](https://join.slack.com/t/linuxgangclub/shared_invite/enQtODYyNDMzNTIzMzYzLWJjYWYxNjBiNGZmYzc1MWIyYmIxZGQxNzRkOGUzNTdkY2NmZTJmOGQ3OWI0YTkzMDU2NGNlMGRmNTA2YWNjMzk)

# Clear Fraction - unofficial repository for [Clear Linux](https://clearlinux.org/)
## FFmpeg, Mpv, Gstreamer and more multimedia applications
## x264, x265(HEVC) and AV1 support


## [TODO](https://github.com/clearfraction/distribution/projects/1)

### How to enable the repository

* `swupd 3rd-party add clearfraction https://gitlab.com/clearfraction/bundles/-/raw/master/update`

* `cp -r /opt/3rd-party/bundles/clearfraction/usr/share/applications/* ~/.local/share/applications/`

* `glib-compile-schemas /opt/3rd-party/bundles/clearfraction/usr/share/glib-2.0/schemas/` if gsettings schema error

Now you can install bundles like `swupd 3rd-party bundle-add codecs`. Check all available bundles [here](https://github.com/clearfraction/bundles/tree/master/configs). 
Copying icons is neccessary 'cause this [bug](https://github.com/clearlinux/swupd-client/issues/1420).

### How to repair

* `sudo swupd 3rd-party repair`

