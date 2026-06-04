---
title: 버퍼 이벤트(지표)
description: 세션 간 합계 및 평균에 대한 버퍼링 이벤트를 계산합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 7%

---


# 버퍼 이벤트(지표)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**버퍼 이벤트**&#x200B;지표를 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.bufferCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [버퍼 이벤트(차원)](/help/reporting/dimensions/buffer-events.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.bufferCount` 필드를 노출합니다.*

>[!ENDSHADEBOX]

**버퍼 이벤트** 지표는 합계, 평균 및 백분위수 롤업에 적합한 세션 간 버퍼링 이벤트를 계산합니다. 지표를 사용하여 보고서 기간 동안의 총 버퍼 볼륨을 계산하고 콘텐츠, 네트워크 또는 플레이어 간의 버퍼 안정성을 비교합니다.

## 이 지표의 계산 방법

미디어 백엔드는 플레이어가 [버퍼 시작](/help/implementation/events/playback/buffer-start.md) 상태에 들어갈 때마다 카운트를 증가시킵니다. 지표는 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bufferCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

세션 수준 부울 보고(세션이 버퍼링을 전혀 경험했는지 여부)의 경우 [버퍼 영향을 받은 스트림](buffer-impacted-streams.md)을 사용하십시오.
