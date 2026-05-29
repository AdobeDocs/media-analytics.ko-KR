---
title: 버퍼 이벤트(차원)
description: 세션당 버퍼링 이벤트 수를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 6%

---


# 버퍼 이벤트(차원)

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**버퍼 이벤트**&#x200B;차원을 다룹니다. Adobe Analytics은 동일한 `a.media.qoe.bufferCount` 컨텍스트 데이터 변수에서 쌍을 이루는 [버퍼 이벤트(지표)](/help/reporting/metrics/buffer-events.md)을 자동으로 채웁니다. Customer Journey Analytics은 차원 또는 지표로 사용할 수 있는 단일 `xdm.mediaReporting.qoeDataDetails.bufferCount` 필드를 노출합니다.*

>[!ENDSHADEBOX]

**버퍼 이벤트** 차원은 세션 중에 발생한 버퍼링 이벤트 수를 보고합니다. 차원을 사용하여 정확한 버퍼 수로 참여를 분류합니다.

## 이 차원이 채워지는 방법

미디어 백엔드는 플레이어가 `buffer` 상태에 들어갈 때마다 카운트를 증가시킵니다. 이 값은 닫기 호출에 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 품질]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.qoe.bufferCount`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 데이터 피드 | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## 차원 항목

각 항목은 닫기 호출에서 보고된 리터럴 버퍼 수 값입니다. 세션 수준 부울 보고(세션이 버퍼링을 전혀 경험했는지 여부)의 경우 [버퍼 영향을 받은 스트림](/help/reporting/metrics/buffer-impacted-streams.md)을 사용하십시오.
