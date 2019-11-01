---
title: JSON 유효성 검사 스키마
description: null
uuid: 7c9d5ce4-f5d2-4129-900e-4d02800907d1
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# JSON 유효성 검사 스키마{#json-validation-schemas}

미디어 분석 백엔드는 JSON 유효성 검사 스키마를 사용하여 각 이벤트 유형에 대한 요청 매개 변수를 검증합니다. 이러한 스키마는 사용자가 사용할 수 있으며 MA API에 사용되는 매개 변수 유형에 대한 현재 권한 역할을 합니다.

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](/help/media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
