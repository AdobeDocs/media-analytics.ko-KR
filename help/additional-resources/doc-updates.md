---
title: 설명서 업데이트
description: null
uuid: 1f3e48df-83b6-418c-8cf7-d7946481f79
index: y
internal: n
snippet: y
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 리소스{#resources}

## 릴리스 노트{#release-notes}

* [릴리스 노트](https://docs.adobe.com/content/help/en/release-notes/experience-cloud/current.html)

## 설명서 업데이트{#documentation-updates}

### Last updated: October, 2019 {#October-2019-update}

다양한 편집 및 서식 수정
Cookbook 주제는 "Media Dimensionside Media Tracking"에 대한 새로운 일반 cookbook 항목을 비롯하여 Media SDK를 넘어 확장되었습니다.


### 최근 업데이트: 2019년 3월 7일 {#March-2019-update}

* 이 업데이트는 주로 JavaScript 및 OTT 플랫폼의 2.2 Media SDK 릴리스를 위한 것입니다.
* JavaScript 및 OTT 플랫폼의 2.2 Media SDK 릴리스는 iOS 및 Android 플랫폼(2018년 11월 1일 업데이트)에 대해 아래에 설명된 것과 동일한 지원을 제공합니다.

### 마지막 업데이트 날짜: 2018년 11월 1일 {#November-2018-update}

* 이 업데이트는 기본적으로 Android 및 iOS 플랫폼에 있는 2.2 Media SDK 릴리스용입니다.
* Android 및 iOS의 2.2 Media SDK 릴리스는 내부 개선 사항과 함께 해당 플랫폼에서의 오디오 추적을 지원합니다.
* 오디오 추적 기능의 추가하여, 이제 Media SDK 및 Media Collection API 모두에서 오디오 추적 기능과 비디오 추적 기능을 모두 사용할 수 있게 되면, 다음과 같이 상대적으로 대규모 이름 지정 업데이트가 필요합니다.

   * 전체적인 솔루션의 제목은 Adobe Analytics for Audio and Video라고 지정됩니다.
   * 이전에 문서 전체에서 사용된 약칭인 "비디오 분석"은 이제 "Media Analytics"입니다.
   * SDK에서 "비디오 하트비트 라이브러리(VHL)"에 대한 참조는 이제 "Media SDK" 입니다.
   * 이전에 "video" 또는 "vhl"을 참조한 파일 이름과 URL(예: API 참조 링크)은 이제 "미디어"를 대신 사용합니다.
   * 코드에서 메타데이터 키의 이름은 "VIDEO" 대신 "MEDIA"를 포함합니다.
   * 등...

* 위와 함께, 표준 메타데이터 구현 및 자체 항목(이전 문서 업데이트의 *코어 추적* 항목에 병합되었음)으로 돌아가는 참조를 포함하여 Media SDK 섹션에 추가적인 재구성이 수행되었습니다. 이 항목들은 *코어 추적*, *찾기 추적* 및 *버퍼링 추적*&#x200B;과 함께 이제 *오디오 및 비디오 재생 추적* 아래에 함께 그룹화되어 있습니다.

* 오디오 추적과 관련된 새로운 매개 변수를 반영하기 위해 Federated Analytics 양식이 버전 3.2로 업데이트되었습니다.

### 업데이트: 2018년 10월 10일 {#October-2018-update}

* 일반적인 추적 항목 아래의 하위 섹션에 제시된 플랫폼별 추적 예제와 함께, 개별(대개 동일함) 플랫폼 구현 안내를 하나의 SDK 구현 섹션에 결합함으로써 문서 구조를 SDK 구현 영역에서 "리팩터링"했습니다.
* 새 문서 시스템으로의 마이그레이션이 예상되어 파일의 이름을 대대적으로 변경했습니다. 각 개념, 참조 및 작업 주제 유형을 나타내는 모든 DITA 접두사( c_, r_, t_ ) 가 제거되었습니다. 모든 밑줄( '_')을 하이픈( '-')으로 대체했습니다. 또한 파일 이름은 이제 항목의 제목과 거의 유사합니다.
* 일반 유효성 검사 및 인증 항목 업데이트.
* 전제 조건, 구현 경로 및 Audience Manager 지원과 함께 측정 선택 사항 프레젠테이션을 포함한 새로운 소개 자료.
* 오디오 분석 기능의 추가를 반영하여 지표 및 메타데이터 및 보고 및 분석 섹션 업데이트.
