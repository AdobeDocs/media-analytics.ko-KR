---
title: iOS에서 표준 메타데이터를 구현하는 방법에 대해 알아보기
description: iOS에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법에 대해 알아봅니다.
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
exl-id: e0981346-3d3c-4a0c-82a4-19942634fd03
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/Gs0IwHZBqv30zfdJ6rdnacIu-1RoDRD9wRaQjK0Q45c
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 100
ht-degree: 89%

---

# iOS에서 표준 메타데이터 구현{#implement-standard-metadata-on-ios}

## 메타데이터 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | 표준 메타데이터를 `MediaInfo ADBMediaObject`에 첨부하기 위한 상수입니다. |

## 구현

1. 표준 메타데이터 키 값 쌍 사전을 를 사용하여 만듭니다. `ADBStandardMetadataKeys`
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
