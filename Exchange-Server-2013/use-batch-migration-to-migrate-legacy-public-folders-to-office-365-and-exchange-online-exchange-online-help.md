---
title: '일괄 처리 마이그레이션을 사용하여 레거시 공용 폴더를 Office 365 및 Exchange Online에 마이그레이션'
TOCTitle: 마이그레이션 일괄 처리를 사용 하 여 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63763688
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 마이그레이션 일괄 처리를 사용 하 여 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션

 

_**적용 대상:** Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-03-26_

**요약:**  Office 365에 Exchange 2007 및 Exchange 2010 공용 폴더를 이동 하려면 다음이 절차를 사용 합니다.

이 항목에서는 Office 365 또는 Exchange Online에 업데이트 롤업 8 Exchange Server 2010 서비스 팩 3 (SP3) 또는 Exchange 2007 s p 3 용 업데이트 롤업 15에서 단독형 또는 미리 구성 된 마이그레이션에 공용 폴더를 마이그레이션하는 방법에 설명 합니다.

이 항목은 *레거시 Exchange 서버*와 Exchange 2010 s p 3 RU8 및 Exchange 2007 s p 3 RU15 서버를 참조합니다. 또한이 항목의 단계는 Exchange Online 및 Office 365에 모두 적용 됩니다. 이 항목의 용어를 바꾸어 사용할 수 있습니다.


> [!NOTE]
> 이 문서에서 설명 하는 일괄 마이그레이션 방법을 Office 365 및 Exchange Online으로 레거시 공용 폴더 마이그레이션에 대 한 지원 되는 유일한 방법입니다. 공용 폴더 마이그레이션에 대 한 이전 직렬 마이그레이션 방법은 되 고 사용 되지 않으며 Microsoft에서 더이상 지원 됩니다.



Office 365 또는 Exchange Online으로 공용 폴더 마이그레이션에 Outlook의 PST 내보내기 기능을 사용 하지 않는 것이 좋습니다. Office 365 및 Exchange online 공용 폴더 사서함 성장 관리 되는 공용 폴더 사서함 분할 하는 것을 초과 하면 하는 자동 분할 기능을 사용 하 여 할당량 크기를 조정 합니다. 자동 분할 PST 내보내기를 사용 하 여 공용 폴더를 마이그레이션하려 하 고 기본 사서함에서에서 데이터를 이동 하려면 자동 분할에 대 한 최대 2 주에 대 한 대기 해야할 수 때 공용 폴더 사서함의 갑자기 증가 처리할 수 없습니다. 이 문서에서 cmdlet 기반 지침을 사용 하 여 Office 365 및 Exchange Online으로 공용 폴더를 마이그레이션하는 것이 좋습니다. 그러나 PST 내보내기를 사용 하 여 공용 폴더 마이그레이션 하려는 경우이 항목 뒷부분에 나오는 Outlook PST를 사용 하 여 Office 365에 공용 폴더 마이그레이션 내보내기 섹션을 참조 합니다.

