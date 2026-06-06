---
title: 미디어 스트림 세그먼트 설명
description: 미디어 스트림 유형에 대한 세그먼트, 설명 및 규칙을 포함하여 미디어 스트림 유형과 연관된 보고 세그먼트에 대해 알아봅니다.
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: cb3770abd06eb8debe4ff92641835f04f62471f7
workflow-type: tm+mt
source-wordcount: 189
ht-degree: 75%

---

# Streaming Media 세그먼트

세그먼트를 사용하여 특성 또는 웹 사이트 상호 작용에 따라 방문자 하위 집합을 식별할 수 있습니다. 스트림 미디어 세그먼트를 사용하면 오디오, 라이브 또는 팟캐스트 스트림과 같은 방문자 스트림 유형을 식별할 수 있습니다. Adobe Analytics 세그먼트에 대한 자세한 내용은 Adobe Analytics 구성 요소 안내서에서 [세그먼트 정보](https://experienceleague.adobe.com/en/docs/analytics/components/segmentation/seg-overview)를 참조하십시오.

| 세그먼트 | 설명 | 규칙 |
|---|---|---|
| 미디어 스트림 유형: 모두 | 모든 *미디어* 스트림 데이터를 세그먼트화합니다. | &quot;콘텐츠(ID)가 존재함&quot; |
| 미디어 스트림 유형: 오디오 | 모든 *오디오* 스트림 데이터를 세그먼트화합니다. | &quot;콘텐츠(ID)가 존재함&quot; AND &quot;미디어 스트림 유형 = `audio`&quot; |
| 미디어 스트림 유형: 비디오 | 모든 *비디오* 스트림 데이터를 세그먼트화합니다. | &quot;콘텐츠(ID)가 존재함&quot; AND &quot;미디어 스트림 유형 != `audio`&quot; |
| 미디어 콘텐츠 유형: VoD | 모든 VoD 콘텐츠를 세그먼트화합니다. | &quot;콘텐츠 유형 = `vod`&quot; |
| 미디어 콘텐츠 유형: 라이브 | 모든 라이브 콘텐츠를 세그먼트화합니다. | &quot;콘텐츠 유형 = `live`&quot; |
| 미디어 콘텐츠 유형: 선형 | 모든 선형 콘텐츠를 세그먼트화합니다. | &quot;콘텐츠 유형 = `linear`&quot; |
| 미디어 콘텐츠 유형: 팟캐스트 | 모든 팟캐스트 콘텐츠를 세그먼트화합니다. | &quot;콘텐츠 유형 = `podcast`&quot; |
| 미디어 콘텐츠 유형: 오디오북 | 모든 오디오북 콘텐츠를 세그먼트화합니다. | &quot;콘텐츠 유형 = `audiobook`&quot; |
| 미디어 콘텐츠 유형: AoD | 모든 AoD 콘텐츠를 세그먼트화합니다. | &quot;콘텐츠 유형 = `aod`&quot; |
