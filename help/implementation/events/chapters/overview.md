---
title: 챕터 및 세그먼트 추적
description: Media SDK를 사용하여 챕터 및 세그먼트 추적을 구현하는 방법입니다.
uuid: 3fe32425-5e2a-4886-8fec-d91d15671bb0
exl-id: d213b633-be3b-4eb8-be71-0ef55e78a570
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PAadkD9nJ7IRf7LdsNzIWtFp0yv54x0xV-Js-ona0Lg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: 191
ht-degree: 39%

---


# 챕터 및 세그먼트 추적

챕터 및 세그먼트 추적은 사용자 지정 미디어 챕터 또는 세그먼트에 사용할 수 있습니다. 일부는 챕터 추적에 사용되며, 야구 이닝과 같은 미디어 콘텐츠를 기반으로 하여 사용자 지정 세그먼트를 정의하거나 광고 브레이크 간의 콘텐츠 세그먼트를 정의합니다. 챕터 추적은 코어 미디어 추적 구현에 필요하지 **않습니다**.

챕터 추적에는 챕터 시작, 챕터 완료, 챕터 건너뛰기가 포함됩니다. 사용자 지정된 세그멘테이션 논리에 미디어 플레이어 API를 사용하여 챕터 이벤트를 식별하고 챕터 변수를 채웁니다.

## 플레이어 이벤트

| 플레이어 이벤트 | 액션 |
| --- | --- |
| 챕터 시작 | 챕터 개체 만들기, ChapterStart 호출 |
| 챕터 완료 | ChapterComplete 호출 |
| 챕터 건너뛰기 | ChapterSkip 호출 |

## 구현 단계

1. 챕터 시작 이벤트가 발생하는 시점을 식별하고 챕터 개체를 작성합니다. 필드 정의는 [챕터 이름](/help/implementation/variables/chapters/chapter-name.md), [챕터 위치](/help/implementation/variables/chapters/chapter-position.md), [챕터 길이](/help/implementation/variables/chapters/chapter-length.md) 및 [챕터 오프셋](/help/implementation/variables/chapters/chapter-offset.md)을 참조하십시오.
1. 필요한 경우 사용자 지정 챕터 메타데이터에 대한 컨텍스트 데이터 변수를 만듭니다.
1. 챕터 추적을 시작하려면 [챕터 시작](/help/implementation/events/chapters/chapter-start.md)을 호출합니다.
1. 재생이 챕터 종료 경계에 도달하면 [챕터 완료](/help/implementation/events/chapters/chapter-complete.md)를 호출합니다.
1. 사용자가 완료하기 전에 챕터를 건너뛸 경우 [챕터 건너뛰기](/help/implementation/events/chapters/chapter-skip.md)를 호출합니다.
1. 추가 챕터의 경우 1~5단계를 반복합니다.
