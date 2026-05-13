---
title: 방송국
description: 오디오 브로드캐스트 콘텐츠에 대한 라디오 방송국 이름 또는 ID를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---


# 방송국

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**Station**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [Station](/help/implementation/variables/standard-metadata/station.md)을 참조하세요.*

>[!ENDSHADEBOX]

**Station** 차원은 오디오 콘텐츠를 브로드캐스트하는 라디오 방송국 이름 또는 ID를 보고합니다(예: `"NPR"` 또는 `"WXYZ-FM"`). 이를 사용하여 신디케이트된 네트워크의 스테이션 간 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

스테이션은 플레이어가 오디오 콘텐츠의 세션 시작 시 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 오디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.station`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoaudiostation` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 스테이션 이름 또는 ID입니다. 참여가 호출 기호 변형 간에 조각화되지 않도록 스테이션당 단일 표준 식별자를 사용하십시오.
