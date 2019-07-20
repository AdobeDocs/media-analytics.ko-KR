---
description: 'null'
seo-description: 'null'
seo-title: Android에서 표준 메타데이터 구현
title: Android에서 표준 메타데이터 구현
uuid: C 48 B 4190-B 062-4 C 4 E -9 C 40-8 DDE 4598 A 50 E
translation-type: tm+mt
source-git-commit: 46797deb402fed1c4d4781507c279407f8c13f2e

---


# Android에서 표준 메타데이터 구현{#implement-standard-metadata-on-android}

## 표준 메타데이터 상수

| 상수 이름 | 설명   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | `MediaObject`에 표준 메타데이터를 첨부하기 위한 상수. |

## 메타데이터 키 API 참조

* Create a `HashMap` of standard metadata key value pairs.
   * [비디오 메타데이터 키](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [오디오 메타데이터 키](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* 메타데이터에 표준 메타데이터 상수를 사용하여 `HashMap`에서 표준 메타데이터 `MediaInfo`을 설정합니다.
* Provide this `MediaInfo` object while invoking the `trackSessionStart()` API.

## 샘플 구현

### 비디오

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardVideoMetadata= new HashMap<String, String>(); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, "Sample Episode"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, "Sample Show"); 
standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, "Sample Season"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardVideoMetadata, standardVideoMetadata);
```

### 오디오

```java
// Sample code to set standard metadata for tracking sessions 
Map <String, String> standardAudiooMetadata= new HashMap<String, String>(); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ARTIST, "Sample Artist"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.ALBUM, "Sample Album"); 
standardAudiooMetadata.put(MediaHeartbeat.AudiooMetadataKeys.LABEL, "Sample Label"); 
mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAudiooMetadata, standardAudiooMetadata);
```
