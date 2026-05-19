---
title: 컨텐츠 유형
description: 스트림 형식(VOD, 라이브, 선형, 팟캐스트, 노래 등)을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

---


# 컨텐츠 유형

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**콘텐츠 형식**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [콘텐츠 형식](/help/implementation/variables/core/content-type.md)을 참조하세요.*

>[!ENDSHADEBOX]

**컨텐츠 유형** 차원은 스트림의 형식을 보고합니다(예: 비디오의 경우 VOD, Live 또는 선형, 오디오의 경우 노래, 팟캐스트 또는 오디오북).

## 이 차원이 채워지는 방법

컨텐츠 유형은 세션 시작 시 플레이어에 의해 설정되고 모든 이벤트를 통해 전달됩니다. 파생되지 않습니다. 보고된 값이 수집 중에 전송된 값과 일치합니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 미디어 코어]](/help/reporting/media-reports-enable.md)이(가) 활성화되면 컨텍스트 데이터 `a.contentType`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>콘텐츠 유형이 설정되지 않았거나 비어 있으면 차원이 세션에 대해 `missing_content_type`을(를) 보고합니다. 이 값을 사용하여 수정해야 하는 구현을 찾으십시오.

## 차원 항목

Adobe 정의 값이 기본 제공 세그먼트 및 보고서를 채웁니다. 사용자 지정 문자열이 허용되지만 기본 제공 세그먼트와 일치하지 않습니다.

| 스트림 유형 | 권장 값 |
| --- | --- |
| 비디오 | `vod`, `live`, `linear`, `ugc`, `dvod` |
| 오디오 | `song`, `podcast`, `audiobook`, `radio` |

## 권장 세그먼트

| 세그먼트 | 규칙 |
| --- | --- |
| [!UICONTROL VOD 콘텐츠] | 콘텐츠 형식 = `vod` |
| [!UICONTROL 라이브 콘텐츠] | 콘텐츠 형식 = `live` |
| [!UICONTROL 선형 콘텐츠] | 콘텐츠 형식 = `linear` |
