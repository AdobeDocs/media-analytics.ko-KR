---
title: 방송 시간대
description: 콘텐츠가 브로드캐스트 또는 재생될 당시의 시간 버킷(아침, 오후, 프라임타임, 늦은 밤)을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 8%

---


# 방송 시간대

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**일 파트**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [일 파트](/help/implementation/variables/standard-metadata/day-part.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**일 부분** 차원은 콘텐츠가 브로드캐스트 또는 재생될 때의 시간 버킷을 보고합니다. 일반적인 값은 `"Morning"`, `"Afternoon"`, `"Primetime"` 및 `"Late Night"`입니다. 이 시각화를 사용하여 뷰어의 현지 시간대와 독립적으로 날짜 간 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

일 부분은 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.dayPart`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 daypart 레이블입니다. 구현 간에 고정된 값 집합을 사용하여 라인 항목을 일관되게 유지합니다.
