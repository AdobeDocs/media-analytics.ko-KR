---
title: 테스트 1 표준 재생
description: 이 항목에서는 유효성 검사에 사용되는 표준 재생 테스트에 대해 설명합니다.
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 테스트 1: 표준 재생{#test-standard-playback}

이 테스트 케이스는 일반적인 재생 및 시퀀스의 유효성을 검사합니다. 인증 요청의 필수 요소입니다.

## 인증 요청 양식

**여기에서 인증 요청 양식을 다운로드하십시오.==&gt;**&#x200B;인증 [요청 양식.](cert_req_form.docx)

## 인증 테스트 1 개요

Media Analytics 구현에는 두 가지 유형의 추적 호출이 포함됩니다.
* Adobe Analytics(AppMeasurement) 서버에 직접 수행된 호출 - 이러한 호출은 "미디어 시작" 및 "광고 시작" 이벤트에서 발생합니다.
* Media Analytics(하트비트) 서버에 대한 호출 - 여기에는 인밴드 및 대역 외 호출이 포함됩니다.
   * 인밴드 - SDK는 컨텐츠 재생 도중 10초 간격으로, 광고 도중 1초 간격으로 시간 재생 호출 또는 "핑"을 전송합니다.
   * 대역 외 - 이러한 호출은 언제든지 발생할 수 있으며 일시 중지, 버퍼링, 오류, 컨텐츠 완료, 광고 완료 등을 포함합니다.

>[!NOTE]
>미디어 추적은 모든 플랫폼에서 동일하게 작동합니다.

## 테스트 절차

다음 작업을 완료하고 순서대로 기록합니다.

1. **페이지 또는 앱 로드**

   **추적 서버**(모든 웹 사이트 및 모바일 앱의 경우):

   * **Adobe Analytics(AppMeasurement) 서버 - Experience** Cloud 방문자 ID 서비스에 대해 RDC 추적 서버로 확인되는 RDC 추적 서버 또는 CNAME이 필요합니다. The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics(하트비트) 서버 - 이** 서버는 항상 "`[namespace].hb.omtrdc.net`" 형식을 가지며, 여기서 회사 이름을 `[namespace]` 지정합니다. 이 이름은 Adobe에서 제공합니다.
   모든 추적 호출에 공통으로 적용되는 특정 키 변수의 유효성을 확인해야 합니다.

   **`mid`Adobe 방문자 ID(**):이 `mid` 변수는 AMCV 쿠키에 설정된 값을 캡처하는 데 사용됩니다. The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. Adobe Analytics(AppMeasurement)와 Media Analytics(하트비트) 호출 모두에 있습니다.

   * **Adobe Analytics 시작 호출**

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

   * **미디어 분석 시작 호출**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >Media Analytics 시작 호출(`s:event:type=start`)에서 `mid` 값이 없을 수 있습니다. 그래도 괜찮습니다. Media Analytics Play 호출( `s:event:type=play`)이 될 때까지 나타나지 않을 수 있습니다.

   * **미디어 분석 재생 호출**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **미디어 플레이어 시작**

   미디어 플레이어가 시작되면 Media SDK는 다음 순서로 두 서버에 키 호출을 전송합니다.

   1. Adobe Analytics 서버 - 시작 호출
   1. Media Analytics 서버 - 시작 호출
   1. Media Analytics 서버 - "Adobe Analytics 시작 호출 요청"
   위의 처음 두 호출에는 추가 메타데이터와 변수가 포함됩니다. 호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   위의 세 번째 호출은 Media Analytics 서버에 Adobe Analytics 시작 호출(`pev2=ms_s`)을 Adobe Analytics 서버로 보내도록 미디어 SDK가 요청했음을 알려줍니다.

1. **가능한 경우 광고 브레이크 보기**

   * **광고 시작**
   광고가 시작되면 다음 키 호출이 순서대로 전송됩니다.

   1. Adobe Analytics 서버 - 광고 시작 호출
   1. Media Analytics 서버 - 광고 시작 호출
   1. Media Analytics 서버 - "Adobe Analytics 광고 시작 호출이 요청됨"
   처음 두 호출에는 추가 메타데이터와 변수가 포함됩니다. 호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   세 번째 호출은 Media Analytics 서버에 Media SDK가 Adobe Analytics 광고 시작 호출(`pev2=msa_s`)을 Adobe Analytics 서버로 보내도록 요청했음을 알려줍니다.

   * **광고 재생**

      광고 재생 중에 Media Analytics SDK는 "광고" 유형의 재생 이벤트를 매초마다 Media Analytics 서버로 보냅니다.

   * **광고 완료**

      광고의 100% 지점에서 미디어 분석 완료 호출을 전송해야 합니다.



1. **가능한 경우 30초 동안 광고 재생 일시 정지.**  **광고 일시 정지**

   광고 일시 중지 동안 SDK에서 미디어 분석 하트비트 또는 "핑" 호출을 매 초마다 Media Analytics 서버로 보냅니다.

   >[!NOTE]
   >
   >재생 헤드 값은 일시 중지 동안 상수로 유지되어야 합니다.

   호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **중단 없이 10분 동안 주요 컨텐츠를 재생할 수 있습니다.**  **컨텐츠 재생**

   기본 컨텐츠 재생 중에 Media SDK는 10초마다 하트비트(재생 호출)를 Media Analytics 서버로 전송합니다.

   참고:

   * 재생 헤드 위치는 Play 호출마다 10씩 증가합니다.
   * `l:event:duration` 값은 마지막 추적 호출 이후의 시간(밀리초)을 나타내며 각 10초 호출에서 거의 동일한 값이어야 합니다.

      호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **재생 도중 적어도 30초 동안 일시 정지.** 미디어 플레이어를 일시 중지하면, 일시 중지 이벤트 호출은 SDK에서 10초마다 Media Analytics 서버로 전송됩니다. 일시 정지가 종료되면 재생 이벤트가 재개되어야 합니다.

   호출 매개 변수 및 메타데이터에 대해서는 호출 세부 [사항 테스트를 참조하십시오.](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **미디어 검색/스크러빙** 그러나 스크러빙 후 미디어 재생이 다시 시작되면 미디어 재생 헤드 값이 기본 컨텐츠 내의 새 위치를 반영해야 하는 경우 미디어 재생 헤드를 스크러빙할 때 특수 추적 호출이 전송되지 않습니다.

1. **미디어 재생(VOD만 해당).** 미디어를 재생하면 새 미디어 시작 호출 세트를 새로 시작하는 것처럼 보내야 합니다.

1. **재생 목록에서 다음 미디어 보기** 재생 목록에서 다음 미디어의 미디어 시작에서 새 미디어 시작 호출 집합을 보내야 합니다.

1. **미디어 또는 스트림 전환** 실시간 스트림을 전환할 때 첫 번째 스트림에 대한 Media Analytics 전체 호출을 전송하지 않아야 합니다. 미디어 시작 호출 및 재생 호출은 새 쇼 및 스트림 이름과 새 쇼의 재생 헤드 및 지속 시간 값으로 시작해야 합니다.

