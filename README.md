# dtv-configs
dtv関連(mirakurn/epgstation)のconfig置き場

[docker-mirakurun-epgstation](https://github.com/l3tnun/docker-mirakurun-epgstation)をPX-W3U4で使いCIR115-NTTComとvaapiを追加したり[advancedbear/EPGS-to-Discord](https://github.com/advancedbear/EPGS-to-Discord)を手動追加したりした。昔はWindowsだった。
- `channels.yml`は環境に合わせて要修正 or `curl -X PUT "http://localhost:40772/api/config/channels/scan"`
- `enc_h264_qsv.js`は昔のなごり

環境
```
FUJITSU Server PRIMERGY TX1310 M3
Intel(R) Pentium(R) CPU G4560 @ 3.50GHz

CentOS Linux release 7.8.2003 (Core)
Docker version 19.03.13, build 4484c46d9d

px4_drv https://github.com/nns779/px4_drv

PLEX PX-W3U4
NTT Communications CIR115-NTTCom
```
host
```
[ys@tx1310m3 ~]# ls -n /dev/dri
total 0
crw-rw----+ 1 0 39 226,   0 Oct 12 06:30 card0
crw-rw----+ 1 0 39 226, 128 Oct 10 23:55 renderD128
```
```
[ys@tx1310m3 ~]$ lsusb
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 003: ID 0511:083f N'Able (DataBook) Technologies, Inc. 
Bus 001 Device 002: ID 046d:c534 Logitech, Inc. Unifying Receiver
Bus 001 Device 004: ID 31aa:1000  
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
container
```
root@ac2398a51e96:/app# ffmpeg -hwaccels
ffmpeg version 4.1 Copyright (c) 2000-2018 the FFmpeg developers
  built with gcc 8 (Debian 8.3.0-6)
  configuration: --prefix=/usr/local --disable-shared --pkg-config-flags=--static --enable-gpl --enable-libass --enable-libfreetype --enable-libmp3lame --enable-libopus --enable-libtheora --enable-libvorbis --enable-libvpx --enable-libx264 --enable-libx265 --enable-nonfree --enable-vaapi --disable-debug --disable-doc
  libavutil      56. 22.100 / 56. 22.100
  libavcodec     58. 35.100 / 58. 35.100
  libavformat    58. 20.100 / 58. 20.100
  libavdevice    58.  5.100 / 58.  5.100
  libavfilter     7. 40.101 /  7. 40.101
  libswscale      5.  3.100 /  5.  3.100
  libswresample   3.  3.100 /  3.  3.100
  libpostproc    55.  3.100 / 55.  3.100
Hardware acceleration methods:
vdpau
vaapi
```