다음 PowerShell 스크립트 외에도 **\*-MigrationBatch** cmdlet을 사용 하 여 마이그레이션을 수행 됩니다.

  - `Export-PublicFolderStatistics.ps1`   이 스크립트는 폴더 이름과 폴더 크기 매핑 파일을 만듭니다. 레거시 Exchange 서버에서 이 스크립트를 실행합니다.

  - `Export-PublicFolderStatistics.psd1`   이 지원 파일은 `Export-PublicFolderStatistics.ps1` 스크립트에서 사용되며 같은 위치로 다운로드해야 합니다.

  - `PublicFolderToMailboxMapGenerator.ps1`   이 스크립트는 `Export-PublicFolderStatistics.ps1` 스크립트의 출력을 사용하여 공용 폴더와 사서함 매핑 파일을 만듭니다. 레거시 Exchange 서버에서 이 스크립트를 실행합니다.

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   이 지원 파일은 `PublicFolderToMailboxMapGenerator.ps1` 스크립트에서 사용되며 같은 위치로 다운로드해야 합니다.

  - `Create-PublicFolderMailboxesForMigration.ps1` 이 스크립트는 마이그레이션에 대 한 대상 공용 폴더 사서함을 만듭니다. 또한이 스크립트는 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)에서 권장 하는 공용 폴더 사서함당 사용자 로그온 수에 대 한 지침에 따라 예상된 사용자 부하를 처리 하는 데 필요한 사서함 수를 계산 합니다.

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` 이 지원 파일은 만들기 PublicFolderMailboxesForMigration.ps1 스크립트에 사용 되며 같은 위치로 다운로드 해야 합니다.

  - `Sync-MailPublicFolders.ps1`   이 스크립트는 로컬 Exchange 배포 및 Office 365 사이 개체를 메일 사용이 가능한 공용 폴더를 동기화합니다. 레거시 Exchange 서버에서이 스크립트를 실행 합니다.

  - `SyncMailPublicFolders.strings.psd1`   `Sync-MailPublicFolders.ps1` 스크립트에서 사용 되는 지원 파일 이며 위의 스크립트와 같은 위치에 복사 해야 합니다.

1 단계: 마이그레이션 스크립트를 다운로드 이러한 스크립트를 다운로드 하는 위치에 대 한 세부 정보를 제공 합니다. 모든 스크립트 같은 위치로 다운로드 되 고 있는지 확인 하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

## 공용 폴더를 Office 365 및 Exchange Online으로 마이그레이션하는 데 지원되는 Exchange 버전

Exchange에서는 다음 레거시 Exchange Server 버전에서 Office 365 및 Exchange Online으로 공용 폴더를 이동하도록 지원됩니다.

  - Exchange 2010 s p 3 RU8 이상

  - Exchange 2007 s p 3 RU15 이상

Exchange Online으로 공용 폴더를 이동 하 고 온-프레미스 서버 최소 지원 버전의 Exchange 2010 또는 Exchange 2007을 실행 하지 않는 라우팅하는 온-프레미스 서버를 업그레이드 하 고는 일괄 마이그레이션 기능을 사용합니다 공용 폴더 마이그레이션 방법만 지원 합니다.

Exchange 2003에서 직접 공용 폴더를 마이그레이션할 수 없습니다. 모든 공용 폴더 데이터베이스 및 Exchange 2010 s p 3 RU8 또는 나중에 복제 데이터베이스 또는 Exchange 2007 SP3 RU10 이동 해야 하는 조직에서 Exchange 2003을 실행 하는 경우 이상입니다. 공용 폴더 복제본 Exchange 2003에 남아 있을 수 있습니다. 또한 Exchange 2003 서버를 통해 Exchange 2013 공용 폴더에 대 한 대상으로 메일을 라우팅할 수 없습니다.

## 시작하기 전에 알아야 할 내용

  - Exchange 2010 서버에서 Exchange 2010 s p 3 RU8를 실행 해야하는 이상입니다.

  - Exchange 2007 서버에서 Exchange 2007 s p 3 RU15를 실행 해야하는 이상입니다.

  - Office 365 및 Exchange Online에서 조직 관리 역할 그룹의 구성원 이어야 해야 합니다. 이 역할 그룹은 Office 365 또는 Exchange Online 구독할 때 사용자에 게 할당 된 사용 권한을과 다릅니다. 조직 관리 역할 그룹을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은, [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)을 참조 하십시오.

  - Exchange 2010, 해야하는 조직 관리 또는 서버 관리 RBAC 역할 그룹의 구성원 이어야 합니다. 자세한 내용은 [역할 그룹에 구성원 추가](https://go.microsoft.com/fwlink/?linkid=299212)를 참조 하십시오.

  - Exchange 2007, 해야 Exchange 조직 관리자 역할 또는 Exchange Server 관리자 역할이 할당 되어야 합니다. 또한 공용 폴더 관리자 역할 및 대상 서버에 대 한 로컬 관리자 그룹에 할당 해야 합니다. 자세한 내용은 [사용자 또는 그룹 관리자 역할을 추가 하는 방법](https://go.microsoft.com/fwlink/p/?linkid=81779)를 참조 하십시오.

  - Exchange 2007 서버에서 [Windows Server 2008 x64 Edition용 Windows PowerShell 2.0 및 WinRM 2.0](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930)으로 업그레이드합니다.

  - 조직에 2GB보다 큰 공용 폴더가 있으면 마이그레이션 전에 해당 폴더의 콘텐츠를 삭제하거나 여러 공용 폴더로 분할하는 것이 좋습니다. 이 두 옵션 중 하나를 사용할 수 없으면 공용 폴더를 Office 365 및 Exchange Online으로 이동하지 않는 것이 좋습니다.

  - Office 365 및 Exchange Online에서 최대 1, 000 공용 폴더 사서함을 만들 수 있습니다.

  - 공용 폴더를 마이그레이션하기 전에 Office 365 및 Exchange Online으로 모든 사용자 사서함을 먼저 이동 하는 것이 좋습니다. 자세한 내용은 [Office 365에 여러 전자 메일 계정으로 마이그레이션하는 방법](https://go.microsoft.com/fwlink/p/?linkid=524030)를 참조 합니다.

  - Outlook Anywhere 레거시 Exchange 서버에서 사용할 수 있어야 합니다. Exchange 2010 서버에서 외부에서 Outlook 사용을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은, [사용 외부에서 Outlook 사용](https://go.microsoft.com/fwlink/p/?linkid=187249)을 참조 하십시오. Exchange 2007 서버에서 외부에서 Outlook 사용을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은, [외부에서 Outlook 설정 하는 방법](https://go.microsoft.com/fwlink/p/?linkid=167210)을 참조 하십시오.

  - 이 절차를 수행 하려면 Exchange 관리 센터 (EAC) 또는 (EMC (Exchange 관리 콘솔)를 사용할 수 없습니다. 레거시 Exchange 서버에서 Exchange 관리 셸 를 사용 하 여 지정 해야 합니다. Exchange Online에 대 한 Exchange Online PowerShell을 사용 해야 합니다. 자세한 내용은 [원격 PowerShell을 사용하여 Exchange Online에 연결](https://technet.microsoft.com/ko-kr/library/jj984289\(v=exchg.150\))을 참조 하십시오.

  - 일부 단계의 경우 가동 중지 시간이 필요하므로 시작하기 전에 이 항목 전체를 읽어 보십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 마이그레이션 스크립트 다운로드

1.  [공용 폴더 마이그레이션 스크립트](https://go.microsoft.com/fwlink/?linkid=299838)에서 모든 스크립트 및 지원 파일을 다운로드 합니다.

2.  PowerShell을 실행할 로컬 컴퓨터에서 C:\\PFScripts 등의 위치에 스크립트를 저장합니다. 모든 스크립트가 같은 위치에 저장되는지 확인합니다.

3.  [메일 사용이 가능한 공용 폴더-디렉터리 동기화 스크립트](https://go.microsoft.com/fwlink/p/?linkid=532376)에서 다음 파일을 다운로드 합니다.
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  2단계와 같은 위치(예: C:\\PFScripts)에 스크립트를 저장합니다.

## 2단계: 마이그레이션 준비

마이그레이션을 시작하기 전에 다음 필수 구성 단계를 수행합니다.

**일반 필수 단계**

  - 없는지 확인는 고아 없는 공용 폴더 메일 개체 Active Directory에 해당 하는 Exchange 개체가 없이 Active Directory의 개체를 의미 합니다.

  - SMTP 전자 메일 주소에서에서 구성 확인 공용 폴더에 대 한 Active Directory 일치 하는 SMTP 전자 메일 주소 Exchange 개체에 합니다.

  - 둘 이상의 Active Directory 개체는 동일한 메일 사용이 가능한 공용 폴더는 가리키는 상황을 방지 하기 위해 Active Directory에서 중복 된 공용 폴더 개체가 없으면이 없는지 확인 합니다.

**레거시 Exchange 서버의 필수 구성 단계**

1.  레거시 Exchange Server에서는 인터넷을 통한 모든 DNS 캐시가 조직이 현재 상주하는 Office 365 또는 Exchange Online DNS를 가리키도록 업데이트될 때까지 Office 365 또는 Exchange Online에 존재하게 될 메일 사용이 가능한 공용 폴더로의 라우팅이 계속 작동되도록 해야 합니다. 이렇게 하려면 다음 명령을 실행하여 잘 알려진 이름을 갖는 허용 도메인을 구성하여 전자 메일 메시지를 Office 365 또는 Exchange Online 도메인으로 적절히 라우팅하도록 합니다.
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  공용 폴더의 이름에 백슬래시(**\\**)가 포함된 경우 마이그레이션이 수행되면 공용 폴더가 상위 공용 폴더에 만들어집니다. 마이그레이션하기 전에 이름에 백슬래시가 있는 공용 폴더의 이름을 바꾸는 것이 좋습니다.
    
    1.  Exchange 2010에서 이름에 백슬래시가 있는 공용 폴더를 찾으려면 다음 명령을 실행합니다.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Exchange 2007에서 이름에 백슬래시가 있는 공용 폴더를 찾으려면 다음 명령을 실행합니다.
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  공용 폴더가 반환되면 다음 명령을 실행하여 이름을 바꿀 수 있습니다.
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  이전 마이그레이션 성공 레코드가 없는지 확인합니다. 레코드가 있으면 해당 값을 `$false`로 설정해야 합니다. 값이 `$true`로 설정될 경우 마이그레이션 요청이 실패합니다.
    
    1.  다음 예에서는 공용 폴더 마이그레이션 상태를 확인합니다.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  *PublicFoldersLockedforMigration* 또는 *PublicFolderMigrationComplete* 속성의 상태가 `$true`인 경우 다음 명령을 실행하여 값을 `$false`로 설정합니다.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    
    > [!CAUTION]
    > 이러한 속성을 다시 설정한 후 새로운 설정을 감지 하는 Exchange에 대 한 대기 해야 합니다. 이 완료 하려면 두 시간까지 걸릴 수 있습니다.


4.  확인을 위해 마이그레이션의 끝에, 현재 공용 폴더 배포의 스냅숏을를 레거시 Exchange 서버에서 다음 Exchange 관리 셸 명령을 먼저 실행 하는 것이 좋습니다.
    
    1.  다음 명령을 실행하여 원래 원본 폴더 구조의 스냅숏을 만듭니다.
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  다음 명령을 실행하여 항목 수, 크기 및 소유자와 같은 공용 폴더 통계에 대한 스냅숏을 만듭니다.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  다음 명령을 실행하여 사용 권한의 스냅숏을 만듭니다.
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    마이그레이션이 완료되면 비교를 위해 위 명령의 정보를 저장합니다.

5.  Microsoft Azure Active Directory에 연결 (Azure AD 연결)을 사용 하 Azure Active Directory와 온-프레미스 디렉터리를 동기화 하는, 하는 경우 다음을 수행 해야 합니다 (Azure AD 연결을 사용 하지 않는 경우이 단계는 건너뛰어도이):
    
    1.  온-프레미스 컴퓨터에 Microsoft Azure Active Directory 연결을 열고 **구성** 을 선택 합니다.
    
    2.  **추가 작업** 화면에서 **사용자 지정 동기화 옵션** 을 선택 하 고 을 클릭 합니다.
    
    3.  **Azure AD에 연결** 화면에서 적절 한 자격 증명을 입력 하 고 을 클릭 합니다. 연결 되 면 **다음** 때까지 계속 클릭 **선택적 기능** 화면에 표시 된 있습니다.
    
    4.  **Exchange 메일 공용 폴더의** 선택 되지 않았는지 확인 합니다. 선택 하지 않은 경우에 *Office 365 또는 Exchange Online의 필수 구성 단계*는 다음 섹션을 계속 수 있습니다. 을 선택 하는 경우 확인란을 선택 취소를 클릭 한 후에 **다음** 을 클릭 합니다.
        

        > [!NOTE]
        > <STRONG>메일 공용 폴더의 Exchange</STRONG> 보이지 않으면 <STRONG>선택적 기능</STRONG> 화면에서 옵션으로 Microsoft Azure Active Directory 연결을 종료 하 고 <EM>Office 365 또는 Exchange Online의 필수 구성 단계</EM>는 다음 섹션으로 이동 수 있습니다.

    
    5.  **Exchange 메일 공용 폴더의** 선택 영역을 선택을 취소 한 후 유지 **구성 준비가** 화면에 나타날 때까지 **다음** 을 클릭 하 고 **구성** 을 클릭 합니다.

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [New-AcceptedDomain](https://technet.microsoft.com/ko-kr/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/ko-kr/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ko-kr/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/ko-kr/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/ko-kr/library/bb124365\(v=exchg.150\))

  - [Get-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Office 365 또는 Exchange Online에서 수행할 필수 단계**

1.  기존 공용 폴더 마이그레이션 요청 없는 없는지 확인 합니다. 가 있는 경우 해당 비우거나 직접 마이그레이션 요청이 실패 합니다. 이 단계는 모든 경우;에 필요 하지 않습니다. 파이프라인에 기존 마이그레이션 요청 수를 생각 하는 경우에 필요에 해당 합니다.
    
    기존 마이그레이션 요청 두 유형 중 하나일 수 있습니다: 마이그레이션 일괄 처리 또는 직렬 마이그레이션입니다. 각 종류의 요청을 제거 하 고 각 형식에 대 한 요청 하 여 검색에 대 한 명령은 다음과 같습니다.
    

    > [!IMPORTANT]
    > 마이그레이션 요청을 제거 하기 전에 이해 하는 이유 기존 했습니다. 다음 명령을 실행 하는 이전 요청이 수행 된 시기를 결정 하 고 발생 했을 수 있는 문제를 진단 하는데 도움이 됩니다. 변경 이유를 확인 하려면 조직에서 다른 관리자와 통신 해야할 수 있습니다.

    
    다음 예제에서는 기존 직렬 마이그레이션 요청을 모두 검색 합니다.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    다음 예제에서는 기존 공용 폴더 직렬 마이그레이션 요청을 모두 제거합니다.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    다음 예제에서는 기존 일괄 마이그레이션 요청을 모두 검색 합니다.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    다음 예제에서는 기존 공용 폴더 일괄 마이그레이션 요청을 모두 제거합니다.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Office 365에 공용 폴더 또는 공용 폴더 사서함이 없는지 확인합니다.
    

    > [!IMPORTANT]
    > Office 365 또는 Exchange Online의 공용 폴더를 표시 하는 경우에 다음과 같은 됩니다 이유 및 공용 폴더 및 공용 폴더 사서함을 제거 하기 전에 공용 폴더 계층 구조를 시작 하면 조직에서 사용자를 확인 하는 것이 중요 합니다.

    
    1.  Office 365 또는 Exchange Online PowerShell에서 다음 명령을 실행하여 공용 폴더 사서함이 있는지 확인합니다.
        
            Get-Mailbox -PublicFolder 
    
    2.  이 명령은 모든 공용 폴더 사서함을 반환 하지 않았으므로, 하는 경우를 계속 받을 3 단계:.csv 파일 생성합니다. 명령은 모든 공용 폴더 사서함을 반환 하는 경우에 공용 폴더가 있는지 확인 하려면 다음 명령을 실행 합니다.
        
            Get-PublicFolder
    
    3.  Office 365 또는 Exchange Online에서 공용 폴더가 있으면 버전을 제거한 다음 PowerShell 명령을 실행 합니다. Office 365의 공용 폴더에 있던 모든 정보를 저장 하면 있는지 확인 하십시오. 공용 폴더를 제거 하면 공용 폴더에 포함 된 모든 정보가 영구적으로 삭제 됩니다.
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  공용 폴더가 제거 되 면 모든 공용 폴더 사서함을 제거 하려면 다음 명령을 실행 합니다.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하세요.

  - [Get-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/ko-kr/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/ko-kr/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/ko-kr/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/ko-kr/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/ko-kr/library/aa995948\(v=exchg.150\))

## 3단계: .csv 파일 생성

1.  레거시 Exchange 서버에서 폴더 이름-폴더 크기 매핑 파일을 만드는 `Export-PublicFolderStatistics.ps1` 스크립트를 실행 합니다. 이 스크립트는 로컬 관리자가 항상 실행 해야 합니다. 파일 두 열이 포함 되어: **FolderName** 및 **FolderSize** 합니다. 바이트에서 **FolderSize** 열에 대 한 값을 표시 됩니다. 예: **\\PublicFolder01,10000** 합니다.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server*는 공용 폴더 계층이 호스트되는 사서함 서버의 정규화된 도메인 이름과 같습니다.
    
      - *Folder to size map path*는 .csv 파일을 저장할 네트워크 공유 폴더의 경로 및 파일 이름과 같습니다. 이 항목 뒷부분에서 Exchange Online PowerShell을 사용하여 이 파일에 액세스해야 합니다. 파일 이름만 지정하면 로컬 컴퓨터의 현재 PowerShell 디렉터리에 파일이 생성됩니다.
    
      - 필요한 경우 계속 하기 전에 스크립트 출력에서 모든 메일 사용이 가능한 시스템 폴더를 제거 합니다.

2.  `PublicFolderToMailboxMapGenerator.ps1` 스크립트를 실행하여 공용 폴더와 사서함 매핑 파일을 만듭니다. 이 파일은 Exchange Online에서 공용 폴더 사서함의 정확한 수를 계산하는 데 사용됩니다.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    

    > [!IMPORTANT]
    > 공용 폴더와 사서함 매핑 파일 1, 000 행을 초과 하지 않아야 합니다. 1, 000 행을 초과 하는이 파일을 간단 하 게 공용 폴더 구조를 만들어야 합니다. 행 1, 000 보다 큰 파일을 진행 하지 않기 및 마이그레이션 오류가 발생할 수 있습니다.

    
      - 스크립트를 실행 하기 전에 Exchange Online 테 넌 트의 현재 공용 폴더 제한 확인 하려면 다음 cmdlet을 사용 합니다. 그런 다음, note 공용 폴더에 대 한 현재 할당량 값입니다. `Get-OrganizationConfig | fl *quota*`
        
        Exchange Online의 기본값은 **DefaultPublicFolderIssueWarningQuota** 에 대 한 1.7 g B 및 **DefaultPublicFolderProhibitPostQuota**에 대 한 2GB 합니다.
    
      - *Maximum mailbox size in bytes* 새 공용 폴더 사서함에 대해 설정 하려는 최대 크기를 같습니다. Exchange Online에서 공용 폴더 사서함의 최대 크기를 100GB 됩니다. 각 공용 폴더 사서함이 커질 공간을 되도록 15GB의 설정을 사용 하는 것이 좋습니다. Exchange Online에 2GB의 기본 공용 폴더 "일 때 게시 금지" 할당량 있습니다. 2GB 보다 큰 경우에 개별 공용 폴더를 사용 하는 경우이 문제를 해결 하려면 다음 옵션 중 하나를 사용할 수 있습니다.
        
          - 마이그레이션 일괄 처리를 시작 하기 전에 다음 cmdlet을 실행 하 여 기본 공용 폴더 "일 때 게시 금지" 할당량을 늘립니다.
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - 마이그레이션 일괄 처리를 시작 하기 전에 콘텐츠 크기를 줄이려면 콘텐츠를 2GB 이하로 공용 폴더를 삭제 합니다.
        
          - 마이그레이션 일괄 처리를 시작 하기 전에 여러 공용 폴더를 각기 2gb 이하인 공용 폴더를 분할 합니다.
        

        > [!NOTE]
        > 공용 폴더는 30 GB 보다 큰 하 고 콘텐츠를 삭제 하거나 여러 공용 폴더로 분할 하는 것이 불가능, 하는 경우 좋습니다 하는 경우 Exchange Online으로 공용 폴더를 이동 하지 않습니다.

    
      - *Folder to size map path* `Export-PublicFolderStatistics.ps1` 스크립트를 실행 했을 때 만든.csv 파일의 파일 경로를 같습니다.
    
      - 이 단계에서 만든 폴더와 사서함.csv 파일의 경로 파일 이름을 *Folder to mailbox map path* 것과 같습니다. 파일 이름만 지정 하면 로컬 컴퓨터에서 현재 PowerShell 디렉터리에 파일 생성 됩니다.


> [!NOTE]
> 스크립트가 실행 된 후.csv 파일이 생성 된 모든 새 공용 폴더 또는 기존 공용 폴더에 대 한 업데이트 수집 되지 않습니다.



## 4단계: Exchange Online에서 공용 폴더 사서함 만들기

1.  대상 공용 폴더 사서함을 만들려면 다음 명령을 실행합니다. 이 스크립트를 실행하면 이전에 3단계에서 PublicFoldertoMailboxMapGenerator.ps1 스크립트를 실행하여 생성한 .csv 파일에 각 사서함의 대상 사서함이 만들어집니다.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv*는 3단계에서 PublicFoldertoMailboxMapGenerator.ps1 스크립트에 의해 생성된 파일입니다. 공용 폴더 계층 구조를 검색하는 예상 동시 사용자 연결 수가 일반적으로 조직의 전체 사용자 수보다 작습니다.

## 5단계: 마이그레이션 요청 시작

1.  레거시 Exchange 서버에서 메일 사용이 가능한 공용 폴더를 동기화 로컬 Active Directory에서 Exchange online에 다음 명령을 실행 합니다.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` Office 365 사용자 이름과 암호는 합니다. `CsvSummaryFile` 는 파일 경로 로그온 하려는입니다. 동기화 작업 및 오류 CSV 형식입니다.
    

    > [!NOTE]
    > 이 스크립트는 실제로 <CODE>-WhatIf</CODE> 매개 변수와 함께 스크립트를 실행 하 여 수행할 수 있는 작업 하는 것을 실행 하기 전에 수행할 작업을 먼저 시뮬레이션 하는 것이 좋습니다.



