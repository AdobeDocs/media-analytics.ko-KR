---
seo-title: JSON 유효성 검사 스키마
title: JSON 유효성 검사 스키마
uuid: 7 C 9 D 5 CE 4-F 5 D 2-4129-900 E -4 D 02800907 D 1
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# JSON 유효성 검사 스키마{#json-validation-schemas}

미디어 분석 백엔드는 JSON 유효성 검사 스키마를 사용하여 각 이벤트 유형에 대한 요청 매개 변수를 검증합니다. 이러한 스키마는 사용자가 사용할 수 있으며, MA API에서 사용되는 매개 변수 유형에 대한 현재 권한으로 사용됩니다.

```
POST
https://{uri}/api/v1/schemas/{event-type}
```

For more information about using the JSON validation schemas, see [Validating event requests.](../../media-collection-api/mc-api-impl/mc-api-validate-reqs.md)
