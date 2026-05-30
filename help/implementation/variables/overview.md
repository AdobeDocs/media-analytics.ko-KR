---
title: 스트리밍 미디어 변수 개요
description: 스트리밍 미디어 변수를 구성하는 방법과 Adobe Analytics 및 Customer Journey Analytics 간에 매핑하는 방법을 알아봅니다.
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 3dbbd5228fcd91cf78c0597dea656c06f367dd40
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 2%

---


# 스트리밍 미디어 변수 개요

변수는 컨텐츠 이름, 스트림 유형, 광고 이름 및 재생 품질과 같이 미디어 플레이어에서 스트림에 대해 제공하는 데이터입니다. 대부분의 변수는 세션 시작 시 설정되고 미디어 백엔드에서 세션 닫기로 전달되며, 미디어 백엔드는 이 변수를 사용하여 보고에 사용하는 차원 및 지표를 채웁니다. 각 변수 페이지는 지원되는 모든 구현 방법에 대해 해당 변수를 설정하는 방법을 설명합니다.

## 변수를 Adobe에 보내는 방법

단일 변수는 모든 Adobe 애플리케이션이나 서비스에 동일한 값을 전달하지만, 해당 값의 형식은 보내는 위치에 따라 다릅니다. 다음 표에는 각 응용 프로그램 또는 서비스와 예상되는 변수 형식이 나열되어 있습니다. 각 변수 페이지의 속성 테이블에는 모든 형식에서 사용할 정확한 값이 표시됩니다.

| 데이터 형식 | 설명 |
| --- | --- |
| 컨텍스트 데이터 변수 | `a.media` 접두사로 이름이 지정된 Adobe Analytics으로 보낸 형식(예: `a.media.name`). |
| XDM 컬렉션 필드 | XDM 필드 패스(예: `xdm.mediaCollection.sessionDetails.name`)로 표현되는 Customer Journey Analytics으로 전송된 형식입니다. |
| Audience Manager 트레이트 | Audience Manager에 전달된 형식이며 접두사가 `c_contextdata`(예: `c_contextdata.a.media.name`)입니다. |

>[!MORELIKETHIS]
>
>* [이벤트 개요](/help/implementation/events/overview.md): 변수를 전달하는 플레이어 이벤트
>* [차원 개요](/help/reporting/dimensions/overview.md): 변수가 채우는 보고 차원
>* [지표 개요](/help/reporting/metrics/overview.md): 변수가 채우는 보고 지표입니다
