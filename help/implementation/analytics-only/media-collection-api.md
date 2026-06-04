---
title: 스트리밍 미디어용 Media Collection API 설정
description: Media Collection API를 사용하여 RESTful HTTP 호출로 스트리밍 미디어 데이터를 Adobe Analytics으로 직접 전송합니다.
feature: Streaming Media
role: Developer
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 1%

---

# 스트리밍 미디어용 Media Collection API 설정

Media Collection API는 RESTful HTTP 호출을 사용하여 스트리밍 미디어 데이터를 Adobe Analytics으로 직접 전송합니다. 완전히 사용자 지정할 수 있으므로 SDK에서 다루지 않는 사용자 지정 추적 및 디바이스를 지원합니다. SDK이 플랫폼에 대한 옵션이 아닌 경우 사용합니다.

* **필수 구성 요소**: [Analytics 전용 구현 개요](overview.md)를 완료합니다.

## API 구현

`sessionStart` 요청이 있는 세션을 연 다음 반환된 세션으로 후속 이벤트를 보냅니다. 전체 요청/응답 형식, 매개 변수, 유효성 검사 스키마 및 구현 지침에 대해서는 [Media Collection API 참조](../media-collection-api/mc-api-overview.md)를 참조하십시오.

## 미디어 이벤트 추적

정확한 페이로드는 각 [이벤트](/help/implementation/events/overview.md) 및 [변수](/help/implementation/variables/overview.md) 페이지에서 **Media Collection API** 탭을 참조하십시오.

## 다음 단계

구현이 완료되면 [Analytics 전용 구현에 대한 보고를 설정](/help/reporting/setup/analytics-reporting.md)할 수 있습니다.

>[!MORELIKETHIS]
>
>* [미디어 컬렉션 API 참조](../media-collection-api/mc-api-overview.md)
>* [이벤트 개요](/help/implementation/events/overview.md)
>* [변수 개요](/help/implementation/variables/overview.md)
