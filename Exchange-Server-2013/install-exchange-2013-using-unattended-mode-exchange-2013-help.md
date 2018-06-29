---
title: '무인 모드로 Exchange 2013 설치: Exchange 2013 Help'
TOCTitle: 무인 모드로 Exchange 2013 설치
ms:assetid: 386465e9-41da-4e26-9816-b3b69be1f8bf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997281(v=EXCHG.150)
ms:contentKeyID: 50482879
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 무인 모드로 Exchange 2013 설치

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-06-19_

무인 설치를 수행하려면 명령 프롬프트에서 Microsoft Exchange Server 2013을 설치해야 합니다. Exchange 2013 계획 및 배포에 대한 자세한 내용은 [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md) 항목을 참조하십시오.

조직의 내부 Active Directory 포리스트 외부에 있는 경계 네트워크에 Edge 전송 역할을 설치하는 것이 좋습니다. 도메인 가입 컴퓨터에 Edge 전송 서버 역할을 설치할 수 있지만 이렇게 하면 Windows 기능 및 설정의 도메인 관리만 가능해집니다. Edge 전송 서버 자체는 Active Directory를 사용하지 않습니다. 대신 AD LDS(Active Directory Lightweight Directory Services) Windows 기능을 사용하여 구성 및 받는 사람 정보를 저장합니다. Edge 전송 역할에 대한 자세한 내용은 [Edge 전송 서버](edge-transport-servers-exchange-2013-help.md)를 참조하세요.


> [!TIP]
> Exchange Server 배포 도우미에 대해 들어보셨습니까? Exchange Server 배포 도우미는 몇 가지 질문을 하고 사용자 지정된 맞춤형 배포 검사 목록을 만들어 조직에 Exchange 2013을 신속하게 배포할 수 있도록 도와주는 무료 온라인 도구입니다. Exchange Server 배포 도우미에 대한 자세한 내용은 <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 배포 도우미</A>를 참조하세요.




> [!NOTE]
> Exchange 2013을 실행하는 컴퓨터에 서버 역할을 설치한 후 Exchange 2013 설치 마법사를 사용하여 그 컴퓨터에 다른 서버 역할을 추가할 수 없습니다. 컴퓨터에 서버 역할을 추가하려면 제어판에서 프로그램 추가/제거를 사용하거나 명령 프롬프트 창에서 Setup.exe를 사용해야 합니다.<BR>Edge 전송 역할은 사서함 또는 클라이언트 액세스 서버 역할과 같은 컴퓨터에 설치할 수 없습니다.



설치 이후에 완료할 작업에 대한 자세한 내용은 [Exchange 2013 설치 후 작업](exchange-2013-post-installation-tasks-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

다음 정보는 모든 Exchange 2013 서버 역할에 적용됩니다.

  - Exchange 2013을 설치하기 전에 릴리스 정보를 읽으십시오. 자세한 내용은 [Exchange Server 2013 릴리스 정보](release-notes-for-exchange-2013-exchange-2013-help.md)를 참조하십시오.

  - Exchange 2013을 설치하는 컴퓨터는 지원되는 운영 체제(예: Windows Server 2008 R2 SP1(서비스 팩 1), Windows Server 2012 R2 또는 Windows Server 2012) 및 충분한 디스크 공간이 있어야 하며 기타 요구 사항을 만족해야 합니다. 시스템 요구 사항에 대한 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md) 항목을 참조하십시오.

  - Exchange 2013 설치를 실행하려면 Microsoft .NET Framework 4.5, Windows Management Framework 및 기타 필수 소프트웨어를 설치해야 합니다. 모든 서버 역할의 선행 조건을 이해하려면 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!WARNING]
> 서버에 Exchange를 설치한 후 서버 이름을 변경하면 안 됩니다. Exchange 서버 역할을 설치한 후에는 서버 이름 바꾸기가 지원되지 않습니다.



