---
title: Roku에서 광고를 추적하는 방법 알아보기
description: Media SDK를 사용하여 Roku 애플리케이션에서 광고 추적을 구현합니다.
uuid: b1567265-7043-4efa-a313-aaaa91c4bb01
exl-id: aaed828d-1aba-486e-83e3-2ffd092305e2
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 97%

---

# Roku에서 광고 추적{#track-ads-on-roku}

다음은 2.x SDK를 사용하는 구현과 관련된 지침입니다.

>[!IMPORTANT]
>
>SDK의 1.x 버전을 구현하는 경우 [SDK 다운로드](/help/getting-started/download-sdks.md)에서 1.x 개발자 안내서를 다운로드할 수 있습니다.

## 광고 추적 상수

| 상수 이름 | 설명   |
|---|---|
| `AdBreakStart` | AdBreak 시작 이벤트 추적을 위한 상수 |
| `AdBreakComplete` | AdBreak 완료 이벤트 추적을 위한 상수 |
| `AdStart` | 광고 시작 이벤트 추적을 위한 상수 |
| `AdComplete` | 광고 완료 이벤트 추적을 위한 상수 |
| `AdSkip` | 광고 건너뛰기 이벤트 추적을 위한 상수 |

## 구현 단계

1. 프리롤을 포함하여 광고 브레이크 경계가 시작되는 시점을 식별하고 광고 브레이크 정보를 사용하여 `AdBreakObject`를 생성합니다.

   `AdBreakObject` 참조:

   | 변수 이름 | 설명 | 필수 여부 |
   | --- | --- | :---: |
   | `name` | 프리롤, 미드롤 및 포스트롤과 같은 광고 브레이크 이름입니다. | 예 |
   | `position` | 1로 시작하는 광고 브레이크의 번호 위치입니다. | 예 |
   | `startTime` | 광고 브레이크의 시작 위치에 있는 플레이헤드 값입니다. | 예 |

   ```
   ‘ Create an adbreak info object
   adBreakInfo = adb_media_init_adbreakinfo()
   adBreakInfo.name = <ADBREAK_NAME>
   adBreakInfo.startTime = <START_TIME>
   adBreakInfo.position = <POSITION>
   ```

1. 광고 브레이크 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdBreakStart`를 사용하여 `trackEvent()`를 호출합니다.

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_START, adBreakInfo, contextData)
   ```

1. 광고 자산이 시작되는 시기를 식별하고, 광고 정보를 사용하여 `AdObject` 인스턴스를 만듭니다.

   ```
   adInfo =  
     adb_media_init_adinfo(ad.title,  
                           ad.id,  
                           ad.position,  
                           ad.duration)
   ```

1. 원할 경우 컨텍스트 데이터 변수를 통해 표준 및/또는 광고 메타데이터를 미디어 추적 세션에 첨부합니다.

   * [Roku에서 표준 광고 메타데이터 구현](/help/use-cases/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-roku.md)
   * **사용자 지정 광고 메타데이터 -**&#x200B;사용자 지정 메타데이터의 경우 사용자 지정 데이터 변수에 대한 변수 개체를 만들고, 현재 광고 자산의 데이터로 채웁니다.

      ```
      contextData = {}
      contextData["adinfo1"] = "adinfo2"
      contextData["adinfo2"] = "adinfo2"
      ```

1. 광고 재생 추적을 시작하려면 `MediaHeartbeat` 인스턴스에서 `AdStart` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_START, adInfo, contextData)
   ```

1. 광고 자산 재생이 광고 끝에 도달하면 `AdComplete` 이벤트를 사용하여 `trackEvent()`를 호출합니다.

   ```
   standardAdMetadata = {}
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_COMPLETE, adInfo, contextData)
   ```

1. 사용자가 광고를 건너뛰도록 선택했기 때문에 광고 재생이 완료되지 않은 경우 `AdSkip` 이벤트를 추적합니다.

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_AD_SKIP, adInfo, contextData
   ```

1. 같은 `AdBreak` 내에 추가 광고가 있는 경우 3~7단계를 다시 반복합니다.
1. 광고 브레이크가 완료되면 `AdBreakComplete` 이벤트를 사용하여 추적합니다.

   ```
   contextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_AD_BREAK_COMPLETE, adBreakInfo, contextData)
   ```

자세한 내용은 추적 시나리오 [프리롤 광고와 함께 VOD 재생](/help/use-cases/tracking-scenarios/vod-preroll-ads.md)을 참조하십시오.
