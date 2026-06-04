---
title: 콘텐츠
description: 컨텐츠 ID로 처리된, 재생되는 각각의 고유한 미디어 부분을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

---


# 콘텐츠

>[!BEGINSHADEBOX]

*이 페이지는&#x200B;**콘텐츠**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 ID](/help/implementation/variables/core/content-id.md)을(를) 참조하십시오.*

>[!ENDSHADEBOX]

**Content** 차원은 세션 시작 시 설정된 콘텐츠 ID로 키로 재생되는 각 고유한 미디어 부분을 보고합니다. 이는 스트리밍 미디어 보고를 위한 기본 분류이며 비디오 이름, 비디오 길이, 에셋 ID, 최초 방송 날짜 및 콘텐츠 등급과 같은 분류 차원에 대한 조인 키입니다.

## 이 차원이 채워지는 방법

콘텐츠는 세션 시작 시 플레이어가 에셋의 안정적인 식별자로 설정합니다. 세션의 후속 이벤트마다 동일한 콘텐츠 ID가 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.name`에서 자동으로 수집됩니다. 방문 기간 동안 지속됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>컨텐츠 ID는 필수입니다. 설정이 해제되었거나 비어 있는 경우, 세션이 스트리밍 미디어 보고에서 삭제되고 미디어 보고서 또는 [!UICONTROL 모든 스트리밍 미디어] 세그먼트에 나타나지 않습니다.

## 차원 항목

각 항목은 세션 시작 시 보고되는 고유한 콘텐츠 ID입니다. 동일한 에셋에 대한 세션이 시간이 지남에 따라 단일 라인 항목으로 롤업되도록 안정적인 식별자(예: 내부 CMS ID, EIDR 또는 TMS/Gracenote와 같은 업계 ID 또는 지속 슬러그)를 사용합니다.

## 권장 세그먼트

| 세그먼트 | 규칙 |
| --- | --- |
| [!UICONTROL 모든 스트리밍 미디어] | 컨텐츠(ID)가 존재함 |
