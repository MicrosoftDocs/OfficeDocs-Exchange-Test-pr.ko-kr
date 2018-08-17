---
title: 'Outlook Web App에 대 한 테마 만들기: Exchange 2013 Help'
TOCTitle: Outlook Web App에 대 한 테마 만들기
ms:assetid: 7e1fa13c-3de3-45c2-b1fa-e74fc8487bda
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201700(v=EXCHG.150)
ms:contentKeyID: 54651826
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App에 대 한 테마 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

*테마* , 배경색, 글꼴, 강조 표시 색상, 아이콘, 및 MicrosoftOutlook Web App 에서 사용 되는 머리글을 정의 합니다. 각 테마는 미디어 파일 및 MicrosoftExchange 서버 \\Client Access\\OWA\\prem\\*version*\\resources\\themes에서 설치 디렉터리에 저장 된 계단식 스타일 시트 (.css) 파일의 컬렉션입니다. 각 테마 \\themes의 자체의 하위 디렉터리에 저장 됩니다.

기본 테마 \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base에서 발견 됩니다. 각 테마 폴더에 테마를 정의 하는 데 필요한 모든 파일을 포함 합니다. 이러한 파일 CSS 파일, 그래픽 및 테마의 이름을 정의 하는.xml 파일을 포함 합니다. 추가 테마를 새 폴더로 하나의 테마에서 모든 파일을 복사 하 고 필요에 따라 해당 파일을 수정 하 여 만들어집니다.

기본적으로 Exchange Server 2013을 설치할 때 다음과 같이 여러 테마가 설치됩니다.

  - CSS(.css) 파일은 색, 그라데이션 및 글꼴을 정의합니다.

  - 이미지(.png) 파일은 아이콘 및 기타 그래픽 요소를 제공합니다. 아이콘을 편집할 경우 크기는 변경하지 마십시오. 그래픽 요소의 크기를 변경한 경우 변경 내용을 테스트하여 요소 크기가 잘 맞는지 확인하십시오.

이러한 파일은 \\Client Access\\OWA\\prem\\*\<version\>*\\resources\\themes에서 설치 디렉터리에 대 한 클라이언트 액세스 서버에 저장 됩니다. 각 테마는 테마의 하위 디렉터리에 저장 됩니다. 기존 테마를 복사 하 여 복사본을 수정 하 여 추가 테마를 만들 수 있습니다.

테마를 만든 후 [Outlook Web App 로그인, 언어 선택 및 오류 페이지를 사용자 지정](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)할 수도 있습니다.


> [!NOTE]
> Outlook Web App Light 버전은 테마를 지원하지 않습니다.




> [!WARNING]
> Outlook Web App을 지원하는 여러 서버가 있는 경우 각 서버에 사용자 지정 테마를 복사해야 합니다. 또한 사용자 지정 테마의 백업 복사본을 만들어야 합니다. Exchange를 다시 설치하거나 업그레이드한 경우 테마 폴더의 모든 파일을 덮어씁니다. 재설치 또는 업그레이드가 완료된 후 테마를 해당 폴더로 다시 복사해야 합니다.<BR>사용자 지정 테마를 만들기 전에 변경할 모든 파일의 백업 복사본을 만듭니다.



## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 60분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 가상 디렉터리" 항목

  - 이 절차를 수행하려면 로컬 서버 관리자 액세스 권한이 있어야 합니다.

  - 기본 색을 변경 하려면 텍스트 편집기 및 이미지를 변경 하려면 그래픽 편집기 필요 합니다. 특정 색과 일치 해야 하는 경우는 일치 하는 것에 대 한 [색상표](https://go.microsoft.com/fwlink/p/?linkid=280679)에서 찾을 수 없는 색상을 샘플링 하 고 HTML RGB 값을 결정 하려면 편집 도구 이미지를 사용할 수 있습니다.

  - Outlook Web App 테마를 변경하거나 만들 때 모범 사례로서 다음 지침을 따르는 것이 가장 좋습니다.
    
      - 기존 테마를 편집하기로 결정한 경우 편집하기 전에 원본 파일의 백업 복사본을 만듭니다.
    
      - 폴더 \\Client Access\\OWA\\prem\\*version*\\resources\\themes\\base 또는 그 안에 파일 중 하나를 삭제 하지 마십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 어떻게 해야 합니까?

## 1단계: 새로운 Outlook Web App 테마 만들기

시작하려면 새 테마의 폴더를 만들고 기존 테마에서 새 폴더로 파일을 복사합니다.

1.  로컬 관리자 그룹의 구성원을 위임받은 계정을 사용하여 Outlook Web App 가상 디렉터리를 호스트하는 Exchange 서버에 로그온합니다.

2.  Windows 탐색기를 열고 Exchange 서버 설치 디렉터리를 찾습니다.

3.  \\Client Access\\OWA\\prem\\*version*\\resources\\themes에서 새 폴더를 만들고 이름을, Fourth Coffee 예입니다.

4.  또 다른 테마에서 새 폴더로 모든 파일을 복사합니다.

## 2단계: 새 테마 이름 지정

새 테마의 표시 이름을 설정하려면 다음을 수행합니다.

1.  방금 만든 사용자 지정 테마 폴더에 있는 themeinfo.xml 복사본을 엽니다.

2.  테마 `displayname` 값을 찾아 사용 하려는 이름에 값을 변경 합니다. 예 `displayname = "Fourth Coffee Theme"`합니다.

3.  themeinfo.xml을 저장하고 닫습니다.

## 3단계: 새 테마의 정렬 순서 변경(옵션)

원하는 경우 themeinfo.xml 파일을 편집하여 새 테마의 정렬 순서를 변경할 수 있습니다. 정렬 순서에 따라 \[설정\] 메뉴의 **테마 변경** 패널에 표시되는 테마 위치가 결정됩니다.

themeinfo.xml 파일을 사용하여 새 테마의 정렬 순서를 변경하려면 다음을 수행합니다.

1.  사용자 지정 테마 폴더에 있는 themeinfo.xml 복사본을 엽니다.

2.  테마 `sortorder` 값을 찾아 목록에 표시 하 여 새 테마를 원하는 위치를 반영 하도록 값을 변경 합니다. 숫자 값 오름차순으로 정렬 하 여 테마를 주문 합니다. 기본적으로 행 1의 기본 테마 및 그 `sortorder` 값은 "0"입니다. 예 `sortorder="<number>"`합니다.

3.  themeinfo.xml을 저장하고 닫습니다.

## 4단계: 새 테마 수정

이제 파일을 복사하고 테마의 이름을 지정했으면 파일을 사용자 지정할 수 있습니다. Outlook Web App 테마에서 다음과 같은 요소를 사용자 지정할 수 있습니다.

  - 이미지 파일(헤더 영역 및 아이콘 정의)

  - CSS 파일(글꼴 및 색 정의)

## 이미지 파일

테마 이미지는 \\themes*\\\<테마 이름\>*\\images\\에 저장됩니다. \\images\\0 폴더에는 왼쪽에서 오른쪽으로 읽는 언어(예: 영어)에서 사용되는 이미지가 포함되며, 오른쪽에서 왼쪽으로 읽는 언어에서는 \\images\\rtl 폴더의 이미지가 사용됩니다.


> [!NOTE]
> \images\rtl 폴더의 일부 이미지는 \images\0 폴더의 이미지와 같으며, 이러한 이미지는 미러링됩니다.



테마를 사용자 지정하려면 이미지 편집 도구를 사용하여 다음 이미지를 열고 수정하면 됩니다.

  - Headerbgmain.png
    
      - 기본 헤더 이미지입니다. 이미지는 30픽셀의 헤더 높이를 초과하지 않는 것이 좋습니다. 기본 테마에서는 배경 이미지가 사용되지 않으므로 이 이미지는 투명합니다. 사용자 지정 배경 이미지가 있는 테마 예를 보려면 **Blueprint** 테마 폴더의 이미지를 참조하십시오.

  - Headerbgright.png
    
      - 헤더 뒤의 바둑판식 배열 이미지로 사용됩니다. 기본 테마에서는 바둑판식 배열 배경 이미지가 사용되지 않으므로 이 이미지는 투명합니다. 사용자 지정 바둑판식 배열 배경 이미지가 있는 테마 예를 보려면 **Blueprint** 테마 폴더의 이미지를 참조하십시오.

  - sprite1.mouse.png
    
      - 테마에 사용된 대부분의 이미지가 포함됩니다. 테마와 일치하도록 이미지 색을 변경할 수 있으며 기본 Outlook Web App 텍스트 로고도 변경할 수 있습니다.
    
      - 문제를 방지하려면 스프라이트에서 개별 아이콘의 크기를 변경하지 마십시오. 그리고 투명한 .png 파일로 저장되었는지 확인하십시오.

  - themepreview.png
    
      - 이 이미지는 Outlook Web App의 \[설정\] 메뉴에 있는 **테마 변경** 패널의 테마를 나타내는 데 사용됩니다.

## 색 및 글꼴

CSS 스타일시트(.css 파일) 파일은 테마에 사용되는 글꼴 및 색을 정의하며, \\themes\\*\<테마 이름\>* 아래의 여러 폴더에 저장됩니다. \\*\<테마 이름\>*\\0 폴더에는 왼쪽에서 오른쪽으로 읽는 언어(예: 영어)에서 사용되는 이미지가 포함되며, 오른쪽에서 왼쪽으로 읽는 언어에서는 \\*\<테마 이름\>*\\rtl 폴더의 .css 파일이 사용됩니다. 해당 언어에서 사용할 .css 파일이 포함된 언어별 폴더(예: \\ja, \\ko, \\zhs 및 \\zht)도 있습니다.

수정 하 여 시작 된 \\*\<theme name\>*\\images\\0 폴더입니다. 사용자 지정할 수 있는 각 테마 전체에서 사용 되는 4 개의 색상 있습니다.

  - BrandColor: \#0072C6

  - NavBarHoverColor: \#4C9CD7

  - UnreadColor: \#2A8DD4

  - FocusColor: \#DFEDFA

메모장과 같은 텍스트 편집기를 사용하여 이러한 값의 인스턴스를 모두 찾아 두 파일 즉 owa2styles.mouseCSS 및 owa2styles2.mouseCSS의 테마 색으로 대체할 수 있습니다. 이 작업은 해당 .css 파일이 있는 새 테마의 모든 폴더에서 수행되어야 합니다.

## 5단계: 기본 Outlook Web App 테마 설정

새 기본 테마를 설정하면 Outlook Web App의 \[설정\] 메뉴를 통해 테마를 변경하지 않은 사용자에게만 영향을 줍니다.

모든 사용자가 기본 테마를 사용하도록 하려면 기본 테마 설정 이외에도 테마 선택을 사용할 수 없도록 설정해야 합니다.

## 셸을 사용하여 Outlook Web App에 대한 기본 테마 설정

이 예에서는 Outlook Web App의 기본 테마를 설정합니다. 여기서 서버 이름은 `fourthcoffee`이고 가상 디렉터리 이름은 `owa`이며, 웹 사이트 이름은 `default web site`이고 테마는 `Custom` 폴더에 있습니다.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom 

구문과 매개 변수에 대한 자세한 내용은 [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 Outlook Web App 테마 선택을 사용하지 않도록 설정

이 예에서는 Outlook Web App의 테마 선택을 사용하지 않도록 설정합니다. 여기서 서버 이름은 `fourthcoffee`이고 가상 디렉터리 이름은 `owa`이며 웹 사이트 이름은 `default web site`입니다.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -themeselectionenabled $false 

다음 예와 같이 두 명령을 동시에 완료할 수도 있습니다.

    set-owavirtualdirectory -identity "fourthcoffee\owa (default web site)" -defaulttheme Custom -themeselectionenabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\))를 참조하십시오.

