---
description: 'null'
seo-description: 'null'
seo-title: Roku에서 표준 메타데이터 구현
title: Roku에서 표준 메타데이터 구현
uuid: AE 14 D 809-343 F -452 C -832 A-F 94 BD 3 D 83 A 90
translation-type: tm+mt
source-git-commit: c6c7afee72d21c832be77c723750ae0551793613

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

[오디오 및 비디오 매개 변수](../../../metrics-and-metadata/audio-video-parameters.md)에서 비디오 메타데이터에 대한 종합 목록을 참조하십시오.

