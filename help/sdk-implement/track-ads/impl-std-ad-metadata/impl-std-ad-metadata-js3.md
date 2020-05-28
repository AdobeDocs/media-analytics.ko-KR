---
title: JavaScript 3.x를 사용하여 표준 광고 메타데이터 구현
description: JavaScript 3.x 앱을 사용하여 브라우저에서 표준 광고 메타데이터를 사용한 방법
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 44%

---


# JavaScript 3.x를 사용하여 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-javascript}

## 표준 광고 메타데이터 구현

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
