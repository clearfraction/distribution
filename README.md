# Clear Fraction - 3rd-party repository for [Clear Linux](https://clearlinux.org/)

- FFmpeg, Mpv, Gstreamer, Brave, VSCodium and more applications

- x264, x265(HEVC) and AAC support

- open source infrastructure and build logs

### How to enable the repository

```bash
sudo swupd 3rd-party add clearfraction https://clearfraction.herokuapp.com/update
sudo mkdir -p /etc/environment.d
sudo tee -a /etc/environment.d/10-cf.conf << EOF
PATH=$PATH:/opt/3rd-party/bundles/clearfraction/bin:/opt/3rd-party/bundles/clearfraction/usr/bin:/opt/3rd-party/bundles/clearfraction/usr/local/bin
LD_LIBRARY_PATH=/opt/3rd-party/bundles/clearfraction/usr/lib64:/opt/3rd-party/bundles/clearfraction/usr/local/lib64${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
XDG_DATA_DIRS=/opt/3rd-party/bundles/clearfraction/usr/share/:/opt/3rd-party/bundles/clearfraction/usr/local/share/:${XDG_DATA_DIRS:-/usr/local/share/:/usr/share/}
XDG_CONFIG_DIRS=/opt/3rd-party/bundles/clearfraction/usr/share/xdg:/opt/3rd-party/bundles/clearfraction/etc/xdg:${XDG_CONFIG_DIRS:-/usr/share/xdg:/etc/xdg}
FONTCONFIG_PATH=/usr/share/defaults/fonts${FONTCONFIG_PATH:+:$FONTCONFIG_PATH}
GST_PLUGIN_PATH_1_0=/opt/3rd-party/bundles/clearfraction/usr/lib64/gstreamer-1.0:${GST_PLUGIN_PATH_1_0:-/usr/lib64/gstreamer-1.0}
EOF
```
Environment tuning needed for better system integration. Related: [swupd-client#1420](https://github.com/clearlinux/swupd-client/issues/1420), [swupd-client#1464](https://github.com/clearlinux/swupd-client/issues/1464), [swupd-client#1463](https://github.com/clearlinux/swupd-client/issues/1463), [swupd-client#1428](https://github.com/clearlinux/swupd-client/issues/1428), [swupd-client#1421](https://github.com/clearlinux/swupd-client/issues/1421).

Optional steps:
- `glib-compile-schemas /opt/3rd-party/bundles/clearfraction/usr/share/glib-2.0/schemas` fix gsettings schema error

- `rm -rf ~/.cache/gstreamer-1.0` fix for gstreamer AAC audio playback

### Install software

- `sudo swupd 3rd-party bundle-list -a` - show available bundles

- `sudo swupd 3rd-party install codecs` - install ffmpeg & gstreamer-libav with dependencies

### Updates

`sudo swupd 3rd-party update`

### How to repair

- `sudo swupd 3rd-party repair`
- `sudo swupd 3rd-party remove clearfraction && sudo swupd 3rd-party add clearfraction https://clearfraction.herokuapp.com/update`


### Video playback in Firefox

```
echo "export LD_LIBRARY_PATH=/opt/3rd-party/bundles/clearfraction/usr/lib64" >> "${HOME}/.config/firefox.conf"
```
