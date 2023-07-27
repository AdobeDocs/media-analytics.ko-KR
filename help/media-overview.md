---
title: 스트리밍 미디어용 Adobe Analytics 개요
description: 스트리밍 미디어용 Analytics를 사용하여 콘텐츠, 오디오 및 광고에 대한 강력한 통찰력을 얻으십시오.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 984f058fda15b1c5e960e4c8d8e2378308d2b541
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 100%

---

# 스트리밍 미디어용 Adobe Analytics 개요

![배너](./assets/media_analytics_banner.png)

스트리밍 미디어용 Adobe Analytics 및 Customer Journey Analytics의 추가 기능으로서, 오디오, 비디오 및 광고를 위한 강력한 측정 도구를 제공합니다. 스트리밍 미디어용 Analytics를 사용하면 비디오 및 오디오 지표를 평가하고 결합할 수 있는 지속 시간, 정지 및 시작에 대한 세부 정보를 거의 실시간으로 얻을 수 있습니다. 이러한 통찰력을 통해 고객의 시청 습관을 이해하고 고도로 개인화된 추천으로 참여를 높일 수 있습니다.

스트리밍 미디어용 Adobe Analytics를 사용하면 사이트 및 스트리밍 앱에서의 전체 고객 여정을 추적할 수 있습니다. Streaming Media 지표를 Audience Analytics, Mobile 또는 Cross-Device Analytics와 같은 다른 Adobe Analytics 기능과 결합할 수 있습니다. 이 지표는 Adobe Analytics 보고서 및 기타 Adobe Experience Platform 제품에 쉽게 통합됩니다. 미디어 측정을 사용하면 데이터를 여러 차원과 세그먼트로 분류하여 완전하고 자세한 분석을 수행하는 데 필요한 모든 메타데이터를 캡처할 수 있습니다. 그런 다음 데이터를 분석하고 성공 기준을 완전히 소비된 미디어, 평균 체류 시간 및 완료된 광고에 연결할 수 있습니다.

프레임, 버퍼링 시간 및 평균 비트율과 같이 체감 품질(QoE)과 관련된 중요한 게재 지표를 측정할 수 있습니다. 또한 측정 지표는 웹 사이트 또는 앱 데이터와 결합하여 고객 경로 및 관심사를 시각화함으로써 향상된 추천을 제공하고 Adobe Experience Platform을 사용하여 고객 경험을 개인화할 수 있습니다.

>[!IMPORTANT]
>
>스트리밍 미디어용 Adobe Analytics를 구현하려면 Adobe 영업 담당자 또는 Adobe 계정 팀에게 문의하여 스트리밍 미디어가 제품 포트폴리오에 포함되어 있는지 확인하십시오.


## 작동 방법

스트리밍 미디어 추적 데이터는 Edge Network SDK/확장용 미디어, 태그가 포함된 Media Extension, Media SDK, Media Edge API 또는 미디어 컬렉션 API를 사용하여 플레이어에서 수집됩니다.

모든 세분화된 데이터(최대 10초)는 개별 재생 세션에 대한 데이터를 수집하고 처리하는 Media Analytics Service 또는 Experience Edge(선택한 [구현 방법](/help/implementation/overview.md)에 따라 다름)로 전송됩니다.

재생 세션이 종료되면 저장 및 보고를 위해 계산된 추적 데이터가 Adobe Analytics 또는 Customer Journey Analytics로 전송됩니다.

>[!NOTE]
>
>Customer Journey Analytics 구현을 사용하면 Experience Edge 또는 ADC(Analytics Data Connector)를 사용하여 데이터를 Customer Journey Analytics로 보낼 수 있습니다.


자세한 내용은 [Adobe Analytics 또는 Customer Journey Analytics용 Streaming Media 구현](/help/implementation/overview.md)을 참조하십시오.

## 기능

스트리밍 미디어용 Adobe Analytics의 이점에는 실시간 모니터링, 세부 분석, 실행 가능한 인사이트 및 수익 창출의 기회가 있습니다.

* **실시간 분석**: 미디어 시작과 같은 핵심 성능 지표를 활하여 여러 채널에 걸쳐 실시간 및 실용적인 결정을 내릴 수 있습니다.

* **참여 유도**: 버퍼링 이벤트 수를 최소화하고, 콘텐츠 내에서 광고를 재생할 위치와 시점을 파악하여 사용자 참여를 유도함으로써 재방문을 제공하는 유연하고 간단한 경험을 제공합니다.

* **전체적인 그림**: 모든 콘텐츠 배포자의 여러 데이터 포인트를 결합하여 모든 미디어 활동에 대한 전체 보기를 표시합니다. Federated Analytics 기능을 통해 가능한 모든 채널의 참여 및 보기/듣기를 측정합니다.

* **증가된 세분기간**: 개별 방문자 시간, 분별 동시 시청자 또는 청취자 및 콘텐츠를 소비한 평균 시간을 포함하여 가장 세분화된 수준에서 보기 동작을 평가합니다.

* **정확한 측정**: OTT, 스마트폰, 태블릿, 데스크탑 등 미디어 이용에 사용된 여러 디바이스를 측정하여 사용자 참여 패턴 및 습관을 모니터링합니다.

* **세분화**: 플레이어, 디바이스, 장르, 챕터 및 프로그램에 분류를 적용하여 각 내용이 전체 보기/듣기 및 콘텐츠, 오디오, 광고 및 결합에 대한 고객 참여에 미치는 영향을 확인합니다.
