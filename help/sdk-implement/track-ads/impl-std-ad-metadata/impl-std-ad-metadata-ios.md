---
description: 'null'
seo-description: 'null'
seo-title: iOS에서 표준 광고 메타데이터 구현
title: iOS에서 표준 광고 메타데이터 구현
uuid: F 15 FB 727-5 A 5 B -46 C 5-BF 12-93 B 376 C 10 FD 1
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# iOS에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-ios}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## 구현 표준 광고 메타데이터

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍의 사전을 만듭니다.

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 메타데이터 키](../../../sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
