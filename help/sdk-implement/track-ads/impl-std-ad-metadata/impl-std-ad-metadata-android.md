---
title: Android에서 표준 광고 메타데이터 구현
description: Android에서 광고 추적에서 표준 광고 메타데이터를 사용하는 방법
uuid: 19b98bc1-c659-418 파섹
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Android에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-android}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 광고 `MediaObject`에 표준 광고 메타데이터를 첨부하기 위한 상수. |

## 구현 표준 광고 메타데이터

표준 광고 메타데이터의 경우 플랫폼용 키를 사용하여 표준 광고 메타데이터 키 값 쌍의 사전을 만듭니다.

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

