---
title: 표시
description: 시리즈의 일부인 비디오 컨텐츠에 대한 프로그램 또는 시리즈 이름을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# 표시

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**표시**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [표시](/help/implementation/variables/standard-metadata/show.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**표시** 차원은 프로그램 또는 시리즈 이름을 보고합니다. 여러 시즌의 에피소드가 동일한 표시 라인 항목으로 롤업되므로 이 항목을 사용하여 시리즈의 전체 라이프타임 동안 참여를 비교할 수 있습니다.

## 이 차원이 채워지는 방법

표시 는 콘텐츠가 시리즈의 일부인 경우 세션 시작 시 플레이어에 의해 설정됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.show`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 표시 이름입니다(예: `"Blinding Light"`). 단어를 공유하는 관련되지 않은 프로그램에서 데이터가 축소되지 않도록 표시당 안정적이고 고유한 이름을 사용합니다.
