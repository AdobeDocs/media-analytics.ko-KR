---
title: Audience Manager 지원
description: null
uuid: 8a7f9343-ebc3-4087-9d7e-5972640d2455
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# Audience Manager 지원{#audience-manager-enablement}

AAM(Adobe Audience Manager)은 DMP(데이터 관리 플랫폼)로서, 대상 데이터 자산을 함께 가져와서 상업적으로 관련이 있는 사이트 방문자에 대한 데이터를 쉽게 수집하고, 마케팅 가능한 세그먼트를 만들고, 타깃팅 광고 및 컨텐츠를 해당 대상에게 제공할 수 있습니다.

AAM을 사용하면 데이터 판매자, 교환 또는 수요측 플랫폼에 연결되지 않습니다. 또한 파트너의 데이터 자산과 관련하여 AAM을 전혀 알 수 없습니다. 여러 데이터 소스에 대한 액세스 권한을 통해 AAM은 디지털 게시자에게 광범위한 타사 데이터와 개인 데이터 co-op을 사용할 수 있는 기능을 제공합니다. AAM에 대한 자세한 내용은 AAM 설명서 [Audience Manager 제품 설명서](https://docs-author.corp.adobe.com/content/help/ko-KR/audience-manager/user-guide/aam-home.html)를 참조하십시오.

**VA에서 AAM으로 데이터 전송 -** 비디오 컨텐츠와 비디오 광고 모두에 대해 솔루션(예약된) 변수를 사용하여 수집된 지표 및 메타데이터는 자동으로 AAM에 전송될 수 있습니다. 데이터 전송은 데스크톱, 모바일 및 OTT를 포함한 모든 플랫폼에서 사용할 수 있습니다. 이 서버측 데이터 전송을 활성화하려면 Adobe Client Care에 연락하여 이 피드를 활성화하도록 요청해야 합니다.

>[!IMPORTANT]
>
>데이터를 AAM에 전송하려면 최신 버전의 Media SDK 라이브러리에 있어야 합니다.

페더레이션된 데이터는 AAM에 대한 데이터 공유를 완벽하게 지원합니다. Adobe 팀과 함께 페더레이션된 데이터 설정 확인하십시오.

## OTT / AAM 메서드 {#ott-aam-methods}

다음 메서드를 사용하여 신호를 보내고 Audience Manager에서 방문자 세그먼트를 검색할 수 있습니다.

### Chromecast {#am-chromecast}

* `getVisitorProfile() -`

   가장 최근 획득한 방문자 프로필을 반환합니다. 아직 신호가 제출되지 않은 경우 빈 개체를 반환합니다.

   ```js
   ADBMobile.audienceManager.getVisitorProfile();
   ```

* `getDpid() -`

   가장 최근 획득한 방문자 프로필을 반환합니다. 아직 신호가 제출되지 않은 경우 빈 개체를 반환합니다.

   ```js
   ADBMobile.audienceManager.getDpid();
   ```

* `getDpuuid() -`

   현재 DPUUID를 반환합니다.

   ```js
   ADBMobile.audienceManager.getDpuuid();
   ```

* `setDpidAndDpuuid() -`

   DPID 및 DPUUID를 설정합니다. DPID 및 DPUUID가 설정되면 각 신호와 함께 전송됩니다.

   ```js
   ADBMobile.audienceManager.SetDpidAndDpuuid("myDpid", "myDpuuid");
   ```

* `submitSignal() -`

   트레이트가 있는 신호를 고객 관리에 보냅니다.

   ```js
   ADBMobile.audienceManager.SubmitSignal();
   ```

### Roku {#am-roku}

* `audienceVisitorProfile -`

   가장 최근 획득한 방문자 프로필을 반환합니다. 아직 신호가 제출되지 않은 경우 빈 개체를 반환합니다.

   ```js
   ADBMobile().audienceVisitorProfile()
   ```

* `audienceDpid -`

   가장 최근 획득한 방문자 프로필을 반환합니다. 아직 신호가 제출되지 않은 경우 빈 개체를 반환합니다.

   ```js
   ADBMobile().audienceDpid()
   ```

* `audienceDpuuid -`

   현재 DPUUID를 반환합니다.

   ```js
   ADBMobile().audienceDpuuid()
   ```

* `audienceSetDpidAndDpuuid -`

   DPID 및 DPUUID를 설정합니다. DPID 및 DPUUID가 설정되면 각 신호와 함께 전송됩니다.

   ```js
   ADBMobile().audienceSetDpidAndDpuuid("myDpid", "myDpuuid")
   ```

* `audienceSubmitSignal -`

   트레이트가 있는 신호를 고객 관리에 보냅니다.

   ```js
   ADBMobile().audienceSubmitSignal()
   ```

