---
title: 미디어 다운로드됨
description: 다운로드한 오프라인 콘텐츠를 재생한 세션에 플래그를 지정합니다.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 미디어 다운로드됨

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**다운로드된 미디어**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [미디어 다운로드 플래그](/help/implementation/variables/core/media-downloaded-flag.md)를 참조하십시오.*

>[!ENDSHADEBOX]

**Media downloaded** 차원은 인터넷에서 라이브 스트림이 아닌 이전에 다운로드한 오프라인 콘텐츠를 재생한 세션에 플래그를 지정합니다. 참여, 완료 또는 품질을 비교할 때 오프라인 재생을 스트리밍된 세션과 구분하는 데 사용합니다.

## 이 차원이 채워지는 방법

다운로드한 플래그는 플레이어가 세 가지 방법 중 하나로 설정합니다. 플래그를 사용하여 추적기를 초기화하거나(Mobile SDK) `sessionStart`을(를) `/downloaded` 끝점 변형(Media Edge API direct)으로 보내거나 `sessionStart` 매개 변수에 `media.downloaded: true`을(를) 포함하십시오(Media Collection API).

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | `a.media.downloaded`을(를) eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을(를) 만듭니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `evar1`-`evar250`, `post_evar1`-`post_evar250`(처리 규칙이 `a.media.downloaded`을(를) 매핑하는 eVar) |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## 차원 항목

| 값 | 설명 |
| --- | --- |
| `true` | 세션이 다운로드한 오프라인 콘텐츠를 재생했습니다. |
| (비어 있음) | 세션이 라이브 스트림을 재생했습니다. 필드가 `false`(으)로 설정되지 않고 생략되었습니다. |
