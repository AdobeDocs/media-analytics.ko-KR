---
seo-title: 테스트 호출 세부 사항
title: 테스트 호출 세부 사항
uuid: D 3 A 0 E 62 F -2 FC 3-413 D-AC 56-ADBBC 9 B 3 E 983
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 테스트 호출 세부 사항{#test-call-details}

## 비디오 플레이어 시작 {#section_qts_xff_f2b}

### Media Analytics 시작 통화

| 매개 변수 | 값(샘플)   |
|---|---|
| `pev2` | ms_s |
| `a.media.friendlyName` | Episode Title |
| `a.media.name` | 123456 |
| `a.media.length` | 120 |
| `a.media.playerName` | HTML5 |
| `a.media.view` | true |
| `a.contentType` | vod |
| `custom.[value]` | 사용자 지정 메타데이터 필드 |
| `a.media.[value]` | 표준 메타데이터 필드 |

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 선형 스트림의 길이는 현재 표시에 대한 최상의 예상 값으로 설정해야 합니다.

### Media Analytics 시작 호출의 표준 메타데이터

| 매개 변수 | 값(샘플)   |
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

### 하트비트 시작 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |
| `s:meta:custom.[value]` | 사용자 지정 메타데이터 필드 |
| `s:meta:a.media.[value]` | 표준 메타데이터 필드 |

### Media Analytics 시작 호출의 미디어 메타데이터

| 매개 변수 | 값(샘플)   |
|---|---|
| `custom.metadataA` | value |
| `custom.metadataB` | value |

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 비디오 시작 시 선형 스트림의 플레이헤드 위치는 0이 아니라, 현재 프로그램의 시작 이후 경과된 시간(초)으로 설정해야 합니다.

### 하트비트 분석 시작 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | aa_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

### 하트비트 시작 호출의 미디어 메타데이터

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 하트비트 시작 호출의 표준 메타데이터

| 매개 변수 | 값(샘플)   |
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

**참고:**

* 이 호출은 하트비트 라이브러리가 분석 서버에 분석 pev2=ms_s 호출을 보내도록 요청했음을 나타냅니다.
* 이 호출은 사용자 지정 메타데이터를 포함하지 않습니다.

## 광고 재생 보기 {#section_wz3_yff_f2b}

### Media Analytics 광고 시작 통화

| 매개 변수 | 값(샘플)   |
|---|---|
| `pev2` | msa_s |
| `a.media.name` | 123456 |
| `a.media.ad.name` | 9378 |
| `a.media.ad.friendlyName` | Video_VPAID_DFA |
| `a.media.ad.podFriendlyName` | preroll |
| `a.media.ad.length` | 15 |
| `a.media.ad.playerName` | HTML5 |
| `a.media.ad.pod` | c27aaf3ff8224bb6b9ebfe1b2e79073d_1 |
| `a.media.ad.podPosition` | 1 |
| `a.media.ad.podSecond` | 0.0 |
| `a.media.ad.view` | True |
| `custom.[value]` | 메타데이터 필드 |
| `a.media.[value]` | 표준 메타데이터 필드 |

**참고:** 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.

### 하트비트 광고 시작 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 4 |
| `s:asset:ad_id` | 9378 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |
| `s:meta:custom.[value]` | 사용자 지정 메타데이터 필드 |
| `s:meta:a.media.[value]` | 표준 메타데이터 필드 |

### Media Analytics 광고 시작 호출의 미디어 메타데이터

| 매개 변수 | 값(샘플)   |
|---|---|
| `custom.metadata` | value |
| `custom.metadata` | value |

### 미디어 분석 광고 시작 호출의 표준 메타데이터

| 매개 변수 | 값(샘플)   |
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

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 광고 시작 시 사용할 수 없는 경우 광고 길이는 -1로 설정할 수 있습니다.

### 하트비트 분석 광고 시작 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | aa_ad_start |
| `l:event:playhead` | 0 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### 하트비트 광고 시작 호출의 미디어 메타데이터

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:meta:custom.metadata` | value |
| `s:meta:custom.metadata` | value |

### 하트비트 광고 시작 호출의 표준 메타데이터

| 매개 변수 | 값(샘플)   |
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

**참고:**

* 추가적인 컨텍스트 데이터 변수가 있고 이 변수가 메타데이터를 포함해야 합니다. 아래의 메타데이터 세부 사항을 참조하십시오.
* 광고 시작 시 사용할 수 없는 경우 광고 길이는 -1로 설정할 수 있습니다.

### 하트비트 광고 완료 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | complete |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

### 하트비트 광고 재생 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 15 |
| `l:event:duration` | 0 |
| `s:asset:ad_id` | 9378 |
| `l:asset:ad_length` | 15 |
| `s:stream:type` | vod |
| `s:asset:type` | ad |

## 주 컨텐츠 재생 {#section_u1l_1gf_f2b}

### 하트비트 재생 호출

| 매개 변수 | 값(샘플)   |
|---|---|
| `s:event:type` | play |
| `l:event:playhead` | 29 |
| `l:event:duration` | 10189 |
| `s:asset:name` | Episode Title |
| `s:asset:video_id` | 123456 |
| `l:asset:length` | 120 |
| `s:stream:type` | vod |
| `s:asset:type` | main |

**참고:**

* 플레이헤드 위치는 모든 재생 호출에서 10씩 증가해야 합니다.
* `l:event:duration` 값은 마지막 추적 호출 이후의 시간(밀리초)을 나타내며 각 10초 호출에서 거의 동일한 값이어야 합니다.

