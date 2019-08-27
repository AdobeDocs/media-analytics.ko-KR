---
seo-title: Test 1 Standard 재생
title: Test 1 Standard 재생
uuid: C 4 B 3 FEAD -1 B 27-484 B-AB 6 A -39 F 1 AE 0 F 03 F 2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# 테스트 1: 표준 재생{#test-standard-playback}

이 테스트 케이스는 일반 재생 및 순서를 확인합니다. 이것은 인증 요청의 필수 요소입니다.

## 인증 요청 양식

**여기에서 인증 요청 양식을 다운로드하십시오. = = &gt;**  [Certification Request Form.](cert_req_form.docx)

## Certification Test 1 Overview

미디어 분석 구현에는 두 가지 추적 호출 유형이 포함됩니다.
* Adobe Analytics (appmeasurement) 서버로 직접 호출 - 이러한 호출은 "미디어 시작" 및 "광고 시작" 이벤트에서 발생합니다.
* 미디어 분석 (하트 비트) 서버에 대한 호출 - 여기에는 밴드 내 및 대역 외 호출이 포함됩니다.
   * In-Band - SDK는 컨텐츠 재생 중에 10 초 간격으로 또는 광고를 진행하는 동안 1 초 간격으로 시간 간격 재생 호출 또는 "ping" 를 보냅니다.
   * 대역 외 - 이러한 호출은 모든 시점에서 발생할 수 있으며 일시 중지, 버퍼링, 오류, 컨텐츠 완료, 광고 완료 등을 포함합니다.

>[!NOTE]
>미디어 추적은 모든 플랫폼에서 동일하게 동작합니다.

## 테스트 절차

다음 작업을 완료하여 기록합니다 (순서대로).

1. **페이지 또는 앱 로드**

   **추적 서버**(모든 웹 사이트 및 모바일 앱의 경우):

   * **Adobe Analytics (appmeasurement) 서버 -** Experience Cloud 방문자 ID 서비스를 사용하려면 RDC 추적 서버로 해결되는 RDC 추적 서버 또는 CNAME 이 필요합니다. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **미디어 분석 (하트 비트) 서버 -** 이 서버는 항상 "`[namespace].hb.omtrdc.net`, 여기서 `[namespace]` 회사 이름을 지정합니다. 이 이름은 Adobe에서 제공합니다.
   모든 추적 호출에서 보편화된 특정 주요 변수의 유효성을 확인해야 합니다.

   **Adobe 방문자 ID (`mid`):** `mid` 변수는 AMCV 쿠키에 설정된 값을 캡처하는 데 사용됩니다. `mid` 이 변수는 웹 사이트와 모바일 앱에 대한 기본 식별 값이며, Experience Cloud 방문자 ID 서비스가 올바르게 설정되었음을 나타냅니다. Adobe Analytics (appmeasurement) 와 Media Analytics (하트비트) 호출에서 모두 찾을 수 있습니다.

   * **Adobe Analytics 시작 통화**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **웹 사이트 페이지 호출**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **라이프사이클 호출**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics 시작 통화**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Media Analytics 시작 호출 (`s:event:type=start`) `mid` 값이 없을 수 있습니다. 그래도 괜찮습니다. 미디어 분석 재생 호출 ( `s:event:type=play`) 이 될 때까지 나타나지 않을 수 있습니다.

   * **Media Analytics Play Call**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **미디어 플레이어 시작**

   미디어 플레이어가 시작되면 Media SDK는 다음 순서로 두 서버에 대한 키 호출을 전송합니다.

   1. Adobe Analytics 서버 - 호출 시작
   1. Media Analytics 서버 - 호출 시작
   1. Media Analytics 서버 - "Adobe Analytics 시작 호출 요청"
   위의 처음 두 호출에는 추가 메타데이터 및 변수가 포함되어 있습니다. 호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   위의 세 번째 호출은 미디어 SDK가 Adobe Analytics 시작 호출 (`pev2=ms_s`) 이 Adobe Analytics 서버로 전송되도록 미디어 SDK를 요청합니다.

1. **가능한 경우 광고 브레이크 보기**

   * **광고 시작**
   광고가 시작되면 다음 순서에 따라 다음 키 호출이 전송됩니다.

   1. Adobe Analytics 서버 - 광고 시작 호출
   1. Media Analytics 서버 - 광고 시작 호출
   1. Media Analytics 서버 - "Adobe Analytics Ad Start Call Requested"
   처음 두 호출에는 추가 메타데이터 및 변수가 포함됩니다. 호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   세 번째 호출은 미디어 SDK가 Adobe Analytics 광고 시작 호출 (`pev2=msa_s`) 이 Adobe Analytics 서버로 전송되도록 미디어 SDK를 요청합니다.

   * **광고 재생**

      광고 재생 중에 미디어 분석 SDK는 매 초 "광고" 유형의 play 이벤트를 Media Analytics 서버로 전송합니다.

   * **광고 완료**

      광고 100%에서 미디어 분석 전체 호출을 보내야 합니다.



1. **가능한 경우 30초 동안 광고 재생 일시 정지.**  **광고 일시 정지**

   광고 일시 중지 동안 SDK가 미디어 분석 하트비트 또는 "ping" 호출을 초당 Media Analytics 서버로 보냅니다.

   >[!NOTE]
   >
   >재생 헤드 값은 일시 정지 중에 일정하게 유지되어야 합니다.

   호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **10 분 동안 기본 컨텐츠를 재생할 수 있습니다.**  **컨텐츠 재생**

   기본 컨텐츠 재생 시 미디어 SDK는 10 초마다 하트비트 (재생 호출) 를 Media Analytics 서버로 전송합니다.

   참고:

   * play playhead position should increment by 10 with every play call.
   * `l:event:duration` 값은 마지막 추적 호출 이후의 시간(밀리초)을 나타내며 각 10초 호출에서 거의 동일한 값이어야 합니다.

      호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **재생 도중 적어도 30초 동안 일시 정지.** 미디어 플레이어 일시 중지 시, 일시 중지 이벤트 호출이 SDK에 의해 10 초마다 Media Analytics 서버로 전송됩니다. 일시 정지가 종료되면 재생 이벤트가 재개되어야 합니다.

   호출 매개 변수 및 메타데이터의 경우 테스트 호출 세부 정보를 참조하십시오 [.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **미디어를 검색/스크러빙합니다.** 미디어 재생 헤드를 스크러빙할 때 특별한 추적 호출이 전송되지 않지만, 스크러빙 후에 미디어 재생이 다시 시작되면 재생 헤드 값이 주 컨텐츠 내의 새 위치를 반영해야 합니다.

1. **미디어 재생 (VOD만 해당)** 미디어가 재생될 때 새로운 미디어 시작 호출 세트를 보내야 합니다 (마치 새로 시작한 것처럼).

1. **재생 목록에서 다음 미디어를 봅니다.** 재생 목록에서 다음 미디어의 미디어 시작 시, 새 미디어 시작 호출 세트를 보내야 합니다.

1. **미디어 또는 스트림 전환** 라이브 스트림을 전환할 때 첫 번째 스트림에 대한 미디어 분석 전체 호출을 보내면 안 됩니다. 미디어 시작 호출 및 재생 호출은 새 표시 및 스트림 이름으로 시작되고 새 쇼의 올바른 재생 헤드 및 지속 시간 값으로 시작해야 합니다.

