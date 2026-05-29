---
title: 콘텐츠 등급
description: TV 유해 컨텐츠 가이드라인 또는 지역 등급 시스템으로 정의된 대상 등급을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---


# 콘텐츠 등급

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**콘텐츠 등급**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 등급](/help/implementation/variables/standard-metadata/content-rating.md)을 참조하세요.*

>[!ENDSHADEBOX]

**콘텐츠 등급** 차원은 각 세션에 대한 대상 등급을 보고합니다. 등급 계층 간 참여 및 광고 로드를 비교하는 데 사용합니다.

## 이 차원이 채워지는 방법

콘텐츠 등급은 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics(처리 규칙) | `a.media.rating`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Adobe Analytics(분류) | [컨텐츠(ID)](content.md) 차원의 분류 — 보고서 세트에 대해 **[[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)**&#x200B;를 활성화하면 Adobe에서 이 분류를 자동으로 만듭니다. 분류 값을 채우고 유지 관리합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드(처리 규칙) | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.rating`을(를) 매핑하는 eVar) |
| 데이터 피드(분류) | 해당 사항 없음 — 데이터 피드는 분류를 지원하지 않습니다. |
| Audience Manager | `c_contextdata.a.media.rating` |

## 분류 접근 방식

보고서 세트에 대해 **[[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)**&#x200B;를 사용하도록 설정하면 Adobe에서 자동으로 콘텐츠 등급 분류 구조를 만듭니다. [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 분류를 채우고 유지 관리합니다.

이 접근 방법에서는 각 콘텐츠 ID와 해당 등급 간에 보장된 1:1 관계를 제공합니다. 분류 업데이트는 해당 ID의 모든 내역 데이터에 소급하여 적용됩니다.

>[!IMPORTANT]
>
>콘텐츠 등급 분류 이름을 변경하지 마십시오. 이름을 바꾸면 Adobe에서 원래 분류를 다시 만들어 복제가 발생할 수 있습니다.

## 처리 규칙 접근 방식

`a.media.rating`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. 이 접근 방법에서는 분류 유지 관리 없이도 컨텐츠 등급을 히트당 값으로 캡처합니다.

콘텐츠 등급과 상위 [콘텐츠(ID)](content.md) 차원 간에 보장된 1:1 관계가 손실되면 절충됩니다. 구현에서 이벤트 간에 동일한 콘텐츠 ID에 대해 일관되지 않은 값을 전송하는 경우 동일한 콘텐츠 아래에 여러 등급이 표시될 수 있습니다. 값 업데이트는 앞으로 이동하는 데이터에만 적용됩니다.

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 등급 값입니다(예: `"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`). 라인 항목이 조각화되지 않도록 하려면 등급 시스템당 고정된 값 세트를 유지하십시오.
