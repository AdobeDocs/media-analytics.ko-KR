---
title: 네트워크
description: 브로드캐스트 네트워크 또는 채널 이름을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 11%

---


# 네트워크

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**네트워크**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [네트워크](/help/implementation/variables/standard-metadata/network.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**Network** 차원은 브로드캐스트 네트워크 또는 채널 이름을 보고합니다(예: `"Fox"` 또는 `"ESPN"`). 이를 사용하여 동일한 스트리밍 속성 내에서 네트워크 간 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

네트워크는 세션 시작 시 플레이어에 의해 설정됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.network`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.network`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videonetwork`, `post_videonetwork` |
| Audience Manager | `c_contextdata.a.media.network` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 네트워크 값입니다. 데이터가 철자 변형 간에 조각화되지 않도록 네트워크당 안정적이고 고유한 이름을 사용하십시오.
