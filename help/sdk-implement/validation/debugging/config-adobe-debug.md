---
title: Adobe Debug 구성
description: 이 항목에서는 Media SDK 구현 문제를 해결하는 데 사용할 수 있는 Adobe Debug를 구성하는 방법을 설명합니다.
uuid: e416458d-f23c-41ce-8d99-fa5076c455f0
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Adobe Debug 구성{#configure-adobe-debug}

## Adobe Debug에 액세스 {#accessing-adobe-debug}

Adobe Debug에 액세스하려면 다음을 수행하십시오.

1. 새 Adobe Experience Cloud 사용자를 [Experience Cloud](https://www.marketing.adobe.com)로 이동하여 생성합니다.

   >[!TIP]
   >
   >이 로그인은 Adobe Analytics에 로그인하는 데 사용하는 사용자 이름/암호와 다릅니다.

1. Experience Cloud 계정이 있는 경우 Adobe 담당자에게 Adobe Debug에 대한 액세스를 요청하십시오.
1. 액세스 권한이 부여되면 [https://debug.adobe.com](https://debug.adobe.com)으로 이동하여 Experience Cloud 자격 증명을 사용하여 로그인하십시오.

   ![](assets/adobe-debug-login.png)

   이 도구에 대해 지원되는 브라우저는 다음과 같습니다.
   * Google Chrome
   * Mozilla Firefox
   * Apple Safari
   * Microsoft Internet Explorer 버전 9~11

권장되는 브라우저는 최신 Chrome 및 Firefox 버전입니다.

## 디버그 프록시 {#debug-proxy}

디버그 프록시를 다운로드하고 구성합니다.

1. 디버그 프록시 앱을 [앱 다운로드](https://debug.adobe.com/#/downloads)에서 다운로드합니다.

   지원되는 운영 체제는 다음과 같습니다.
   * OS X 10.7 64비트 이상
   * Windows 7.1 64비트 이상
   ![](assets/debug-proxy-app.png)

1. 디버그 프록시 서버는 포트 33284의 로컬 시스템에서 실행되며 시스템 프록시로 설정됩니다.

   OS 및 브라우저를 기반으로 하여 브라우저 설정을 조정해야 할 수 있습니다.

## 데스크탑 또는 앱에 SSL 인증서 다운로드 및 설치 {#download-and-install-sSL-desktop}

Adobe Debug를 처음 실행하면 고유한 SSL 인증서가 생성됩니다. 데스크톱 및/또는 앱에서 HTTPS 트래픽을 지원하는 경우 SSL 인증서를 다운로드하여 설치해야 합니다.

SSL 인증서를 다운로드하고 설치합니다:

1. Adobe Debug가 설치되고 시작되면 [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)로 이동하여 인증을 다운로드합니다.
1. 인증서를 가져옵니다

   **Mac OS**
   1. 루트 CA 인증서를 두 번 클릭하여 키체인 접근에서 엽니다.
   1. 루트 CA 인증서가 로그인에 나타납니다.
   1. 루트 CA 인증서를 시스템으로 이동(드래그)합니다.
   1. 모든 사용자 및 로컬 시스템 프로세스에서 신뢰할 수 있도록 인증서를 시스템에 복사해야 합니다.
   1. 루트 CA 인증서를 열고 신뢰를 확장한 다음 [항상 신뢰]를 선택하고 변경 사항을 저장합니다.
   **Windows**
   1. 다음 절차 중 하나를 완료하십시오.

      * [로컬 컴퓨터에 대한 신뢰할 수 있는 루트 인증 기관 저장소에 인증서 추가](https://technet.microsoft.com/ko-kr/library/cc754841.aspx#BKMK_addlocal)
<!--        * [How To Import a Trusted Root Certification Authority In Windows 7/Vista/XP](https://www.sqlservermart.com/HowTo/Windows_Import_Certificate.aspx) You might need to quit and reopen your browser to see the change.
-->

    1. Firefox의 경우 [Mozilla Firefox에 루트 인증서 설치]의 절차를 완료합니다.](https://wiki.wmtransfer.com/projects/webmoney/wiki/Installing_root_certificate_in_Mozilla_Firefox)
    
    변경 내용을 보려면 Firefox를 종료했다가 다시 열어야 할 수 있습니다.
    
    **iOS 장치**
    1. **[!UICONTROL 설정 앱]** **&gt;** **[!UICONTROL Wi-Fi 설정]**을 클릭하여 Adobe Debug를 해당 HTTP 프록시로 사용하도록 iOS 장치를 설정합니다.
    
    1. Safari에서 [Debug로 이동합니다.](https://proxy.debug.adobe.com/ssl)
    
    Safari에서 SSL 인증서를 설치하라는 메시지를 표시합니다.

## 모바일 장치에 대한 SSL 인증서 설치 {#install-sSL-for-mobile-device}

Adobe Debug에서 HTTPS 호출을 놓친 경우 모바일 장치에서 Adobe Debug용 SSL 인증서를 설치해야 합니다.

### iOS

iOS 장치에 SSL 인증서를 설치하려면 다음을 수행하십시오.

1. 랩톱에서 디버그 프록시를 켜고 [Adobe Debug](https://debug.adobe.com)로 이동합니다.
1. iOS 장치에서 다음 단계를 완료합니다.
   1. 장치를 비행기 모드로 전환합니다.
   1. 랩톱에서 사용한 동일한 Wi-Fi 신호를 선택합니다.
   1. 랩톱에서 디버그 프록시 앱에 표시된 IP 및 포트를 수동으로 설정합니다.
   1. Apple Safari 브라우저 창을 엽니다.
   1. [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)로 이동합니다.
   1. SSL 인증서를 다운로드하고 설치합니다.

1. 랩톱에서 Adobe Debug 세션을 시작합니다.
1. iOS 장치에서 테스트를 시작합니다.

### Android

Android 장치에 SSL 인증서를 설치하려면 다음을 수행하십시오.

1. 노트북에서 디버그 프록시를 켜고 [Adobe Debug](https://debug.adobe.com)로 이동합니다.
1. Android 장치에서 다음 단계를 완료합니다.
   1. 장치를 비행기 모드로 설정합니다.
   1. 랩톱에서 사용한 동일한 Wi-Fi 신호를 선택합니다.
   1. 랩톱에서 디버그 프록시 앱에 표시된 IP 및 포트를 수동으로 설정합니다.
   1. 브라우저 창을 엽니다.
   1. [https://proxy.debug.adobe.com/ssl](https://proxy.debug.adobe.com/ssl)로 이동합니다.
   1. SSL 인증서를 다운로드하고 설치합니다.

1. 랩톱에서 Adobe Debug 세션을 시작합니다.
1. Android 장치에서 테스트를 시작합니다.

