---
title: 세그먼트
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 세그먼트{#segments}

>[!NOTE]
>
>These reporting segments associated with Media Stream Type were introduced on 9/13/18 along with the `streamType` parameter.

| 세그먼트 | 설명 | 규칙 |
|---|---|---|
| 미디어 스트림 유형: 모두 | 모든 *미디어* 스트림 데이터를 세그먼트화합니다. | "컨텐츠(ID)가 존재함" |
| 미디어 스트림 유형: 오디오 | 모든 *오디오* 스트림 데이터를 세그먼트화합니다. | "컨텐츠(ID)가 존재함" AND "미디어 스트림 유형 = `audio`" |
| 미디어 스트림 유형: 비디오 | 모든 *비디오* 스트림 데이터를 세그먼트화합니다. | "컨텐츠(ID)가 존재함" AND "미디어 스트림 유형 != `audio`" |
| 미디어 컨텐츠 유형: VoD | 모든 VoD 컨텐츠를 세그먼트화합니다. | "컨텐츠 유형 = `vod`" |
| 미디어 컨텐츠 유형: 라이브 | 모든 라이브 컨텐츠를 세그먼트화합니다. | "컨텐츠 유형 = `live`" |
| 미디어 컨텐츠 유형: 선형 | 모든 선형 컨텐츠를 세그먼트화합니다. | "컨텐츠 유형 = `linear`" |
| 미디어 컨텐츠 유형: 팟캐스트 | 모든 팟캐스트 컨텐츠를 세그먼트화합니다. | "컨텐츠 유형 = `podcast`" |
| 미디어 컨텐츠 유형: 오디오북 | 모든 오디오북 컨텐츠를 세그먼트화합니다. | "컨텐츠 유형 = `audiobook`" |
| 미디어 컨텐츠 유형: AoD | 모든 AoD 컨텐츠를 세그먼트화합니다. | "컨텐츠 유형 = `aod`" |

