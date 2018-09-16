---
title: 'Outlook Web App 가상 디렉터리 보기 또는 구성: Exchange 2013 Help'
TOCTitle: Outlook Web App 가상 디렉터리 보기 또는 구성
ms:assetid: 90babcf6-4486-4e01-9819-6d3ca4ed756c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298140(v=EXCHG.150)
ms:contentKeyID: 50483646
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App 가상 디렉터리 보기 또는 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-08-12_

EAC 또는 셸을 사용하여 Outlook Web App 가상 디렉터리의 속성을 보거나 구성할 수 있습니다.

> [!CAUTION]
> Exchange Online에서 관리자는 Outlook Web App 가상 디렉터리를 보거나 구성할 수 없습니다.


셸을 사용하여 Outlook Web App 가상 디렉터리의 속성을 보는 경우 반환되는 정보는 사용할 수 있는 정보의 하위 집합입니다. 예를 들어 **Get-OWAVirtualDirectory** cmdlet을 사용하여 속성을 보는 경우 Exchange에서 반환되는 정보는 다음과 같습니다.

  - 가상 디렉터리 이름

  - 서버 이름

  - Exchange 서버 버전

사용 가능한 매개 변수를 사용하여 특정 서버의 특정 가상 디렉터리에 대한 정보를 검색할 수도 있습니다. **Get-OWAVirtualDirectory** cmdlet 매개 변수에 대한 자세한 내용은 [Get-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/aa998588\(v=exchg.150\))를 참조하십시오.

EAC를 사용하여 Outlook Web App 가상 디렉터리의 속성을 보는 경우 해당 가상 디렉터리의 속성 대부분을 볼 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "Outlook Web App 가상 디렉터리" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Web App 가상 디렉터리 속성 보기 또는 구성

1.  EAC에서 **서버** \> **가상 디렉터리**를 클릭합니다.
    
    드롭다운 목록을 사용하여 서버 및 가상 디렉터리 유형을 선택할 수 있습니다. 기본적으로 모든 서버 및 가상 디렉터리가 표시됩니다.

2.  결과 창에서 보거나 편집하려는 가상 디렉터리를 클릭하여 선택하고 **편집**을 클릭합니다.

3.  **일반** 탭에서 Outlook Web App 기본 웹 사이트의 속성을 보고 외부 URL과 내부 URL을 지정할 수 있습니다. 다음 옵션을 보거나 선택합니다.
    
      - **서버**   (읽기 전용) **서버**는 Outlook Web App 가상 디렉터리를 호스트하는 서버의 이름을 표시합니다.
    
      - **버전**   (읽기 전용) **버전**에는 가상 디렉터리가 있는 Exchange 서버의 버전이 표시됩니다.
    
      - **웹 사이트**   (읽기 전용) **웹 사이트**에는 웹 사이트의 이름이 표시됩니다.
    
      - **Outlook Web App 버전**    (읽기 전용) **Outlook Web App 버전**에는 Exchange 서버 버전이 표시됩니다.
    
      - **수정한 날짜**   (읽기 전용) **수정한 날짜**는 가상 디렉터리가 수정된 마지막 날짜와 시간을 표시합니다.
    
      - **내부 URL**   이 텍스트 상자에 내부 네트워크에서 이 웹 사이트에 액세스하는 데 사용할 URL을 지정합니다. Exchange 2013을 설치하는 동안 내부 URL이 자동으로 구성됩니다. 인터넷 연결 서버 또는 인터넷 연결 서버가 아닌 서버에 대한 기본 내부 URL 설정은 https://\<컴퓨터 이름\>/owa입니다.
    
      - **외부 URL**   이 텍스트 상자에 인터넷에서 이 웹 사이트에 액세스하는 데 사용할 URL을 지정합니다. 기본적으로 **외부 URL**은 비어 있습니다. 인터넷 연결 클라이언트 액세스 서버에 대한 **외부 URL**은 해당 Active Directory 사이트에 대해 DNS에 게시된 값으로 설정해야 합니다. 인터넷에 연결되지 않은 Exchange 2013 서버의 경우 **외부 URL** 설정을 비워 두어야 합니다.

