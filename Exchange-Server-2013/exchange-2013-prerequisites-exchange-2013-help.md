---
title: 'Exchange 2013 필수 구성 요소: Exchange 2013 Help'
TOCTitle: Exchange 2013 필수 구성 요소
ms:assetid: e21cf744-7813-48b3-9293-5cecd89a6c25
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691354(v=EXCHG.150)
ms:contentKeyID: 50484395
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013 필수 구성 요소

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-03-20_

이 항목에서는 Microsoft Exchange 2013 사서함, 클라이언트 액세스 서버 및 Edge 전송 서버 역할에 필요한 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2 SP1(서비스 팩 1) 운영 체제 필수 구성 요소를 설치하기 위한 단계가 제공됩니다. 또한 Windows 8, Windows 8.1 및 Windows 7 클라이언트 컴퓨터에 Exchange 2013 관리 도구를 설치하는 데 필요한 필수 구성 요소도 설명합니다.

  - 시작하기 전에 알아야 할 내용

  - Active Directory 준비

  - Windows Server 2012 R2 및 Windows Server 2012 필수 구성 요소
    
      - 사서함 또는 클라이언트 액세스 서버 역할
    
      - Edge 전송 서버 역할

  - Windows Server 2008 R2 SP1 필수 구성 요소
    
      - 사서함 또는 클라이언트 액세스 서버 역할
    
      - Edge 전송 서버 역할

  - Windows 7 필수 구성 요소(관리 도구에만 해당)

  - Windows 8 및 8.1 Windows 필수 구성 요소(관리 도구에만 해당)

## 시작하기 전에 알아야 할 내용

  - 이 항목의 정보는 Exchange 2013 서비스 팩 1 이상 버전에 적용됩니다.

  - Edge 전송 서버 역할은 Exchange 2013 SP1부터 제공됩니다.

  - 포리스트의 기능 수준이 Windows Server 2003 이상인지 확인하고 스키마 마스터가 Windows Server 2003 서비스 팩 2 이상을 실행 중인지 확인하십시오. Windows 기능 수준에 대한 자세한 내용은 [도메인 및 포리스트 관리](https://go.microsoft.com/fwlink/p/?linkid=137037)를 참조하십시오.

  - Exchange 2013 서버 역할 또는 관리 도구를 실행 중인 모든 서버에서 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2 SP1의 전체 설치 옵션을 사용해야 합니다.

  - 먼저 컴퓨터를 해당 내부 Active Directory 포리스트 및 도메인에 가입시켜야 합니다.

  - 일부 필수 구성 요소의 설치를 완료하려면 서버를 다시 부팅해야 합니다.

  - 컴퓨터에 최신 Windows 업데이트를 설치합니다. 자세한 내용은 [배포 보안 검사 목록](deployment-security-checklist-exchange-2013-help.md)을 참조하십시오.
    

    > [!NOTE]
    > 사서함 서버 역할을 설치할 때 서버가 DAG(데이터베이스 사용 가능 그룹)의 구성원이 되도록 하려면 Windows Server 2012 R2 Standard 또는 Datacenter Edition, Windows Server 2012 Standard 또는 Datacenter Edition, Windows Server 2008 R2 SP1 Enterprise Edition을 실행해야 합니다. Windows Server 2008 R2 SP 1 Standard Edition은 DAG에 필요한 기능을 지원하지 않습니다.<BR>Windows 서버에 Exchange가 설치된 경우에는 Windows를 업그레이드할 수 없습니다.<BR>Microsoft UCMA(Unified Communications Managed API) 4.0으로 업그레이드하려면 먼저 <STRONG>프로그램 추가/제거</STRONG>를 사용하여 설치되어 있는 이전 버전의 UCMA를 모두 제거해야 합니다.




> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Active Directory 준비

Exchange 2013를 위해 Active Directory를 준비하는 데 사용할 컴퓨터는 몇 가지 필수 구성 요소를 충족해야 합니다.

Active Directory를 준비하는 데 사용할 컴퓨터에 다음 소프트웨어를 표시된 순서대로 설치하세요.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)(Windows Server 2012 R2에 포함됨)

위에 나열된 소프트웨어를 설치한 후에는 다음 단계를 완료하여 원격 도구 관리 팩을 설치합니다. 원격 도구 관리 팩을 설치한 후에는 해당 컴퓨터를 사용하여 Active Directory를 준비할 수 있습니다. Active Directory 준비에 대한 자세한 내용은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)를 참조하세요.

1.  Windows PowerShell을 엽니다.

2.  원격 도구 관리 팩을 설치합니다.
    
      - Windows Server 2012 R2 또는 Windows Server 2012 컴퓨터에서 다음 명령을 실행합니다.
        
            Install-WindowsFeature RSAT-ADDS
    
      - Windows Server 2008 R2 SP1 컴퓨터에서 다음 명령을 실행합니다.
        
            Add-WindowsFeature RSAT-ADDS

