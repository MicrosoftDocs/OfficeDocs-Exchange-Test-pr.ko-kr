---
title: '일괄 처리 마이그레이션을 사용하여 Exchange 2013 공용 폴더를 Office 365 그룹에 마이그레이션'
TOCTitle: 마이그레이션 일괄 처리를 사용 하 여 Office 365 그룹에 Exchange 2013 공용 폴더 마이그레이션
ms:assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt843873(v=EXCHG.150)
ms:contentKeyID: 74468759
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 마이그레이션 일괄 처리를 사용 하 여 Office 365 그룹에 Exchange 2013 공용 폴더 마이그레이션

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2018-03-26_

<strong>요약:</strong>  Office 365 그룹에 Exchange 2013 공용 폴더를 이동 하는 방법입니다.

*마이그레이션 일괄 처리*라고 하는 프로세스를 통해 Office 365 그룹에 Exchange 2013 공용 폴더의 일부 또는 전부를 이동할 수 있습니다. 그룹은 공용 폴더에 비해 특정 이점을 제공 하는 Microsoft에서 제공 하는 새로운 공동 작업입니다. [Office 365 그룹에 공용 폴더 마이그레이션](https://docs.microsoft.com/ko-kr/exchange/collaboration-exo/public-folders/migrate-your-public-folders-to-office-365-groups) 공용 폴더 및 그룹 및 조직 수 또는 그룹에 전환에서 혜택을 받는 하지 이유 이유 간의 차이점에 대 한 개요를 참조 하십시오.

이 문서는 Exchange 2013 공용 폴더의 실제 일괄 처리 마이그레이션을 수행 하기 위한 단계별 절차를 포함 합니다.

## 시작하기 전에 알아야 할 내용

마이그레이션을 준비 하기 전에 다음 조건을 모두 충족 하는지 확인 합니다.

  - Exchange 2013 서버에서 <strong>Exchange 2013 CU15</strong> 를 실행 해야하는 이상입니다.

  - Exchange Online에서 조직 관리 역할 그룹의 구성원 이어야 해야 합니다. 이 역할 그룹은 Office 365 또는 Exchange Online 구독할 때 사용자에 게 할당 된 사용 권한을과 다릅니다. 조직 관리 역할 그룹을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은, [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)을 참조 하십시오.

  - Exchange 2013, 해야하는 조직 관리 또는 서버 관리 RBAC 역할 그룹의 구성원 이어야 합니다. 자세한 내용은 [역할 그룹에 구성원 추가](https://go.microsoft.com/fwlink/?linkid=299212)를 참조 하십시오.

  - Office 365 그룹에 공용 폴더를 마이그레이션하기 전에 먼저 이동 하는 사용자 사서함 Office365 마이그레이션 후 Office 365 그룹에 대 한 액세스를 요구 하는 사용자에 대 한 것이 좋습니다. 자세한 내용은 [Office 365에 여러 전자 메일 계정으로 마이그레이션하는 방법](https://support.office.com/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842)을 참조 하십시오.

  - MRS 프록시 하나 이상의 Exchange 서버에서 사용할 수 있어야 및 해당 서버 해야도 될 호스팅 공용 폴더 사서함입니다. 자세한 내용 은 [원격 이동에 대 한 MRS 프록시 끝점을 사용 하도록 설정](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md) 참조 하십시오.

  - 이 절차를 수행 하려면 Exchange 관리 센터 (EAC) 또는 (EMC (Exchange 관리 콘솔)를 사용할 수 없습니다. Exchange 2013 서버에서 Exchange 관리 셸을 사용 하 여 지정 해야 합니다. Exchange Online에 대 한 Exchange Online PowerShell 를 사용 하 여 지정 해야 합니다. 자세한 내용은 [원격 PowerShell을 사용 하는 Exchange Online에 연결](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx)을 참조 하십시오.

  - 만 형식 일정 및 메일의 공용 폴더 수로 마이그레이션할 수 Office 365 그룹 시킵니다. 공용 폴더에 있는 다른 유형의 마이그레이션 지원 되지 않습니다. 또한 Office 365에서 대상 그룹은 것으로 예상 되는 마이그레이션 전에 만들 수 있습니다.

  - 일괄 처리 마이그레이션 프로세스만 복사 하는 메시지 및 일정 항목 마이그레이션에 대 한 공용 폴더에서 Office 365 그룹에 있습니다. 이후 Office 365 그룹에서 지원 하지 않는 것 정책, 규칙 및 사용 권한과 같은 공용 폴더의 다른 엔터티 복사할 하지 않습니다.

  - Office 365 그룹 50GB 사서함 함께 제공 됩니다. 마이그레이션하는 공용 폴더 데이터의 합계가 50GB 보다 작은 있는지 확인 합니다. 또한 사용자가 나중에 추가 될 추가 콘텐츠에 대 한 저장 공간이 마이그레이션 후 둡니다. 공용 폴더 마이그레이션 총에서 25GB 보다 더 클수록 크기를 조정 하는 것이 좋습니다.

  - 이것은 "전부 또는 nothing" 마이그레이션의 아닙니다. 하면 선택할 수 있습니다를 마이그레이션하려면 특정 공용 폴더 및 해당 공용 폴더에만 마이그레이션됩니다. 마이그레이션되는 공용 폴더에 하위 폴더가 있는 경우 해당 하위 폴더는 마이그레이션에 자동으로 포함 되지 않습니다. 마이그레이션합니다 해야하는 경우에 명시적으로를 포함 해야 합니다.

  - 이 마이그레이션에 의해 공용 폴더는 방식으로 적용 되지 않습니다. 그러나 한번 사용해 잠금 스크립트를 사용 하면 읽기 전용 사용자에 게 공용 폴더 대신 Office 365 그룹을 사용 하 여 강제로 마이그레이션된 공용 폴더를 확인 합니다.

  - 시작 하기 전에 것이 좋습니다 전체,이 문서를 읽어 가동 중지 시간 is 일부 단계의 필요 합니다.

## 1 단계: 스크립트 가져오기

이 문서의 아래 설명에 따라 Office 365 그룹에 일괄 마이그레이션 마이그레이션에서는 서로 다른 시점에서 다양 한 스크립트를 실행 하 필요 합니다. 스크립트를 다운로드 하 고 [이 위치에서](https://www.microsoft.com/en-us/download/details.aspx?id=55985)파일을 자신의 지원 합니다. 모든 스크립트 및 파일을 다운로드 한 후 `c:\PFtoGroups\Scripts`와 같은 동일한 위치에 저장 합니다.

계속 하기 전에 다운로드 하 고 다음 스크립트 및 파일의 모든 저장 했는지 확인 합니다.


> [!NOTE]
> 동일한 위치에 모든 스크립트 및 파일을 저장 하려면 있는지 확인 합니다.



  - <strong>AddMembersToGroups.ps1</strong>.이 스크립트는 원본 공용 폴더의 사용 권한 항목을 기반으로 구성원 및 소유자 Office 365 그룹에 추가 합니다.

  - <strong>AddMembersToGroups.strings.psd1</strong>.이 지원 파일은 스크립트 `AddMembersToGroups.ps1`사용 됩니다.

  - <strong>LockAndSavePublicFolderProperties.ps1</strong>.이 스크립트 가능 공용 폴더 수정 하지 못하게 하려면 읽기 전용으로 설정 하 고 전송할 공용 폴더 메일 관련 속성 (공용 폴더는 메일 사용이 가능한) 제공 대상 그룹에는 대상 그룹에 공용 폴더에서 전자 메일을 경로 조정 됩니다. 이 스크립트는 또한 수정 하기 전에 사용 권한 항목 및 메일 속성을 백업 합니다.

  - <strong>LockAndSavePublicFolderProperties.strings.psd1</strong>:이 지원 파일은 스크립트 `LockAndSavePublicFolderProperties.ps1`사용 됩니다.

  - <strong>UnlockAndRestorePublicFolderProperties.ps1</strong>.이 스크립트는 액세스 권한 및 `LockandSavePublicFolderProperties.ps1`에서 만든 백업 파일을 사용 하 여 공용 폴더의 메일 속성 복원 합니다.

  - <strong>UnlockAndRestorePublicFolderProperties.strings.psd1</strong>.이 지원 파일은 스크립트 `UnlockAndRestorePublicFolderProperties.ps1`사용 됩니다.

  - <strong>WriteLog.ps1</strong>.이 스크립트 로그를 쓸 수 위의 세 스크립트를 사용할 수 있도록 합니다.

  - <strong>RetryScriptBlock.ps1</strong>.이 스크립트 일시적인 오류 발생 시 특정 작업을 다시 시도를 `AddMembersToGroups`, `LockAndSavePublicFolderProperties`및 `UnlockAndRestorePublicFolderProperties` 스크립트를 사용할 수 있도록 합니다.

`AddMembersToGroups.ps1`하는 방법에 대 한 자세한 내용은, `LockAndSavePublicFolderProperties.ps1`및 `UnlockAndRestorePublicFolderProperties.ps1`및 사용자 환경에서 실행 하는 작업이이 문서 뒷부분의 마이그레이션 스크립트 참조 합니다.

## 2단계: 마이그레이션 준비

다음 단계는 마이그레이션에 대 한 조직을 준비 하는 데 필요한 합니다.

1.  Office 365 그룹에 마이그레이션할 공용 폴더 (메일 및 일정 유형) 목록을 컴파일하십시오.

2.  마이그레이션되는 각 공용 폴더에 대 한 해당 대상 그룹의 목록이 있습니다. 각 공용 폴더에 대 한 Office 365에서 새 그룹을 만들 수도 있고 기존 그룹을 사용 합니다. 새 그룹을 만드는 경우 [Office 365 그룹에 대 한 설명](https://go.microsoft.com/fwlink/p/?linkid=858521) 그룹 있어야 설정을 이해를 참조 하십시오. 공용 폴더를 마이그레이션하는 기본 권한 집합 <strong>작성자</strong> 에 게 또는 위에 있으면 Office 365에서는 해당 그룹을 만들어 해야 <strong>공개</strong> 개인정보 보호 설정을 사용 하 여 표시. 그러나 사용자가 Outlook에서 <strong>그룹</strong> 노드 아래에서 공용 그룹을 볼 수, 여전히 갖게 됩니다 해당 그룹에 가입 합니다.

3.  이름에 백슬래시 (<strong>\\</strong> )를 포함 하는 모든 공용 폴더를 이름을 바꿉니다. 그렇지 않은 경우 해당 공용 폴더 수 마이그레이션되지 올바르게 합니다.

4.  마이그레이션 기능을 <strong>PAW</strong> Office 365 테 넌 트를 사용 하도록 설정 해야 합니다. 이 확인 하려면 Exchange Online PowerShell에서 다음 명령을 실행 합니다.
    
    ```powershell
Get-MigrationConfig
```
    
    <strong>기능</strong> 에서 출력 <strong>PAW</strong>, 다음 기능을 사용 하도록 목록과를 계속 받을 수 있습니다 하는 경우 *3 단계:.csv 파일 Crete*합니다.
    
    발 없는 아직 테 넌 트를 사용할 수 이기 때문일 수 있는 일부 기존 마이그레이션 일괄 처리 하는 경우 공용 폴더 일괄 처리 또는 사용자 일괄 처리 합니다. 이러한 일괄 처리 완료를 포함 하 여 모든 상태일에서 수 있습니다. 이 경우 완료 하 고 `Get-MigrationBatch`를 실행 하는 경우 반환 된 레코드가 없을 때까지 모든 기존 마이그레이션 일괄 처리를 제거 하십시오. 모든 기존 일괄 처리 제거 되 면 발을 자동으로 활성화 가져올 해야 합니다. 변경을 반영 하지 못하는 `Get-MigrationConfig` 즉시에 하는 note 합니다. 이 단계가 완료 되 면 사용자 마이그레이션의 새 일괄 처리 만들기 (영문)을 계속할 수 있습니다.

## 3 단계:.csv 파일 만들기

마이그레이션 스크립트 중 하나에 대 한 입력을 제공 하는.csv 파일을 만듭니다.

.Csv 파일 다음 열을 포함 해야 합니다.

  - <strong>FolderPath</strong>합니다. 마이그레이션해야 하는 공용 폴더의 경로입니다.

  - <strong>TargetGroupMailbox</strong>합니다. Office 365에서 대상 그룹의 SMTP 주소입니다. 기본 SMTP 주소를 참조 하려면 다음 명령을 실행할 수 있습니다.
    
    ```powershell
Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress
```

예제.csv의 경우:

    "FolderPath","TargetGroupMailbox"
    "\Sales","sales@contoso.onmicrosoft.com"
    "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"

참고 Office 365에서 단일 그룹으로 메일 폴더와 일정 폴더를 병합할 수 있습니다. 그러나 그룹에 병합 하는 여러 공용 폴더의 다른 시나리오는 단일 마이그레이션 일괄 처리 내에서 지원 되지 않습니다. 동일한 Office 365 그룹에 여러 공용 폴더를 매핑할 필요가 사람에 게에 연속적으로 실행 되어야 하는 다양 한 마이그레이션 일괄 처리를 실행 하 여이 수행할 수 있습니다. 각 마이그레이션 일괄 처리의 최대 500 개의 항목을 가질 수 있습니다.

공용 폴더는 하나의 마이그레이션 일괄 처리의 하나만 그룹으로 마이그레이션해야 합니다.

## 4 단계: 마이그레이션 요청 시작

이 단계에서 Exchange 환경에서 정보를 수집 하 고 해당 정보를 사용 하면 Exchange Online PowerShell 에서 마이그레이션 일괄 처리 만들기. 그런 다음 마이그레이션을 시작 합니다.

1.  Exchange 2013 서버에서 MRS 프록시 끝점 서버 찾아 것을 기록해둡니다. 마이그레이션 요청을 실행 하는 경우에 나중에이 정보를 해야 합니다.

2.  Exchange Online PowerShell 다음 명령을 실행 하는 1 단계에서 위의 반환 된 정보를 사용 합니다. 이 명령에서 변수 1 단계에서 값이 됩니다.
    
    1.  변수 `$Source_Credential`으로 Exchange 2013 환경에서 관리자 권한이 있는 사용자의 자격 증명을 전달 합니다. 결국을 실행 하면 마이그레이션 요청 Exchange 온라인 Exchange Online을 통해 콘텐츠를 복사 하기 위해 Exchange 2013 서버에 액세스를이 자격 증명을 사용 합니다.
        
            $Source_Credential = Get-Credential
            <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  위의 1 단계에서에서 적어둔 Exchange 2013 환경의 MRS 프록시 서버 정보를 사용 하 고 변수 `$Source_RemoteServer`으로 해당 값을 전달 합니다.
        
        ```powershell
$Source_RemoteServer = "<MRS proxy endpoint>"
```

3.  Exchange Online PowerShell 마이그레이션 끝점을 만들려면 다음 명령을 실행 합니다.
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential

4.  새 공용 폴더-Office 365 그룹 마이그레이션 일괄 처리를 만들려면 다음 명령을 실행 합니다. 이 명령 합니다.
    
      - <strong>CSVData</strong> 에서 앞에서 만든.csv 파일은 *3 단계:.csv 파일을 만들고*합니다. 이 파일의 전체 경로 제공 해야 합니다. 어떤 이유로 든 파일을 이동 하는 경우에 확인 하 고 새 위치를 사용 해야 합니다.
    
      - <strong>NotificationEmails</strong> 은 상태와 진행률 마이그레이션에 대 한 알림을 받을 수 있는 전자 메일 주소를 설정 하는데 사용할 수 있는 선택적 매개 변수입니다.
    
      - <strong>자동 시작</strong> 되는 선택적 매개 변수는 사용 하는 경우 생성 되는 즉시 마이그레이션 일괄 처리를 시작 합니다.
    
      - <strong>PublicFolderToUnifiedGroup</strong> 는 공용 폴더 Office 365 그룹 마이그레이션 일괄 처리를 표시 하려면 매개 변수입니다.
    
    <!-- end list -->
    
        New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

5.  Exchange Online PowerShell 에서 다음 명령을 실행 하 여 마이그레이션을 시작 합니다. Note이 단계는 4 단계에서 위의 일괄 처리를 만드는 동안 `-AutoStart` 매개 변수는 사용 되지 않았습니다 하는 경우에 필요 합니다.
    
    ```powershell
Start-MigrationBatch PublicFolderToGroupMigration
```

마이그레이션 일괄 처리를 Exchange Online PowerShell 에서 `New-MigrationBatch` cmdlet을 사용 하 여 만들 필요가 하는 동안 마이그레이션 진행 상황을 볼 하 고 Exchange 관리 센터 에서 관리할 수 있습니다. 또한 [Get-MigrationBatch](https://technet.microsoft.com/ko-kr/library/jj219164\(v=exchg.150\)) 및 [Get-MigrationUser](https://technet.microsoft.com/ko-kr/library/jj218702\(v=exchg.150\)) cmdlet을 실행 하 여 마이그레이션의 진행률을 볼 수 있습니다. `New-MigrationBatch` cmdlet은 각 Office 365 그룹 사서함에 대 한 마이그레이션 사용자를 시작 하 고 사서함 마이그레이션 페이지를 사용 하 여 이러한 요청의 상태를 볼 수 있습니다.

사서함 마이그레이션 페이지를 보려면:

1.  Exchange Online에서 Exchange 관리 센터 를 엽니다.

2.  <strong>받는 사람</strong> 게 이동한 다음 <strong>마이그레이션</strong> 을 선택 합니다.

3.  방금 만든 마이그레이션 요청을 선택 하 고 <strong>세부 정보</strong> 창에서 <strong>자세히 보기를</strong> 선택 합니다.

일괄 처리 상태 <strong>완료</strong> 되 면 이동할 수 있습니다에 *5 단계: 공용 폴더에서 Office 365 그룹에 구성원을 추가*합니다.

## 5 단계: 공용 폴더에서 Office 365 그룹에 구성원 추가

수동으로 필요에 따라 Office 365에서 대상 그룹에 구성원을 추가할 수 있습니다. 그러나 공용 폴더의 사용 권한 항목을 기준으로 그룹에 구성원을 추가 하려는 경우 다음 명령에 표시 된 것 처럼 Exchange 2013 서버에서 `AddMembersToGroups.ps1` 스크립트 실행 하 여 작업을 수행 해야 합니다. 사용자 사서함은 Office 365 그룹의 구성원으로 추가 하기 위해 Exchange Online으로 동기화 해야 합니다. Office 365에서 그룹의 구성원으로 추가 하는 공용 폴더 사용 권한을 자격이 알아야이 문서 뒷부분의 마이그레이션 스크립트 를 참조 하십시오.

다음 명령 합니다.

  - <strong>MappingCsv</strong> 에서 앞에서 만든.csv 파일은 *3 단계:.csv 파일을 만들고*합니다. 이 파일의 전체 경로 제공 해야 합니다. 어떤 이유로 든 파일을 이동 하는 경우에 확인 하 고 새 위치를 사용 해야 합니다.

  - <strong>BackupDir</strong> 는 마이그레이션 로그 파일을 저장할 디렉터리입니다.

  - <strong>ArePublicFoldersOnPremises</strong> 는 공용 폴더에 있는 온-프레미스에 대해 여부 또는 Exchange Online에서 나타내려면 매개 변수입니다.

  - <strong>자격 증명</strong> 은 Exchange Online 사용자 이름 및 암호입니다.

<!-- end list -->

    .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

사용자가 Office 365에서 그룹에 추가 된, 해당를 사용 하 여 시작할 수 있습니다.

## 6 단계: 공용 잠그려면 폴더 (공용 폴더 가동 중지 시간 필요)

Office 365 그룹에는 대부분의 공용 폴더의 데이터는 마이그레이션되면 읽기 전용 공용 폴더를 확인 하려면 Exchange 2013 서버에서 `LockAndSavePublicFolderProperties.ps1` 스크립트 실행할 수 있습니다. 이 단계를 사용 하면 마이그레이션 완료 되기 전에 새 데이터가 없는 공용 폴더에 추가 됩니다.


> [!NOTE]
> 공용 간의 메일 사용이 가능한 공용 폴더 (MEPFs) 경우 마이그레이션 중인 폴더가이 단계는 MEPFs SMTP 주소 등의 일부 속성 Office 365에서 해당 그룹에 복사한 다음 메일 사용할 수 없도록 설정할 공용 폴더. 마이그레이션 MEPFs가 될 메일 비활성화 된 후이 스크립트를 실행 하는, 때문에 해당 그룹에 수신 대신 MEPFs로 보낸 전자 메일 표시를 시작 합니다. 자세한 내용은이 문서의 뒷부분에 마이그레이션 스크립트 를 참조 하십시오.



다음 명령 합니다.

  - <strong>MappingCsv</strong> 에서 앞에서 만든.csv 파일은 *3 단계:.csv 파일을 만들고*합니다. 이 파일의 전체 경로 제공 해야 합니다. 어떤 이유로 든 파일을 이동 하는 경우에 확인 하 고 새 위치를 사용 해야 합니다.

  - <strong>BackupDir</strong> 는 사용 권한 항목, MEPF 속성과 마이그레이션 로그 파일에 대 한 백업 파일을 저장할 디렉터리입니다. 공용 폴더를 롤백할 수 있어야 하는 경우에이 백업 유용 합니다.

  - <strong>ArePublicFoldersOnPremises</strong> 는 공용 폴더에 있는 온-프레미스에 대해 여부 또는 Exchange Online에서 나타내려면 매개 변수입니다.

  - <strong>자격 증명</strong> 은 Exchange Online 사용자 이름 및 암호입니다.

<!-- end list -->

    .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

## 7 단계: 공용 폴더를 Office 365 그룹 마이그레이션 완료

수행한 후 공용 폴더 읽기 전용, 마이그레이션을 다시 수행 해야 합니다. 데이터의 마지막 증분 복사본에 대 한 필요한입니다. 마이그레이션을 다시을 실행 하려면 먼저 다음 명령을 실행 하 여 수행할 수 있는 기존 일괄 처리를 제거 해야 합니다.

```powershell
Remove-MigrationBatch <name of migration batch>
```

다음에 다음 명령을 실행 하 여 같은.csv 파일이 포함 된 새 일괄 처리를 만듭니다. 이 명령 합니다.

  - <strong>CsvData</strong> 에서 앞에서 만든.csv 파일은 *3 단계:.csv 파일을 만들고*합니다. 이 파일의 전체 경로 제공 해야 합니다. 어떤 이유로 든 파일을 이동 하는 경우에 확인 하 고 새 위치를 사용 해야 합니다.

  - <strong>NotificationEmails</strong> 은 상태와 진행률 마이그레이션에 대 한 알림을 받을 수 있는 전자 메일 주소를 설정 하는데 사용할 수 있는 선택적 매개 변수입니다.

  - <strong>자동 시작</strong> 되는 선택적 매개 변수는 사용 하는 경우 생성 되는 즉시 마이그레이션 일괄 처리를 시작 합니다.

<!-- end list -->

    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

새 일괄 처리를 만든 후에 Exchange Online PowerShell 에서 다음 명령을 실행 하 여 마이그레이션을 시작 합니다. 이 단계는 `-AutoStart` 매개 변수는 이전 명령에서 사용 되지 않은 경우에 필요한만 note 합니다.

```powershell
Start-MigrationBatch PublicFolderToGroupMigration
```

(사용 하면 일괄 처리 상태가 <strong>완료 됨</strong> )이이 단계를 완료 한 후 Office 365 그룹에 모든 데이터를 복사 된 있는지 확인 합니다. 이때 그룹 환경에 만족할 제공 마이그레이션된 공용 폴더를 Exchange 2013 환경에서에서 삭제를 시작할 수 있습니다.


> [!IMPORTANT]
> 지원 되는 마이그레이션 롤백 하 고 절차를 공용 폴더를 반환 하는 동안이 할 수 없습니다 원본 공용 폴더를 삭제 한 후. 참조 어떻게 수행 합니까 롤백할 공용 폴더를 Office 365 그룹에서? 에 대 한 자세한 내용은 합니다.



## 알려진 문제

다음과 같은 알려진된 문제는 Office 365 그룹 마이그레이션에 일반적인 공용 폴더 하는 동안 발생할 수 있습니다.

  - 스크립트는 Office 365 그룹에 메일 사용이 가능한 공용 폴더에서 전송 SMTP 주소 전용으로 추가 하는 주소 보조 전자 메일 주소를 Exchange Online. 이 때문에 사용자 환경에서 Exchange Online Protection (EOP) 또는 메일 흐름에 집중 설치 프로그램을 설치한 경우 마이그레이션 후 (보조 전자 메일 주소)에 그룹에 전자 메일을 발송 하는 문제를 해야 합니다.

  - .Csv 매핑 파일에 잘못 된 공용 폴더 경로 함께 항목이 통해 오류가 발생 하지 않고 <strong>완료</strong> 로 표시 하는 마이그레이션 일괄 처리 하 고 추가 데이터를 복사 합니다.

## 마이그레이션 스크립트

참조용으로이 섹션에서는 세 마이그레이션 스크립트 및 Exchange 환경에서 실행 하는 작업에 대 한 자세한 설명이 제공 됩니다. 모든 스크립트 및 지원 파일 [이 위치에서 다운로드할](https://www.microsoft.com/en-us/download/details.aspx?id=55985)수 있습니다.

## AddMembersToGroups.ps1

이 스크립트 마이그레이션되는 공용 폴더의 사용 권한을 읽고 구성원 및 소유자 그룹에 추가할 Office 365 다음과 같이 됩니다.

  - 다음 사용 권한 역할을 가진 사용자는 Office 365의 그룹에 구성원으로 추가 됩니다. <strong>사용 권한 역할:</strong>  소유자 "," PublishingEditor "," 편집기 "," PublishingAuthor "," 만든이

  - 또한 위의 인 사용자에 게 다음과 같은 최소 액세스 권한도 추가 됩니다 구성원으로 Office 365의 그룹에 있습니다. <strong>액세스 권한:</strong>  ReadItems, CreateItems, foldervisible가, EditOwnedItems, DeleteOwnedItems

  - 오른쪽 "소유자"으로 추가할 소유자 그룹에 액세스할 수 있는 사용자 및 다른 가능한 액세스 권한이 있는 사용자가 구성원으로 추가 됩니다.

  - Office 365의 그룹을 구성원으로 보안 그룹을 추가할 수 없습니다. 따라서 이러한 확장 됩니다. 하 고 개별 사용자가으로 추가할 구성원 또는 소유자를 기반으로 보안 그룹의 액세스 권한 그룹입니다.

  - 보안 그룹에는 보유 한 사용자 액세스 권한을 통해 공용 폴더 사용 권한이 자신 명시적 같은 공용 폴더를 통해, 명시적인 사용 권한이 우선 적용 됩니다. 예, 보안 그룹 "SG1" 이라고 하는 경우에 구성원이 User1 및 사용자 2가 하는 것이 좋습니다. 공용 폴더 "p f 1"에 대 한 사용 권한 항목은 다음과 같습니다.
    
    P f 1에서 SG1: 작성자
    
    P f 1에서 User1: 소유자
    
    이 경우 User1 소유자로 Office 365의 그룹에 추가 됩니다.

  - 마이그레이션 중인 공용 폴더의 기본 권한 '작성자' 때 이상이 면 'Public'으로 설정 하는 해당 그룹의 개인 설정 스크립트를 제안 합니다.

이 스크립트 실행될수 공용 폴더의 잠금 한 후에 매개 변수와 함께 ArePublicFoldersLocked $true로 설정 합니다. 이 시나리오에서는 스크립트 백업 잠금 중에 만들어진 파일에서에서 사용 권한을 설명 합니다.

## LockAndSavePublicFolderProperties.ps1

이 스크립트 읽기 전용 마이그레이션되는 공용 폴더를 만듭니다. 메일 사용이 가능한 공용 폴더 마이그레이션되는 경우 이러한는 먼저 될 메일-사용 안함 및 해당 SMTP 주소를 Office 365에서 해당 그룹에 추가 됩니다. 그런 다음 사용 권한 항목을 읽기 전용으로 수정 됩니다. 모든 수정 사항은 연산을 수행 하기 전에 메일 사용이 가능한 공용 폴더의 메일 속성의 모든 공용 폴더 사용 권한 항목의 백업 복사 됩니다.

여러 마이그레이션 일괄 처리 경우 각 매핑.csv 파일와 별도 백업 디렉터리를 사용 해야 합니다.

Office 365 그룹과 해당 메일 사용이 가능한 공용 폴더와 함께 다음 메일 속성 저장 됩니다.

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - SendAs 트러스트를 받을 목록

위의 메일 속성을 다시 프로세스의 롤백에 사용할 수 있는.csv 파일에 저장 됩니다 (공용 폴더를 사용 하 여 반환할을 참조 하려면 어떻게 수행 합니까 롤백할 공용 폴더를 Office 365 그룹에서? 에 대 한 자세한 내용은)입니다. 메일 사용이 가능한 공용 폴더의 속성의 스냅숏은 PfMailProperties.csv 라는 파일에도 저장 됩니다. 이 파일의 롤백 프로세스에 대 한 필요는 없지만 참조용으로 계속 사용할 수 있습니다.

다음 메일 속성 잠그기의 일환으로 대상 그룹에 마이그레이션됩니다.

  - PrimarySMTPAddress

  - EmailAddresses

  - SendAs 트러스트를 받을 목록

  - GrantSendOnBehalfTo

스크립트는 PrimarySMTPAddress 및 메일 사용이 가능한 공용 폴더 마이그레이션하는 EmailAddresses로 추가할 Office 365에서 해당 그룹의 보조 SMTP 주소를 확인 합니다. 또한 메일 사용이 가능한 공용 폴더에 있는 사용자의 SendAs 및 SendOnBehalfTo 권한 하 게 할 동등한 권한은 해당 대상 그룹에 합니다.

<strong>허용 되는 액세스 권한</strong>

모든 사용자에 대 한 읽기 전용 공용 폴더 이루어지는지 확인 하는 사용자에 대 한 다음 액세스 권한이 허용 됩니다. 이러한 <strong>ListOfAccessRightsAllowed</strong> 에 저장 됩니다.

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

사용 권한 항목은 다음과 같이 수정 합니다.

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>잠그기 전에</th>
    <th>잠그기 후</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>없음</p></td>
    <td><p>없음</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>참가자</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Reviewer</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Aughor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>Editor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>소유자</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  읽기 권한이 없는 사용자에 대 한 액세스 권한을 그대로 유지 됩니다 및 읽기 권한에서 차단 될를 계속 합니다.

3.  사용자 지정 역할을 사용 하 여 사용자, <strong>ListOfAccessRightsAllowed</strong> 에 포함 되지 않은 모든 액세스 권한은 제거 됩니다. 사용자를 설치 하지 않은 모든 액세스 권한이 허용된 목록에서 필터링 한 후 이러한 사용자의이 액세스 권한을 '없음'으로 설정 됩니다.

중단 폴더는 메일-사용 안함 및 해당 SMTP 주소 Office 365 그룹에 추가 하는 경우 메일 사용이 가능한 공용 폴더를 전자 메일을 사이의 시간 동안 보내는에 있을 수 있습니다.

## UnlockAndRestorePublicFolderProperties.ps1

이 스크립트에는 백업 잠금 공용 폴더 중에 작성 되는 파일에 기반 하는 공용 폴더에 다시 사용 권한을 다시 할당 됩니다. 이 스크립트는 또한 메일 사용이 가능한 공용 폴더를 명의 된 메일 비활성화 된 후 Office 365의 각 그룹에서 폴더의 SMTP 주소를 제거 합니다. 이 과정에서 약간의 가동 중지 시간 있을 수 있습니다.

## 어떻게 수행 합니까 롤백할 공용 폴더를 Office 365 그룹에서?

사용자의 생각을 변경 하 고 Office 365 그룹을 아래에 나열 된 명령을 사용 하는 상태로 환경의 복원 후 공용 폴더를 사용 하 여 반환할는 마이그레이션 전 했습니다. 다시 롤은 백업 파일이 존재 하는 하기만 하 고 마이그레이션 후 공용 폴더를 삭제 하지 않은으로으로 수행할 수 있습니다.

Exchange 2013 서버에서 다음 명령을 실행 합니다. 이 명령 합니다.

  - <strong>BackupDir</strong> 는 사용 권한 항목, MEPF 속성과 마이그레이션 로그 파일에 대 한 백업 파일을 저장할 디렉터리입니다. 에 지정 된 동일한 위치를 사용 하는지 확인 <em>6 단계: 단독형에 공용 폴더 잠그기 (공용 폴더 가동 중지 시간 필요)</em>합니다.

  - <strong>ArePublicFoldersOnPremises</strong> 는 공용 폴더에 있는 온-프레미스에 대해 여부 또는 Exchange Online에서 나타내려면 매개 변수입니다.

  - <strong>자격 증명</strong> 은 Exchange Online 사용자 이름 및 암호입니다.

<!-- end list -->

    .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Office 365 그룹 또는 그룹에 수행 되는 모든 편집 작업에 추가 된 항목이 공용 폴더에 다시 복사 되지 않습니다에 유의 합니다. 따라서 데이터가 손실 될, 공용 폴더 그룹 동안 추가 된 새 데이터를 가정 합니다.

Note도 것이 어떤 의미는 공용 폴더의 모든 마이그레이션된 복원 되어야 하는 공용 폴더의 하위 집합을 복원할 수 없습니다.

Office 365에서 해당 그룹의 롤백 다시 프로세스의 일부로 삭제 되지 않습니다. 정리 하거나 이러한 그룹을 수동으로 삭제 해야 합니다.

