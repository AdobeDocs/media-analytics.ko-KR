---
title: Chromecast에서 표준 메타데이터를 구현하는 방법에 대해 알아보기
description: Chromecast에서 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 알아봅니다.
uuid: 1560d3e0-29f5-4678-9f01-c672e0ae547b
exl-id: 052ede4b-ea8a-4ca6-bf02-0aab22a8bcda
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '59'
ht-degree: 100%

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

오디오 및 비디오 메타데이터의 전체 목록을 [오디오 및 비디오 매개 변수](/help/implementation/variables/audio-video-parameters.md)에서 참조하십시오.
