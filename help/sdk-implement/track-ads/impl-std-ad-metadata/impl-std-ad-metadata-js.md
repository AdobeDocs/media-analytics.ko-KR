---
title: JavaScript에서 표준 광고 메타데이터 구현
description: 브라우저(JS) 앱에서 광고 추적에서 표준 광고 메타데이터를 사용하는 방법
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# JavaScript에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-javascript}

## 광고 상수

| 상수 이름 | 설명   |
|---|---|
| `StandardAdMetadata` | 광고 개체에 표준 광고 메타데이터를 첨부하기 위한 상수 |

## 구현 표준 광고 메타데이터

표준 광고 메타데이터의 경우 플랫폼용 키를 사용하여 표준 광고 메타데이터 키 값 쌍의 사전을 만듭니다.

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

