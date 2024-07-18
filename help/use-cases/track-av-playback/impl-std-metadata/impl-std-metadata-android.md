---
title: Android에서 표준 메타데이터를 구현하는 방법에 대해 알아보기
description: Android에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 알아봅니다.
uuid: c48b4190-b062-4c4e-9c40-8dde4598a50e
exl-id: 31afd8b5-0f23-4025-afcb-6df906cf6be5
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 100%

---

# Android에서 표준 메타데이터 구현{#implement-standard-metadata-on-android}

## 표준 메타데이터 상수

| 상수 이름 | 설명   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardMediaMetadata` | `MediaObject`에 표준 메타데이터를 첨부하기 위한 상수. |

## 메타데이터 키 API 참조

* 표준 메타데이터 키 값 쌍의 `HashMap`을 만듭니다.
   * [비디오 메타데이터 키](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.VideoMetadataKeys.html)
   * [오디오 메타데이터 키](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.AudioMetadataKeys.html)
* 메타데이터에 표준 메타데이터 상수를 사용하여 `HashMap`에서 표준 메타데이터 `MediaInfo`을 설정합니다.
* 이 `trackSessionStart()` 개체를 `MediaInfo` API를 호출하는 동안 제공합니다.

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