2.  레거시 Exchange 서버에서 마이그레이션 요청을 실행하는 데 필요한 다음 정보를 가져옵니다.
    
    1.  Public Folder Administrator 역할 구성원인 사용자 계정의 `LegacyExchangeDN`을 찾습니다. 이 절차의 3단계에서 바로 이 사용자의 자격 증명이 필요합니다.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  공용 폴더 데이터베이스가 있는 사서함 서버의 `LegacyExchangeDN` 를 소개 합니다.
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  외부에서 Outlook 사용 호스트 이름의 FQDN을 찾습니다. 외부에서 Outlook 사용 인스턴스가 여러 개이면 마이그레이션 끝점에서 가장 가까운 인스턴스 또는 레거시 Exchange 조직의 공용 폴더 복제본에 가장 가까운 인스턴스를 선택하는 것이 좋습니다. 다음 명령은 외부에서 Outlook 사용의 모든 인스턴스를 찾습니다.
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  Office 365 PowerShell에서 다음 마이그레이션 요청에 사용 되는 변수가 이전 단계에서 반환 된 정보를 전달 하려면 다음 명령을 실행 합니다.
    
    1.  변수 `$Source_Credential`에 레거시 Exchange 서버에 대 한 관리 권한이 있는 사용자의 자격 증명을 전달 합니다. 가 실행 하는 Exchange Online 마이그레이션 요청을 통해 콘텐츠를 복사 하 여 레거시 Exchange 서버에 대 한 액세스를 확보 합니다.이 자격 증명을 사용 합니다.
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  2a 단계에서에서 확인 하 고 변수 `$Source_RemoteMailboxLegacyDN`으로 전달 레거시 Exchange 서버에서 마이그레이션 사용자의 `ExchangeLegacyDN` 를 사용 합니다.
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  위의 2b 단계에서에서 찾은 변수 `$Source_RemotePublicFolderServerLegacyDN`으로 전달 하는 공용 폴더 서버의 `ExchangeLegacyDN` 를 사용 합니다.
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  외부 호스트 이름을의 외부에서 Outlook 사용 위의 2c 단계에서 확인 하 고 변수 `$Source_OutlookAnywhereExternalHostName`으로 전달 합니다.
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  마지막으로, Exchange Online PowerShell에서 마이그레이션 요청을 만들려면 다음 명령을 실행 합니다.
    

    > [!NOTE]
    > 외부에서 Outlook 사용 설정에 맞게 다음 Exchange 관리 셸 예제 요구 사항에서 인증 방법, 그렇지 않은 경우 명령이 실패 합니다.

    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    \<*folder\_mapping.csv*\> 파일이 파일에서 생성 된 3 단계:.csv 파일 생성합니다.

