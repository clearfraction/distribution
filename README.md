<div id="logo" align="center">
<br />
<img src="https://clearfraction.cf/media/logo.svg" alt="Clear Fraction logo" width="200" />
<h1>Clear Fraction</h1>
<h3>Third-party repository for [Clear Linux](https://clearlinux.org/) optimized for performance</h3>  
</div>


### Features:

- FFmpeg, Mpv, Gstreamer, VSCodium, Brave and [more applications](https://github.com/clearfraction/bundles/tree/master/configs)

- popular media codecs support including ffmpeg with SVT-AV1 encoder

- open source workflow and build logs

## Table of Contents

- [How to enable the repository](#how-to-enable-the-repository)

- [Install software](#install)

- [How to get updates](#updates)

- [Repair](#repair)

- [Video playback in Firefox](#firefox)

- [Documentation](#docs) 

- [Donate](#donate)

### <a id="how-to-enable-the-repository"></a>How to enable the repository

- note 1: for old CPUs without AVX2 support use the `https://v2download.clearfraction.cf/update`, you can fix it anytime in the swupd config `/opt/3rd-party/repo.ini`.
- note 2: do not install `mpv` from Clear repository, strange things will happen. [Enabling](https://wiki.gentoo.org/wiki/Mpv#Broken_hardware_video_decoding.2Fhigh_CPU_usage) hardware acceleration may be a good idea.

```bash
sudo swupd 3rd-party add clearfraction https://download.clearfraction.cf/update
sudo mkdir -p /etc/environment.d /etc/profile.d
sudo tee -a /etc/environment.d/10-cf.conf << 'EOF'
PATH=$PATH:/opt/3rd-party/bundles/clearfraction/bin:/opt/3rd-party/bundles/clearfraction/usr/bin:/opt/3rd-party/bundles/clearfraction/usr/local/bin
LD_LIBRARY_PATH=/usr/lib64:/opt/3rd-party/bundles/clearfraction/usr/lib64:/opt/3rd-party/bundles/clearfraction/usr/local/lib64${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}
XDG_DATA_DIRS=${XDG_DATA_DIRS:-/usr/local/share/:/usr/share/}:/opt/3rd-party/bundles/clearfraction/usr/share/:/opt/3rd-party/bundles/clearfraction/usr/local/share/
XDG_CONFIG_DIRS=${XDG_CONFIG_DIRS:-/usr/share/xdg:/etc/xdg}:/opt/3rd-party/bundles/clearfraction/usr/share/xdg:/opt/3rd-party/bundles/clearfraction/etc/xdg
FONTCONFIG_PATH=/usr/share/defaults/fonts${FONTCONFIG_PATH:+:$FONTCONFIG_PATH}
GST_PLUGIN_PATH_1_0=${GST_PLUGIN_PATH_1_0:-/usr/lib64/gstreamer-1.0}:/opt/3rd-party/bundles/clearfraction/usr/lib64/gstreamer-1.0
EOF

sudo tee -a /etc/profile.d/10-cf.sh << 'EOF'
[[ ! ${PATH} =~ "/opt/3rd-party/bundles/clearfraction/bin" ]] && \
  PATH=$PATH:/opt/3rd-party/bundles/clearfraction/bin:/opt/3rd-party/bundles/clearfraction/usr/bin:/opt/3rd-party/bundles/clearfraction/usr/local/bin

[[ ! ${LD_LIBRARY_PATH} =~ "/opt/3rd-party/bundles/clearfraction/usr/lib64" ]] && \
  LD_LIBRARY_PATH=/usr/lib64:/opt/3rd-party/bundles/clearfraction/usr/lib64:/opt/3rd-party/bundles/clearfraction/usr/local/lib64${LD_LIBRARY_PATH:+:$LD_LIBRARY_PATH}

[[ ! ${XDG_DATA_DIRS} =~ "/opt/3rd-party/bundles/clearfraction/usr/share" ]] && \
  XDG_DATA_DIRS=${XDG_DATA_DIRS:-/usr/local/share/:/usr/share/}:/opt/3rd-party/bundles/clearfraction/usr/share/:/opt/3rd-party/bundles/clearfraction/usr/local/share/

[[ ! ${XDG_CONFIG_DIRS} =~ "/opt/3rd-party/bundles/clearfraction/usr/share/xdg" ]] && \
  XDG_CONFIG_DIRS=${XDG_CONFIG_DIRS:-/usr/share/xdg:/etc/xdg}:/opt/3rd-party/bundles/clearfraction/usr/share/xdg:/opt/3rd-party/bundles/clearfraction/etc/xdg

[[ ! ${FONTCONFIG_PATH} =~ "/usr/share/defaults/fonts" ]] && \
  FONTCONFIG_PATH=/usr/share/defaults/fonts${FONTCONFIG_PATH:+:$FONTCONFIG_PATH}

[[ ! ${GST_PLUGIN_PATH_1_0} =~ "/opt/3rd-party/bundles/clearfraction/usr/lib64/gstreamer-1.0" ]] && \
  GST_PLUGIN_PATH_1_0=${GST_PLUGIN_PATH_1_0:-/usr/lib64/gstreamer-1.0}:/opt/3rd-party/bundles/clearfraction/usr/lib64/gstreamer-1.0
EOF
```


Environment tuning needed for better system integration. Related: [swupd-client#1420](https://github.com/clearlinux/swupd-client/issues/1420), [swupd-client#1464](https://github.com/clearlinux/swupd-client/issues/1464), [swupd-client#1463](https://github.com/clearlinux/swupd-client/issues/1463), [swupd-client#1428](https://github.com/clearlinux/swupd-client/issues/1428), [swupd-client#1421](https://github.com/clearlinux/swupd-client/issues/1421).

Optional steps:

- `glib-compile-schemas /opt/3rd-party/bundles/clearfraction/usr/share/glib-2.0/schemas` fix the gsettings schema error

- `rm -rf ~/.cache/gstreamer-1.0` fix for gstreamer AAC audio playback

### <a id="install"></a>Install software

The repository provides separate `codecs` and `codecs-cuda` bundles. Preferably, choose one and not install both. If needed, remove the existing codecs installation first.

- `sudo swupd 3rd-party bundle-list -a` - show available bundles

- `sudo swupd 3rd-party bundle-add codecs` - install ffmpeg & gstreamer-libav with dependencies, supporting Intel (qsv, vaapi) and AMD (vaapi) 

- `sudo swupd 3rd-party bundle-add codecs-cuda` - install ffmpeg & gstreamer-libav with dependencies, supporting AMD (vaapi, vdpau), Intel (qsv, vaapi), and NVIDIA (nvdec, vaapi, vdpau), also includes the (nvdec, vdpau) backend vaapi drivers


### <a id="updates"></a>How to get updates

`sudo swupd 3rd-party update`

### <a id="repair"></a>How to repair

- `sudo swupd 3rd-party repair`
- `sudo swupd 3rd-party remove clearfraction && sudo swupd 3rd-party add clearfraction https://download.clearfraction.cf/update`

### <a id="firefox"></a>Video playback in Firefox

```
echo "export LD_LIBRARY_PATH=/opt/3rd-party/bundles/clearfraction/usr/lib64" >> "${HOME}/.config/firefox.conf"
```
Apply the following Firefox settings via `about:config`:

- `media.ffmpeg.vaapi.enabled` to `true`
- `media.ffvpx.enabled` and `media.av1.enabled` to `false` - useful for Youtube if your hardware doesn't supports VP9 or AV1 acceleration

For NVidia graphics recommend to try the [config](https://github.com/marioroy/nvidia-driver-on-clear-linux/blob/main/HWAccel/firefox/firefox.conf) written by @marioroy:

```
curl -L https://github.com/marioroy/nvidia-driver-on-clear-linux/raw/main/HWAccel/firefox/firefox.conf -o "${HOME}/.config/firefox.conf"
```

For NVidia hardware acceleration set the `widget.dmabuf.force-enabled` to `true` in `about:config`.

### <a id="docs"></a>Documentation

- [Docs](https://github.com/clearfraction/docs)
  - [How it works](https://github.com/clearfraction/docs/blob/main/README.md#how-it-works)
  - [How to build software using Clear Fraction libraries like x264, x265 or CUDA](https://github.com/clearfraction/docs/blob/main/README.md#how-to-build-software-using-clear-fraction-libraries-like-x264-x265-or-cuda) 



### <a id="donate"></a>Donate

- [Patreon](https://www.patreon.com/clearfraction)

- BTC: bc1qpzse7xm76cx34dn5vc52ng5s68v2glp7ce55as

- [PayPal](https://www.paypal.com/donate/?hosted_button_id=L7ML8QJSLBTUE)

Patrons: 

- Air Dedman - CF Worshipper

Special thanks to:

- @kuboosoft & @lebensterben for tech consulting
