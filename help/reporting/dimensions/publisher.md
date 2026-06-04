---
title: 게시자
description: 오디오 콘텐츠 게시자를 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# 게시자

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**게시자**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [게시자](/help/implementation/variables/standard-metadata/publisher.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**게시자** 차원은 오디오 콘텐츠 게시자(예: 팟캐스트 네트워크 또는 오디오북 게시자)를 보고합니다. 이를 사용하여 조정된 오디오 카탈로그의 게시자 간 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

플레이어가 오디오 콘텐츠의 세션 시작 시 게시자를 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 오디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.publisher`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 게시자 이름입니다.
