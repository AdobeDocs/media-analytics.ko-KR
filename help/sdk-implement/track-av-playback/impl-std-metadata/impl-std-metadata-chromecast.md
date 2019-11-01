---
title: Chromecast에서 표준 메타데이터 구현
description: Chromecast에서 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 설명합니다.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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

See the comprehensive list of audio and video metadata here: [Audio and video parameters.](/help/metrics-and-metadata/audio-video-parameters.md)
