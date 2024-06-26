---
title: Android에서 표준 광고 메타데이터를 구현하는 방법에 대해 알아보기
description: Android에서 광고 추적에 표준 광고 메타데이터를 사용하는 방법입니다.
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 100%

---

# Android에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-android}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 광고 `MediaObject`에 표준 광고 메타데이터를 첨부하기 위한 상수. |

## 표준 광고 메타데이터 구현

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
