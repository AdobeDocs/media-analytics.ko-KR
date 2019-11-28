---
title: Roku에서 표준 광고 메타데이터 구현
description: Roku에서 광고 추적에 표준 광고 메타데이터를 사용하는 방법입니다.
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Roku에서 표준 광고 메타데이터 구현{#implement-standard-ad-metadata-on-roku}

## 표준 광고 메타데이터 구현

표준 광고 메타데이터의 경우, 플랫폼에 대한 키를 사용하여 표준 광고 메타데이터 키 값 쌍 사전을 만드십시오.

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