4.  **인증** 탭에서 인증 방법, 로그인 형식 및 로그인 도메인을 지정합니다.
    
      - **표준 인증 방법 하나 이상 사용**   다음 표준 인증 방법 중 하나 이상을 사용하려면 이 옵션을 선택합니다.
        
        **Windows 통합 인증**   이 방법을 사용하는 경우 사용자가 정보에 액세스하려면 올바른 Windows Server 2008 또는 Windows Server 2012 사용자 계정 이름 및 암호를 가지고 있어야 합니다. 사용자에게 계정 이름과 암호를 묻는 메시지가 표시되지 않습니다. 대신 서버가 클라이언트 컴퓨터에 설치된 Windows 보안 패키지와 협상합니다. 통합된 Windows 인증을 사용하면 정보를 입력하라는 메시지를 표시하거나 네트워크를 통해 암호화되지 않은 정보를 전송하지 않고 서버에서 사용자를 인증할 수 있습니다. 이 방법을 실행하려면 클라이언트 컴퓨터가 Exchange를 실행하는 서버와 동일한 도메인의 구성원이거나 Exchange 서버가 있는 도메인에서 신뢰하는 도메인의 구성원이어야 합니다.
        
        **Windows 도메인 서버의 다이제스트 인증** 이 방법은 네트워크를 통해 추가 보안을 위한 해시 값 암호를 전송합니다. 다이제스트 인증은 Windows Server 2008에 해당 계정이 저장되어 있는 사용자에 대해 Windows Server 2012 및 Active Directory 도메인에서만 사용할 수 있습니다. 다이제스트 인증에 대한 자세한 내용은 Windows Server 설명서를 참조하십시오.
        
        **기본 인증(암호를 일반 텍스트로 보냄)**   이 방법은 사용자의 자격 증명을 서버로 보내기 전에 사용자의 로그인 이름과 암호를 인코딩하는 HTTP 사양에 따라 정의되는 간단한 인증 메커니즘입니다. 암호를 최대한 안전하게 하려면 클라이언트 액세스 서버 역할이 설치되어 있는 서버와 클라이언트 컴퓨터 사이에 SSL(Secure Sockets Layer) 암호화를 사용해야 합니다.
    
      - **양식 기반 인증 사용**   양식 기반 인증은 Outlook Web App 가상 디렉터리의 보안을 향상시킵니다. 폼 기반 인증에서는 Outlook Web App에 대한 로그인 페이지를 만듭니다. 폼 기반 인증에서 사용할 로그인 프롬프트 유형을 구성할 수 있습니다. 예를 들어 사용자가 Outlook Web App 로그인 페이지에서 도메인\\사용자 이름 형식으로 도메인과 사용자 이름 정보를 입력해야 하도록 폼 기반 인증을 구성할 수 있습니다.
        

        > [!IMPORTANT]
        > SSL을 사용하도록 설정하지 않으면 폼 기반 인증에서 보안 채널을 제공하지 않습니다.

        
        다음 중 하나를 선택합니다.
        
        **도메인\\사용자 이름**   사용자가 도메인과 사용자 이름을 도메인\\사용자 이름 형식으로 입력해야 합니다. 예를 들어 Contoso 도메인에 있는 Kweku라는 사용자의 경우 로그인은 contoso\\kweku가 됩니다.
        
        **UPN(사용자 계정 이름)** UPN(사용자 계정 이름) 로그인 형식을 지정하는 경우 Outlook Web App 로그인 페이지의 **사용자 이름** 상자에 전자 메일 주소(예: kweku@contoso.com)를 입력하라는 메시지가 표시됩니다. 사용자 UPN이 전자 메일 주소와 일치하지 않으면 사용자가 **PrincipalName** 로그인 프롬프트를 사용하여 Outlook Web App에 액세스할 수 없습니다. 사용자 UPN이 전자 메일 주소와 일치하는 경우에만 **PrincipalName** 로그인 프롬프트를 사용하는 것이 좋습니다.
        
        **사용자 이름만** 사용자가 도메인 이름을 포함하지 않고 사용자 이름만 입력하면 됩니다(예: Kweku). 양식 기반 인증에 **사용자 이름만** 로그인 프롬프트를 사용하는 경우에는 **로그온 도메인** 속성도 지정해야 합니다. **로그온 도메인** 속성은 사용자가 Outlook Web App에 로그인하려고 할 때 사용하는 기본 도메인을 결정합니다. 예를 들어 기본 도메인이 Contoso이고 Kweku라는 도메인 사용자가 Outlook Web App에 로그인하는 경우 사용자 이름으로 Kweku만 입력해야 합니다. 서버는 기본 도메인 Contoso를 사용합니다. 사용자가 Contoso 도메인의 구성원이 아닌 경우에는 도메인과 사용자 이름을 입력해야 합니다.

