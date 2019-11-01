---
title: iOS에서 표준 광고 메타데이터 구현
description: iOS에서 광고 추적에서 표준 광고 메타데이터를 사용하는 방법.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# iOS에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-ios}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## 구현 표준 광고 메타데이터

표준 광고 메타데이터의 경우 플랫폼용 키를 사용하여 표준 광고 메타데이터 키 값 쌍의 사전을 만듭니다.

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 메타데이터 키](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
