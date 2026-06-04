---
title: 비트율 변경(차원)
description: 세션당 비트율 변경 이벤트 수를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 5%

---


# 비트율 변경(차원)

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**비트율 변경**&#x200B;차원을 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.bitrateChangeCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [비트율 변경(지표)](/help/reporting/metrics/bitrate-changes.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` 필드를 노출합니다. 비트 전송률 변경 이벤트를 실행하는 방법은 [비트 전송률 변경](/help/implementation/variables/quality/bitrate-change.md)을 참조하십시오.*

>[!ENDSHADEBOX]

**비트율 변경** 차원은 세션 중에 발생한 비트율 변경 이벤트의 수를 보고합니다. 차원을 사용하여 정확한 변경 수 값(예: &quot;비트율 변경이 3개인 세션과 0개인 세션&quot;)으로 참여와 품질을 분석합니다.

## 이 차원이 채워지는 방법

미디어 백엔드는 세션 중에 받은 모든 [비트율 변경](/help/implementation/events/playback/bitrate-change.md) 이벤트에 대한 카운트를 증가시킵니다. 이 값은 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bitrateChangeCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoebitratechangecountevar`, `post_videoqoebitratechangecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

## 차원 항목

각 항목은 닫기 호출에서 보고된 리터럴 변경-수 값입니다. 세션 수준 부울 보고(세션에서 비트율 변경이 전혀 있었는지 여부)의 경우 [비트율 변경의 영향을 받은 스트림](/help/reporting/metrics/bitrate-change-impacted-streams.md)을 사용하십시오.