5.  다음 명령을 사용 하 여 마이그레이션을 시작 합니다.
    
        Start-MigrationBatch PublicFolderMigration

마이그레이션 일괄 처리를 Exchange 관리 셸 에서 **New-MigrationBatch** cmdlet을 사용 하 여 만들 필요가 하는 동안 진행 상황 및 마이그레이션이 완료 되 면 표시 하 고 관리할 수 EAC에서 합니다. **New-migrationbatch** cmdlet가 각 공용 폴더 사서함에 대 한 사서함 마이그레이션 요청을 시작 하기 때문에 사서함 마이그레이션 페이지를 사용 하 여 이러한 요청의 상태를 볼 수 있습니다. 사서함 마이그레이션 페이지로 이동 하 고 다음을 수행 하 여, 발송 될 수 있는 마이그레이션 보고서를 만들 수 있습니다.

1.  Exchange Online에 로그인 하 고 EAC를 엽니다.

2.  **사서함** \> **마이그레이션**으로 이동합니다.

3.  방금 만든 마이그레이션 요청을 선택 하 고 **세부 정보** 창에서 **자세히 보기를** 클릭 합니다.

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하세요.

  - [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/ko-kr/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/ko-kr/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ko-kr/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/ko-kr/library/jj218697\(v=exchg.150\))

