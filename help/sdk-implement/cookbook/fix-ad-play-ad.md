---
title: 광고 사이에 표시되는 기본 재생 해결
description: '"광고 사이에 표시되는 main:play 호출을 처리하는 방법을 배웁니다."'
uuid: 228b4812-c23e-40c8-ae2b-e15ca69b0bc2
exl-id: f27ce2ba-7584-4601-8837-d8316c641708
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 96%

---

# 광고 사이에 표시되는 main:play 해결{#resolving-main-play-appearing-between-ads}

## 문제

일부 광고 추적 시나리오에서는 한 광고가 끝나고 다음 광고가 시작되는 사이에 예기치 않게 `main:play` 호출이 발생할 수 있습니다. 광고 완료 호출과 다음 광고 시작 호출 사이의 지연 시간이 250밀리초보다 크면 Media SDK가 `main:play` 호출 전송으로 폴백합니다. 프리롤 광고 브레이크 중에`main:play`로 이 폴백이 발생하면 컨텐츠 시작 지표가 초기에 설정될 수 있습니다.

위에서 설명한 것과 같은 광고 사이의 간격은 광고 컨텐츠로 겹치지 않으므로 Media SDK에 의해 기본 컨텐츠로 해석됩니다. Media SDK에는 광고 정보가 설정되어 있지 않으며, 플레이어가 재생 중 상태에 있습니다. 광고 정보가 없고 플레이어 상태가 재생 중인 경우, Media SDK는 기본적으로 기본 컨텐츠에 대한 간격 기간을 크레딧합니다. null 광고 정보에 대한 재생 기간을 크레딧할 수 없습니다.

## 식별

Adobe Debug 또는 Charles와 같은 네트워크 패킷 스니퍼를 사용하는 동안 프리롤 광고 브레이크 중 다음 하트비트 호출이 이 순서로 표시되는지 확인합니다.

* 세션 시작: `s:event:type=start` &amp; `s:asset:type=main`
* 광고 시작: `s:event:type=start` &amp; `s:asset:type=ad`
* 광고 재생: `s:event:type=play` &amp; `s:asset:type=ad`
* 광고 완료: `s:event:type=complete` &amp; `s:asset:type=ad`
* 기본 컨텐츠 재생: `s:event:type=play` &amp; `s:asset:type=main` **(예기치 않음)**

* 광고 시작: `s:event:type=start` &amp; `s:asset:type=ad`
* 광고 재생: `s:event:type=play` &amp; `s:asset:type=ad`
* 광고 완료: `s:event:type=complete` &amp; `s:asset:type=ad`
* 기본 컨텐츠 재생: `s:event:type=play` &amp; `s:asset:type=main` **(예상함)**

## 해결 방법

***광고 완료 호출 트리거를 지연시킵니다.***

첫 번째 광고에 대해 `trackEvent:AdComplete`를 늦게 호출한 후 두 번째 광고에 대해 `trackEvent:AdStart`를 바로 호출하여 플레이어 내에서 간격을 처리합니다. 첫 번째 광고가 완료된 후에 `AdComplete` 이벤트 호출 시 앱을 시작하지 않아야 합니다. 광고 브레이크에서 마지막 광고에 대한 `trackEvent:AdComplete`를 호출하십시오. 플레이어가 현재 광고 자산이 광고 브레이크에서 마지막 자산임을 식별할 수 있는 경우 `trackEvent:AdComplete`를 즉시 호출합니다. 이 해결 방법으로 인해 이전 광고 단위와 관련된 추가 광고 소요 시간이 1초 미만이 됩니다.

**프리롤을 포함하여 광고 브레이크 시작 시:**

* 광고 브레이크에 대한 `adBreak` 개체 인스턴스(예: `adBreakObject`)를 만듭니다.

* 호출 `trackEvent(MediaHeartbeat.Event.AdBreakStart, adBreakObject);`.

**모든 광고 자산 시작 시:**

* **호출`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >이전 광고가 완료되지 않은 경우에만 이를 호출합니다. 이전 광고에 대한 &quot;`isinAd`&quot; 상태를 유지 관리하려면 부울 값을 고려하십시오.

* 광고 자산에 대한 광고 개체 인스턴스(예: `adObject`)를 만듭니다.
* 광고 메타데이터, `adCustomMetadata`를 채웁니다.
* 호출 `trackEvent(MediaHeartbeat.Event.AdStart, adObject, adCustomMetadata);`.
* 프리롤 광고 브레이크의 첫 번째 광고인 경우 `trackPlay()`를 호출합니다.

**모든 광고 자산 완료 시:**

* **호출하지 않음**

   >[!NOTE]
   >
   >애플리케이션이 광고 브레이크의 마지막 광고를 알고 있는 경우 여기서 `trackEvent:AdComplete`를 호출하고 `trackEvent:AdBreakComplete`에서 `trackEvent:AdComplete` 설정을 건너뜁니다.

**광고를 건너뛸 때:**

* 호출 `trackEvent(MediaHeartbeat.Event.AdSkip);`.

**광고 브레이크 완료 시:**

* **호출`trackEvent(MediaHeartbeat.Event.AdComplete);`**

   >[!NOTE]
   >
   >이 단계를 마지막 `trackEvent:AdComplete` 호출의 일부로 위에서 이미 수행한 경우에는 건너뛸 수 있습니다.

* 호출 `trackEvent(MediaHeartbeat.Event.AdBreakComplete);`.
