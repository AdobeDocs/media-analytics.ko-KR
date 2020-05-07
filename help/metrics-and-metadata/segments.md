---
title: 세그먼트
description: null
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 세그먼트{#segments}

>[!NOTE]
>
>미디어 스트림 유형과 연관된 이 보고 세그먼트는 `streamType` 매개 변수와 함께 18/9/13에 도입되었습니다.

| 세그먼트 | 설명 | 규칙 |
|---|---|---|
| 미디어 스트림 유형: 모두 | 모든 *미디어* 스트림 데이터를 세그먼트화합니다. | &quot;컨텐츠(ID)가 존재함&quot; |
| 미디어 스트림 유형: 오디오 | 모든 *오디오* 스트림 데이터를 세그먼트화합니다. | &quot;컨텐츠(ID)가 존재함&quot; AND &quot;미디어 스트림 유형 = `audio`&quot; |
| 미디어 스트림 유형: 비디오 | 모든 *비디오* 스트림 데이터를 세그먼트화합니다. | &quot;컨텐츠(ID)가 존재함&quot; AND &quot;미디어 스트림 유형 != `audio`&quot; |
| 미디어 컨텐츠 유형: VoD | 모든 VoD 컨텐츠를 세그먼트화합니다. | &quot;컨텐츠 유형 = `vod`&quot; |
| 미디어 컨텐츠 유형: 라이브 | 모든 라이브 컨텐츠를 세그먼트화합니다. | &quot;컨텐츠 유형 = `live`&quot; |
| 미디어 컨텐츠 유형: 선형 | 모든 선형 컨텐츠를 세그먼트화합니다. | &quot;컨텐츠 유형 = `linear`&quot; |
| 미디어 컨텐츠 유형: 팟캐스트 | 모든 팟캐스트 컨텐츠를 세그먼트화합니다. | &quot;컨텐츠 유형 = `podcast`&quot; |
| 미디어 컨텐츠 유형: 오디오북 | 모든 오디오북 컨텐츠를 세그먼트화합니다. | &quot;컨텐츠 유형 = `audiobook`&quot; |
| 미디어 컨텐츠 유형: AoD | 모든 AoD 컨텐츠를 세그먼트화합니다. | &quot;컨텐츠 유형 = `aod`&quot; |