## Windows Server 2012 R2 및 Windows Server 2012 필수 구성 요소

Windows Server 2012 R2 또는 Windows Server 2012 컴퓨터에 Exchange 2013을 설치하는 데 필요한 필수 구성 요소는 설치하려는 Exchange 역할에 따라 다릅니다. 아래에서 설치하려는 역할과 일치하는 섹션을 읽어 보십시오.

## 사서함 또는 클라이언트 액세스 서버 역할

다음을 수행하려는 Windows Server 2012 R2 또는 Windows Server 2012 컴퓨터에 필수 구성 요소를 설치하려면 이 섹션의 지시를 따르세요.

  - 컴퓨터에 사서함 서버 역할만 설치합니다.

  - 컴퓨터에 클라이언트 액세스 서버 역할만 설치합니다.

  - 동일한 컴퓨터에 사서함 서버 역할과 클라이언트 액세스 서버 역할을 모두 설치합니다.

필요한 Windows 역할 및 기능을 설치하려면 다음을 수행합니다.

1.  Windows PowerShell을 엽니다.

2.  필요한 Windows 구성 요소를 설치하려면 다음 명령을 실행합니다.
    
        Install-WindowsFeature AS-HTTP-Activation, Desktop-Experience, NET-Framework-45-Features, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Clustering-CmdInterface, RSAT-Clustering-Mgmt, RSAT-Clustering-PowerShell, Web-Mgmt-Console, WAS-Process-Model, Web-Asp-Net45, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext45, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, Windows-Identity-Foundation, RSAT-ADDS

운영 체제 역할 및 기능을 설치한 후 다음 소프트웨어를 표시된 순서대로 설치합니다.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16과 이후에 <STRONG>요구되는</STRONG> .NET Framework 4.6.2. Exchange 2013 CU16 설치 전 귀하의 서버를 .NET Framework 4.6.2로 업그레이드하지 않으면 오류가 발생할 수 있습니다. .NET Framework 4.5.2가 Exchange 서버에 설치되어 있으면 .NET Framework 4.6.2를 설치하기 전에 서버를 Exchange 2013 CU15로 업그레이드합니다.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)(Windows Server 2012 R2에 포함됨)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64비트](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Edge 전송 서버 역할

컴퓨터에 Edge 전송 서버 역할을 설치하려는 Windows Server 2012 R2 또는 Windows Server 2012 컴퓨터에 필수 구성 요소를 설치하려면 이 섹션의 지시를 따르세요.

필요한 Windows 역할 및 기능을 설치하려면 다음을 수행합니다.

1.  Windows PowerShell을 엽니다.

2.  필요한 Windows 구성 요소를 설치하려면 다음 명령을 실행합니다.
    
        Install-WindowsFeature ADLDS

설치하려는 Exchange 2013 버전에 해당하는 Microsoft .NET Framework 버전을 설치하세요.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16과 이후에 <STRONG>요구되는</STRONG> .NET Framework 4.6.2. Exchange 2013 CU16 설치 전 귀하의 서버를 .NET Framework 4.6.2로 업그레이드하지 않으면 오류가 발생할 수 있습니다. .NET Framework 4.5.2가 Exchange 서버에 설치되어 있으면 .NET Framework 4.6.2를 설치하기 전에 서버를 Exchange 2013 CU15로 업그레이드합니다.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)(Windows Server 2012 R2에 포함됨)

## Windows Server 2008 R2 SP1 필수 구성 요소

Windows Server 2008 R2 SP1 컴퓨터에 Exchange 2013을 설치하는 데 필요한 필수 구성 요소는 설치하려는 Exchange 역할에 따라 다릅니다. 아래에서 설치하려는 역할과 일치하는 섹션을 읽어 보십시오.

## 사서함 또는 클라이언트 액세스 서버 역할

다음을 수행하려는 Windows Server 2008 R2 SP1 컴퓨터에 필수 구성 요소를 설치하려면 이 섹션의 지시를 따르십시오.

  - 컴퓨터에 사서함 서버 역할만 설치합니다.

  - 컴퓨터에 클라이언트 액세스 서버 역할만 설치합니다.

  - 동일한 컴퓨터에 사서함 서버 역할과 클라이언트 액세스 서버 역할을 모두 설치합니다.

필요한 Windows 역할 및 기능을 설치하려면 다음을 수행합니다.

1.  Windows PowerShell을 엽니다.

2.  서버 관리자 모듈을 로드하려면 다음 명령을 실행합니다.
    
        Import-Module ServerManager

