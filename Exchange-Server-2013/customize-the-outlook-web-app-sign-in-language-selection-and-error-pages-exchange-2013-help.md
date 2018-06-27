---
title: 'Outlook Web App 로그인, 언어 선택 및 오류 페이지를 사용자 지정: Exchange 2013 Help'
TOCTitle: Outlook Web App 로그인, 언어 선택 및 오류 페이지를 사용자 지정
ms:assetid: d8d9f735-7181-428f-9049-b9886dce5159
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633483(v=EXCHG.150)
ms:contentKeyID: 54651829
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 로그인, 언어 선택 및 오류 페이지를 사용자 지정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 색 및 이미지는 로그인, 언어 선택 및 Outlook Web App 에 대 한 오류 페이지의 사용자 지정 하는 방법에 설명 합니다.

Outlook Web App 로그인 사람, 언어 선택 및 오류 페이지 테마 리소스 폴더의 그래픽 및.css 파일에 따라 만들어집니다. Outlook Web App 모든 테마에 대 한 로그인, 언어 선택 및 오류 페이지 집합이 하나만 사용합니다. 이러한 페이지에 대 한 수정 내용은 모든 사용자에 게 표시 됩니다. V15\\FrontEnd\\HttpProxy\\owa\\auth\\version\\themes\\resources에서 Exchange 설치 디렉터리에서 테마 리소스 폴더를 찾을 수 있습니다. 기본 색을 변경 하려면 텍스트 편집기 및 이미지를 변경 하려면 그래픽 편집기 필요 합니다. 특정 색과 일치 해야 하는 경우는 일치 하는 것에 대 한 [색상표](https://go.microsoft.com/fwlink/p/?linkid=280679)에서 찾을 수 없는 색상을 샘플링 하 고 HTML RGB 값을 결정 하려면 편집 도구 이미지를 사용할 수 있습니다.

Outlook Web App 를 지 원하는 여러 서버가 있는 하도록 하려면 모든 동일한 로그인 사람, 언어 및 오류 페이지를 사용 하는 경우에 각 서버에 수정 된 파일을 복사 해야 합니다. 사용자 지정 된 파일의 백업 복사본을 만들어야 합니다. 다시 설치 또는 Exchange를 업그레이드 하는 경우 테마 폴더에 있는 모든 파일을 덮어씁니다. 다시 설치한 후 사용자 지정 된 파일의 적절 한 폴더로 복사 해야 또는 업그레이드를 완료 합니다.


> [!IMPORTANT]
> 사용자 지정 로그인 및 로그 아웃 페이지를 만드는 시작 하기 전에 변경 될 것 이라고 모든 파일의 복사본을 백업 합니다.



사용자 지정 테마 만들기 (영문) 하는 방법에 대 한 정보를 [Outlook Web App에 대 한 테마 만들기](create-a-theme-for-outlook-web-app-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 45분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 의 "Outlook Web App 사용 권한"에서 "그래픽 편집기" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 로그인 페이지의 색을 사용자 지정

1.  Exchange 서버에 로그온 하 고 Windows 탐색기를 사용 하 여 Exchange 서버 설치 디렉터리로 이동 하 고 \< 버전 \> \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\ \\themes\\resources를 찾습니다.

2.  메모장과 같은 텍스트 편집기를 사용 하 여 logon.css를 엽니다.

3.  기본 색상 값 \#0072 c 6 검색 및 사용 하 여 사용할 색에 대 한 HTML RGB 값으로 대체 합니다. HTML RGB 여기에 값을 찾을 수: [색상표](https://go.microsoft.com/fwlink/p/?linkid=280679)합니다.

4.  파일을 저장하고 닫습니다.

## 오류 페이지의 색을 사용자 지정

1.  Exchange 서버에 로그온 하 고 Windows 탐색기를 사용 하 여 Exchange 서버 설치 디렉터리로 이동 하 고 \< 버전 \> \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\ \\themes\\resources를 찾습니다.

2.  메모장과 같은 텍스트 편집기를 사용 하 여 errorFE.css를 엽니다.

3.  기본 색상 값 \#0072 c 6 검색 및 사용 하 여 사용할 색에 대 한 HTML RGB 값으로 대체 합니다. HTML RGB 여기에 값을 찾을 수: [색상표](https://go.microsoft.com/fwlink/p/?linkid=280679)합니다.

4.  파일을 저장하고 닫습니다.

## 언어 선택 페이지의 색을 사용자 지정

1.  Exchange 서버에 로그온 하 고 Windows 탐색기를 사용 하 여 Exchange 서버 설치 디렉터리로 이동 하 고 \\V15\\Client Access\\OWA\\version\\Owa2\\resources\\styles를 찾습니다.

2.  메모장과 같은 텍스트 편집기를 사용 하 여 LanguageSelection.css를 엽니다.

3.  기본 색상 값 \#0072 c 6 검색 및 사용 하 여 사용할 색에 대 한 HTML RGB 값으로 대체 합니다. HTML RGB 여기에 값을 찾을 수: [색상표](https://go.microsoft.com/fwlink/p/?linkid=280679)합니다.

4.  파일을 저장하고 닫습니다.

## 로그인 하 고 오류 페이지에 이미지를 사용자 지정

이미지 편집 도구를 사용 하 여 열고 로그인 하 고 오류 페이지를 작성 하는데 사용 되는 이미지를 편집 합니다.

1.  Exchange 서버에 로그온 하 고 Windows 탐색기를 사용 하 여 Exchange 서버 설치 디렉터리로 이동 하 고 \< 버전 \> \\V15\\FrontEnd\\HttpProxy\\owa\\auth\\ \\themes\\resources를 찾습니다.

2.  그래픽 편집기를 사용 하 여 연 다음 파일을 수정 합니다.
    
      - owa\_text\_blue.png, "Outlook Web App" 텍스트 로고를 변경할 수 있습니다.
    
      - olk\_logo\_white.png 왼쪽된 표시줄에 응용 프로그램 로고를 변경할 수 있습니다.
    
      - olk\_logo\_white\_cropped.png 오류 페이지의 왼쪽 패널에서 이미지를 변경할 수 있습니다.
    
      - 아이콘 변경 하려면 sign\_in\_arrow.png "로그인" 단추 왼쪽입니다.
    
      - olk\_exchange\_text\_blue.png tnarrow 레이아웃에 "Outlook Mobile" 로고를 변경할 수 있습니다.
    
      - olk\_logo\_white\_small.png은 tnarrow에 사용 됩니다.
    
      - olk\_exchange\_text\_stacked\_white\_small.png은 tnarrow에 사용 됩니다.

3.  기본 색상 값 \#0072 c 6 검색 및 사용 하 여 사용할 색에 대 한 HTML RGB 값으로 대체 합니다. HTML RGB 여기에 값을 찾을 수: [색상표](https://go.microsoft.com/fwlink/p/?linkid=280679)합니다.

4.  파일을 저장하고 닫습니다.

## 작동 여부는 어떻게 확인합니까?

Internet Explorer에서 Outlook Web App 로그인 페이지를 엽니다. Outlook Web App 가상 디렉터리를 호스팅하는 서버의 기본 웹사이트에 변경 내용을 테스트 하는 경우에 Internet Explorer를 열고 URL https://localhost/owa를 입력 하 여 테스트할 수 있습니다.

변경 내용을 보이지 않으면 다음을 수행 합니다.

1.  도구 모음에서 **설정** 을 선택 \> **인터넷 옵션** \> **일반** 합니다.

2.  **검색 기록** **삭제** 를 선택 합니다.

3.  **임시 인터넷 파일 및 웹사이트 파일을** 선택한 다음 **삭제** 를 선택 합니다.

4.  Internet Explorer **인터넷 옵션** 을 닫힐 때까지 삭제, select **확인** 을 완료 되 면 합니다.

5.  브라우저 창을 새로 고쳐 합니다.


> [!TIP]
> 변경 내용을의 효과 보려면 편집 중인.css 파일을 열어 수 있으며 각 변경 내용을 저장 한 후 브라우저 창을 새로 고쳐 키를 누릅니다.


