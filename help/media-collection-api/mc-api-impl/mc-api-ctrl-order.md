---
title: 이벤트 순서 제어
description: null
uuid: 007fccc6-be72-4b79-826d-588c957ccf15
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 이벤트 순서 제어{#controlling-the-order-of-events}

Media Collection API는 RESTful이고 비디오 추적은 시간 종속적인 작업이기 때문에 구현자는 순서가 잘못된 시간에 도달하는 Media Collection API 추적 호출에 대해 염려할 수 있습니다. 백 엔드는 *개체에 제공된 타임스탬프를 기반으로 하여 이벤트 대기 및 재정렬을*&#x200B;시도합니다`playerTime`. 그러나 이 기능에는 제한이 있습니다. 현재 순서가 잘못된 호출 사이의 지연 시간이 2초 이상이면 순서 조정이 실패할 수 있습니다. 이 "허용 가능한 지연 시간"은 최적화되거나 이후 업데이트에서 구성할 수 있습니다.
