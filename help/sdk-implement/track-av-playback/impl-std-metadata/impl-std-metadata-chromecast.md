---
description: 'null'
seo-description: 'null'
seo-title: Chromecast에서 표준 메타데이터 구현
title: Chromecast에서 표준 메타데이터 구현
uuid: 1560 d 3 e 0-29 f 5-4678-9 f 01-c 672 e 0 ae 547 b
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Chromecast에서 표준 메타데이터 구현{#implement-standard-metadata-on-chromecast}

표준 메타데이터 개체를 인스턴스화하고, 원하는 변수를 채우고, 미디어 하트비트 개체에서 메타데이터 개체를 설정합니다. 예:

```js
var standardVideoMetadata = {}; 
standardVideoMetadata[VideoMetadataKeys.SHOW] = "Sample show"; 
standardVideoMetadata[VideoMetadataKeys.SEASON] = "Sample season"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardVideoMetadata] = standardVideoMetadata;
```

```js
var standardAudioMetadata = {}; 
standardAudioMetadata[AudioMetadataKeys.ARTIST] = "Sample artist"; 
standardAudioMetadata[AudioMetadataKeys.ALBUM] = "Sample album"; 
 
mediaObject[ADBMobile.media.MediaObjectKey.StandardAudioMetadata] = standardAudioMetadata;
```

See the comprehensive list of audio and video metadata here: [Audio and video parameters.](../../../metrics-and-metadata/audio-video-parameters.md)
