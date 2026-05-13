---
title: 시작 시간(지표)
description: 세션 간 합계 및 평균의 시작 시간을 보고합니다.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# 시작 시간(지표)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**시작 시간**&#x200B;지표를 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.timeToStart` 컨텍스트 데이터 변수에서 쌍을 이루는 [시작 시간(차원)](/help/reporting/dimensions/time-to-start.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `mediaReporting.qoeDataDetails.timeToStart` 필드를 노출합니다. 이 변수를 수집하는 방법은 [시작 시간](/help/implementation/variables/quality/time-to-start.md)을 참조하세요.*

>[!ENDSHADEBOX]

**시작 시간** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 시작 시간을 보고합니다. 지표를 사용하여 보고서 기간 동안의 평균 시작 시간을 계산하고 콘텐츠, 네트워크 또는 플레이어 간의 시작 성능을 비교할 수 있습니다. Adobe은 값을 초 단위로 저장하고 플레이어가 보고하는 밀리초부터 수집 시 전환합니다.

## 이 지표의 계산 방법

세션이 시작되기 전에 플레이어가 QoE 개체에 `timeToStart`을(를) 설정합니다. 백엔드가 닫기 호출에 대한 값을 보고합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.timeToStart`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
