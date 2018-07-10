---
title: 'Exchange 2013 서버에서 사용자 사서함이 있는 레거시 공용 폴더 구성: Exchange 2013 Help'
TOCTitle: Exchange 2013 서버에서 사용자 사서함이 있는 레거시 공용 폴더 구성
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281151
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 서버에서 사용자 사서함이 있는 레거시 공용 폴더 구성

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2017-03-27_

Exchange 2013 또는 Exchange 2016 사용자 액세스 Exchange 2010 또는 이전 공용 폴더 (로 알려져 레거시 공용 폴더)로 설정 하는 방법입니다.

## 시작하기 전에 알아야 할 내용

사용자 사서함이 Exchange Server 2013 또는 Exchange Server 2016에 있는 Outlook Web App, 웹, Outlook 또는 Outlook for mac입니다.에서 레거시 공용 폴더에 액세스할 수 없습니다. 이 문서의 단계는 Exchange 2013 및 Exchange 2016 모두에 대해 작동 합니다.


> [!NOTE]
> 이 문서의 단계를 수행한 후 Mac 사용자를 위한 outlook 2016 레거시 공용 폴더에 액세스할 수 있습니다. 조직의 클라이언트에서에서 Outlook 2016 for Mac을 사용 하는 경우 2016 년 4 월 업데이트를 설치한 있는지 확인 합니다. 그렇지 않은 경우 해당 사용자가 동시 사용 또는 하이브리드 토폴로지에서 공용 폴더에 액세스할 수 없습니다. 자세한 내용은 <A href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Mac 용 Outlook 2016와 공용 폴더 액세스 (영문)</A>을 참조 하십시오.



## 1단계: Exchange 2010 공용 폴더를 검색 가능하게 설정

1.  공용 폴더에 있는 경우 Exchange 2010 또는 최신 서버, 공용 폴더 데이터베이스를 포함 하는 모든 사서함 서버에 클라이언트 액세스 서버 역할을 설치 해야 합니다. 이 공용 폴더에 액세스 하는 모든 클라이언트를 허용 하는 Microsoft Exchange RpcClientAccess 서비스를를 실행 하 고, 수 있습니다. 클라이언트 액세스 역할 Exchange 2007 공용 폴더 서버에 대 한 필요는 없으며이 단계는 필요 하지 않습니다. 자세한 내용은 [Exchange Server 2010 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)를 참조 하십시오.
    

    > [!NOTE]
    > 이 서버는 클라이언트 액세스 부하 분산의 일부가 될 필요가 없습니다. 자세한 내용은 <A href="https://technet.microsoft.com/en-us/library/ff625247(v=exchg.141).aspx">이해 부하 분산 Exchange 2010</A>을 참조 하십시오.



2.  각 공용 폴더 서버에 빈 사서함 데이터베이스를 만듭니다.
    
    Exchange 2010의 경우 다음 명령을 실행합니다. 이 명령은 부하 분산 장치를 프로비저닝하는 사서함에서 사서함 데이터베이스를 제외합니다. 그러면 이 데이터베이스에 새 사서함이 자동으로 추가되지 않습니다.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true 
    
    Exchange 2007의 경우 다음 명령을 실행합니다.
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!NOTE]
    > 이 데이터베이스에는 3단계에서 만드는 프록시 사서함만 추가하는 것이 좋습니다. 이 사서함 데이터베이스에서 다른 사서함을 만들어서는 안 됩니다.



3.  새 사서함 데이터베이스 내에서 프록시 사서함을 만들고 주소록에서 해당 사서함을 숨깁니다. 이 사서함의 SMTP는 자동 검색에서 *DefaultPublicFolderMailbox* SMTP로 반환되므로 클라이언트는 이 SMTP를 확인하여 공용 폴더 액세스를 위해 레거시 Exchange 서버에 연결할 수 있습니다.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Exchange 2010의 경우 자동 검색에서 프록시 공용 폴더 사서함을 반환하도록 설정합니다. Exchange 2007의 경우에는 이 단계를 수행할 필요가 없습니다.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  조직의 모든 공용 폴더 서버에 대해 위의 단계를 반복합니다.

## 2단계: 레거시 공용 폴더에 액세스하도록 사용자 사서함 구성

이 절차의 마지막 단계에서는 레거시 온-프레미스 공용 폴더에 대한 액세스를 허용하도록 사용자 사서함을 구성합니다.

Exchange Server 2013 온-프레미스 사용자가 레거시 공용 폴더에 액세스하도록 허용합니다. 이렇게 하려면 [Step 2: Make remote public folders discoverable](configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md)에서 만든 모든 프록시 공용 폴더 사서함을 가리킵니다. CU5 이상 업데이트가 설치된 Exchange 2013 서버에서 다음 명령을 실행합니다.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3


> [!NOTE]
> Active Directory 동기화가 완료될 때까지 기다려야 변경 내용이 표시됩니다. 이 프로세스를 수행하는 데 몇 시간이 걸릴 수 있습니다.



## 작동 여부를 확인하려면 어떻게 해야 합니까?

사서함이 Exchange Server 2013 CU5 이상 서버에 있는 사용자에 대해 Outlook으로 로그온하고 다음 공용 폴더 테스트를 수행합니다.

1.  Outlook 클라이언트가 실행 중인지 확인합니다.

2.  Ctrl 키를 누른 채로 Windows 작업 표시줄 오른쪽의 알림 영역에 있는 Outlook 아이콘을 마우스 오른쪽 단추로 클릭합니다.

3.  **전자 메일 자동 구성 테스트...**를 선택합니다.

4.  전자 메일 자동 구성 테스트 도구가 XML 탭에 다음 정보를 반환하는지 확인합니다.
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<SMTP Address for public folder mailbox\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  Outlook 클라이언트에서 다음 작업을 수행합니다.
    
      - 공용 폴더 계층 구조를 확인합니다.
    
      - 사용 권한을 확인합니다.
    
      - 공용 폴더를 만들고 삭제합니다.
    
      - 공용 폴더에 콘텐츠를 게시한 후 삭제합니다.

