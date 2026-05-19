---
title: iOS에서 표준 광고 메타데이터를 구현하는 방법에 대해 알아보기
description: iOS에서 광고 추적에 표준 광고 메타데이터를 사용하는 방법입니다.
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/a02N5s2UCX1r6eRbaO-8e8djvDA-r9jhWFcELICBY8E
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 65
ht-degree: 93%

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

[iOS 메타데이터 키](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
