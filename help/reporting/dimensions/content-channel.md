---
title: 콘텐츠 채널
description: 각 세션이 재생되는 배포 스테이션, 네트워크 또는 속성을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 7%

---


# 콘텐츠 채널

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 채널**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 채널](/help/implementation/variables/core/content-channel.md)을 참조하세요.*

>[!ENDSHADEBOX]

**콘텐츠 채널** 차원은 각 세션이 재생되는 배포 스테이션, 네트워크 또는 속성을 보고합니다. 이 플러그인을 사용하여 속성의 네트워크 또는 섹션별 재생을 분석합니다.

## 이 차원이 채워지는 방법

채널은 세션 시작 시 플레이어에 의해 설정되며 세션 기간 동안 지속됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.channel`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>채널이 설정되지 않은 경우 해당 세션에 대해 차원이 채워지지 않습니다.

## 차원 항목

각 항목은 세션 시작 시 설정된 리터럴 문자열입니다. 모든 문자열이 허용됩니다. 일반적인 값은 네트워크 이름, 사이트 경로의 일부 또는 내부 속성 식별자입니다.
