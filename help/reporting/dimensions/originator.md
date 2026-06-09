---
title: 작성자
description: 콘텐츠의 작성자 또는 프로덕션 스튜디오를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---


# 작성자

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**작성자**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Originator](/help/implementation/variables/standard-metadata/originator.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**Originator** 차원은 콘텐츠의 작성자 또는 프로덕션 스튜디오를 보고합니다(예: `"Warner Brothers"` 또는 `"Sony"`). 이 패널을 사용하여 콘텐츠 소유자 또는 권한 보유자 간의 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

세션 시작 시 플레이어가 발신자를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics(처리 규칙) | `a.media.originator`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Adobe Analytics(분류) | [콘텐츠(ID)](content.md) 차원의 분류입니다. 보고서 세트에 대해 **[[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)**&#x200B;을(를) 사용하도록 설정하면 Adobe에서 이 분류를 자동으로 만듭니다. 분류 값을 채우고 유지 관리합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드(처리 규칙) | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.originator`을(를) 매핑하는 eVar) |
| 데이터 피드(분류) | 해당 사항 없음 — 데이터 피드는 분류를 지원하지 않습니다. |
| Audience Manager | `c_contextdata.a.media.originator` |

## 분류 접근 방식

보고서 세트에 대해 **[[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)**&#x200B;를 사용하도록 설정하면 Adobe에서 자동으로 작성자 분류 구조를 만듭니다. [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 분류를 채우고 유지 관리합니다.

이 접근 방법에서는 각 콘텐츠 ID와 해당 작성자 간에 보장된 1:1 관계를 제공합니다. 분류 업데이트는 해당 ID의 모든 내역 데이터에 소급하여 적용됩니다.

>[!IMPORTANT]
>
>작성자 분류 이름을 변경하지 마십시오. 이름을 바꾸면 Adobe에서 원래 분류를 다시 만들어 복제가 발생할 수 있습니다.

## 처리 규칙 접근 방식

`a.media.originator`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. 이 접근 방법에서는 분류 유지 관리 없이도 작성자를 히트당 값으로 캡처합니다.

교환은 보낸 사람과 상위 [콘텐츠(ID)](content.md) 차원 간에 보장된 1:1 관계를 잃는 것입니다. 구현에서 이벤트 간에 동일한 콘텐츠 ID에 대해 일관되지 않은 값을 전송하는 경우 동일한 콘텐츠 아래에 여러 작성자가 나타날 수 있습니다. 값 업데이트는 앞으로 이동하는 데이터에만 적용됩니다.

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 작성자 값입니다. 관련이 없는 엔터티 간에 참여가 축소되지 않도록 스튜디오별로 안정적이고 고유한 이름을 사용합니다.
