---
title: Roku에서 표준 메타데이터를 구현하는 방법을 알아봅니다.
description: Roku에서 추적 호출을 사용하여 전송할 표준 비디오 및 광고 메타데이터를 설정하는 방법을 알아봅니다.
uuid: ae14d809-343f-452c-832a-f94bd3d83a90
exl-id: 1552b16a-3c2d-4caa-b571-e6628f0b6866
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 61%

---

# Roku에서 표준 메타데이터 구현{#implement-standard-metadata-on-roku}

표준 메타데이터 개체를 인스턴스화하고, 원하는 변수를 채우고, 미디어 하트비트 개체에서 메타데이터 개체를 설정합니다.

**비디오:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySHOW] = "sample show" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeySEASON] = "sample season" 
standardMetadata[ADBMobile().MEDIA_VideoMetadataKeyEPISODE] = "sample episode" 

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

**오디오:**

```
standardMetadata = {} 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyARTIST] = "sample artist" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyALBUM] = "sample album" 
standardMetadata[ADBMobile().MEDIA_AudioMetadataKeyLABEL] = "sample label"

mediaInfo[ADBMobile().MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata 
```

[오디오 및 비디오 매개 변수](/help/metrics-and-metadata/audio-video-parameters.md)에서 비디오 메타데이터에 대한 종합 목록을 참조하십시오.
