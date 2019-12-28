# Clear Fraction - unofficial repository for [Clear Linux](https://clearlinux.org/)
## FFmpeg, Mpv, Gstreamer and more multimedia applications



### How to enable this repository:

* Istall `dnf` package manager: `swupd bundle-add package-utils`
* Enable RPM repository:
`dnf config-manager --add-repo https://gitlab.com/clearfraction/repository/raw/repos/`
`dnf config-manager --add-repo https://download.clearlinux.org/current/x86_64/os/`



### Available applications

* Multimedia codecs pack

```
cd /tmp/
dnf download ffmpeg fdk-aac-free ffmpeg-libs gsm-lib libmp3lame0 x264 x264-libs x265-libs snappy-lib LuaJIT-lib gstreamer1-libav
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

* Meteo - advanced weather

```
dnf download meteo
rpm -ivh --nodeps *rpm
rm -rf *rpm
```
