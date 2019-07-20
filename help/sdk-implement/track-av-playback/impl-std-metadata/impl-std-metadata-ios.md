---
description: 'null'
seo-description: 'null'
seo-title: iOS에서 표준 메타데이터 구현
title: iOS에서 표준 메타데이터 구현
uuid: 75 A 80 F 08-4 A 95-49 D 4-A 27 A -8 CE 531 D 64 D 31
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# iOS에서 표준 메타데이터 구현{#implement-standard-metadata-on-ios}

## 메타데이터 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | Constant for attaching standard metadata on `MediaInfo ADBMediaObject` |

## 구현

1. Create a dictionary of standard metadata key value pairs using the `ADBStandardMetadataKeys`
   [IOS 메타데이터 키](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. 메타데이터에 표준 메타데이터 상수를 사용하여 `MediaInfo``ADBMediaObject`   인스턴스에 표준 메타데이터 사전을 설정합니다.

1. Provide this `MediaInfo` object while invoking the `trackSessionStart` API.

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