다음 정보는 Exchange 2013 사서함 및 클라이언트 액세스 서버 역할에 적용됩니다.

  - 예상 완료 시간: 60분

  - 각 조직에 대해 적어도 클라이언트 액세스 서버 한 개와 사서함 서버 한 개가 Active Directory 포리스트에 있어야 합니다. 또한 사서함 서버가 포함된 각 Active Directory 사이트에 클라이언트 액세스 서버도 하나 이상 포함되어야 합니다. 서버 역할을 구분하려면 먼저 사서함 서버 역할을 설치하는 것이 좋습니다.

  - Exchange 2013을 설치하는 컴퓨터는 Active Directory 도메인의 구성원이어야 합니다.

  - 이전에 Active Directory 스키마를 준비하지 않은 경우에는 사용하는 계정이 Schema Admins 그룹의 구성원으로 위임되었는지 확인해야 합니다. 조직에 첫 번째 Exchange 2013 서버를 설치하는 경우 사용하는 계정에 Enterprise Administrators 그룹의 구성원 자격이 있어야 합니다. 이미 스키마를 준비했고 조직에서 첫 번째 Exchange 2013 서버를 설치하지 않은 경우 사용하는 계정이 Exchange 2013 Organization Management 관리 역할 그룹의 구성원이어야 합니다.
    
    Delegated Setup 역할 그룹의 구성원인 관리자는 Organization Management 역할 그룹 구성원에 의해 이전에 프로비전된 Exchange 2013 서버를 배포할 수 있습니다.

다음 정보는 Exchange 2013 Edge 전송 서버 역할에 적용됩니다.

  - 예상 완료 시간: 40분

  - Edge 전송 역할은 Exchange 2013 SP1 이상에서 사용할 수 있습니다.

  - 컴퓨터에서 기본 DNS 접미어를 구성해야 합니다. 예를 들어 컴퓨터의 정규화된 도메인 이름이 edge.contoso.com이면 컴퓨터의 DNS 접미어는 contoso.com입니다. 자세한 내용은 [주 DNS 접미사가 없거나,](primary-dns-suffix-is-missing-exchange-2013-help.md)을 참조하세요.

  - Exchange 2007 및 Exchange 2010 허브 전송 서버는 해당 서버와 Exchange 2013 Edge 전송 서버 간에 EdgeSync 구독을 만들기 위해 업데이트가 필요합니다. 이 업데이트를 설치하지 않으면 EdgeSync 구독이 제대로 작동하지 않습니다. 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md)의 "지원되는 동시 사용 시나리오" 섹션을 참조하세요.

  - 사용하는 계정이 Edge 전송 역할을 설치하려는 컴퓨터에서 로컬 관리자 그룹의 구성원인지 확인합니다.

## Setup.exe를 사용하여 무인 모드로 Exchange 2013 설치


> [!NOTE]
> 최신 버전의 Exchange 2013을 다운로드하려면 <A href="updates-for-exchange-2013-exchange-2013-help.md">Exchange 2013용 업데이트</A>를 참조하세요.



1.  Exchange 2013을 설치할 컴퓨터에 로그온합니다.

2.  Exchange 2013 설치 파일의 네트워크 위치로 이동합니다.

3.  명령 프롬프트에서 조직에 맞는 명령을 실행합니다.
    

    > [!IMPORTANT]
    > UAC(사용자 액세스 제어)를 사용하도록 설정한 경우 관리자 권한 명령 프롬프트에서 <CODE>Setup.exe</CODE>를 실행해야 합니다.

    
        Setup.exe [/Mode:<setup mode>] [/IAcceptExchangeServerLicenseTerms]
        [/Roles:<server roles to install>] [/InstallWindowsComponents] 
        [/OrganizationName:<name for the new Exchange organization>] 
        [/TargetDir:<target directory>] [/SourceDir:<source directory>]
        [/UpdatesDir:<directory from which to install updates>] 
        [/DomainController:<FQDN of domain controller>] [/DisableAMFiltering]
        [/AnswerFile:<filename>] [/DoNotStartTransport] 
        [/EnableErrorReporting] [/CustomerFeedbackEnabled:<True | False>] 
        [/AddUmLanguagePack:<UM language pack name>] 
        [/RemoveUmLanguagePack:<UM language pack name>] 
        [/NewProvisionedServer:<server>] [/RemoveProvisionedServer:<server>] 
        [/MdbName:<mailbox database name>] [/DbFilePath:<Edb file path>] 
        [/LogFolderPath:<log folder path>] [/ActiveDirectorySplitPermissions:<True | False>]
        [/TenantOrganizationConfig:<path>]

