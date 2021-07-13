---
title: iOS에서 표준 광고 메타데이터를 구현하는 방법을 알아봅니다.
description: iOS에서 광고 추적에 표준 광고 메타데이터를 사용하는 방법입니다.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 86%

---

# iOS에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-ios}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | 표준 광고 메타데이터를 `AdInfo ADBMediaObject`에 첨부하기 위한 상수 |

## 표준 광고 메타데이터 구현

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 메타데이터 키](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
