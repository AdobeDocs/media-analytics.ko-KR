---
title: 스트리밍 미디어 컬렉션 릴리스 정보
description: 스트리밍 미디어 컬렉션 릴리스 정보에 대한 릴리스 정보를 확인하십시오.
feature: Release Notes
role: User, Admin, Data Engineer
exl-id: ef068aa6-fdf4-4a5c-b5d0-b93ad31894e8
source-git-commit: 0088d41f557b1dc49ac2b3b6d0a812f22d8849e9
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 78%

---

# Streaming Media Collection 릴리스 정보 (2023년 5월)

**마지막 업데이트**: 2024년 5월 29일 목요일

## 관련 리소스

새로운 기능, 수정 사항 및 관리자를 위한 중요 정보에 대한 정보는 다음 리소스를 참조하십시오.

* [Adobe Analytics 릴리스 정보](https://experienceleague.adobe.com/docs/analytics/release-notes/latest.html?lang=ko)
* [Customer Journey Analytics 릴리스 정보](https://experienceleague.adobe.com/docs/analytics-platform/using/releases/latest.html?lang=ko)
* [Adobe Experience Cloud 제품](https://business.adobe.com/products/adobe-experience-cloud-products.html)의 최신 릴리스 업데이트

* [Adobe Analytics 튜토리얼](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/overview.html?lang=ko)

## *현재 릴리스 정보*

## Adobe 스트리밍 미디어 컬렉션의 새로운 기능 및 업데이트된 기능 {#cja-features}

| 기능 | 설명 | 목표 일자 |
| ----------- | ---------- | ------- |
| 웹 SDK을 사용하여 Adobe Experience Platform Edge Network에 웹 데이터 보내기 | 이제 [Adobe Experience Platform Web SDK을 사용하여 스트리밍 미디어 웹 데이터를 Adobe Experience Platform Edge Network으로 전송](/help/implementation/edge/edge-web-sdk.md)할 수 있으므로 더 개인화된 캠페인을 작성하고 더 개인화된 콘텐츠를 제공하여 보고할 더 많은 추적 데이터를 얻을 수 있습니다.<p>이 개선 사항으로 Customer Journey Analytics, RT-CDP, AJO, 이벤트 전달 등 모든 플랫폼 솔루션 전반에 걸쳐 웹 구현을 위한 통합 수집 방법이 확보됩니다. 이전까지 스트리밍 미디어 웹 데이터를 Edge Network로 보내는 유일한 방법은 Media Edge API를 사용하는 것이었습니다. | 2024년 5월 29일 |
| Adobe Experience Platform Edge으로 Roku 데이터 보내기 | 이제 [Experience Platform Edge과 함께 스트리밍 미디어 컬렉션을 설치](/help/implementation/edge/implementation-edge.md)할 때 Adobe Experience Platform Roku SDK을 사용하여 스트리밍 미디어 데이터를 Adobe Experience Platform으로 보낼 수 있습니다. | 2024년 4월 12일 |
| Media Collection: Experience Edge(API 및 Mobile SDK)와 통합 | 이제 Experience Edge API 및 Mobile SDK을 사용하여 Adobe Streaming Media Collection을 구현할 수 있습니다. 이를 통해 보다 개인화된 캠페인을 구축하고 보다 개인화된 콘텐츠를 제공하여 보고할 더 많은 추적 데이터를 생성할 수 있습니다.<p>이러한 향상된 기능은 Customer Journey Analytics 보고, RT-CDP, AJO 및 이벤트 전달과 같은 모든 솔루션에 통합 수집 방법을 제공합니다.  [자세히 알아보기](/help/implementation/edge/implementation-edge.md) | 2023년 5월 12일 토요일 |
| 미디어 동시 뷰어 패널 | 최대 동시성이 발생한 위치 또는 중단이 발생한 위치를 이해합니다. 콘텐츠 및 뷰어 참여의 품질에 대한 중요한 통찰력을 얻고 볼륨 및 규모에 대한 문제 해결 또는 계획을 수립하는 데 도움이 됩니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-concurrent-viewers.html?lang=ko) | 2022년 8월 9일 |
| 미디어 재생 소요 시간 패널 | 미디어 재생 소요 시간은 시청자 참여에 대한 가치 있는 통찰력을 제공하며 미디어 조직에서는 시간대 지정 기능이 있는 고급 소요 시간 분석을 통해 분 단위 사용자 참여에 대한 보다 심층적이고 세부적인 통찰력을 얻을 수 있습니다. 특정 시점에 미디어 스트림을 보는 데 소요된 시간을 관찰할 수 있습니다. 새로운 5분, 15분, 30분 단위를 포함하여 다양한 단위로 재생 시간을 분할할 수 있습니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-workspace/panels/media-playback-timespent/media-playback-time-spent.html?lang=ko) | 2022년 8월 9일 |
| 모바일 스코어카드에서 주석 공유 | 모바일 스코어카드에서 작업 영역에 생성된 주석을 표시할 수 있습니다. 이를 통해 Analytics 대시보드 모바일 앱에서 볼 수 있는 모바일 스코어카드 프로젝트 내에서 조직 및 캠페인에 대한 상황별 데이터 뉘앙스와 통찰력을 직접 공유할 수 있습니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/mobile-annotations.html?lang=ko) | 2022년 6월 15일 |
| Customer Journey Analytics 업데이트 Report Builder | 스케줄링 및 데이터 블록 관리자와 같은 기능을 포함합니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-reportbuilder/manage-reportbuilder.html?lang=ko) | 2022년 5월 18일 |
| 작업 영역의 주석 | 작업 영역의 주석을 사용하면 상황별 데이터 뉘앙스와 통찰력을 조직에 효과적으로 전달할 수 있습니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-components/annotations/overview.html?lang=ko) | 2022년 3월 23일 점진적 롤아웃 시작 |
| 모바일 스코어카드 프로젝트 미리보기 모드 | 스코어카드 빌더에서 직접 모바일 스코어카드가 Analytics 대시보드 앱에 어떻게 표시되는지 미리보기를 시작해 보십시오. 미리보기 모드를 통해 사용자는 앱에서와 동일한 방식으로 필터 및 차트 및 상호 작용할 수 있으므로 스코어카드를 저장하고 공유하기 전에 환경을 미리 확인할 수 있습니다. 사용자는 미리보기 모드에서 디바이스 선택기를 사용하여 다른 디바이스에서 스코어카드가 어떻게 보이는지 확인할 수도 있습니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dashboards/create-scorecard.html?lang=ko#preview) | 2022년 2월 16일 |


