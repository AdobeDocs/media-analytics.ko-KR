---
title: Pod 이름
description: 각 광고 브레이크의 친숙한 이름을 보고합니다. 분류 또는 사용자 지정 처리 규칙을 사용하여 Adobe Analytics에서 수집합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Pod 이름

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**Pod 이름**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [광고 브레이크 이름](/help/implementation/variables/ads/ad-break-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

**Pod name** 차원은 각 광고 브레이크의 알기 쉬운 이름을 보고합니다(예: `"pre-roll"`, `"mid-roll-1"`). Customer Journey Analytics에서 이 차원은 구현 변수에서 직접 채워지는 개별 차원입니다. Adobe Analytics에서는 [광고 pod](ad-pod.md) 차원의 분류나 처리 규칙을 사용하여 채워진 eVar의 두 가지 접근 방식을 통해 사용할 수 있습니다.

## 이 차원이 채워지는 방법

Pod 이름은 플레이어가 [광고 브레이크 시작](/help/implementation/events/ads/ad-break-start.md)에 설정한 [광고 브레이크 이름](/help/implementation/variables/ads/ad-break-name.md) 값에서 가져온 것입니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics(처리 규칙) | `a.media.ad.podFriendlyName`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Adobe Analytics(분류) | 광고 Pod 차원의 분류 — 보고서 세트에 대해 **[[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)**&#x200B;가 활성화되면 Adobe에서 자동으로 이 분류를 만듭니다. 분류 값을 채우고 유지 관리합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| 데이터 피드(처리 규칙) | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.ad.podFriendlyName`을(를) 매핑하는 eVar) |
| 데이터 피드(분류) | 해당 사항 없음 — 데이터 피드는 분류를 지원하지 않습니다. |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## 분류 접근 방식

보고서 세트에 대해 **[[!UICONTROL 미디어 광고]](/help/reporting/media-reports-enable.md)**&#x200B;를 사용하도록 설정하면 Adobe에서 Pod 이름 분류 구조를 자동으로 만듭니다. [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 분류를 채우고 유지 관리합니다.

이 접근 방식은 각 pod ID와 알기 쉬운 이름 간에 보장된 1:1 관계를 제공합니다. 분류 업데이트는 해당 ID의 모든 내역 데이터에 소급하여 적용됩니다.

>[!IMPORTANT]
>
>Pod 이름 분류 이름을 변경하지 마십시오. 이름을 바꾸면 Adobe에서 원래 분류를 다시 만들어 복제가 발생할 수 있습니다.

## 처리 규칙 접근 방식

`a.media.ad.podFriendlyName`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. 이 접근 방법에서는 분류 유지 관리 없이도 친숙한 이름을 히트당 값으로 캡처합니다.

Pod 이름과 상위 [광고 pod](ad-pod.md) 차원 간에 보장된 1:1 관계를 잃게 됩니다. 구현에서 이벤트 간에 동일한 pod ID에 대해 일관되지 않은 값을 전송하는 경우 동일한 광고 pod 아래에 여러 이름이 표시될 수 있습니다. 값 업데이트는 앞으로 이동하는 데이터에만 적용됩니다.

## 차원 항목

각 항목은 [광고 브레이크 시작](/help/implementation/events/ads/ad-break-start.md)에 보고된 리터럴 광고 브레이크 이름입니다.