## 6단계: 최종 마이그레이션을 위해 레거시 Exchange 서버에서 공용 폴더 잠그기(가동 중지 시간 필요)

마이그레이션 프로세스의이 시점까지 사용자가 참가 한 공용 폴더에 액세스할 수 있습니다. 다음 단계 레거시 공용 폴더에서 사용자를 로그 오프 하 고 마이그레이션 해당 최종 동기화를 완료 하는 동안 폴더를 잠글 됩니다. 사용자가이 과정에서 공용 폴더에 액세스할 수 없습니다. 또한 메일 사용이 가능한 공용 폴더에 보낸 모든 메일은 대기 하 고 공용 폴더 마이그레이션 완료 될 때까지 배달 되지 않습니다.

아래 설명과 같이 `PublicFoldersLockedForMigration` 명령을 실행 하기 전에 모든 작업을 **동기화 됨** 상태에 있는지 확인 합니다. `Get-PublicFolderMailboxMigrationRequest` 명령을 실행 하 여이 수행할 수 있습니다. 모든 작업을 **동기화 됨** 상태에 있는지 확인 한 후에이 단계를 계속 합니다.

레거시 Exchange 서버에서 다음 명령을 실행하여 마이그레이션 완료를 위해 레거시 공용 폴더를 잠급니다.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