## Adobe 스트리밍 미디어 컬렉션의 새로운 기능 및 업데이트된 기능 {#sm-features}

| 기능 | 설명 | 목표 일자 |
| ----------- | ---------- | ------- |
| 여러 플레이어 상태 추적 | 미디어 컬렉션 API를 사용하여 여러 플레이어 상태 추적을 구현합니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/media-analytics/using/player-state-tracking/multiple-player-states.html?lang=ko) | 2022년 9월 |
| 이름이 변경된 XDM 필드 | 일관성을 유지하기 위해 이름이 변경된 XDM 필드 이름:<br>*오디오 및 비디오 매개변수<br>*광고 매개변수<br>*챕터 매개변수<br>*플레이어 상태 매개변수<br>*품질 매개변수 | 2022년 9월 |
| Device Co-op 참조 | Adobe Experience Cloud Device Co-op 및 Experience Cloud ID 서비스 요구 사항에 대한 참조가 제거되었습니다. | 2022월 8월 |
| 업데이트된 컬렉션 및 보고 필드 이름 및 XDM 패스 | 업데이트된 사항:<br>*오디오 및 비디오 매개변수<br>*광고 매개변수<br>*챕터 매개변수<br>*플레이어 상태 매개변수<br>*품질 매개변수 | 2022월 8월 |
| 대상자 분당 평균 시청 시간 | Media Analytics 고객은 평균 분당 시청자 패널을 사용하여 평균적인 콘텐츠 소비에 대해 더 잘 이해할 수 있습니다. <br>평균 분당 시청자를 통해 모든 길이 또는 모든 장르의 프로그램을 비교할 수 있습니다. 또한 디지털 평균 분당 시청자를 유선 TV 평균 분당 지표와 비교하거나 추가할 수 있습니다. 이 패널을 통해 기간 분류가 업데이트된 경우에도 사용자 정의 기간의 대상자 평균을 보다 유연하게 측정할 수 있습니다. [자세히 알아보기](https://experienceleague.adobe.com/docs/media-analytics/using/media-reports/average-minute-audience.html?lang=ko) | 2022년 3월 16일 |
| 미디어 재생 소요 시간 패널 | 미디어 재생 소요 시간 패널을 통해 미디어 사용자가 선택한 세부 기간을 하루 동안 시청한 시간을 기준으로 시청률을 파악하는 방법에 대해 알아봅니다. <br>[미디어 재생 소요 시간 패널 (튜토리얼)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/media-analytics/measuring-media-analytics/media-playback-time-spent-panel.html?lang=kr) | 2022년 1월 |


## *이전 릴리스 정보*

| 기능 | 설명 | 목표 일자 또는 업데이트 일자 |
| ----------- | ---------- | -------------- |
| 미디어 재생 소요 시간 | Adobe 스트리밍 미디어 재생 소요 시간은 시청자 참여에 대한 가치 있는 통찰력을 제공하며 미디어 조직에서는 시간대 지정 기능이 있는 고급 소요 시간 분석을 통해 분 단위 사용자 참여에 대한 보다 심층적이고 세부적인 통찰력을 얻을 수 있습니다. 특정 시점에 미디어 스트림을 보는 데 소요된 시간을 관찰할 수 있습니다. 새로운 5분, 15분, 30분 단위를 포함하여 다양한 단위로 재생 시간을 분할할 수 있습니다. [자세히 알아보기...](/help/reporting/workspace/media-playback-time-spent.md) | 2021년 9월 |
| Analytics Workspace의 미디어 동시 뷰어 패널 | 최대 동시성이 발생한 위치 또는 중단이 발생한 위치를 이해합니다. 콘텐츠 및 뷰어 참여의 품질에 대한 중요한 통찰력을 얻고 볼륨 및 규모에 대한 문제 해결 또는 계획을 수립하는 데 도움이 됩니다. [자세히 알아보기…](/help/reporting/workspace/media-concurrent-viewers-overview.md) <br><br>[Analytics Workspace의 미디어 동시 뷰어 패널(튜토리얼)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/analysis-workspace/using-panels/media-concurrent-viewers-panel-in-analysis-workspace.html?lang=kr#analysis-workspace) | 2020년 9월 <br><br><br>2021년 1월 |
| 지원되는 디바이스 및 플랫폼 | 이제 AEP SDK가 포함된 미디어 실행 확장자는 다음과 같은 OTT 디바이스를 지원합니다. <div><ul><li>Apple TV (tvOS)</li><li>Fire TV (Fire OS)</li><li>Android TV</li></ul></div> | 2020년 6월 |


<!-- ## Important notices for [!DNL Analytics] administrators

**Updated on March 3, 2022**

| Notice | Date Added or Updated  | Description |
| ----------- | ---------- | ---------- |
| description | date | description |
| description | date | description |
| description | date | description |
| description | date | description | -->
