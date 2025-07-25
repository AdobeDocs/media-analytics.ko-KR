---
title: 페더레이션 미디어
description: Federated Media 서비스는 두 파트너 간에 스트리밍 미디어 데이터를 공유하는 시스템을 제공합니다.
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
exl-id: 81970370-663c-49d5-b13c-628d294be178
feature: Streaming Media
role: User, Admin, Data Engineer
source-git-commit: a6a9d550cbdf511b93eea132445607102a557823
workflow-type: tm+mt
source-wordcount: '571'
ht-degree: 61%

---

# 페더레이션 미디어{#federated-media}

Federated Media 서비스는 두 파트너 간에 스트리밍 미디어 데이터(오디오 및 비디오)를 공유하는 시스템을 제공합니다.
스트리밍 미디어 컬렉션에서 만든 표준화된 측정 데이터는 동일한 데이터를 여러 소스에서 단일 보고서에 병합될 수 있도록 하는 Federated Media의 특징입니다.
Federated Media를 제어하는 규칙과 로직을 통해 각 파트너십의 요구 사항을 충족하도록 데이터를 쉽게 제어하고 개별화할 수 있습니다.
Federated Media를 통해 오디오 및 비디오 측정을 보다 효율적이고 능률적이며 작동 가능하게 할 수 있습니다.


![](assets/media-federated.png)

## 이점 {#benefits}

* **투명:** 여러 회사에서 동일한 논리를 사용하여 데이터 작성의 비밀스런 부분 제거
* **광범위:**&#x200B;파트너십, 플랫폼 및 디바이스 간의 완전한 연결과 오디오 및 비디오 사용이 미치는 영향 이해
* **보안:** 규칙 및 논리를 통해 서버측 데이터 공유 제어
* **표준화:** 파트너와 동일한 데이터 언어 사용
* **동작 가능:** Adobe Analytics를 통해 플레이어를 벤치마킹하고, 트렌드를 모니터링하고, 이상 현상을 감지하도록 오디오 및 비디오 데이터 정량화
* **중앙 집중식:** 한 Adobe 위치에서 오디오 및 비디오 측정 데이터 수집
* **계약:** 법적 데이터 공유 요구 사항을 쉽게 충족
* **적시:** 거의 실시간으로 데이터 전송 및 수신
* **용이:** Adobe SDK를 사용하여 한 번에 플레이어에 태그를 지정하고 데이터를 많은 파트너에게 공유

## 정의 {#definitions}

* **보낸 사람:** 소유한 플레이어에서 오디오 및 비디오 분석 데이터를 생성하는 고객
* **받는 사람:** 보낸 사람으로부터 오디오 및 비디오 분석 데이터를 받는 고객

## 요구 사항 {#requirements}

* **Media 스트림 계약:** 보낸 사람과 받는 사람은 Adobe Analytics 내의 오디오 및 비디오 데이터에 액세스하려면 Adobe Analytics for Media Streams에 등록해야 합니다. 자세한 내용은 계정 팀에게 문의하십시오.
* **연합 부록:** 데이터를 전송하거나 수신하기 전에 각 발신자와 수신자는 Adobe와 함께 서명된 부록이 있어야 합니다. 고객당 하나의 부록이 필요합니다. 파트너십당 하나의 부록이 아닙니다. 자세한 내용은 계정 팀에게 문의하십시오.

* **스트리밍 미디어 컬렉션 구현:** 보낸 사람이 페더레이션 데이터 세트의 일부가 될 모든 플레이어에 스트리밍 미디어 컬렉션을 구현해야 합니다. 스트리밍 미디어 데이터만 페더레이션에 사용할 수 있습니다. 자세한 내용은 [Adobe 스트리밍 미디어 컬렉션 개요](/help/media-overview.md)를 참조하십시오.

* **Adobe Consulting Contract:**&#x200B;보낸 사람과 받은 사람 간의 초기 페더레이션 규칙 설정의 경우 컨설팅 서비스 팀과 함께 작업하여 데이터를 검토하고 데이터 공유 계약을 작성하는 것이 중요합니다.

## Federated Media 양식 다운로드

Federated Media에 참여하려면 [페더레이션 규칙 계약](assets/federated_analytics_form.pdf) 양식을 다운로드하여 작성하십시오.

## 프로세스 {#process}

1. 보낸 사람과 받은 사람은 함께 페더레이션 규칙 계약 양식을 작성합니다. 페더레이션 규칙 계약 양식은 엔지니어링 팀을 위한 특수 필드를 포함하며 Adobe Acrobat만 사용하여 편집해야 합니다. [Acrobat을 무료로 다운로드하십시오.](https://get.adobe.com/reader/)
1. 데이터 파일이 있다면 컨설팅 서비스는 보낸 사람의 플레이어에서 실제 데이터가 있는 받는 사람에게 샘플 데이터 파일을 제공하여 올바른 데이터 공유 규칙이 정의되어 있는지 확인합니다.
1. 보낸 사람과 받는 사람은 데이터 공유 계약이 두 당사자 간의 계약 요구 사항을 모두 충족하는지 확인합니다.
1. 컨설팅 서비스는 완성된 양식을 Adobe 엔지니어링 팀에 보내 데이터 공유 규칙을 설정합니다.
1. 데이터는 받는 사람이 데이터를 검토하고 확인하는 개발 Adobe Analytics 보고서 세트 또는 Adobe Experience Platform 데이터스트림에 공유됩니다.
1. 데이터가 올바른 것으로 수신자가 확인하면 Adobe Engineering은 규칙을 업데이트하여 프로덕션 Analytics 보고서 세트 또는 Adobe Experience Platform 데이터스트림을 지정합니다.
1. 받는 사람은 Production Analytics 보고서 세트 또는 Adobe Experience Platform 데이터스트림의 데이터를 검토하고 확인합니다.
1. 차후에 데이터 세트가 변경되면 발신자나 수신자는 고객 지원 티켓을 제출하여 지원을 받을 수 있습니다.
