---
title: 비트율 변경(지표)
description: 세션 간 합계 및 평균에 대한 비트율 변경 이벤트를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%

---


# 비트율 변경(지표)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**비트율 변경**&#x200B;지표를 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.bitrateChangeCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [비트율 변경(차원)](/help/reporting/dimensions/bitrate-changes.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `mediaReporting.qoeDataDetails.bitrateChangeCount` 필드를 노출합니다. 비트 전송률 변경 이벤트를 실행하는 방법은 [비트 전송률 변경](/help/implementation/variables/quality/bitrate-change.md)을 참조하십시오.*

>[!ENDSHADEBOX]

**비트율 변경** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 비트율 변경 이벤트를 계산합니다. 지표를 사용하여 보고서 기간의 비트율 변경 총량을 계산하고 콘텐츠, 네트워크 또는 플레이어 간에 비트율 안정성을 비교할 수 있습니다.

## 이 지표의 계산 방법

미디어 백엔드는 세션 중에 받은 모든 [비트율 변경](/help/implementation/events/playback/bitrate-change.md) 이벤트에 대한 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bitrateChangeCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

세션 수준 부울 보고(세션에서 비트율 변경이 전혀 있었는지 여부)의 경우 [비트율 변경의 영향을 받은 스트림](bitrate-change-impacted-streams.md)을 사용하십시오.
