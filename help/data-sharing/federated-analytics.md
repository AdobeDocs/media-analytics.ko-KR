---
seo-title: 페더레이션 분석
title: 페더레이션 분석
uuid: a82ace81-c2f6-4799-9a62-4c6a737a7dab
translation-type: tm+mt
source-git-commit: b20cce8df3631690a7de6de502828e961d154665

---


# 페더레이션 분석{#federated-analytics}

Federated Analytics 서비스는 두 파트너 간에 Adobe Media(오디오와 비디오) Analytics 데이터를 공유하는 시스템을 제공합니다. Media Analytics에서 만든 표준화된 비디오 측정 데이터는 동일한 데이터를 여러 소스에서 단일 보고서에 병합될 수 있도록 하는 Federated Analytics의 특징입니다. 페더레이션 분석을 제어하는 규칙 및 로직을 통해 각 파트너십의 요구를 충족하도록 데이터를 쉽게 제어하고 개별화할 수 있습니다. Federated Analytics를 통해 오디오 및 비디오 측정을 보다 효율적이고 능률적이며 작동 가능하게 할 수 있습니다.

## 이점 {#section_804FFE8671594A6FB769CBE79EF9D627}

* **투명:**&#x200B;회사 간에 동일한 논리를 사용하여 검정 상자의 데이터 생성 제거
* **광범위:** 파트너십, 플랫폼 및 장치 간의 완전한 연결과 오디오 및 비디오 사용이 미치는 영향 이해
* **보안:**&#x200B;규칙 및 로직을 통한 서버 측 데이터 공유 제어
* **표준화:**&#x200B;파트너와 동일한 데이터 언어 말하기
* **동작 가능:** Adobe Analytics를 통해 플레이어를 벤치마킹하고, 트렌드를 모니터링하고, 이상 현상을 감지하도록 오디오 및 비디오 데이터 정량화
* **중앙 집중식:** 한 Adobe 위치에서 오디오 및 비디오 측정 데이터 수집
* **계약:**&#x200B;법률 데이터 공유 요구 사항을 쉽게 충족
* **적시:**&#x200B;실시간으로 데이터 전송 및 수신
* **쉬움:** Adobe SDK를 사용하여 플레이어에 태그를 한 번 지정하고, 데이터를 여러 파트너에게 공유

## 정의 {#section_ypl_mb3_vbb}

* **보낸 사람:** 소유한 플레이어에서 오디오 및 비디오 분석 데이터를 생성하는 고객
* **받는 사람:** 보낸 사람으로부터 오디오 및 비디오 분석 데이터를 받는 고객

## 요구 사항 {#section_4758843A8941441B9A4D0D7A61077A6E}

* **Media 스트림 계약:** 보낸 사람과 받는 사람은 Adobe Analytics 내의 오디오 및 비디오 데이터에 액세스하려면 Adobe Analytics for Media Streams에 등록해야 합니다. 자세한 내용은 계정 팀에 문의하십시오.
* **페더레이션 추록:**&#x200B;보낸 사람과 받는 사람은 각각 데이터를 보내거나 받기 전에 Adobe와 함께 서명한 추록이 있어야 합니다. 파트너십 당 하나의 추록이 아니라, 고객 당 하나의 추록이 필요합니다. 자세한 내용은 계정 팀에 문의하십시오.
* **Media Analytics 구현:** 보낸 사람은 모든 플레이어에 Media Analytics가 구현되어 있어야 합니다. 이러한 분석은 페더레이션 데이터 세트의 일부가 됩니다. Media Analytics 데이터만 페더레이션될 수 있습니다. See documentation: [Measuring audio and video in Adobe Analytics](/help/media-overview.md)

* **Adobe Consulting Contract:**&#x200B;보낸 사람과 받은 사람 간의 초기 페더레이션 규칙 설정의 경우 컨설팅 서비스 팀과 함께 작업하여 데이터를 검토하고 데이터 공유 계약을 작성하는 것이 중요합니다.

## Download the Federated Analytics Form

**Download the current version of the form here:`===>`**   [Federation Rules Agreement Form.](/assets/federated_analytics_form.pdf) `<===`

## 프로세스 {#section_byb_kb3_vbb}

1. 보낸 사람과 받은 사람은 함께 페더레이션 규칙 계약 양식을 작성합니다. The Federated Rules Agreement form contains special fields for our engineering team and should ONLY be edited using Adobe Acrobat. [Acrobat을 무료로 다운로드합니다.](https://get.adobe.com/reader/)
1. 데이터 파일이 있다면, 컨설팅 서비스는 보낸 사람의 플레이어에서 실제 데이터가 있는 받는 사람에게 샘플 데이터 파일을 제공하여 올바른 데이터 공유 규칙이 정의되어 있는지 확인합니다.
1. 보낸 사람과 받는 사람은 데이터 공유 계약이 두 당사자 간의 계약 요구 사항을 모두 충족하는지 확인합니다.
1. 컨설팅 서비스는 작성된 양식을 Adobe 엔지니어링 부서로 보내어 데이터 공유 규칙을 설정합니다.
1. 데이터는 받는 사람이 데이터를 검토하고 확인하는 개발 보고서 세트에 공유됩니다.
1. 받는 사람이 데이터가 올바른지 확인하면, Adobe 엔지니어링 부서에서 프로덕션 보고서 세트를 가리키도록 규칙을 업데이트합니다.
1. 받는 사람은 프로덕션 보고서 세트의 데이터를 검토하고 확인합니다.
1. 나중에 데이터 세트기 변경되면 보낸 사람 또는 받는 사람이 지원을 위해 고객 지원 티켓을 제출할 수 있습니다.

