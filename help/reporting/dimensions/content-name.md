---
title: 콘텐츠 이름
description: 각 미디어 세션의 사람이 읽을 수 있는 제목을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 10%

---


# 콘텐츠 이름

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**콘텐츠 이름**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 이름](/help/implementation/variables/core/content-name.md)을 참조하세요.*

>[!ENDSHADEBOX]

**콘텐츠 이름** 차원은 사용자가 읽을 수 있는 각 미디어 세션의 제목을 보고합니다.

## 이 차원이 채워지는 방법

친숙한 이름은 세션 시작 시 플레이어가 설정합니다. 보고된 값은 전송된 값과 일치합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.friendlyName`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>Adobe Analytics에서 이 값은 [콘텐츠](content.md) 차원의 **비디오 이름** 분류에도 해당합니다. 해당 분류를 별도로 채우고 유지 관리할 책임이 있습니다. Customer Journey Analytics은 이 차원을 직접 사용합니다.

>[!IMPORTANT]
>
>컨텐츠 이름이 설정되지 않으면 해당 세션에 대한 차원이 채워지지 않습니다.

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 제목입니다(예: `"Blinding Light"`).
