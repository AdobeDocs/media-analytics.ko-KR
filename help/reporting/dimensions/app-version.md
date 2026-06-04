---
title: 앱 버전
description: 각 스트리밍 세션에 사용되는 미디어 플레이어 애플리케이션의 버전을 보고합니다.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 4%

---


# 앱 버전

>[!BEGINSHADEBOX]

*이 페이지에서는&#x200B;**앱 버전**&#x200B;보고 차원을 다룹니다. 이 변수를 수집하는 방법은 [앱 버전](/help/implementation/variables/core/app-version.md)을 참조하세요.*

>[!ENDSHADEBOX]

**앱 버전** 차원은 SDK 초기화에서 구성된 미디어 플레이어 응용 프로그램의 버전 문자열을 보고합니다. 이를 사용하여 현재 사용 중인 플레이어 버전을 식별하고, 품질 또는 동작 변경 사항을 특정 릴리스와 상호 연관시키고, 널리 사용되는 버전에 대한 지원의 우선 순위를 지정합니다.

>[!NOTE]
>
>이 차원은 Adobe의 SDK 라이브러리가 아닌 **미디어 플레이어 응용 프로그램**&#x200B;의 버전을 캡처합니다. Adobe의 자체 SDK 라이브러리 버전은 별도의 내부 필드로 자동으로 수집됩니다.

## 이 차원이 채워지는 방법

앱 버전은 SDK 초기화 시 한 번 설정되고 모든 세션 시작 요청에 자동으로 포함됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | Edge 구현을 사용할 때 XDM 필드 매핑을 통해 자동으로 수집됩니다. Analytics 전용 구현의 경우 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.md)을 사용하여 컨텍스트 데이터 `media.sdkVersion`을(를) 사용자 지정 eVar에 매핑합니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.appVersion`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | 전용 데이터 피드 열이 없습니다. Analytics 전용 구현의 경우 처리 규칙을 통해 구성된 사용자 지정 eVar의 데이터 피드 열을 사용하십시오. |
| Audience Manager | `c_contextdata.media.sdkVersion`(Analytics 전용 구현) |

## 차원 항목

각 항목은 SDK 초기화 시 구성된 리터럴 버전 문자열입니다. 버전 문자열이 보고서에 예측 가능하게 롤업되도록 구현에서 일관된 버전 지정 체계를 사용하십시오.