3.  필요한 Windows 구성 요소를 설치하려면 다음 명령을 실행합니다.
    
        Add-WindowsFeature Desktop-Experience, NET-Framework, NET-HTTP-Activation, RPC-over-HTTP-proxy, RSAT-Clustering, RSAT-Web-Server, WAS-Process-Model, Web-Asp-Net, Web-Basic-Auth, Web-Client-Auth, Web-Digest-Auth, Web-Dir-Browsing, Web-Dyn-Compression, Web-Http-Errors, Web-Http-Logging, Web-Http-Redirect, Web-Http-Tracing, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Lgcy-Mgmt-Console, Web-Metabase, Web-Mgmt-Console, Web-Mgmt-Service, Web-Net-Ext, Web-Request-Monitor, Web-Server, Web-Stat-Compression, Web-Static-Content, Web-Windows-Auth, Web-WMI, RSAT-ADDS

운영 체제 역할 및 기능을 설치한 후 다음 소프트웨어를 표시된 순서대로 설치합니다.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16과 이후에 <STRONG>요구되는</STRONG> .NET Framework 4.6.2. Exchange 2013 CU16 설치 전 귀하의 서버를 .NET Framework 4.6.2로 업그레이드하지 않으면 오류가 발생할 수 있습니다. .NET Framework 4.5.2가 Exchange 서버에 설치되어 있으면 .NET Framework 4.6.2를 설치하기 전에 서버를 Exchange 2013 CU15로 업그레이드합니다.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64비트](https://go.microsoft.com/fwlink/p/?linkid=258269)

4.  [Microsoft 기술 자료 문서 KB974405(Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

5.  [기술 자료 문서 KB2619234(RPC over HTTP에 사용되는 연결 쿠키/GUID를 Windows 7과 Windows Server 2008 R2의 RPC 계층에서도 사용되도록 설정)(기계 번역)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2619234)

6.  [기술 자료 문서 KB2533623(비보안 라이브러리 로드로 원격 코드 실행 가능)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=2533623)
    

    > [!NOTE]
    > 컴퓨터에 보안 업데이트를 설치하도록 Windows 업데이트를 구성한 경우 이 핫픽스가 이미 설치되어 있을 수 있습니다.



## Edge 전송 서버 역할

컴퓨터에 Edge 전송 서버 역할을 설치하려는 Windows Server 2008 R2 SP1 컴퓨터에 필수 구성 요소를 설치하려면 이 섹션의 지시를 따르세요.

필요한 Windows 역할 및 기능을 설치하려면 다음을 수행합니다.

1.  Windows PowerShell을 엽니다.

2.  서버 관리자 모듈을 로드하려면 다음 명령을 실행합니다.
    
        Import-Module ServerManager

3.  필요한 Windows 구성 요소를 설치하려면 다음 명령을 실행합니다.
    
        Add-WindowsFeature NET-Framework, ADLDS

운영 체제 역할 및 기능을 설치한 후 다음 소프트웨어를 표시된 순서대로 설치합니다.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)
    

    > [!IMPORTANT]
    > Exchange 2013 CU16과 이후에 <STRONG>요구되는</STRONG> .NET Framework 4.6.2. Exchange 2013 CU16 설치 전 귀하의 서버를 .NET Framework 4.6.2로 업그레이드하지 않으면 오류가 발생할 수 있습니다. .NET Framework 4.5.2가 Exchange 서버에 설치되어 있으면 .NET Framework 4.6.2를 설치하기 전에 서버를 Exchange 2013 CU15로 업그레이드합니다.



2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [Microsoft Unified Communications Managed API 4.0, Core Runtime 64비트](https://go.microsoft.com/fwlink/p/?linkid=258269)

## Windows 7 필수 구성 요소(관리 도구에만 해당)

Exchange 관리 도구를 설치하려는 도메인 가입 Windows 7 64비트 컴퓨터에 필수 구성 요소를 설치하려면 이 섹션의 지시를 따르세요.

1.  **제어판**을 연 다음 **프로그램**을 선택합니다.

2.  **Windows 기능 사용/사용 안 함**을 클릭합니다.

3.  **인터넷 정보 서비스** \> **웹 관리 도구** \> **IIS 6 관리 호환성**으로 이동합니다.

4.  **IIS 6 관리 콘솔** 확인란을 선택한 다음 **확인**을 클릭합니다.

운영 체제 기능을 설치한 후 다음 소프트웨어를 표시된 순서대로 설치합니다.

1.  [.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

2.  [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/p/?linkid=390234)

3.  [기술 자료 문서 KB974405(Windows Identity Foundation)](http://go.microsoft.com/fwlink/?linkid=3052&kbid=974405)

## Windows 8 및 Windows 8.1 필수 구성 요소(관리 도구에만 해당)

[.NET Framework 4.6.2](https://go.microsoft.com/fwlink/p/?linkid=808659)

