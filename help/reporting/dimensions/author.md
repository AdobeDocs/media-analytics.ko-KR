---
title: 작성자
description: 콘텐츠 작성자를 보고합니다. 오디오북에 주로 사용됩니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 11%

---


# 작성자

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**작성자**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [작성자](/help/implementation/variables/standard-metadata/author.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**작성자** 차원은 콘텐츠 작성자를 보고합니다(예: `"Eleanor Clementine"`). 오디오북에 주로 사용되지만 관련 속성이 호스트나 제작자인 팟캐스트에 대해서도 유효합니다.

## 이 차원이 채워지는 방법

작성자는 오디오 콘텐츠에 대한 세션 시작 시 플레이어에 의해 설정됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 오디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.author`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 작성자 이름입니다.
