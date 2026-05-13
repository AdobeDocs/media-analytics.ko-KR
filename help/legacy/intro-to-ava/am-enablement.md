---
title: Adobe Audience Manager 지원 소개
description: 추가 처리 규칙 및 사용자 정의 변수 없이도 애플리케이션 작업을 미디어 추적 데이터에 연결 방법을 알아보십시오.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/oInE3GwgI1k5-UbqMUm9yvjXfIF0SsRXPrnUWmWT9Ww
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: e7d92df1-c5ba-4e93-85df-f83171b889be
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 408
ht-degree: 100%

---

# Audience Manager 지원{#audience-manager-enablement}

DMP(데이터 관리 플랜)인 AAM(Adobe Audience Manager)은 대상자 데이터 에셋을 통합하여 사이트 방문자에 대한 상업적인 연관성 있는 정보를 손쉽게 수집하고, 마케팅 가능한 세그먼트를 생성하고, 타겟팅 광고 및 콘텐츠를 적절한 대상자에게 제공할 수 있도록 하는 데 도움이 됩니다.

AAM을 사용하면 데이터 판매자, 교환 또는 DSP(광고 구매 플랫폼)에 묶여 있지 않습니다. 또한 AAM은 파트너의 데이터 에셋의 측면에서 완전히 불가지론자적 태도를 갖습니다. AAM은 여러 데이터 소스에 대한 액세스를 통해 디지털 게시자에게 광범위한 서드파티 데이터를 사용할 수 있는 기능을 제공합니다. AAM에 대한 자세한 내용은 AAM 설명서인 [Audience Manager 제품 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=ko-KR)를 참조하십시오.

**VA에서 AAM으로 데이터 전송 -** 비디오 콘텐츠와 비디오 광고 모두에 대해 솔루션(예약된) 변수를 사용하여 수집된 지표 및 메타데이터는 자동으로 AAM에 전송될 수 있습니다. 데이터 전송은 데스크탑, 모바일, OTT를 비롯한 모든 플랫폼에서 사용할 수 있습니다. 이 서버측 데이터 전송을 사용하려면 Adobe Client Care에 연락하여 이 피드를 활성화하도록 요청해야 합니다.

>[!IMPORTANT]
>
>데이터를 AAM에 전송하려면 최신 버전의 Media SDK 라이브러리에 있어야 합니다.

페더레이션 데이터는 AAM에 대한 데이터 공유를 완전히 지원합니다. 페더레이션 데이터 설정을 확인하려면 Adobe 팀과 협력하십시오.

## OTT / AAM 메서드 {#ott-aam-methods}

다음 메서드를 사용하여 신호를 보내고 Audience Manager에서 방문자 세그먼트를 검색할 수 있습니다.

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

  가장 최근 획득한 방문자 프로필을 반환합니다. 아직 어떤 신호도 전송되지 않은 경우 빈 개체를 반환합니다.

  ```js
  ADBMobile.audienceManager.getVisitorProfile();
  ```

* `getDpid() -`

  가장 최근 획득한 방문자 프로필을 반환합니다. 아직 어떤 신호도 전송되지 않은 경우 빈 개체를 반환합니다.

  ```js
  ADBMobile.audienceManager.getDpid();
  ```

* `getDpuuid() -`

  현재 DPUUID를 반환합니다.

  ```js
  ADBMobile.audienceManager.getDpuuid();
  ```

* `setDpidAndDpuuid() -`

  DPID 및 DPUUID를 설정합니다. DPID 및 DPUUID가 설정되면 이 값들이 각 신호와 함께 전송됩니다.

  ```js
  ADBMobile.audienceManager.setDpidAndDpuuid("myDpid", "myDpuuid");
  ```

* `submitSignal() -`

  트레이트가 있는 신호를 대상자 관리에 보냅니다.

  ```js
  ADBMobile.audienceManager.submitSignal({"sampleTrait":"sampleValue"});
  ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

  가장 최근 획득한 방문자 프로필을 반환합니다. 아직 어떤 신호도 전송되지 않은 경우 빈 개체를 반환합니다.

  ```js
  ADBMobile().audienceVisitorProfile()
  ```

* `audienceDpid -`

  가장 최근 획득한 방문자 프로필을 반환합니다. 아직 어떤 신호도 전송되지 않은 경우 빈 개체를 반환합니다.

  ```js
  ADBMobile().audienceDpid()
  ```

* `audienceDpuuid -`

  현재 DPUUID를 반환합니다.

  ```js
  ADBMobile().audienceDpuuid()
  ```

* `audienceSetDpidAndDpuuid -`

  DPID 및 DPUUID를 설정합니다. DPID 및 DPUUID가 설정되면 이 값들이 각 신호와 함께 전송됩니다.

  ```js
  ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
  ```

* `audienceSubmitSignal -`

  트레이트가 있는 신호를 대상자 관리에 보냅니다.

  ```js
  traitData = {}
  traitData["sampleTrait"] = "sampleValue"
  ADBMobile().audienceSubmitSignal(traitData)
  ```