구문과 매개 변수에 대한 자세한 내용은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\))를 참조하십시오.

조직에 여러 공용 폴더 데이터베이스가 있는 경우 공용 폴더 복제가 완료되어 모든 공용 폴더 데이터베이스에서 `PublicFoldersLockedForMigration` 플래그를 선택하고 사용자가 최근에 폴더에 수행한 보류 중인 변경 내용이 조직 전체에 적용되었음이 확인될 때까지 기다려야 합니다. 이 작업을 수행하는 데 몇 시간이 걸릴 수 있습니다.

## 7단계: 공용 폴더 마이그레이션 완료(가동 중지 시간 필요)

공용 폴더 마이그레이션을 완료 하려면 다음 명령을 실행 합니다.

    Complete-MigrationBatch PublicFolderMigration

마이그레이션 완료 하면 Exchange 레거시 Exchange 서버와 Exchange Online 간의 최종 동기화를 수행 합니다. 마지막 동기화가 성공적으로, Exchange Online의 공용 폴더를 잠금이 해제 됩니다 하 고 마이그레이션 일괄 처리의 상태가 **완료** 로 변경 됩니다. 일반적으로 마이그레이션 일괄 처리 **동기화 됨** 에서 **완료** 상태는 변경 하기 전에 몇 시간까지 걸릴, 나타나는데 최종 동기화 시작 됩니다.

