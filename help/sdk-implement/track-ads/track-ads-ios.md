---
seo-title: iOS에서 광고 추적
title: iOS에서 광고 추적
uuid: E 979 E 679-CDE 5-4 C 30-8 F 34-867 FECEAC 13 A
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# iOS에서 광고 추적{#track-ads-on-ios}

>[!IMPORTANT]
>
>다음 지침은 2. x SDK를 사용한 구현에 대한 지침을 제공합니다. If you are implementing a 1.x version of the SDK, you can download 1.x Developers Guides here: [Download SDKs.](../../sdk-implement/download-sdks.md)

## 광고 추적 상수

| 상수 이름 | 설명   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | AdBreak 시작 이벤트 추적을 위한 상수 |
| `ADBMediaHeartbeatEventAdBreakComplete` | AdBreak 완료 이벤트 추적을 위한 상수 |
| `ADBMediaHeartbeatEventAdStart` | 광고 시작 이벤트 추적을 위한 상수 |
| `ADBMediaHeartbeatEventAdComplete` | 광고 완료 이벤트 추적을 위한 상수 |
| `ADBMediaHeartbeatEventAdSkip` | 광고 건너뛰기 이벤트 추적을 위한 상수 |

## 구현 단계

1. 프리롤을 포함하여 광고 브레이크 경계가 시작되는 시점을 식별하고 광고 브레이크 정보를 사용하여 `AdBreakObject`를 생성합니다.

   `AdBreakObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 프리롤, 미드롤 및 포스트롤과 같은 광고 브레이크 이름입니다. | 예 |
   | `position` | 컨텐츠 내 광고 브레이크의 번호 위치로서, 1로 시작합니다. | 예 |
   | `startTime` | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. | 예 |

   광고 브레이크 개체 작성:

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
   }
   ```

1. 광고가 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   `AdObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 친숙한 광고 이름입니다. | 예 |
   | `adId` | 광고의 고유 식별자. | 예 |
   | `position` | 광고 브레이크 내 광고 번호 위치로서, 1로 시작합니다. | 예 |
   | `length` | 광고 길이 | 예 |

   광고 개체 작성:

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. 선택적으로 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 미디어 추적 세션에 첨부할 수 있습니다.

   * [iOS에서 표준 광고 메타데이터 구현](../../sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **사용자 지정 광고 메타데이터 -**&#x200B;사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고의 데이터로 채웁니다.

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   사용자 지정 메타데이터 변수(또는 빈 개체)에 대한 참조를 이벤트 호출의 세 번째 매개 변수로 포함하십시오.

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

자세한 내용은 추적 시나리오 [프리롤 광고와 함께 VOD 재생](../../sdk-implement/tracking-scenarios/vod-preroll-ads.md)을 참조하십시오.
