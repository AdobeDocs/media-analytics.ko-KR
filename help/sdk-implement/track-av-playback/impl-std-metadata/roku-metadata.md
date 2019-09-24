---
seo-title: Roku 메타데이터 키
title: Roku 메타데이터 키
uuid: 2ca6bb1d-c545-43d3-9c3e-63b890aa268d
translation-type: tm+mt
source-git-commit: 959ff714d3546a06123293cac8a17b94fae1c1ff

---


# Roku 메타데이터 키{#roku-metadata-keys}

표준 비디오, 오디오 및 광고 메타데이터는 각각 미디어 및 광고 정보 개체에 설정할 수 있습니다. 비디오/광고 메타데이터에 상수 키를 사용하여 추적 API를 호출하기 전에 정보 개체에 표준 메타데이터를 포함하는 사전을 설정합니다. 아래 표에서 표준 메타데이터 상수의 전체 목록과 샘플을 참조하십시오.

## 비디오 메타데이터 상수 {#section_D26B0478688D4DC5AEFD82E9AC0F0C0D}

| 메타데이터 이름 | 컨텍스트 데이터 키 | 상수 이름 |
| --- | --- | --- |
| 표시 | `a.media.show` | `MEDIA_VideoMetadataKeySHOW` |
| 시즌 | `a.media.season` | `MEDIA_VideoMetadataKeySEASON` |
| 에피소드 | `a.media.episode` | `MEDIA_VideoMetadataKeyEPISODE` |
| 자산 | `a.media.asset` | `MEDIA_VideoMetadataKeyASSET_ID` |
| 장르 | `a.media.genre` | `MEDIA_VideoMetadataKeyGENRE` |
| 최초 방송 날짜 | `a.media.airDate` | `MEDIA_VideoMetadataKeyFIRST_AIR_DATE` |
| 최초 디지털 방송 날짜 | `a.media.digitalDate` | `MEDIA_VideoMetadataKeyFIRST_DIGITAL_DATE` |
| 등급 | `a.media.rating` | `MEDIA_VideoMetadataKeyRATING` |
| 작성자 | `a.media.originator` | `MEDIA_VideoMetadataKeyORIGINATOR` |
| 네트워크 | `a.media.network` | `MEDIA_VideoMetadataKeyNETWORK` |
| 표시 유형 | `a.media.type` | `MEDIA_VideoMetadataKeySHOW_TYPE` |
| 광고 로드 | `a.media.adLoad` | `MEDIA_VideoMetadataKeyAD_LOAD` |
| MVPD | `a.media.pass.mvpd` | `MEDIA_VideoMetadataKeyMVPD` |
| 인증됨 | `a.media.pass.auth` | `MEDIA_VideoMetadataKeyAUTHORIZED` |
| 방송 시간대 | `a.media.dayPart` | `MEDIA_VideoMetadataKeyDAY_PART` |
| 피드 | `a.media.feed` | `MEDIA_VideoMetadataKeyFEED` |
| 스트림 형식 | `a.media.format` | `MEDIA_VideoMetadataKeySTREAM_FORMAT` |

## Audio metadata constants {#audio-metadata-constants}

| 메타데이터 이름 | 컨텍스트 데이터 키 | 상수 이름 |
| --- | --- | --- |
| 아티스트 | `a.media.artist` | `MEDIA_AudioMetadataKeyARTIST` |
| 앨범 | `a.media.album` | `MEDIA_AudioMetadataKeyALBUM` |
| 레이블 | `a.media.label` | `MEDIA_AudioMetadataKeyLABEL` |
| Author | `a.media.author` | `MEDIA_AudioMetadataKeyAUTHOR` |
| 방송국 | `a.media.station` | `MEDIA_AudioMetadataKeySTATION` |
| 게시자 | `a.media.publisher` | `MEDIA_AudioMetadataKeyPUBLISHER` |

## 광고 메타데이터 상수 {#section_5290E1BA54A24D30875F4F55C6CF9458}

| 메타데이터 이름 | 컨텍스트 데이터 키 | 상수 이름 |
| --- | --- | --- |
| 광고주 | `a.media.ad.advertiser` | `MEDIA_AdMetadataKeyADVERTISER` |
| 캠페인 ID | `a.media.ad.campaign` | `MEDIA_AdMetadataKeyCAMPAIGN_ID` |
| 광고 ID | `a.media.ad.creative` | `MEDIA_AdMetadataKeyCREATIVE_ID` |
| 게재위치 ID | `a.media.ad.placement` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| 사이트 ID | `a.media.ad.site` | `MEDIA_AdMetadataKeyPLACEMENT_ID` |
| 광고 URL | `a.media.ad.creativeURL` | `MEDIA_AdMetadataKeyCREATIVE_URL` |

