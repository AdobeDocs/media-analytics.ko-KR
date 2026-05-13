---
title: 아티스트
description: 오디오 콘텐츠에 대한 공연 아티스트를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

---


# 아티스트

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**아티스트**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [아티스트](/help/implementation/variables/standard-metadata/artist.md)를 참조하세요.*

>[!ENDSHADEBOX]

**아티스트** 차원은 오디오 콘텐츠(예: `"Crested Larks"`)에 대해 공연 아티스트를 보고합니다. 연주자별로 음악이나 팟캐스트 카탈로그에 대한 참여를 분산하는 데 사용합니다.

## 이 차원이 채워지는 방법

아티스트는 오디오 콘텐츠에 대한 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 오디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.artist`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoaudioartist` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 아티스트 이름입니다. 형식 변형 간에 데이터가 조각화되지 않도록 아티스트당 안정적인 정식 이름을 사용하십시오.
