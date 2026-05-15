---
title: 스트림 형식
description: 각 세션의 품질 계층(일반적으로 HD 또는 SD)을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# 스트림 형식

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**스트림 형식**보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [스트림 형식](/help/implementation/variables/standard-metadata/stream-format.md)을 참조하세요.*

>[!ENDSHADEBOX]

**스트림 형식** 차원은 각 세션의 품질 계층을 보고합니다(일반적으로 `"HD"` 또는 `"SD"`이지만 모든 문자열은 허용됨). 이를 사용하여 게재 품질 계층 간의 참여, 완료 및 품질을 비교할 수 있습니다.

## 이 차원이 채워지는 방법

스트림 형식은 세션 시작 시 플레이어가 설정합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.format`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.format`을(를) 매핑하는 eVar) |
| Audience Manager | `c_contextdata.a.media.format` |

## 차원 항목

각 항목은 세션 시작 시 보고된 리터럴 형식 값입니다. 라인 항목이 철자 변형에서 조각화되지 않도록 안정적인 값 집합(`HD`, `SD`, `4K`, `UHD`)을 사용합니다.
