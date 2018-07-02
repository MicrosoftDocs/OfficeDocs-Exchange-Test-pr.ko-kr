---
title: '마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션: Exchange 2013 Help'
TOCTitle: 마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64126827
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-03-26_

**요약**:이 문서는 Exchange 2007 또는 Exchange 2010에서 Exchange 2013 공용 폴더를 이동 하는 방법을 보여줍니다.

이 문서에서는 Microsoft Exchange Server 2013 CU7 또는 같은 포리스트 내의 나중에 Exchange Server 2010 s p 3 RU8 또는 Exchange 2007 s p 3 RU15에서 공용 폴더를 마이그레이션하는 방법에 설명 합니다.

*레거시 Exchange 서버*와 Exchange 2010 s p 3 RU8 및 Exchange 2007 s p 3 RU15 서버에 지칭 합니다.


> [!NOTE]
> 이 문서에서 설명 하는 일괄 마이그레이션 방법을 마이그레이션 레거시 공용 폴더를 Exchange 2013에 대 한 지원 되는 유일한 방법입니다. 공용 폴더 마이그레이션에 대 한 이전 직렬 마이그레이션 방법은 되 고 사용 되지 않으며 Microsoft에서 더이상 지원 됩니다.



문제를 해결 하는 것에 대 한 **\*MigrationBatch** cmdlet 및 **\*PublicFolderMigrationRequest** cmdlet을 사용 하 여 마이그레이션을 수행 합니다. 또한 다음 PowerShell 스크립트를 사용 합니다.

  - `Export-PublicFolderStatistics.ps1` 이 스크립트는 폴더 이름-폴더 크기 매핑 파일을 만듭니다.

  - ` Export-PublicFolderStatistics.psd1` 이 지원 파일은 Export-publicfolderstatistics.ps1 스크립트에 사용 되며 같은 위치로 다운로드 해야 합니다.

  - `PublicFolderToMailboxMapGenerator.ps1` 이 스크립트는 공용 폴더와 사서함 매핑 파일을 만듭니다.

  - `PublicFolderToMailboxMapGenerator.strings.psd1` 이 지원 파일은 PublicFolderToMailboxMapGenerator.ps1 스크립트에서 사용 하 고 같은 위치로 다운로드 해야 합니다.

  - `Create-PublicFolderMailboxesForMigration.ps1` 이 스크립트는 마이그레이션에 대 한 대상 공용 폴더 사서함을 만듭니다. 또한이 스크립트는 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)에서 권장 하는 공용 폴더 사서함당 사용자 로그온 수에 대 한 지침에 따라 예상된 사용자 부하를 처리 하는 데 필요한 사서함 수를 계산 합니다.

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` 이 지원 파일은 만들기 PublicFolderMailboxesForMigration.ps1 스크립트에 사용 되며 같은 위치로 다운로드 해야 합니다.

1 단계: 마이그레이션 스크립트를 다운로드 이러한 스크립트를 다운로드 하는 위치에 대 한 세부 정보를 제공 합니다. 모든 스크립트 같은 위치로 다운로드 되 고 있는지 확인 하십시오.

공용 폴더와 관련된 추가 관리 작업에 대한 자세한 내용은 [공용 폴더 절차](public-folder-procedures-exchange-2013-help.md)를 참조하십시오.

## 공용 폴더를 Exchange 2013으로 마이그레이션하는 데 지원되는 Exchange 버전은 무엇입니까?

Exchange에서 공용 폴더의 이동을 지원하는 Exchange Server의 레거시 버전은 다음과 같습니다.

  - Exchange 2010 s p 3 RU8 이상

  - Exchange 2007 s p 3 RU15 이상

Exchange 2013 공용 폴더를 이동 하는 경우 온-프레미스 서버 최소 지원 버전의 Exchange 2010 또는 Exchange 2007을 실행 하지 않는 [직렬 마이그레이션을 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션](https://technet.microsoft.com/ko-kr/library/jj150486\(v=exchg.150\))체크아웃 합니다. 직렬 마이그레이션 옵션 이지만는 것이 좋습니다 온-프레미스 서버를 업그레이드 하 고 마이그레이션 일괄 처리 기능을 사용 합니다. 훨씬 더 빠르고 더 많은 안정성에 대 한 마이그레이션 일괄 처리 수 있습니다.

Exchange 2003에서 직접 공용 폴더를 마이그레이션할 수 없습니다. 조직에서 Exchange 2003을 실행 하는 경우 모든 공용 폴더 데이터베이스 및 Exchange 2010 s p 3 RU8 또는 나중에 Exchange 2007 s p 3 RU15 또는 나중에 복제 데이터베이스를 이동 해야 합니다. 공용 폴더 복제본 Exchange 2003에 남아 있을 수 있습니다. 또한 Exchange 2003 서버를 통해 Exchange 2013 공용 폴더에 대 한 대상으로 메일을 라우팅할 수 없습니다.

## 시작하기 전에 알아야 할 내용

  - 일부 단계의 경우 가동 중지 시간이 필요하므로 시작하기 전에 이 항목 전체를 읽어 보십시오.

  - Exchange 2010 서버에서 Exchange 2010 s p 3 RU8를 실행 해야하는 이상입니다.

  - Exchange 2007 서버에서 Exchange 2007 s p 3 RU15를 실행 해야하는 이상입니다.

  - 단일 마이그레이션에 Exchange 2013으로 마이그레이션할 수 있는 공용 폴더의 최대 수는 500, 000입니다.

  - Exchange 2013, 해야하는 조직 관리 역할 그룹의 구성원 이어야 합니다. 조직 관리 역할 그룹을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은, [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)을 참조 하십시오.

  - Exchange 2010, 해야하는 조직 관리 또는 서버 관리 RBAC 역할 그룹의 구성원 이어야 합니다. 자세한 내용은 [역할 그룹에 구성원 추가](https://go.microsoft.com/fwlink/?linkid=299212)를 참조 하십시오.

  - Exchange 2007, 해야 Exchange 조직 관리자 역할 또는 Exchange Server 관리자 역할이 할당 되어야 합니다. 또한 공용 폴더 관리자 역할 및 대상 서버에 대 한 로컬 관리자 그룹에 할당 해야 합니다. 자세한 내용은 [사용자 또는 그룹 관리자 역할을 추가 하는 방법](https://go.microsoft.com/fwlink/p/?linkid=81779)를 참조 하십시오.

  - Exchange 2007 서버에서 [Windows Server 2008 x64 Edition용 Windows PowerShell 2.0 및 WinRM 2.0](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930)으로 업그레이드합니다.

  - 마이그레이션하기 전에 [공용 폴더의 제한](limits-for-public-folders-exchange-2013-help.md)을 고려해야 합니다.

  - 를 마이그레이션하기 전에 Exchange 2007 또는 Exchange 2010 사서함을 가진 사용자는 Exchange 2013에 있는 공용 폴더에 액세스 권한이 없는 하기 때문에 모든 사용자 사서함을 Exchange 2013으로 이동 합니다. 자세한 내용은 [Exchange 2013 사서함 이동](mailbox-moves-in-exchange-2013-exchange-2013-help.md)를 참조 합니다.

  - 다중 도메인 환경에서 메일 사용이 가능한 공용 폴더는 Exchange 자식 도메인에서 실행 중인 경우 Exchange 2013으로 마이그레이션 후 올바르게 작동 중지 됩니다. 해야 하기 때문에 Exchange 2013, 메일 사용이 가능한 공용 폴더 개체는 루트 도메인에서 사용 중인 것입니다. 이 해결 하려면 메일 불가능 하 여 메일 사용이 가능한 공용 폴더 및 다음 메일 사용이 가능한 다시, 올바른 도메인 위치로 이동 하는 수 있도록 해야 합니다.

  - 마이그레이션 후은 **익명** 사용자에 게 수에 필요한 외부의 보낸 사람이 마이그레이션된 메일 사용이 가능한 공용 폴더에 메일을 보낼 수를 원하는 경우 완료 권한이 적어도 **항목 만들기**. 이렇게 하지 않으면 외부 보낸 사람이 배달 실패 알림의 받을 하 고 마이그레이션된 메일 사용이 가능한 공용 폴더에 메시지를 배달 하지 않습니다. 읽기를 익명 사용자에 대해 사용 권한을 설정 하는 방법에 대 한 자세한 [메일 사용이 가능한 또는 공용 폴더 메일-사용 안함](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 마이그레이션 스크립트 다운로드

1.  [공용 폴더 마이그레이션 스크립트](https://go.microsoft.com/fwlink/?linkid=299838)에서 모든 스크립트 및 지원 파일을 다운로드 합니다.

2.  PowerShell을 실행할 로컬 컴퓨터에서 C:\\PFScripts 등의 위치에 스크립트를 저장합니다. 모든 스크립트가 같은 위치에 저장되는지 확인합니다.

## 2단계: 마이그레이션 준비

마이그레이션을 시작하기 전에 다음 필수 구성 단계를 수행합니다.

**레거시 Exchange 서버의 필수 구성 단계**

1.  확인을 위해 마이그레이션의 끝에, 현재 공용 폴더 배포의 스냅숏을를 레거시 Exchange 서버에서 다음 명령을 먼저 실행 하는 것이 좋습니다.
    
      - 원래 원본 폴더 구조의 스냅숏을 하려면 다음 명령을 실행 합니다.
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
      - 항목 수, 크기 및 소유자와 같은 공용 폴더 통계에 대 한 스냅숏을 하려면 다음 명령을 실행 합니다.
        
            Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
      - 하 여 사용 권한의 스냅숏을 다음 명령을 실행 합니다.
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    마이그레이션이 완료된 후 비교를 위해 이전 명령의 정보를 저장합니다.

2.  공용 폴더의 이름에 백슬래시(**\\**)가 포함된 경우 마이그레이션이 수행되면 공용 폴더가 상위 공용 폴더에 만들어집니다. 마이그레이션하기 전에 이름에 백슬래시가 있는 공용 폴더의 이름을 바꾸는 것이 좋습니다.
    
    1.  Exchange 2010에서 이름에 백슬래시가 있는 공용 폴더를 찾으려면 다음 명령을 실행합니다.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Exchange 2007에서 이름에 백슬래시가 있는 공용 폴더를 찾으려면 다음 명령을 실행합니다.
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  공용 폴더가 반환되면 다음 명령을 실행하여 이름을 바꿀 수 있습니다.
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  다음과 같은 성공적인 마이그레이션의 이전 레코드를 있지 않은지 확인 합니다.
    
    1.  다음 예에서는 공용 폴더 마이그레이션 상태를 확인합니다.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        
        이전 성공적인 마이그레이션이 되었으면, *PublicFoldersLockedforMigration* 또는 *PublicFolderMigrationComplete* 속성의 값은 `$true`합니다. `$false`에 값을 설정 하려면 3b 단계에서에서 명령을 사용 합니다. 값 `$true`로설정하면 마이그레이션 요청이 실패 합니다.
    
    2.  *PublicFoldersLockedforMigration* 또는 *PublicFolderMigrationComplete* 속성의 상태가 `$true`인 경우 다음 명령을 실행하여 값을 `$false`로 설정합니다.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>이러한 속성을 다시 설정한 후 새로운 설정을 감지 하는 Exchange에 대 한 대기 해야 합니다. 이 완료 하려면 두 시간까지 걸릴 수 있습니다.</td>
    </tr>
    </tbody>
    </table>


구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-PublicFolder](https://technet.microsoft.com/ko-kr/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ko-kr/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/ko-kr/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/ko-kr/library/bb124365\(v=exchg.150\))

  - [Get-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-organizationconfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Exchange 2013 서버의 필수 구성 요소 단계**

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

2.  없는 공용 폴더 또는 공용 폴더 사서함이 Exchange 2013 서버에 존재 하는지 확인 합니다.
    
    1.  공용 폴더 사서함이 있는지 확인 하려면 다음 명령을 실행 합니다.
        
            Get-Mailbox -PublicFolder 
    
    2.  이 명령은 모든 공용 폴더 사서함을 반환 하지 않았으므로, 하는 경우를 계속 받을 3 단계:.csv 파일 생성합니다. 명령은 모든 공용 폴더를 반환 하는 경우에 공용 폴더가 있는지 확인 하려면 다음 명령을 실행 합니다.
        
            Get-PublicFolder
    
    3.  공용 폴더가 있으면 다음 PowerShell 명령을 사용하여해당 폴더를 제거를 실행 합니다. 공용 폴더에 있던 모든 정보를 저장 하면 있는지 확인 하십시오.
        

        > [!NOTE]
        > 공용 폴더에 포함 된 정보를 모두 제거 하면 영구적으로 삭제 됩니다.

        
            Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
            Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

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

1.  레거시 Exchange 서버에서 폴더 이름-폴더 크기 매핑 파일을 만드는 `Export-PublicFolderStatistics.ps1` 스크립트를 실행 합니다. 이 스크립트는 로컬 관리자가 실행 해야 합니다. 파일 두 열이 포함 되어: **FolderName** 및 **FolderSize** 합니다. 바이트에서 **FolderSize** 열에 대 한 값을 표시 됩니다. 예: **\\PublicFolder01,10000** 합니다.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server*는 공용 폴더 계층이 호스트되는 사서함 서버의 정규화된 도메인 이름과 같습니다.
    
      - .csv 파일을 저장 하려는 네트워크 공유 폴더의 경로 파일 이름을 *Folder to size map path* 것과 같습니다. 이 항목의 뒷부분에 Exchange 2013 서버에서이 파일에 액세스 해야 합니다. 파일 이름만 지정 하면 로컬 컴퓨터에서 현재 PowerShell 디렉터리에 파일을 생성 됩니다.

2.  공용 폴더와 사서함 매핑 파일을 만들려면 `PublicFolderToMailboxMapGenerator.ps1` 스크립트를 실행 합니다. 이 파일은 Exchange 2013 사서함 서버에서 공용 폴더 사서함의 올바른 수를 계산 하는데 사용 됩니다.
    

    > [!NOTE]
    > <STRONG>\</STRONG> 백슬래시를 포함 하는 공용 폴더의 이름, 공용 폴더의 상위 공용 폴더에 만들어집니다. .Csv 파일을 검토 하 고 백슬래시를 포함 하는 이름을 편집 하는 것이 좋습니다.

    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    
      - *Maximum mailbox size in bytes* 새 공용 폴더 사서함에 설정할 최대 크기를 같습니다. 이 설정을 지정 하는 경우에 공용 폴더 사서함이 커질 공간을 있도록 확장을 허용 해야 합니다.
    
      - *Folder to size map path*는 `Export-PublicFolderStatistics.ps1` 스크립트를 실행할 때 만든 .csv 파일의 파일 경로와 같습니다.
    
      - *Folder to mailbox map path*는 이 단계에서 만들 폴더-사서함 .csv 파일의 파일 이름 및 경로와 같습니다. 파일 이름만 지정하면 로컬 컴퓨터의 현재 PowerShell 디렉터리에 파일이 생성됩니다.

## 4 단계: 공용 폴더 사서함을 Exchange 2013를 만들기

1.  대상 공용 폴더 사서함을 만들려면 다음 명령을 실행합니다. 이 스크립트를 실행하면 이전에 3단계에서 PublicFoldertoMailboxMapGenerator.ps1 스크립트를 실행하여 생성한 .csv 파일에 각 사서함의 대상 사서함이 만들어집니다.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv*는 3단계에서 PublicFoldertoMailboxMapGenerator.ps1 스크립트에 의해 생성된 파일입니다. 공용 폴더 계층 구조를 검색하는 예상 동시 사용자 연결 수가 일반적으로 조직의 전체 사용자 수보다 작습니다.

## 5단계: 마이그레이션 요청 시작

Exchange 2007 공용 폴더 마이그레이션에 대 한 단계는 Exchange 2010 공용 폴더 마이그레이션에 대 한 단계와에서 다릅니다.


> [!TIP]
> 일괄 마이그레이션 요청 적절 한 cmdlet을 사용 하 여 만든 후에 Exchange 2007 또는 Exchange 2010에서 마이그레이션, 있는지 여부를 있습니다는 요청을 보려면 하 고 수 EAC에서이 관리 합니다.



**Exchange 2007 공용 폴더 마이그레이션**

1.  예: OWAScratchPad 및 스키마 루트 폴더 하위 트리 레거시 시스템 공용 폴더 Exchange 2007 Exchange 2013에서 인식할 수 없습니다 고 따라서 "불량" 항목으로 취급 됩니다. 이렇게 하면 마이그레이션이 실패 합니다. 마이그레이션 요청의 일부로 `BadItemLimit` 매개 변수에 대 한 값을 지정 해야 합니다. 이 값이 있는 공용 폴더 데이터베이스의 수에 따라 달라 집니다. 다음 명령을 포함 하 고 마이그레이션 요청에 대 한 `BadItemLimit` 계산 얼마나 많은 공용 폴더 데이터베이스를 결정 합니다.
    
        $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
    
        $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)

2.  Exchange 2013 서버에서 다음 명령을 실행 합니다.
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  다음 명령을 사용 하 여 마이그레이션을 시작 합니다.
    
        Start-MigrationBatch PFMigration

**Exchange 2010 공용 폴더 마이그레이션**

1.  Exchange 2013 서버에서 다음 명령을 실행 합니다.
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    
    `NotificationEmails` 매개 변수는 선택 사항입니다.

2.  다음 명령을 사용 하 여 마이그레이션을 시작 합니다.
    
        Start-MigrationBatch PFMigration
    
    또는
    
    EAC에서 마이그레이션을 시작할 수 있습니다.
    
    1.  Exchange Online에 로그인 하 고 EAC를 엽니다.
    
    2.  **받는 사람** 에 게 이동 \> **마이그레이션** 입니다.
    
    3.  방금 만든 마이그레이션 일괄 처리를 선택 하 고 시작 단추를 클릭 합니다.

**상태** 열에는 초기 일괄 처리 상태가 **만들어짐**으로 표시됩니다. 마이그레이션 동안에는 상태가 **동기화 중**으로 바뀝니다. 마이그레이션 요청이 완료되면 상태가 **동기화됨**으로 바뀝니다. 일괄 처리를 두 번 클릭하여 일괄 처리 내의 개별 사서함 상태를 볼 수 있습니다. 사서함 작업은 **대기** 상태로 시작합니다. 작업이 시작되면 상태는 **동기화 중**이 되고, `InitialSync`가 완료되면 **동기화됨**이 됩니다.

진행 상황 및 마이그레이션이 완료 되 면 볼 고 EAC에서 관리할 수 있습니다. **New-migrationbatch** cmdlet가 각 공용 폴더 사서함에 대 한 사서함 마이그레이션 요청을 시작 하기 때문에 사서함 마이그레이션 페이지를 사용 하 여 이러한 요청의 상태를 볼 수 있습니다. 사서함 마이그레이션 페이지로 이동 하 고 다음을 수행 하 여, 발송 될 수 있는 마이그레이션 보고서를 만들 수 있습니다.

1.  Exchange Online에 로그인 하 고 EAC를 엽니다.

2.  **사서함** \> **마이그레이션**으로 이동합니다.

3.  방금 만든 마이그레이션 요청을 선택 하 고 **세부 정보** 창에서 **자세히 보기를** 클릭 합니다.

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/ko-kr/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/ko-kr/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/ko-kr/library/jj218697\(v=exchg.150\))

## 6단계: 최종 마이그레이션을 위해 레거시 Exchange 서버에서 공용 폴더 잠그기(가동 중지 시간 필요)

마이그레이션의 이 시점까지는 사용자가 공용 폴더에 액세스할 수 있습니다. 다음 단계에서는 마이그레이션의 최종 동기화가 완료되는 동안 사용자가 레거시 공용 폴더에서 로그오프되고 공용 폴더가 잠깁니다. 사용자는 이 프로세스 동안 공용 폴더에 액세스할 수 없습니다. 또한 메일 사용 가능 공용 폴더로 전송된 메일이 대기 상태가 되고 공용 폴더 마이그레이션이 완료될 때까지 배달되지 않습니다.

아래 설명과 같이 `PublicFoldersLockedForMigration` 명령을 실행 하기 전에 모든 작업을 **동기화 됨** 상태에 있는지 확인 합니다. `Get-PublicFolderMailboxMigrationRequest` 명령을 실행 하 여이 수행할 수 있습니다. 모든 작업을 **동기화 됨** 상태에 있는지 확인 한 후에이 단계를 계속 합니다.

레거시 Exchange 서버에서 다음 명령을 실행하여 마이그레이션 완료를 위해 레거시 공용 폴더를 잠급니다.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true


> [!NOTE]
> 어떤 이유로 든 마이그레이션 일괄 처리에 대 한 파일 레거시 서버에서 사용 하는 (<STRONG>PublicFolderMigrationComplete</STRONG> 디스플레이 <STRONG>False</STRONG> ) 마무리 하지 않는, 정보 저장소 (IS)를 다시 시작 합니다.



구문과 매개 변수 정보에 대한 자세한 내용은 [Set-OrganizationConfig](https://technet.microsoft.com/ko-kr/library/aa997443\(v=exchg.150\))를 참조하십시오.

조직에 여러 공용 폴더 데이터베이스가 있는 경우 공용 폴더 복제가 완료되어 모든 공용 폴더 데이터베이스에서 `PublicFoldersLockedForMigration` 플래그를 선택하고 사용자가 최근에 폴더에 수행한 보류 중인 변경 내용이 조직 전체에 적용되었음이 확인될 때까지 기다려야 합니다. 이 작업을 수행하는 데 몇 시간이 걸릴 수 있습니다.

## 7단계: 공용 폴더 마이그레이션 완료(가동 중지 시간 필요)

먼저, Exchange 2013 배포 형식을 **원격** 으로 변경 하려면 다음 cmdlet를 실행 합니다.

    Set-OrganizationConfig -PublicFoldersEnabled Remote

이 작업이 끝나면 다음 명령을 실행하여 공용 폴더 마이그레이션을 완료할 수 있습니다.

    Complete-MigrationBatch PublicFolderMigration

또는 EAC에서 **이 마이그레이션 일괄 처리 완료**를 클릭하여 마이그레이션을 완료할 수 있습니다.

마이그레이션 완료 하면 Exchange 레거시 Exchange 서버와 Exchange 2013 간의 최종 동기화를 수행 합니다. 최종 동기화에 성공한 경우 Exchange 2013 서버에서 공용 폴더를 잠금이 해제 됩니다 하 고 마이그레이션 일괄 처리의 상태를 **완료** 한 다음 **완료** 를 변경 됩니다. 일반적으로 마이그레이션 일괄 처리 **동기화 됨** 에서 **완료** 상태는 변경 하기 전에 몇 시간까지 걸릴, 나타나는데 최종 동기화 시작 됩니다.

## 8단계: 공용 폴더 마이그레이션 테스트 및 잠금 해제

공용 폴더 마이그레이션을 완료한 후에는 다음 테스트를 실행하여 마이그레이션이 성공적으로 완료되었는지 확인해야 합니다. 이를 통해 Exchange 2013 공용 폴더를 사용하도록 전환하기 전에 마이그레이션된 공용 폴더 계층 구조를 테스트할 수 있습니다.

1.  PowerShell에서 새로 마이그레이션된 공용 폴더 사서함을 기본 공용 폴더 사서함으로 사용할 일부 테스트 사서함에 할당 하려면 다음 명령을 실행 합니다.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  이전 단계에서 식별된 테스트 사용자로 Outlook 2007 이상에 로그온하여 다음 공용 폴더 테스트를 수행합니다.
    
      - 계층 구조를 확인합니다.
    
      - 사용 권한을 확인합니다.
    
      - 공용 폴더를 만들고 삭제합니다.
    
      - 공용 폴더에 콘텐츠를 게시한 후 삭제합니다.

3.  문제를 실행 하는 경우이 항목의 뒷부분에 마이그레이션 롤백 을 참조 합니다. 수 있는 적절 한 및 예상한 대로 작동 하는 공용 폴더 콘텐츠 및 계층 구조를 하는 경우에 다른 모든 사용자에 대 한 공용 폴더의 잠금을 해제 하려면 다음 명령을 실행 합니다.
    
        Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    

    > [!IMPORTANT]
    > 초기 마이그레이션 유효성 검사를 완료한 후에는 <EM>IsExcludedFromServingHierarchy</EM> 매개 변수를 사용하지 마십시오. 이 매개 변수는 Exchange Online용으로 자동화된 저장소 관리 서비스에 사용됩니다.



4.  레거시 Exchange 서버에서 다음 명령을 실행하여 공용 폴더 마이그레이션이 완료되었음을 나타냅니다.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  마이그레이션이 완료 되는 확인 한 후 다음 명령을 실행 합니다.
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

6.  마지막으로, 외부의 보낸 사람이 마이그레이션된 메일 사용이 가능한 공용 폴더에 메일을 보낼 수를 원하는 경우 **익명** 사용자 최소한의 **항목 만들기** 에 게 권한을 부여 해야 합니다. 이렇게 하지 않으면 외부 보낸 사람이 배달 실패 알림의 받을 하 고 마이그레이션된 메일 사용이 가능한 공용 폴더에 메시지를 배달 하지 않습니다.
    
    익명 사용자에 대해 사용 권한을 설정 하는 셸 또는 Outlook을 사용할 수 있습니다. 읽기를 익명 사용자에 대해 사용 권한을 설정 하는 방법에 대 한 자세한 [메일 사용이 가능한 또는 공용 폴더 메일-사용 안함](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

2 단계: 마이그레이션 준비, 마이그레이션을 시작 하기 전에 공용 폴더 구조, 통계, 그리고 사용 권한의 스냅숏을 가능 하다. 다음 단계는 마이그레이션이 완료 된 후 동일한 스냅숏을 수행 하 여 공용 폴더 마이그레이션 완료 되었는지 확인 하는 데 도움이 됩니다. 그런 다음 성공 여부를 확인 하려면 두 파일의 데이터를 비교할 수 있습니다.

1.  다음 명령을 실행하여 새 폴더 구조의 스냅숏을 만듭니다.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  다음 명령을 실행하여 항목 수, 크기 및 소유자와 같은 공용 폴더 통계에 대한 스냅숏을 만듭니다.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  다음 명령을 실행하여 사용 권한의 스냅숏을 만듭니다.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## 레거시 Exchange 서버에서 공용 폴더 데이터베이스 제거

마이그레이션이 완료되고 Exchange 2013 공용 폴더가 정상적으로 작동하는 것을 확인한 후에는 레거시 Exchange 서버에서 공용 폴더 데이터베이스를 제거해야 합니다.

  - Exchange 2007 서버에서 공용 폴더 데이터베이스를 제거 하는 방법에 대 한 자세한 내용은, [공용 폴더 데이터베이스 제거](https://go.microsoft.com/fwlink/?linkid=123678)을 참조 하십시오.

  - Exchange 2010 서버에서 공용 폴더 데이터베이스를 제거 하는 방법에 대 한 자세한 내용은, [공용 폴더 데이터베이스 제거](https://go.microsoft.com/fwlink/?linkid=81409)을 참조 하십시오.

## 마이그레이션 롤백

마이그레이션과 관련된 문제가 발생하여 레거시 Exchange 공용 폴더를 다시 활성화해야 하는 경우 다음 단계를 수행하십시오.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>롤백하는 경우 마이그레이션 레거시 Exchange 서버에, 메일 사용이 가능한 공용 폴더 또는 마이그레이션 후 Exchange 2013의 공용 폴더에 게시 된 콘텐츠에 게 보낸 모든 전자 메일을 손실 됩니다. 이 콘텐츠를 저장 하려면 공용 폴더 콘텐츠를.pst 파일로 내보내고 롤백을 완료 되 면 레거시 공용 폴더를 가져올 해야 합니다.</td>
</tr>
</tbody>
</table>


1.  레거시 Exchange 서버에서 다음 명령을 실행하여 레거시 Exchange 공용 폴더의 잠금을 해제합니다. 이 프로세스를 수행하는 데 몇 시간이 걸릴 수 있습니다.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  Exchange 2013 서버에서 공용 폴더 사서함을 제거 하려면 다음 명령을 실행 합니다.
    
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false

3.  레거시 Exchange 서버에서 다음 명령을 실행하여 `PublicFolderMigrationComplete` 플래그를 `$false`로 설정합니다.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

