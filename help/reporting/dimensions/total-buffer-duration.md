---
title: 총 버퍼 지속 시간(차원)
description: 세션당 버퍼링에 소요된 누적 시간(초)을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# 총 버퍼 지속 시간(차원)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**총 버퍼 지속 시간**&#x200B;차원을 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.bufferTime` 컨텍스트 데이터 변수에서 쌍을 이루는 [총 버퍼 지속 시간(지표)](/help/reporting/metrics/total-buffer-duration.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.bufferTime` 필드를 노출합니다.*

>[!ENDSHADEBOX]

**총 버퍼 지속 시간** 차원은 플레이어가 세션 중 버퍼 상태에서 보낸 누적 시간(초)을 보고합니다. 차원을 사용하여 정확한 버퍼 지속 시간 값으로 참여를 분류합니다.

## 이 차원이 채워지는 방법

미디어 백엔드는 모든 버퍼 간격([버퍼 시작](/help/implementation/events/playback/buffer-start.md)부터 다음 상태 변경까지)의 기간을 합합니다. 이 값은 닫기 호출에 보고됩니다. Analysis Workspace은 값을 `HH:MM:SS`(으)로 표시합니다. 데이터 피드, Data Warehouse 및 보고 API는 값(초)을 표시합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bufferTime`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## 차원 항목

각 항목은 닫기 호출에 대해 보고된 리터럴 기간 값(초)입니다.
