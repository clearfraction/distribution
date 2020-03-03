[![Slack](https://img.shields.io/badge/Community-Slack-orange.svg)](https://join.slack.com/t/linuxgangclub/shared_invite/enQtODYyNDMzNTIzMzYzLWJjYWYxNjBiNGZmYzc1MWIyYmIxZGQxNzRkOGUzNTdkY2NmZTJmOGQ3OWI0YTkzMDU2NGNlMGRmNTA2YWNjMzk)

# Clear Fraction - unofficial repository for [Clear Linux](https://clearlinux.org/)
## FFmpeg, Mpv, Gstreamer and more multimedia applications makes Clear Linux great again! Full x264, x265(HEVC), AAC, MP3 support.

## [TODO](https://github.com/clearfraction/distribution/projects/1)

### How to enable this repository:

* Install `dnf` package manager: `swupd bundle-add package-utils`
* Enable RPM repository:
`dnf config-manager --add-repo https://gitlab.com/clearfraction/repository/raw/repos/`
`dnf config-manager --add-repo https://download.clearlinux.org/current/x86_64/os/`

### Package updating & delete

* Updating: `dnf download pkg1 pkg2 && rpm -U --nodeps *rpm`
* Delete: `dnf remove pkg1 pkg2`

### Available applications

* Multimedia codecs pack

```
cd /tmp/
dnf download ffmpeg fdk-aac-free ffmpeg-libs gsm-lib libmp3lame0 x264 x264-libs x265-libs \
snappy-lib LuaJIT-lib gstreamer1-libav jack2-lib
rpm -ivh --nodeps *rpm
rm -rf *rpm
```

* Mpv player

```
dnf download mpv mpv-bin mpv-data mpv-lib libplacebo-lib glslang-lib
rpm -ivh --nodeps *rpm
rm -rf *rpm
```

* Foliate - EPUB/Mobi reader

```
dnf download foliate
rpm -ivh --nodeps *rpm
rm -rf *rpm
```

* Meteo - advanced weather app

```
dnf download meteo
rpm -ivh --nodeps *rpm
rm -rf *rpm
```

* Vocal - podcast streaming

```
dnf download vocal granite
rpm -ivh --nodeps *rpm
rm -rf *rpm
```

* PasswordSafe - passwords manager for GNOME

```
dnf download passwordsafe pykeepass-python3 construct-python3 pycryptodome-python3 lxml-python3 \
libpwquality-python3 argon2_cffi-python3 python-dateutil-python3 python-future-python3

rpm -ivh --nodeps *rpm
rm -rf *rpm
```


