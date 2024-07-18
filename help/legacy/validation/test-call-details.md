---
title: 테스트 호출 세부 사항
description: 구현의 유효성을 확인하기 위해 수행해야 하는 호출에 대해 살펴봅니다.
uuid: d3a0e62f-2fc3-413d-ac56-adbbc9b3e983
exl-id: 5e167714-3f0c-4afa-b171-7d51cff6522e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 100%

---

# 테스트 호출 세부 사항{#test-call-details}

## 미디어 플레이어 시작 {#start-the-media-player}

### Adobe Analytics(AppMeasurement) 시작 호출 {#aa-start-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| _**`a.media.name`**_ | _**123456**_ |
| _**`a.media.length`**_ | _**120**_ |
| `a.media.playerName` | HTML5 |
| _**`a.media.view`**_ | _**true**_ |
| `a.contentType` | vod |
| _**`custom.[value]`**_ | _**사용자 지정 메타데이터 필드**_ |
| _**`a.media.[value]`**_ | _**표준 메타데이터 필드**_ |

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 선형 스트림의 길이는 현재 표시에 대한 최상의 예상 값으로 설정해야 합니다.

### Adobe Analytics(AppMeasurement) 시작 호출의 표준 메타데이터 {#std-metadata-aa}

| 매개 변수 |  값(샘플)  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016년 7월 4일 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics(AppMeasurement) 시작 호출의 사용자 지정 메타데이터 {#custom-metadata-aa}

| 매개 변수 |  값(샘플)  |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

### Media Analytics(하트비트) 시작 호출 {#ma-start-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| `s:event:type` | start |
| _**`l:event:playhead`**_ | _**0**_ |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| _**`s:meta:custom.[value]`**_ | _**사용자 지정 메타데이터 필드**_ |
| _**`s:meta:a.media.[value]`**_ | _**표준 메타데이터 필드**_ |

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 비디오 시작 시 선형 스트림의 플레이헤드 위치는 0이 아니라, 현재 프로그램의 시작 이후 경과된 시간(초)으로 설정해야 합니다.

### Media Analytics(하트비트) 시작 호출의 표준 메타데이터 {#std-metadata-ma}

| 매개 변수 |  값(샘플)  |
|---|---|
| `s:meta:a.media.show` | 표시 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018년 7월 4일 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics(하트비트) 시작 호출의 사용자 지정 메타데이터 {#custom-metadata-ma}

| 매개 변수 |  값(샘플)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics(하트비트) Adobe Analytics 시작 호출의 {#ma-aa-start}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**aa_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**참고:**

* 이 호출은 Media SDK가 Adobe Analytics(AppMeasurement) 서버로 Adobe Analytics `pev2=ms_s` 호출을 전송하도록 요청했음을 나타냅니다.
* 이 호출은 사용자 지정 메타데이터를 포함하지 않습니다.

## 광고 재생 보기 {#view-ad-playback}

### Adobe Analytics(AppMeasurement) 광고 시작 호출 {#aa-ad-start-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`pev2`**_ | _**msa_s**_ |
| `a.media.name` | 123456 |
| _**`a.media.ad.name`**_ | _**9378**_ |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| _**`a.media.ad.length`**_ | _**15**_ |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| _**`a.media.ad.view`**_ | _**참**_ |
| _**`custom.[value]`**_ | _**메타데이터 필드**_ |
| _**`a.media.[value]`**_ | _**표준 메타데이터 필드**_ |

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 광고 시작 시 사용할 수 없는 경우 광고 길이는 -1로 설정할 수 있습니다.

### Adobe Analytics(AppMeasurement) 광고 시작 호출의 표준 메타데이터 {#std-metadata-aa-ad-start}

| 매개 변수 |  값(샘플)  |
|---|---|
| `a.media.show` | Show Title |
| `a.media.season` | 6 |
| `a.media.episode` | Episode Title |
| `a.media.asset_id` | 123456 |
| `a.media.genre` | comedy |
| `a.media.first_air_date` | 2016년 7월 4일 |
| `a.media.rating` | TV-14 |
| `a.media.originator` | production house |
| `a.media.network` | network |
| `a.media.ad_load` | 1 |
| `a.media.mvpd` | mvpd |
| `a.media.authorized` | unlocked |
| `a.media.feed` | no feed |
| `a.media.stream_format` | 0 |

### Adobe Analytics(AppMeasurement) 광고 시작 호출의 사용자 지정 메타데이터 {#custom-metadata-aa-ad-start}

| 매개 변수 |  값(샘플)  |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### Media Analytics(하트비트) 광고 시작 호출 {#ma-ad-start-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| _**`l:asset:length`**_ | _**120**_ |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |
| _**`s:meta:custom.[value]`**_ | _**사용자 지정 메타데이터 필드**_ |
| _**`s:meta:a.media.[value]`**_ | _**표준 메타데이터 필드**_ |

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 광고 시작 시 사용할 수 없는 경우 광고 길이는 -1로 설정할 수 있습니다.

### Media Analytics(하트비트) 광고 시작 호출의 표준 메타데이터 {#std-metadata-ma-ad-start}

| 매개 변수 |  값(샘플)  |
|---|---|
| `s:meta:a.media.show` | 표시 |
| `s:meta:a.media.season` | 6 |
| `s:meta:a.media.episode` | Episode Title |
| `s:meta:a.media.asset_id` | 123456 |
| `s:meta:a.media.genre` | comedy |
| `s:meta:a.media.first_air_date` | 2018년 7월 4일 |
| `s:meta:a.media.rating` | TV-14 |
| `s:meta:a.media.originator` | production house |
| `s:meta:a.media.network` | network |
| `s:meta:a.media.ad_load` | 1 |
| `s:meta:a.media.mvpd` | mvpd |
| `s:meta:a.media.authorized` | unlocked |
| `s:meta:a.media.feed` | no feed |
| `s:meta:a.media.stream_format` | 0 |

### Media Analytics(하트비트) 광고 시작 호출의 사용자 지정 메타데이터 {#custom-metadata-ma-ad-start}

| 매개 변수 |  값(샘플)  |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### Media Analytics(하트비트) Adobe Analytics 광고 시작 호출 {#ma-aa-ad-start-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**aa_ad_start**_ |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### Media Analytics(하트비트) 광고 재생 호출 {#ma-ad-play-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**play**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics(하트비트) 광고 일시 중지 호출 {#ma-ad-pause-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

### Media Analytics(하트비트) Adobe Analytics 광고 전체 호출 {#ma-aa-ad-complete-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**complete**_ |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| _**`s:asset:type`**_ | _**ad**_ |

## 주 콘텐츠 재생 {#play-main-content}

### Media Analytics(하트비트) 재생 호출 {#ma-play-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| `s:event:type` | play |
| _**`l:event:playhead`**_ | _**29**_ |
| _**`l:event:duration`**_ | _**10189**_ |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**참고:**

* 플레이헤드 위치는 모든 재생 호출에서 10초씩 증가해야 합니다.
* `l:event:duration` 값은 마지막 추적 호출 이후의 시간(밀리초)을 나타내며 각 10초 호출에서 거의 동일한 값이어야 합니다.

## 기본 콘텐츠 일시 중지 {#pause-main-content}

### Media Analytics(하트비트) 일시 중지 호출 {#ma-pause-call}

| 매개 변수 |  값(샘플)  |
|---|---|
| _**`s:event:type`**_ | _**pause**_ |
| _**`l:event:playhead`**_ | _**29**_ |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
