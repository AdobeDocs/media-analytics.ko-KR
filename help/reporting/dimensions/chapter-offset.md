---
title: 챕터 오프셋
description: 컨텐츠 내의 각 챕터의 오프셋을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---


# 챕터 오프셋

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**챕터 오프셋**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [챕터 오프셋](/help/implementation/variables/chapters/chapter-offset.md)을 참조하십시오.*

>[!ENDSHADEBOX]

**챕터 오프셋** 차원은 처음부터 초 단위로 측정된 콘텐츠 내의 각 챕터의 오프셋을 보고합니다.

## 이 차원이 채워지는 방법

챕터 오프셋은 플레이어가 [챕터 시작](/help/implementation/events/chapters/chapter-start.md) 이벤트마다 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics(처리 규칙) | `a.media.chapter.offset`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Adobe Analytics(분류) | [챕터](chapter.md) 차원의 분류입니다. 보고서 세트에 대해 **[[!UICONTROL 미디어 챕터]](/help/reporting/setup/analytics-reporting.md)**&#x200B;를 사용하도록 설정하면 Adobe에서 이 분류를 자동으로 만듭니다. 분류 값을 채우고 유지 관리합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| 데이터 피드(처리 규칙) | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.chapter.offset`을(를) 매핑하는 eVar) |
| 데이터 피드(분류) | 해당 사항 없음 — 데이터 피드는 분류를 지원하지 않습니다. |
| Audience Manager | `c_contextdata.a.media.chapter.offset` |

## 분류 접근 방식

보고서 세트에 대해 **[[!UICONTROL 미디어 챕터]](/help/reporting/setup/analytics-reporting.md)**&#x200B;를 사용하도록 설정하면 Adobe에서 자동으로 챕터 오프셋 분류 구조를 만듭니다. [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 분류를 채우고 유지 관리합니다.

이 접근 방법에서는 각 챕터 ID와 해당 오프셋 간에 보장된 1:1 관계를 제공합니다. 분류 업데이트는 해당 ID의 모든 내역 데이터에 소급하여 적용됩니다.

>[!IMPORTANT]
>
>챕터 오프셋 분류 이름을 변경하지 마십시오. 이름을 바꾸면 Adobe에서 원래 분류를 다시 만들어 복제가 발생할 수 있습니다.

## 처리 규칙 접근 방식

`a.media.chapter.offset`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. 이 접근 방법에서는 분류 유지 관리 없이도 챕터 오프셋을 히트당 값으로 캡처합니다.

챕터 오프셋과 상위 [챕터](chapter.md) 차원 간의 보장된 1:1 관계를 잃게 됩니다. 구현에서 이벤트 간에 동일한 챕터 ID에 대해 일관되지 않은 값을 전송하는 경우 동일한 챕터에 여러 오프셋이 나타날 수 있습니다. 값 업데이트는 앞으로 이동하는 데이터에만 적용됩니다.

## 차원 항목

각 항목은 [챕터 시작](/help/implementation/events/chapters/chapter-start.md)에 보고된 정수 오프셋 값(초)입니다.
