---
description: 'null'
seo-description: 'null'
seo-title: Roku에서 표준 광고 메타데이터 구현
title: Roku에서 표준 광고 메타데이터 구현
uuid: 20 A 437 D 7-18 B 8-4099-AC 81-9 F 3628384236
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Roku에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-roku}

## 구현 표준 광고 메타데이터

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍의 사전을 만듭니다.

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

