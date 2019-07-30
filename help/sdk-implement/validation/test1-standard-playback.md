---
seo-title: Test 1 Standard 재생
title: Test 1 Standard 재생
uuid: C 4 B 3 FEAD -1 B 27-484 B-AB 6 A -39 F 1 AE 0 F 03 F 2
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 테스트 1: 표준 재생{#test-standard-playback}

이 테스트 케이스는 일반 재생 및 순서 지정을 인증하며 인증 요청 양식의 일부로 필요합니다. 여기에서 인증 요청 양식을 다운로드:[ 인증 요청 양식.](cert_req_form_nielsen.docx)

비디오 구현은 다음과 같은 유형의 추적 호출로 구성됩니다.
* 비디오 및 광고 시작 호출은 AppMeasurement 서버에 직접 전송됩니다.
* 미디어 분석 (MA) 하트비트 호출은 Adobe VA 추적 서버로 10 초마다 전송됩니다.

>[!NOTE]
>비디오 추적은 모든 플랫폼, 데스크톱 및 모바일에서 동일하게 작동합니다.

다음 순서로 작업을 완료하고 기록해야 합니다.

1. **페이지 또는 앱 로드**

   **추적 서버**(모든 웹 사이트 및 모바일 앱의 경우):

   * **AppMeasurement(Adobe Analytics) -** RDC 서버로 확인되는 RDC 추적 서버 또는 CNAME이 Experience Cloud 방문자 ID 서비스에 필요합니다. The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **미디어 분석 (하트 비트) -** 이 서버는 항상 형식을 `[namespace].hb.omtrdc.net`가지며, 여기서 `[namespace]` 로그인 회사에 의해 정의되며 Adobe가 제공합니다.
   모든 추적 호출에서 특정 주요 범용 변수의 유효성을 검사해야 합니다:

   **Adobe 방문자 ID (`mid`):** `mid` 변수는 AMCV 쿠키에 설정된 값을 캡처하는 데 사용됩니다. `mid` 이 변수는 웹 사이트와 모바일 앱에 대한 기본 식별 값이며, Experience Cloud 방문자 ID 서비스가 올바르게 설정되었음을 나타냅니다. Appmeasurement 및 MA (Media Analytics) 호출에서 모두 찾을 수 있습니다.

   * **하트비트 재생 호출**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics 시작 통화**

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

   * **하트비트 시작 호출**

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `s:event:type` | start |

   * **VA 시작 호출**

      >[!NOTE]
      >
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. 그래도 괜찮습니다. They may not appear until the VA Play Calls ( `s:event:type=play`).

      | 매개 변수 | 값(샘플) |
      |---|---|
      | `pev2` | ms_s |


1. **비디오 플레이어 시작**

   비디오 플레이어가 시작되면 다음 순서로 주요 호출이 전송됩니다.

   1. 비디오 분석 시작
   1. 하트비트 시작
   1. 하트비트 분석 시작
   위의 처음 두 호출에는 추가 메타데이터 및 변수가 포함되어 있습니다. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **가능한 경우 광고 브레이크 보기**

   * **광고 시작**
   비디오 광고가 시작되면 다음 주요 호출이 다음 순서로 전송됩니다.

   1. 비디오 광고 분석 시작
   1. 하트비트 광고 시작
   1. 하트비트 광고 분석 시작
   처음 두 호출에는 추가 메타데이터 및 변수가 포함됩니다. For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **광고 재생**

      광고 재생 중에 하트비트 호출은 매초마다 하트비트 서버로 전송됩니다.

   * **광고 완료**

      비디오 광고의 100% 포인트에서 하트비트 전체 호출이 전송됩니다.



1. **가능한 경우 30초 동안 광고 재생 일시 정지.**  **광고 일시 정지**

   광고 일시 중지 중에 하트비트 호출은 매초마다 하트비트 서버로 전송됩니다.

   >[!NOTE]
   >
   >재생 헤드 값은 일시 정지 중에 일정하게 유지되어야 합니다.

1. **10분 동안 중단 없이 기본 컨텐츠 비디오 재생.** **컨텐츠 재생 **

   기본 컨텐츠 재생 중에 하트비트 호출은 10초마다 하트비트 서버로 전송됩니다.

   참고:

   * 플레이헤드 위치는 모든 재생 호출에서 10씩 증가해야 합니다.
   * `l:event:duration` 값은 마지막 추적 호출 이후의 시간(밀리초)을 나타내며 각 10초 호출에서 거의 동일한 값이어야 합니다.

      For call parameters and metadata, see [Test call details](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **재생 도중 적어도 30초 동안 일시 정지.** 비디오 플레이어를 일시 정지하면 일시 정지 이벤트 호출이 10초마다 전송됩니다. 일시 정지가 종료되면 재생 이벤트가 재개되어야 합니다.

1. **비디오 탐색/스크럽.** 비디오 플레이헤드를 스크럽할 때 특수 추적 호출이 전송되지 않지만, 스크럽 후 비디오 재생이 재개될 때는 플레이헤드 값이 기본 컨텐츠 내의 새로운 위치를 반영해야 합니다.

1. **비디오 재생(vod만 해당).** 비디오가 재생되면 새로운 비디오 시작 호출 세트가 새로운 비디오 보기인 것처럼 전송됩니다.

1. **재생 목록의 다음 비디오 보기.** 재생 목록의 다음 비디오 시작 시 새로운 비디오 시작 호출 세트가 전송되어야 합니다.

1. **비디오 또는 스트림 전환.** 라이브 스트림을 전환할 때 첫 번째 스트림에 대한 하트비트 전체 호출이 전송되지 않아야 합니다. 비디오 시작 호출 및 비디오 재생 호출은 새로운 프로그램 및 스트림 이름과 새로운 프로그램에 대한 올바른 플레이헤드 및 기간 값으로 시작해야 합니다.

