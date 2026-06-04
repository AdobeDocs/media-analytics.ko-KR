---
title: 페더레이션된 데이터
description: 고객 자체 구현이 아닌 페더레이션 데이터 공유를 통해 받은 세션을 카운트합니다.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# 페더레이션된 데이터

>[!AVAILABILITY]
>
>Federated Analytics 서비스는 Adobe Analytics에서 스트리밍 미디어 기능을 사용하는 경우에만 사용할 수 있습니다. Federated Analytics은 Customer Journey Analytics에서 사용할 수 없습니다.

**페더레이션 데이터** 지표는 자체 구현이 아닌 페더레이션 데이터 공유를 통해 받은 세션을 계산합니다. 이를 사용하여 파트너 공유 세션의 볼륨을 측정하고 참여, 완료 또는 품질을 자사 세션과 비교할 수 있습니다.

자세한 내용은 [Federated Media](/help/use-cases/federated-media.md) 사용 사례를 참조하십시오.

>[!TIP]
>
>페더레이션 데이터를 차원으로 사용하려면 `a.media.federated` 컨텍스트 데이터 변수를 eVar에 매핑하는 [처리 규칙](https://experienceleague.adobe.com/ko/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)을 만드십시오.

## 이 지표의 계산 방법

세션이 페더레이션 채널을 통해 도달하면 미디어 백엔드가 이 플래그를 설정합니다. 지표는 자격 부여 세션당 한 번씩 증가하며 닫기 호출 시 보고됩니다.

| 보고 시스템 | 소스 |
| --- | --- |
| Adobe Analytics | [[!UICONTROL 비디오 메타데이터]](/help/reporting/setup/analytics-reporting.md)이(가) 활성화되면 컨텍스트 데이터 `a.media.federated`에서 자동으로 수집됩니다. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isFederated`](https://experienceleague.adobe.com/ko/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 데이터 피드 | `event_list`, `post_event_list`([`event.tsv`](https://experienceleague.adobe.com/ko/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files) 조회 참조) |
| Audience Manager | `c_contextdata.a.media.federated` |