4.  Exchange 2013을 설치할 컴퓨터로 설치 파일이 로컬로 복사됩니다.

5.  또한 설치 중인 서버 역할과 관련된 모든 선행 조건을 포함한 선행 조건을 검사합니다. 모든 선행 조건을 충족하지 않으면 설치가 실패하고 실패 이유를 설명하는 오류 메시지가 반환됩니다. 선행 조건을 모두 충족하면 Exchange 2013이 설치됩니다.

6.  Exchange 2013이 완료된 후 컴퓨터를 다시 시작합니다.

7.  [Exchange 2013 설치 후 작업](exchange-2013-post-installation-tasks-exchange-2013-help.md)에서 제공된 작업을 수행하여 배포를 완료합니다.

## 예

다음은 Setup.exe를 사용하는 예입니다.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /OrganizationName:MyOrg /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 Active Directory에서 MyOrg라는 Exchange 2013 조직을 만들고 클라이언트 액세스 서버 역할, 사서함 서버 역할 및 관리 도구를 설치한 다음 Exchange 2013 사용 조건에도 동의합니다.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /TargetDir:"C:\\Exchange Server" /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 클라이언트 액세스 서버 역할, 사서함 서버 역할 및 관리 도구를 "C:\\Exchange Server" 디렉터리에 설치합니다. 이 명령은 Exchange 2013 조직이 이미 준비되었다고 가정합니다.

  - **Setup.exe /mode:Install /r:CA,MB /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 클라이언트 액세스 서버 역할, 사서함 서버 역할 및 관리 도구를 기본 설치 위치에 설치합니다.

  - **Setup.exe /mode:Install /r:EdgeTransport /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 Edge 전송 서버 역할과 관리 도구를 기본 설치 위치에 설치합니다.

  - **Setup.exe /mode:Install /r:ET /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 Edge 전송 서버 역할과 관리 도구를 기본 설치 위치에 설치합니다.

  - **Setup.exe /mode:Uninstall /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 서버에서 Exchange 2013을 완전히 제거하고 이 서버의 Exchange 구성을 Active Directory에서 제거합니다.

  - **Setup.exe /PrepareAD /on:"My Org" /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 My Org라는 Exchange 조직을 만들고 Exchange 2013용 Active Directory를 준비합니다.

  - **C:\\ExchangeServer\\bin\\Setup.exe /m:Install /r:ClientAccess /SourceDir:d:\\amd64 /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 D:\\amd64를 원본 디렉터리로 사용하여, 기존 Exchange 2013 서버에 클라이언트 액세스 서버 역할을 추가합니다.

  - **Setup.exe /role:ClientAccess,Mailbox /UpdatesDir:"C:\\ExchangeServer\\New Patches" /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 지정된 디렉터리에서 패치를 사용하여 ExchangeServer.msi를 업데이트한 후, 클라이언트 액세스 서버 역할, 사서함 서버 역할 및 관리 도구를 설치합니다. 언어 팩 번들이 이 디렉터리에 포함된 경우 언어 팩도 설치됩니다.

  - **Setup.exe /mode:Install /role:ClientAccess,Mailbox /DomainController:DC01 /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 클라이언트 액세스 서버 역할, 사서함 서버 역할 및 관리 도구를 설치하면서 도메인 컨트롤러 DC01을 사용하여 Active Directory를 쿼리 및 변경합니다.

  - **Setup.exe /mode:Install /role:ClientAccess /AnswerFile:c:\\ExchangeConfig.txt /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 ExchangeConfig.txt 파일의 설정을 사용하여 클라이언트 액세스 서버 역할을 설치합니다.

  - **Setup.exe /rprs:Exchange03 /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 Active Directory에서 Exchange03 개체를 제거합니다.

  - **Setup.exe /AddUmLanguagePack:ko-KR /IAcceptExchangeServerLicenseTerms**
    
    이 명령은 %ExchangeSourceDir%\\ServerRoles\\UnifiedMessaging 디렉터리에서 한국어 통합 메시징 언어 팩을 설치합니다.

## 작동 여부는 어떻게 확인합니까?

Exchange 2013이 성공적으로 설치되었는지 확인하려면 [Exchange 2013 설치를 확인 합니다.](verify-an-exchange-2013-installation-exchange-2013-help.md) 항목을 참조하십시오.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

