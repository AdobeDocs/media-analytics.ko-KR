---
title: 최초 디지털 날짜
description: 콘텐츠가 디지털 플랫폼에 처음 나타난 날짜를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# 최초 디지털 날짜

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**첫 번째 디지털 날짜**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [첫 번째 디지털 날짜](/help/implementation/variables/standard-metadata/first-digital-date.md)를 참조하세요.*

>[!ENDSHADEBOX]

**첫 번째 디지털 날짜** 차원은 콘텐츠가 디지털 플랫폼에 처음 나타난 날짜를 보고합니다. [첫 방송 날짜](first-air-date.md)와 함께 사용하여 디지털 릴리스 시기를 원본 브로드캐스트와 비교합니다.

## 이 차원이 채워지는 방법

첫 번째 디지털 날짜는 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics(처리 규칙) | `a.media.digitalDate`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Adobe Analytics(분류) | [컨텐츠(ID)](content.md) 차원의 분류 — 보고서 세트에 대해 **[[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)**&#x200B;를 활성화하면 Adobe에서 이 분류를 자동으로 만듭니다. 분류 값을 채우고 유지 관리합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드(처리 규칙) | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.digitalDate`을(를) 매핑하는 eVar) |
| 데이터 피드(분류) | 해당 사항 없음 — 데이터 피드는 분류를 지원하지 않습니다. |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## 분류 접근 방식

Adobe은 보고서 세트에 대해 **[[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)**&#x200B;을(를) 사용하도록 설정하면 첫 번째 디지털 날짜 분류 구조를 자동으로 만듭니다. [분류 세트](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)를 사용하여 분류를 채우고 유지 관리합니다.

이 접근 방법에서는 각 콘텐츠 ID와 첫 번째 디지털 날짜 간에 보장된 1:1 관계를 제공합니다. 분류 업데이트는 해당 ID의 모든 내역 데이터에 소급하여 적용됩니다.

>[!IMPORTANT]
>
>첫 번째 디지털 날짜 분류 이름을 변경하지 마십시오. 이름을 바꾸면 Adobe에서 원래 분류를 다시 만들어 복제가 발생할 수 있습니다.

## 처리 규칙 접근 방식

`a.media.digitalDate`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. 이 접근 방법에서는 분류 유지 관리 없이도 첫 번째 디지털 날짜를 히트당 값으로 캡처합니다.

첫 번째 디지털 날짜와 상위 [콘텐츠(ID)](content.md) 차원 간에 보장된 1:1 관계가 손실되는 것이 단점입니다. 구현에서 이벤트 간에 동일한 콘텐츠 ID에 대해 일관되지 않은 값을 전송하는 경우 동일한 콘텐츠 아래에 여러 개의 첫 번째 디지털 날짜가 표시될 수 있습니다. 값 업데이트는 앞으로 이동하는 데이터에만 적용됩니다.

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 날짜 문자열입니다. 구현 전반에 걸쳐 일관된 형식을 사용합니다. Adobe에서는 `YYYY-MM-DD`을(를) 권장합니다.
