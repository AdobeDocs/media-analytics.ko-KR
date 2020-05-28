---
title: JavaScript 2.x를 사용하여 표준 광고 메타데이터 구현
description: JavaScript 2.x 앱을 사용하여 브라우저에서 표준 광고 메타데이터를 사용한 방법
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

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
