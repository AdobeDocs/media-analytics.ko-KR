---
title: 스트리밍 미디어용 Adobe Analytics 개요
description: 스트리밍 미디어 분석을 사용하여 컨텐츠, 오디오 및 광고에 대한 강력한 통찰력을 얻을 수 있습니다.
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
exl-id: 826530f7-2c39-41ef-b3b4-d3f44b46858f
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 16%

---

# 스트리밍 미디어용 Adobe Analytics 개요

![배너](./assets/media_analytics_banner.png)

Adobe Analytics for Streaming Media는 Adobe Analytics의 추가 기능으로서, 오디오, 비디오 및 광고를 위한 강력한 측정 도구를 제공합니다. 스트리밍 미디어용 Analytics를 사용하면 비디오 및 오디오 지표를 평가하고 결합할 수 있는 거의 실시간으로 세분화된 지속 시간, 중지 및 시작을 얻을 수 있습니다. 이러한 인사이트를 통해 고객의 보기 및 청취 습관을 파악하고 개인화된 추천을 통해 참여를 높일 수 있습니다.

Adobe Analytics for Streaming Media를 사용하면 사이트 및 스트리밍 앱에서 전체 고객 여정을 추적할 수 있습니다. 스트리밍 미디어 지표를 Audience Analytics, 모바일 또는 교차 장치 분석과 같은 다른 Adobe Analytics 기능과 결합할 수 있습니다. 이 지표는 Adobe Analytics 보고서 및 기타 Adobe Experience Platform 제품에 쉽게 통합됩니다. 미디어 측정을 사용하면 데이터를 여러 차원과 세그먼트로 분류하여 완전하고 자세한 분석을 수행하는 데 필요한 모든 메타데이터를 캡처할 수 있습니다. 그런 다음 데이터를 분석하고 성공 기준을 완전히 소비된 미디어, 평균 체류 시간 및 완료된 광고에 연결할 수 있습니다.

프레임, 버퍼링 시간 및 평균 비트율과 같이 체감 품질(QoE)과 관련된 중요한 게재 지표를 측정할 수 있습니다. 또한 측정 지표는 웹 사이트나 앱 데이터와 결합하여 고객 경로 및 관심사를 시각화함으로써 향상된 추천을 제공하고 Adobe Experience Platform을 사용하여 고객 경험을 개인화할 수 있습니다.

## 작동 방법

스트리밍 미디어 추적 데이터는 Media SDK, Media Collection API 또는 Media 확장 프로그램(태그 포함)을 사용하여 플레이어에서 수집됩니다. 세분화된 모든 데이터(최대 10초)는 각 개별 재생 세션에 대한 데이터를 수집하고 처리하는 Media Analytics 서비스로 전송됩니다. 재생 세션이 종료되면 계산된 추적 데이터는 저장 및 보고를 위해 Adobe Analytics으로 전송됩니다. CJA(Adobe Customer Journey Analytics) 구현을 통해 ADC(Analytics Data Connector)를 사용하여 CJA로 데이터를 전송할 수 있으므로 고객이 CJA를 보고 도구로 사용할 수 있습니다.

<!-- ![streaming media process](./assets/streaming-process1.png) -->

<div style="text-align: center;">
<img src="./assets/streaming-process1.png" alt="스트리밍 미디어 프로세스" width="75%">
</div>

## 기능

스트리밍 미디어용 Adobe Analytics의 이점에는 실시간 모니터링, 세부 분석, 실행 가능한 인사이트 및 수익 창출의 기회가 있습니다.

* **실시간 분석**: 여러 채널에서 미디어 시작과 같은 주요 성능 지표를 활용하여 실시간으로 실행 가능한 결정을 내릴 수 있습니다.

* **참여 유도**: 버퍼링 이벤트 수를 최소화하고, 컨텐츠 내에서 광고를 재생할 위치와 시점을 파악하여 사용자 참여를 유도함으로써 재방문을 제공하는 유연하고 간단한 경험을 제공합니다.

* **전체적인 그림**: 모든 컨텐츠 배포자의 여러 데이터 포인트를 결합하여 모든 미디어 활동에 대한 전체 보기를 표시합니다. Federated Analytics 기능을 통해 가능한 모든 채널의 참여 및 보기/듣기를 측정합니다.

* **증가된 세부기간**: 개별 방문자 시간, 분별 Concurrent Viewer 또는 Listener 및 컨텐츠를 소비한 평균 시간을 포함하여 가장 세분화된 수준에서 보기 동작을 평가합니다.

* **정확한 측정**: OTT, 스마트폰, 태블릿, 데스크탑 등을 포함하여 미디어 이용에 사용된 여러 장치를 측정하여 사용자 참여 패턴 및 습관을 모니터링합니다.

* **세그먼테이션**: 플레이어, 장치, 장르, 장 및 쇼에 분류를 적용하여 각 분류가 컨텐츠, 오디오, 광고 및 결합에 대한 전체 보기/듣기 및 고객 참여에 어떤 영향을 미치는지 확인할 수 있습니다.
