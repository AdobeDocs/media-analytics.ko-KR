---
title: Adobe Audience Manager 지원 소개
description: 추가 처리 규칙 및 사용자 지정 변수 없이도 애플리케이션 작업을 미디어 추적 데이터에 연결 방법을 알아보십시오.
exl-id: c0d73bc2-4713-498a-8882-ff66c7f3dd50
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: ht
source-wordcount: '409'
ht-degree: 100%

---

# Audience Manager 지원{#audience-manager-enablement}

DMP(데이터 관리 플랜)인 AAM(Adobe Audience Manager)은 고객 데이터 자산을 통합하여 사이트 방문자에 대한 상업적인 연관성 있는 정보를 손쉽게 수집하고, 마케팅 가능한 세그먼트를 생성하고, 타기팅된 광고 및 콘텐츠를 적절한 고객에게 제공할 수 있도록 하는 데 도움이 됩니다.

AAM을 사용하면 데이터 판매자, 교환 또는 DSP(광고 구매 플랫폼)에 묶여 있지 않습니다. 또한 AAM은 파트너의 데이터 자산의 측면에서 완전히 불가지론자적 태도를 갖습니다. AAM은 여러 데이터 소스에 대한 액세스를 통해 디지털 게시자에게 광범위한 서드파티 데이터와 Adobe의 개인 데이터 협업을 사용할 수 있는 기능을 제공합니다. AAM에 대한 자세한 내용은 AAM 설명서인 [Audience Manager 제품 설명서](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html?lang=ko-KR)를 참조하십시오.

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

   트레이트가 있는 신호를 고객 관리에 보냅니다.

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

   트레이트가 있는 신호를 고객 관리에 보냅니다.

   ```js
   traitData = {}
   traitData["sampleTrait"] = "sampleValue"
   ADBMobile().audienceSubmitSignal(traitData)
   ```
