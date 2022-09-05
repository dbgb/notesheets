# Working with FFMPEG: Notesheet

## Flags

|    flag     |                                    description |
| :---------: | ---------------------------------------------: |
|     -an     |                                       no audio |
|     -ar     |                       audio sampling frequency |
| -c:v / -c:a | codec: video/audio (eg. aac, libmp3lame, copy) |
| -b:v / -b:a |                           bitrate: video/audio |
|    -q:a     |    quality factor for vbr audio (eg. 2 for V2) |
|    -crf     |                   quality factor for vbr video |
|   -aspect   |                   aspect ratio (eg. 16:9, 4:3) |
|     -r      |                               video frame rate |
|     -ss     |                           start of file offset |
|     -t      |                              encoding duration |

## Examples

```shell
ffmpeg -i nelly.flv \
-c:a libmp3lame -q:a 2 -ar 44100 -c:v libx264 -b:v 300k -r 30 nomorenelly.mp4

ffmpeg -i vdubproblems.flv \
-an -c:v libx264 -b:v 1800k -r 25 -ss 01:00:00 -t 00:10:00 vdubbableclip.mp4

ffmpeg -i bigfile.vob \
-r 25 -c:a aac -b:a 192k -c:v libx265 -crf 28 -s 640x480 transcoded_x265.mp4

ffmpeg -i bigfile2.wmv \
-c:a copy -c:v libx264 -b:v 1600k -s 1920x1080 transcoded_x264.mp4

ffmpeg -i badrotation.mp4 \
-codec copy -map_metadata 0 -metadata:s:v "rotate=90" goodrotation.mp4

ffmpeg -i "http://example.com/hls_video_url.m3u8" \
-c copy -bsf:a aac_adtstoasc "nomorehls.mp4"

ffmpeg -i somefile.mp3 -f segment -segment_time 3600 -c copy "%03d-split_track.mp3"

# https://trac.ffmpeg.org/wiki/Concatenate
ffmpeg -f concat -i mylist.txt -c copy output.foo
```

```bash
#!/bin/bash

shopt -s nullglob # Expand to null string when $1 matches nothing
shopt -s nocaseglob # Enable case insensitive globbing
IFS=$'\n' # For globbing, only split on newlines - not spaces or tabs

CRF=28
SIZE="720x576"
SUFFIX="[HEVC]"
EXTENSION="mp4"

for f in $1; do
  OUTPUTNAME="${f%.*}"_"$SUFFIX"."$EXTENSION"
  ./ffmpeg -i "$f" -c:v libx265 -crf "$CRF" -s "$SIZE" -r 25 \
  -c:a libmp3lame -q:a 2 "$OUTPUTNAME";
done
```
