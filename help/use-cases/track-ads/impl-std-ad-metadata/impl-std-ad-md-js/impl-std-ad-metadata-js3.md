---
title: JavaScript 3.x를 사용하여 표준 광고 메타데이터를 구현하는 방법을 알아봅니다
description: JavaScript 3.x 앱을 사용하는 브라우저에서 광고 추적에 표준 광고 메타데이터를 사용하는 방법입니다.
exl-id: ba9abf1d-3778-49ef-a2fc-6c0eafa3b227
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 42%

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
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