## 6단계: iisreset/noforce를 실행하여 변경 사항 저장

테마를 추가하거나 변경한 경우, 테마 이름을 변경한 경우 또는 테마 정렬 순서를 변경한 경우 변경 내용을 적용하려면 IIS(인터넷 정보 서비스)를 중지한 다음 다시 시작해야 합니다. 이 작업을 수행하려면 새 테마를 만든 서버에서 명령 프롬프트 창을 열고 **iisresest /nforce** 명령을 실행합니다.

## 이 작업의 작동 여부는 어떻게 확인합니까?

1.  새 테마를 만든 서버의 가상 디렉터리를 사용하여 Outlook Web App에 로그인합니다. Outlook Web App 가상 디렉터리를 호스트하는 Exchange 서버의 기본 웹 사이트에 대한 변경 내용을 테스트하려면 Internet Explorer을 열어 URL https://localhost/owa를 입력합니다.

2.  \[설정\] 메뉴 \> **테마 변경**을 선택하고 사용자 지정 테마를 선택하여 사용자 지정 테마로 전환합니다.

## 최신 변경 내용이 표시되지 않을 경우 iisreset/noforce 실행

1.  Internet Explorer 도구 모음에서 \[설정\] 메뉴 \> **인터넷 옵션**을 선택합니다.

2.  **일반** 탭에서 **검색 기록** 아래의 **삭제**를 선택한 후 **임시 인터넷 파일 및 웹 사이트 파일**이 선택되어 있는지 확인합니다. 그런 다음 **삭제**를 선택하여 해당 파일을 제거합니다.

3.  **확인**을 클릭하여 **인터넷 옵션**을 닫습니다.

4.  **새로 고침**을 선택하여 변경 내용을 확인합니다.

테마 파일을 변경할 때마다 이 단계를 반복하여 변경 내용을 확인해야 할 수 있습니다. 여러 항목을 변경한 경우 Outlook Web App을 열어두고 서버에서 **iisreset/noforce** 실행 및 Internet Explorer의 임시 파일 지우기(필요한 경우)를 반복할 수 있습니다.

