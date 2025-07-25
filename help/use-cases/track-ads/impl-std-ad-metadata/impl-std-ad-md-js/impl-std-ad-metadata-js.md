---
title: JavaScript 2.x를 사용하여 표준 광고 메타데이터를 구현하는 방법에 대해 알아보기
description: JavaScript 2.x 앱을 사용하여 브라우저에서 광고 추적에 표준 광고 메타데이터를 사용하는 방법입니다.
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 100%

---

# JavaScript 2.x를 사용하여 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-javascript}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `StandardAdMetadata` | 광고 개체에 표준 광고 메타데이터를 첨부하기 위한 상수 |

## 표준 광고 메타데이터 구현

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
