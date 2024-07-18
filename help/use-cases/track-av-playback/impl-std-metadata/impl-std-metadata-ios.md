---
title: iOS에서 표준 메타데이터를 구현하는 방법에 대해 알아보기
description: iOS에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 알아봅니다.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 100%

---

# iOS에서 표준 메타데이터 구현{#implement-standard-metadata-on-ios}

## 메타데이터 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | 표준 메타데이터를 `MediaInfo ADBMediaObject`에 첨부하기 위한 상수입니다. |

## 구현

1. 표준 메타데이터 키 값 쌍 사전을 `ADBStandardMetadataKeys`를 사용하여 만듭니다.
   [iOS 메타데이터 키](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. 메타데이터에 표준 메타데이터 상수를 사용하여 `MediaInfo` `ADBMediaObject` 인스턴스에 표준 메타데이터 사전을 설정합니다.

1. 이 `trackSessionStart` 개체를 `MediaInfo` API를 호출하는 동안 제공합니다.

### 샘플 구현

표준 메타데이터 개체를 인스턴스화하고, 원하는 변수를 채우고, 미디어 하트비트 개체에서 메타데이터 개체를 설정합니다. 예:

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```
