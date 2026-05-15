---
title: 오류 이벤트
description: 세션 간 합계 및 평균에 대한 오류 이벤트를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 8%

---


# 오류 이벤트

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**오류 이벤트**지표를 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.errorCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [오류 차원](/help/reporting/dimensions/errors.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `mediaReporting.qoeDataDetails.errorCount` 필드를 노출합니다.*

>[!ENDSHADEBOX]

**오류 이벤트** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 오류 이벤트를 계산합니다. 지표를 사용하여 보고서 기간의 총 오류 볼륨을 계산하고 콘텐츠, 네트워크 또는 플레이어 간의 오류율을 비교할 수 있습니다.

## 이 지표의 계산 방법

미디어 백엔드는 플레이어가 보고한 모든 오류에 대한 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.errorCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

세션 수준 부울 보고(오류가 전혀 발생했는지 여부)의 경우 [오류 영향을 받은 스트림](error-impacted-streams.md)을 사용하십시오.
