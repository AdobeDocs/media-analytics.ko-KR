---
title: 광고 추적
description: Media SDK를 사용하여 광고 추적을 구현하는 개요입니다.
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b3f03848-ae12-48b2-8aab-cad18567eb32id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# 광고 추적

광고 재생 추적에는 광고 브레이크, 광고 시작, 광고 완료 및 광고 건너뛰기가 포함됩니다. 미디어 플레이어의 API를 사용하여 주요 플레이어 이벤트를 식별하고 필수 광고 변수를 채웁니다.

## 플레이어 이벤트

| 플레이어 이벤트 | 액션 |
| --- | --- |
| 광고 브레이크 시작 | 광고 브레이크 개체 만들기, AdBreakStart 호출 |
| 광고 시작 | 광고 개체 만들기, AdStart 호출 |
| 광고 완료 | AdComplete 호출 |
| 광고 건너뛰기 | AdSkip 호출 |
| 광고 브레이크 완료 | AdBreakComplete 호출 |

## 구현 단계

1. 프리롤을 포함하여 광고 브레이크 경계가 시작되는 시점을 식별하고 광고 브레이크 개체를 만듭니다. 필드 정의는 [광고 브레이크 이름](/help/implementation/variables/ads/ad-break-name.md) 및 [광고 브레이크 시작 시간](/help/implementation/variables/ads/ad-break-start-time.md)을 참조하십시오.
1. 광고 브레이크 추적을 시작하려면 [광고 브레이크 시작](/help/implementation/events/ads/ad-break-start.md)을 호출하십시오.
1. 광고가 시작되는 시기를 식별하고, 광고 개체를 만듭니다. 필드 정의는 [광고 이름](/help/implementation/variables/ads/ad-name.md), [광고 ID](/help/implementation/variables/ads/ad-id.md), [광고 길이](/help/implementation/variables/ads/ad-length.md), [Pod 위치의 광고](/help/implementation/variables/ads/ad-in-pod-position.md) 및 [광고 플레이어 이름](/help/implementation/variables/ads/ad-player-name.md)을 참조하십시오.
1. 선택적으로 표준 광고 메타데이터를 첨부합니다. 사용 가능한 키는 [광고주](/help/implementation/variables/ads/advertiser.md), [캠페인 ID](/help/implementation/variables/ads/campaign-id.md), [Creative ID](/help/implementation/variables/ads/creative-id.md), [Creative URL](/help/implementation/variables/ads/creative-url.md), [배치 ID](/help/implementation/variables/ads/placement-id.md) 및 [사이트 ID](/help/implementation/variables/ads/site-id.md)를 참조하십시오.
1. 광고 추적을 시작하려면 [광고 시작](/help/implementation/events/ads/ad-start.md)을(를) 호출하십시오.
1. 광고가 완료될 때까지 재생되면 [광고 완료](/help/implementation/events/ads/ad-complete.md)를 호출합니다.
1. 뷰어가 광고를 건너뛴 경우 광고 완료 대신 [광고 건너뛰기](/help/implementation/events/ads/ad-skip.md)를 호출하십시오.
1. 동일한 광고 브레이크에 있는 추가 광고의 경우 3~7단계를 반복합니다.
1. 광고 브레이크가 완료되면 [광고 브레이크 완료](/help/implementation/events/ads/ad-break-complete.md)를 호출합니다.

>[!IMPORTANT]
>
>**프리롤 광고: `AdBreakStart` 및 `AdStart` 전에 `trackPlay`을(를) 호출하지 마십시오.** 기본 콘텐츠의 첫 번째 `play` ping은 [콘텐츠 시작](/help/reporting/metrics/content-starts.md)을 증가시킵니다. 프리롤 광고 이벤트가 실행되기 전에 `trackPlay`이(가) 호출되고 광고 중에 뷰어가 사라지면 기본 콘텐츠가 재생되지 않았더라도 콘텐츠 시작이 증가합니다. 프리롤 시나리오의 경우 `AdBreakStart` 및 `AdStart`이(가) 전송될 때까지 `trackPlay`을(를) 지연합니다.

>[!NOTE]
>
>광고 재생 중에 보고된 플레이헤드 값은 광고 내부가 아닌 **기본 콘텐츠** 내의 뷰어 위치를 나타냅니다. 10분 비디오 앞에 있는 프리롤 광고의 경우 플레이헤드는 전체 광고에서 `0`입니다. 5분 표시에서 시작하는 미드롤 광고의 경우 플레이헤드는 광고 기간 동안 `300`(초)에 유지됩니다.

## 일반적인 문제

### 광고 사이에 예기치 않은 주:play 호출이 있습니다.

연속 광고 사이에 `main:play`개의 호출이 발생하는 경우 AdComplete 호출과 다음 AdStart 호출 사이에 250밀리초 이상의 간격이 있습니다. 이 간격이 발생하면 Media SDK은 기본 컨텐츠 Ping 전송으로 대체되며, 이는 프리롤 시나리오에 대해 컨텐츠 시작 지표를 조기에 설정할 수 있습니다.

**원인:** Media SDK에 광고 정보가 설정되어 있지 않고 플레이어가 재생 상태이므로 기본 콘텐츠에 간격 기간을 크레딧합니다.

**해결 방법:** 광고가 끝날 때 바로 호출하지 않고 각 광고(마지막 광고 제외)에 대한 AdComplete 호출을 지연시킵니다. 다음과 같이 호출을 배치합니다.

* **광고 시작**&#x200B;마다: 이전 광고가 있고 아직 완료로 표시되지 않은 경우 새 광고에 대해 AdStart를 호출하는 AdComplete *이전*&#x200B;을(를) 호출합니다.
* **광고 자산 끝**&#x200B;마다: AdComplete를 즉시 호출하지 마십시오. 지연합니다.
* **광고 브레이크 완료**: 마지막 광고에 대해 AdComplete를 호출한 후(아직 호출되지 않은 경우) AdBreakComplete를 호출합니다.

이 패턴을 사용하면 AdComplete와 다음 AdStart가 연속해서 실행되므로 간격이 발생하지 않습니다.