## 상수 {#section_F55145DBE77F45B988849C42C044C7DA}

다음 상수를 사용하여 미디어 이벤트를 추적할 수 있습니다.

### 기타 상수

| 상수 | 설명   |
|---|---|
| `ERROR_SOURCE_PLAYER` | 플레이어의 오류 소스에 대한 상수 |

### MediaObjectkey 상수(MediaObject 인스턴스 내의 키로 사용됨)

| 상수 | 설명   |
| --- | --- |
| `MEDIA_STANDARD_MEDIA_METADATA` | Constant to set metadata on the  `MediaInfo``trackLoad` |
| `MEDIA_STANDARD_AD_METADATA` | Constant to set the ad metadata on the `EventData``trackEvent` |
| `MEDIA_RESUMED` | 비디오가 재개된 하트비트를 전송하기 위한 상수입니다. To resume video tracking of previously stopped content, you need to set the `MEDIA_RESUMED` property on the `mediaInfo` object when you call `mediaTrackLoad`. (`MEDIA_RESUMED` is not an event that you can track using the `mediaTrackEvent` API.) `MEDIA_RESUMED`는 사용자가 시청을 중단했지만 현재 시청을 재개하려는 컨텐츠를 애플리케이션이 계속 추적하려는 경우 true로 설정해야 합니다. <br/><br/>예를 들어, 사용자가 컨텐츠의 30%를 시청한 다음 앱을 닫는다고 가정합니다. 이 경우 세션이 종료됩니다. Later, if the same user returns to the same content, and the application allows that user to resume from the same point where they left off, then the application should set `MEDIA_RESUMED` to "true" while calling the `mediaTrackLoad` API. 결국 동일한 비디오 컨텐츠에 대해 서로 다른 두 개의 미디어 세션을 함께 연결할 수 있습니다. 다음은 구현 예제입니다. <br/><br/> `mediaInfo =` <br/>   `adb_media_init_mediainfo(` <br/>     `"test_media_name",` <br/>     `"test_media_id",`<br/>      `10,` <br/>     `"vod"` <br/> `)` <br/> `mediaInfo[ADBMobile().MEDIA_RESUMED] = true` <br/> `mediaContextData = {}` <br/>  `ADBMobile().mediaTrackLoad(mediaInfo, mediaContextData)` <br/><br/>이렇게 하면 비디오에 대한 새 세션이 생성되지만, SDK가 이벤트 유형이 "이력서"인 하트비트 요청을 전송하게 됩니다. 이 이벤트 유형은 두 개의 서로 다른 미디어 세션을 함께 연결하여 보고하는 데 사용할 수 있습니다. |

### 컨텐츠 유형 상수

| 상수 | 설명   |
|---|---|
| `MEDIA_STREAM_TYPE_LIVE` | 스트림 유형 LIVE에 대한 상수 |
| `MEDIA_STREAM_TYPE_VOD` | 스트림 유형 VOD에 대한 상수 |

### 이벤트 유형 상수(trackEvent 호출에 사용됨)

| 상수 | 설명   |
|---|---|
| `MEDIA_BUFFER_START` | 버퍼 시작에 대한 이벤트 유형 |
| `MEDIA_BUFFER_COMPLETE` | 버퍼 완료에 대한 이벤트 유형 |
| `MEDIA_SEEK_START` | 찾기 시작에 대한 이벤트 유형 |
| `MEDIA_SEEK_COMPLETE` | 찾기 완료에 대한 이벤트 유형 |
| `MEDIA_BITRATE_CHANGE` | 비트율 변경에 대한 이벤트 유형 |
| `MEDIA_CHAPTER_START` | 챕터 시작에 대한 이벤트 유형 |
| `MEDIA_CHAPTER_COMPLETE` | 챕터 완료에 대한 이벤트 유형 |
| `MEDIA_CHAPTER_SKIP` | 광고 시작에 대한 이벤트 유형 |
| `MEDIA_AD_BREAK_START` | 광고 시작에 대한 이벤트 유형 |
| `MEDIA_AD_BREAK_COMPLETE` | 광고 브레이크 완료에 대한 이벤트 유형 |
| `MEDIA_AD_BREAK_SKIP` | 광고 브레이크 건너뛰기에 대한 이벤트 유형 |
| `MEDIA_AD_START` | 광고 시작에 대한 이벤트 유형 |
| `MEDIA_AD_COMPLETE` | 광고 완료에 대한 이벤트 유형 |
| `MEDIA_AD_SKIP` | 광고 건너뛰기에 대한 이벤트 유형 |

