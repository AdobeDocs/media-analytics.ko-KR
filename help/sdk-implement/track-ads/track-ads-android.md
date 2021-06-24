---
title: Android에서 광고를 추적하는 방법 알아보기
description: Media SDK를 사용하여 Android 애플리케이션에서 광고 추적을 구현합니다.
uuid: 4a4249fb-dc39-4947-a14d-a51d972f32d4
exl-id: 1f96dde9-c924-4fce-8b14-7dec7137f265
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 98%

---

# Android에서 광고 추적{#track-ads-on-android}

>[!IMPORTANT]
>
>다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다. SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/sdk-implement/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 광고 추적 상수

| 상수 이름 | 설명 |
| --- | --- |
| `MediaHeartbeat.Event.AdBreakStart` | AdBreak 시작 이벤트 추적을 위한 상수 |
| `MediaHeartbeat.Event.AdBreakComplete` | AdBreak 완료 이벤트 추적을 위한 상수 |
| `MediaHeartbeat.Event.AdStart` | 광고 시작 이벤트 추적을 위한 상수 |
| `MediaHeartbeat.Event.AdComplete` | 광고 완료 이벤트 추적을 위한 상수 |
| `MediaHeartbeat.Event.AdSkip` | 광고 건너뛰기 이벤트 추적을 위한 상수 |

## 구현 단계

1. 프리롤을 포함하여 광고 브레이크 경계가 시작되는 시점을 식별하고 광고 브레이크 정보를 사용하여 `AdBreakObject`를 생성합니다.

   `AdBreakObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 프리롤, 미드롤 및 포스트롤과 같은 광고 브레이크 이름입니다. | 예 |
   | `position` | 컨텐츠 내 광고 브레이크의 번호 위치로서, 1로 시작합니다. | 예 |
   | `startTime` | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. | 예 |

   광고 브레이크 개체 작성:

   ```java
   MediaObject adBreakInfo =  
     MediaHeartbeat.createAdBreakObject(<ADBREAK_NAME>,  
                                        <POSITION>,  
                                        <START_TIME>);
   ```

1. 광고 브레이크 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdBreakStart`를 사용하여 `trackEvent()`를 호출합니다.

   ```java
   public void onAdBreakStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakStart,  
                             adBreakInfo,  
                             null); 
   }
   ```

1. 광고가 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   `AdObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 친숙한 광고 이름. | 예 |
   | `adId` | 광고의 고유 식별자. | 예 |
   | `position` | 광고 브레이크 내 광고 번호 위치로서, 1로 시작합니다. | 예 |
   | `length` | 광고 길이 | 예 |

   광고 개체 작성:

   ```java
   MediaObject adInfo =  
     MediaHeartbeat.createAdObject(<AD_NAME> 
                                   <AD_ID>,  
                                   <POSITION>,  
                                   <LENGTH>);
   ```

1. 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 미디어 추적 세션에 첨부합니다.

   * [Android에서 표준 광고 메타데이터 구현](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-android.md)
   * **사용자 지정 광고 메타데이터 -**&#x200B;사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고의 데이터로 채웁니다.

      ```java
      // Setting Ad Metadata 
      HashMap<String, String> adMetadata = new HashMap<String, String>(); 
      adMetadata.put("affiliate", "Sample affiliate"); 
      adMetadata.put("campaign", "Sample ad campaign");
      ```

1. 광고 재생 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdStart` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   사용자 지정 메타데이터 변수(또는 빈 개체)에 대한 참조를 이벤트 호출의 세 번째 매개 변수로 포함하십시오.

   ```java
   public void onAdStart(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdStart,  
                             adInfo,  
                             adMetadata); 
   }
   ```

1. 광고 재생이 광고 끝에 도달하면 `AdComplete` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   ```java
   public void onAdComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdComplete, null, null); 
   }
   ```

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.

   ```java
   public void onAdSkip(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdSkip, null, null); 
   }
   ```

1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

   ```java
   public void onAdBreakComplete(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.AdBreakComplete, null, null); 
   }
   ```

자세한 내용은 추적 시나리오 [프리롤 광고와 함께 VOD 재생](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)을 참조하십시오.
