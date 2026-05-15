---
title: 유형 표시
description: 콘텐츠 형식(전체 에피소드, 미리보기, 클립 또는 기타)을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# 유형 표시

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**표시 유형**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [유형 표시](/help/implementation/variables/standard-metadata/show-type.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**표시 형식** 차원은 문자열 정수 코드를 사용하여 콘텐츠 형식을 보고합니다. 참여를 측정할 때 트레일러 및 클립과 같은 짧은 형식의 콘텐츠에서 전체 프로그램 보기를 분리하는 데 사용합니다.

## 이 차원이 채워지는 방법

세션 시작 시 플레이어가 표시 유형을 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.type`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## 차원 항목

| 값 | 설명 |
| --- | --- |
| `0` | 전체 에피소드 |
| `1` | 미리보기 또는 트레일러 |
| `2` | 클립 |
| `3` | 기타 |

값은 문자열로 보고됩니다. 사용자 지정 값은 허용되지만 4개의 기본 제공 버킷으로 롤업되지 않습니다.