온-프레미스 Exchange 서버와 Office 365 간의 하이브리드 배포를 구성한 경우 다음 명령을 실행 Exchange Online PowerShell 마이그레이션이 완료 된 후 해야 합니다.

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 8단계: 공용 폴더 마이그레이션 테스트 및 잠금 해제

공용 폴더 마이그레이션을 완료한 후에는 다음 테스트를 실행하여 마이그레이션이 성공했는지 확인해야 합니다. 이를 통해 Office 365 또는 Exchange Online 공용 폴더를 사용하도록 전환하기 전에 마이그레이션된 공용 폴더 계층 구조를 테스트할 수 있습니다.

1.  Office 365 또는 Exchange Online PowerShell에서 새로 마이그레이션된 공용 폴더 사서함을 기본 공용 폴더 사서함으로 사용할 일부 테스트 사서함을 지정합니다.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  이전 단계에서 식별된 테스트 사용자로 Outlook 2007 이상에 로그온하여 다음 공용 폴더 테스트를 수행합니다.
    
      - 계층 구조를 확인합니다.
    
      - 사용 권한을 확인합니다.
    
      - 공용 폴더를 만들고 삭제합니다.
    
      - 공용 폴더에 콘텐츠를 게시한 후 삭제합니다.

3.  문제를 실행 하는 경우이 항목의 뒷부분에 마이그레이션 롤백 을 참조 합니다. 허용 되는 및 예상한 대로 작동 하는 공용 폴더 콘텐츠 및 계층 구조, 하는 경우 다음 단계를 계속 합니다.

4.  레거시 Exchange 서버에서 다음 명령을 실행하여 공용 폴더 마이그레이션이 완료되었음을 나타냅니다.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  마이그레이션이 완료 되는 확인 한 후 다음 명령을 실행 Exchange Online PowerShell **Set-OrganizationConfig** 에서 *PublicFoldersEnabled* 매개 변수는 `Local`로 설정 되어 있는지 확인 하려면:
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

[Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

2 단계: 마이그레이션 준비, 마이그레이션을 시작 하기 전에 공용 폴더 구조, 통계, 그리고 사용 권한의 스냅숏을 가능 하다. 다음 단계는 마이그레이션이 완료 된 후 동일한 스냅숏을 수행 하 여 공용 폴더 마이그레이션 완료 되었는지 확인 하는 데 도움이 됩니다. 그런 다음 성공 여부를 확인 하려면 두 파일의 데이터를 비교할 수 있습니다.

1.  Exchange Online PowerShell에서 다음 명령을 실행하여 새 폴더 구조의 스냅숏을 만듭니다.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  Exchange Online PowerShell에서 다음 명령을 실행하여 항목 수, 크기 및 소유자와 같은 공용 폴더 통계에 대한 스냅숏을 만듭니다.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  Exchange Online PowerShell에서 다음 명령을 실행하여 사용 권한의 스냅숏을 만듭니다.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 레거시 Exchange 서버에서 공용 폴더 데이터베이스 제거

마이그레이션이 완료되고 Exchange Online 공용 폴더가 예상대로 작동하는 것을 확인한 후에는 레거시 Exchange 서버에서 공용 폴더 데이터베이스를 제거해야 합니다.


> [!IMPORTANT]
> 사용자 사서함의 모든 Office 365에 공용 폴더 마이그레이션 전에 마이그레이션한 이후의 것이 좋습니다 (분산 된 메일 흐름) Office 365를 통해 트래픽을 라우팅하는 온-프레미스 환경을 통해 중앙집중식된 메일 흐름 대신 합니다. 중앙 집중화 하는 메일 흐름을 유지 하려는 경우 온-프레미스 조직에서 공용 폴더 사서함 데이터베이스를 제거 했을 때 이후에서 공용 폴더에 배달 문제를 일으킬 수 있습니다.



  - Exchange 2007 서버에서 공용 폴더 데이터베이스를 제거 하는 방법에 대 한 자세한 내용은, [공용 폴더 데이터베이스 제거](https://go.microsoft.com/fwlink/?linkid=123678)을 참조 하십시오.

  - Exchange 2010 서버에서 공용 폴더 데이터베이스를 제거 하는 방법에 대 한 자세한 내용은, [공용 폴더 데이터베이스 제거](https://go.microsoft.com/fwlink/?linkid=81409)을 참조 하십시오.

## 마이그레이션 롤백

마이그레이션과 관련된 문제가 발생하여 레거시 Exchange 공용 폴더를 다시 활성화해야 하는 경우 다음 단계를 수행하십시오.

> [!CAUTION]
> 롤백하는 경우 마이그레이션 레거시 Exchange 서버에, 메일 사용이 가능한 공용 폴더 또는 공용 폴더 마이그레이션 후 게시 된 콘텐츠에 게 보낸 모든 전자 메일을 손실 됩니다. 이 콘텐츠를 저장 하려면 공용 폴더 콘텐츠를.pst 파일로 내보내고 롤백을 완료 되 면 레거시 공용 폴더를 가져올 해야 합니다.


1.  레거시 Exchange 서버에서 다음 명령을 실행하여 레거시 Exchange 공용 폴더의 잠금을 해제합니다. 이 프로세스를 수행하는 데 몇 시간이 걸릴 수 있습니다.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  Exchange Online PowerShell에서 다음 명령을 실행하여 모든 Exchange Online 공용 폴더를 제거합니다.
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  레거시 Exchange 서버에서 다음 명령을 실행하여 `PublicFolderMigrationComplete` 플래그를 `$false`로 설정합니다.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Outlook PST 내보내기를 사용하여 공용 폴더를 Office 365로 마이그레이션

온-프레미스 공용 폴더 계층 구조가 30GB보다 크면 공용 폴더를 Office 365 또는 Exchange Online으로 마이그레이션할 때 Outlook의 PST 내보내기 기능을 사용하지 않는 것이 좋습니다. Office 365 온라인 공용 폴더 사서함이 크기 할당량을 초과하면 사서함을 분할하는 자동 분할 기능을 사용하여 Exchange 온라인 공용 폴더 사서함 크기 증가를 관리합니다. PST 내보내기를 사용하여 공용 폴더를 마이그레이션하는 경우 자동 분할 기능이 공용 폴더 사서함의 갑작스러운 크기 증가를 처리할 수 없으므로 자동 분할 기능이 데이터를 기본 사서함에서 이동할 때까지 최대 2주 동안 기다려야 할 수 있습니다. 또한 Outlook PST를 사용하여 Office 365 또는 Exchange Online으로 공용 폴더를 내보내기 전에 다음 사항을 고려하세요.

  - 이 프로세스 중에는 공용 폴더 사용 권한이 손실됩니다. 마이그레이션하기 전에 현재 사용 권한을 캡처하고 마이그레이션이 완료된 후에 수동으로 다시 추가합니다.

  - 복잡한 사용 권한을 사용하거나 마이그레이션할 폴더가 많은 경우에는 cmdlet 방식을 통해 마이그레이션하는 것이 좋습니다.

  - PST 내보내기 마이그레이션 중에 원본 공용 폴더에 적용한 모든 항목 및 폴더 변경 내용은 손실됩니다. 따라서 이 내보내기 및 가져오기 프로세스를 완료하는 데 시간이 오래 걸리는 경우에는 cmdlet 방식을 사용하는 것이 좋습니다.

그래도 PST 파일을 사용하여 공용 폴더를 마이그레이션하려는 경우 다음 단계를 통해 마이그레이션이 정상적으로 수행되는지 확인하세요.

1.  지침을 사용 하 여 1 단계: 마이그레이션 스크립트를 다운로드 마이그레이션 스크립트를 다운로드 합니다. `PublicFolderToMailboxMapGenerator.ps1` 파일을 다운로드 해야 합니다.

2.  단계 중 2 단계에 따라 3 단계:.csv 파일 생성 공용 폴더와 사서함 매핑 파일을 만듭니다. 이 파일은 Exchange Online의 공용 폴더 사서함의 올바른 수를 계산 하는데 사용 됩니다.

3.  매핑 파일을 기준으로 필요한 공용 폴더 사서함을 만듭니다. 자세한 내용은 [공용 폴더 사서함 만들기](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/create-public-folder-mailbox)를 참조하세요.

4.  New-PublicFolder cmdlet을 사용하여 각 공용 폴더 사서함의 최상위 공용 폴더를 만듭니다(*Mailbox* 매개 변수 사용).

5.  Outlook을 사용하여 PST 파일을 내보내거나 가져옵니다.

6.  EAC를 사용하여 공용 폴더에 사용 권한을 설정합니다. 자세한 내용은 [새 조직에서 공용 폴더 설정](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/set-up-public-folders) 항목의 [Step 3: Assign permissions to the public folder](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/set-up-public-folders)을 참조하세요.

> [!CAUTION]
> PST 마이그레이션을 이미 시작했는데 기본 사서함이 가득 찬 문제가 발생하는 경우에는 두 가지 옵션을 통해 PST 마이그레이션을 복구할 수 있습니다.
> <ol>
> <li><p>자동 분할 기능이 기본 사서함에서 데이터를 이동할 때까지 기다립니다. 데이터가 이동되려면 최대 2주가 걸릴 수 있습니다. 그러나 자동 분할이 완료될 때까지 완전히 채워진 공용 폴더 사서함의 모든 공용 폴더는 새 콘텐츠를 받을 수 없습니다.</p></li>
> <li><p><a href="https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/create-public-folder-mailbox">공용 폴더 사서함 만들기</a>를 수행한 다음 <em>Mailbox</em> 매개 변수를 포함한 <strong>New-PublicFolder</strong> cmdlet을 사용하여 보조 공용 폴더 사서함에 나머지 공용 폴더를 만듭니다. 이 예에서는 보조 공용 폴더 사서함에 PF201이라는 새 공용 폴더를 만듭니다.</p>
> <pre><code>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</code></pre></li>
> </ol>


## Office 365의 새로운 기능


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="LinkedIn Learning용 단축 아이콘" alt="LinkedIn Learning용 단축 아이콘" /> <strong>Office 365를 처음 사용하시나요?</strong><br />
LinkedIn Learning에서 제공하는 <a href="https://support.office.com/en-us/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>의 무료 비디오 과정을 확인해보세요.</p></td>
</tr>
</tbody>
</table>

