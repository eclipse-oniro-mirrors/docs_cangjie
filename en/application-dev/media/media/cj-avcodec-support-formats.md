# AVCodec Supported Formats

## Media Codecs

### Video Decoding

Currently supported decoding capabilities:

| Video Hardware Decoding Types | Video Software Decoding Types |
| ----------------------------- | ----------------------------- |
| AVC(H.264), HEVC(H.265)<!--RP14--><!--RP14End--> | MPEG2, MPEG4, H.263, AVC(H.264)<!--RP12--><!--RP12End--> |

### Video Encoding

Currently supported encoding capabilities:

| Video Encoding Types          |
| ----------------------------- |
| HEVC(H.265), AVC(H.264)       |

### Audio Decoding

Currently supported decoding capabilities:

AAC, MPEG(MP3), Flac, Vorbis, AMR(amrnb, amrwb), G711mu, APE<!--RP1--><!--RP1End-->.

### Audio Encoding

Currently supported encoding capabilities:

AAC, Flac, MP3, G711mu<!--RP3--><!--RP3End-->.

## Media Container Formats and Parsing

### Media Parsing

Supported demuxing formats:

| Media Type | Container Format       | Stream Format                      |
| ---------- | ---------------------- | ---------------------------------- |
| AV         | mp4                    |<!--RP4-->Video: AVC(H.264), MPEG4; Audio: AAC, MPEG(MP3); Subtitles: WEBVTT<!--RP4End-->|
| AV         | fmp4                   |<!--RP5-->Video: AVC(H.264); Audio: AAC, MPEG(MP3)<!--RP5End-->|
| AV         | mkv                    |<!--RP6-->Video: AVC(H.264); Audio: AAC, MPEG(MP3), OPUS<!--RP6End-->|
| AV         | mpeg-ts                |<!--RP7-->Video: AVC(H.264), MPEG2, MPEG4; Audio: AAC, MPEG(MP3)<!--RP7End-->|
| AV         | flv                    |<!--RP8-->Video: AVC(H.264); Audio: AAC<!--RP8End-->|
| AV         | mpeg-ps                |Video: AVC(H.264), MPEG2; Audio: MPEG(MP2, MP3)|
| AV         | avi                    |Video: H.263, AVC(H.264), MPEG2, MPEG4; Audio: AAC, MPEG(MP2, MP3), PCM|
| Audio      | m4a                    |<!--RP9-->Audio: AAC<!--RP9End-->|
| Audio      | aac                    |Audio: AAC|
| Audio      | mp3                    |Audio: MPEG(MP3)|
| Audio      | ogg                    |Audio: Vorbis|
| Audio      | flac                   |Audio: Flac|
| Audio      | wav                    |Audio: PCM, G711mu|
| Audio      | amr                    |Audio: AMR(amrnb, amrwb)|
| Audio      | ape                    |Audio: APE|
| Subtitles  | srt                    |Subtitles: SRT|
| Subtitles  | webvtt                 |Subtitles: WEBVTT|

### Media Muxing

Currently supported muxing capabilities:

| Container Format | Video Codec Types       | Audio Codec Types       | Cover Types       |
| ---------------- | ----------------------- | ----------------------- | ----------------- |
| mp4              | AVC(H.264)<!--RP11--><!--RP11End--> | AAC, MPEG(MP3)          | jpeg, png, bmp    |
| m4a              | -                       | AAC                     | jpeg, png, bmp    |
| mp3              | -                       | MPEG(MP3)               | -                 |
| amr              | -                       | AMR(amrnb, amrwb)       | -                 |
| wav              | -                       | G711mu(pcm-mulaw)       | -                 |
| aac              | -                       | AAC                     | -                 |

> **Notes:**
>
> - For MP4 container with MPEG(MP3) audio, the sample rate must be ≥16000Hz.
> - For MP4/M4A containers with AAC audio, the number of channels must be between 1-7.