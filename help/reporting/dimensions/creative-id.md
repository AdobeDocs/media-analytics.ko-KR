---
title: 광고 ID
description: 광고 크리에이티브 식별자를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 3%

---


# 광고 ID

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**Creative ID**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Creative ID](/help/implementation/variables/ads/creative-id.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**Creative ID** 차원은 광고 크리에이티브 식별자를 보고합니다. 차원을 사용하여 크리에이티브를 공유하는 광고 간에 참여를 롤업할 수 있습니다.

## 이 차원이 채워지는 방법

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics(처리 규칙) | `a.media.ad.creative`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Adobe Analytics(분류) | [광고](ad.md) 차원의 분류 — 보고서 세트에 대해 **[[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)**&#x200B;가 활성화되면 Adobe에서 이 분류를 자동으로 만듭니다. 분류 값을 채우고 유지 관리합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 데이터 피드(처리 규칙) | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.ad.creative`을(를) 매핑하는 eVar) |
| 데이터 피드(분류) | 해당 사항 없음 — 데이터 피드는 분류를 지원하지 않습니다. |
| Audience Manager | `c_contextdata.a.media.ad.creative` |

## 분류 접근 방식

보고서 세트에 대해 **[[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)**&#x200B;를 사용하도록 설정하면 Adobe에서 Creative ID 분류 구조를 자동으로 만듭니다. [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 분류를 채우고 유지 관리합니다.

이 접근 방법에서는 각 광고 ID와 광고 ID 간의 1:1 관계를 보장합니다. 분류 업데이트는 해당 ID의 모든 내역 데이터에 소급하여 적용됩니다.

>[!IMPORTANT]
>
>Creative ID 분류 이름을 변경하지 마십시오. 이름을 바꾸면 Adobe에서 원래 분류를 다시 만들어 복제가 발생할 수 있습니다.

## 처리 규칙 접근 방식

`a.media.ad.creative`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. 이 접근 방법에서는 분류 유지 관리 없이도 크리에이티브 ID를 히트당 값으로 캡처합니다.

광고 ID와 상위 [Ad](ad.md) 차원 간에 보장된 1:1 관계가 손실되는 것이 단점입니다. 구현에서 이벤트 간에 동일한 광고 ID에 대해 일관되지 않은 값을 전송하는 경우 동일한 광고에 여러 광고 ID가 표시될 수 있습니다. 값 업데이트는 앞으로 이동하는 데이터에만 적용됩니다.

## 차원 항목

각 항목은 고유한 크리에이티브 ID입니다. 캠페인에서 동일한 크리에이티브가 단일 라인 항목으로 롤업되도록 크리에이티브당 안정적인 식별자를 사용합니다.