5.  **기능** 탭에서 가상 디렉터리의 Outlook Web App 사용자에 대해 사용하거나 사용하지 않도록 설정할 기능을 지정합니다.
    

    > [!NOTE]
    > 개별 사용자에 대한 기능 설정은 가상 디렉터리 설정을 재정의합니다. <STRONG>Set-CASMailbox</STRONG> cmdlet을 사용하거나 Outlook Web App&nbsp;사서함 정책을 사용하여 개별 사용자의 조각화 설정을 변경할 수 있습니다. 자세한 내용은 <A href="https://docs.microsoft.com/ko-kr/exchange/clients-and-mobile-in-exchange-online/outlook-on-the-web/outlook-web-app-mailbox-policies">Outlook Web App 사서함 정책</A>을 참조하십시오.

    
    확인란을 사용하여 기능을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 가장 일반적인 기능이 표시됩니다. 사용하거나 사용하지 않도록 설정할 수 있는 모든 기능을 보려면 **기타 옵션**을 클릭합니다.
    

    > [!NOTE]
    > <STRONG>고급 환경 클라이언트</STRONG>&gt; 확인란을 사용하여 Outlook Web App의 표준 버전을 사용하거나 사용하지 않도록 설정하는 옵션은 더 이상 사용되지 않으며 설정에서 제거될 예정입니다. 표준 버전의 Outlook Web App은 항상 사용하도록 설정됩니다.



6.  **파일 액세스** 탭에서 확인란을 사용하여 사용자에 대한 파일 액세스 및 보기 옵션을 구성합니다. 파일 액세스를 통해 사용자는 전자 메일 메시지에 첨부된 파일의 내용을 열거나 볼 수 있습니다.
    
    파일 액세스는 사용자가 공용 컴퓨터에 로그인했는지 또는 개인 컴퓨터에 로그인했는지에 따라 제어할 수 있습니다. 사용자가 개인 컴퓨터 액세스나 공용 컴퓨터 액세스를 선택하는 옵션은 양식 기반 인증을 사용하고 있을 때만 사용할 수 있습니다. 다른 모든 인증 형태는 기본적으로 개인 컴퓨터 액세스로 지정됩니다.
    
      - **직접 파일 액세스**   직접 파일 액세스를 사용하도록 설정하려면 이 확인란을 선택합니다. 직접 파일 액세스를 통해 사용자는 전자 메일 메시지에 첨부된 파일을 열 수 있습니다.
    
      - **WebReady 문서 보기**   지원되는 문서를 HTML로 변환하고 웹 브라우저에 표시할 수 있도록 하려면 이 확인란을 선택합니다.
    
      - **변환기를 사용할 수 있는 경우 WebReady 문서 보기 허용**   사용자가 보기 응용 프로그램에서 열기 전에 문서를 강제로 HTML로 변환하고 웹 브라우저에 표시하려면 이 확인란을 선택합니다. 직접 파일 액세스가 사용하도록 설정된 경우에만 보기 응용 프로그램에서 문서를 열 수 있습니다.

7.  **저장**을 클릭하여 정책을 업데이트합니다.

## 셸을 사용하여 Outlook Web App 가상 디렉터리 속성 구성

이 예에서는 Contoso 서버의 기본 Outlook Web App 가상 디렉터리에서 폼 기반 인증을 사용하도록 설정합니다.

    set-OwaVirtualDirectory -Identity "Contoso\owa (default web site)" -FormsAuthentication $true

구문과 매개 변수에 대한 자세한 내용은 [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 Outlook Web App 가상 디렉터리 속성 보기

이 예에서는 Outlook Web App 조직에 클라이언트 액세스 서버 역할이 설치되어 있는 모든 컴퓨터에서 모든 IIS(인터넷 정보 서비스) 웹 사이트에 있는 모든 Exchange 가상 디렉터리의 속성을 볼 수 있습니다.

    Get-OWAVirtualDirectory

이 예에서는 로컬 Outlook Web App 서버에서 기본 IIS 웹 사이트에 있는 Exchange 가상 디렉터리의 속성을 볼 수 있습니다.

    Get-OWAVirtualDirectory -identity "<Exchange Server Name>\owa (default web site)"

이 예에서는 특정 Outlook Web App 서버에서 IIS 웹 사이트에 있는 모든 Exchange 가상 디렉터리의 속성을 볼 수 있습니다.

    Get-OWAVirtualDirectory -server <Exchange Server Name>

이 예에서는 Outlook Web App 조직의 모든 클라이언트 액세스 서버에서 모든 IIS 웹 사이트에 있는 각 Exchange 가상 디렉터리의 속성 값을 볼 수 있습니다.

    Get-OWAVirtualDirectory | format-list

구문과 매개 변수에 대한 자세한 내용은 [Get-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/aa998588\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

Outlook Web App 가상 디렉터리가 편집되었는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **서버** \> **가상 디렉터리**를 클릭하고 특정 Outlook Web App 가상 디렉터리를 선택합니다.

2.  **편집** 단추를 클릭하여 가상 디렉터리의 속성을 봅니다.

3.  **저장** 또는 **취소**를 클릭하여 속성 페이지를 닫습니다.

