---
title: 이벤트 순서 제어
description: 이벤트 순서 제어 및 경우에 따라 playerTime 개체에 제공된 타임스탬프를 기반으로 이벤트가 재정렬되는 방법에 대해 알아봅니다.
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/LSKiNN-obuHzVYKbAai52SQ2MvI6-gzgb-G-x0DH2dE
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: 331
ht-degree: 73%

---

# 이벤트 순서 제어{#controlling-the-order-of-events}

스트리밍 비디오 추적은 매우 시간 의존적인 작업이며 때로는 미디어 컬렉션 API 추적 호출이 잘못된 백엔드에 도착합니다. 이 경우, 백 엔드는 `playerTime` 개체에 제공된 타임스탬프를 기반으로 하여 이벤트 대기 및 재정렬을 시도합니다.  이로 인해 일부 제한 사항이 발생합니다. 현재 순서가 잘못된 호출 사이의 지연 시간이 2초 이상이면 순서 조정이 실패할 수 있습니다. 향후 업데이트에서 &#39;허용 가능한 지연 시간&#39;을 최적화하고 구성할 수 있습니다.

## 잘못된 이벤트 예

이벤트가 때때로 지연을 유발하는 네트워크를 통과할 때 잘못된 이벤트가 발생합니다.

예를 들어 `adBreakStart` 이벤트 다음에 `adStart` 이벤트를 보낼 수 있습니다. 광고가 광고 브레이크 내에 시작되기 위해 필요하기 때문에 이는 일반적인 사용 사례입니다.

광고가 준비되었으며 버퍼가 필요하지 않은 경우 두 이벤트가 거의 즉시 발생하고 두 이벤트의 `playerTime.ts`이(가) 서로 매우 가깝습니다. 하지만 정렬 알고리즘이 먼저 발생한 이벤트를 알 수 없기 때문에 이 두 이벤트가 같아서는 안 됩니다. 모든 연속 이벤트에 대해 항상 최소 1밀리초의 타임스탬프 차이를 유지합니다.

네트워크 호출을 시작할 때 두 이벤트가 서로 매우 가까운 시간에 발생하기 때문에 잘못된 순서로 도착할 수 있습니다 이 예에서 `adStart` 이벤트는 `adBreakStart` 이벤트 전에 도착합니다.

5초 또는 최대 10개의 이벤트와 같이 시간이 지정된 이벤트 창이 있습니다. 이벤트는 처리 파이프라인으로 보내기 전에 버퍼링됩니다. 조건이 충족되면(5초가 경과하거나 10개가 넘는 이벤트가 수신됨) 이벤트는 `playerTime.ts`을(를) 기준으로 재정렬된 다음, 새로운 순서로 처리 파이프라인으로 전송됩니다.

>[!IMPORTANT]
>
>처리 파이프라인으로 바로 보내는 예외 이벤트가 있는데, `sessionStart`이벤트입니다.
