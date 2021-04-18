---
title: 이벤트 순서 제어
description: 이벤트 순서 제어
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
exl-id: c0cac319-2bea-42c8-8674-641dfbb44fa2
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 100%

---

# 이벤트 순서 제어{#controlling-the-order-of-events}

Media Collection API는 RESTful이고 비디오 추적이 시간 종속적 작업이므로, 구현자가 잘못된 순서로 백 엔드에 도달하는 Media Collection API 추적 호출에 대해 염려할 수 있습니다. 백 엔드는 *개체에 제공된 타임스탬프를 기반으로 하여 이벤트 대기 및 재정렬을*&#x200B;시도합니다`playerTime`. 그러나 이 기능에는 제한이 있습니다. 현재 순서가 잘못된 호출 사이의 지연 시간이 2초 이상이면 순서 조정이 실패할 수 있습니다. 이 &quot;허용 가능한 지연 시간&quot;은 최적화되거나 이후 업데이트에서 구성할 수 있습니다.
