---
title: '마이그레이션 일괄 처리를 사용 하 여 Exchange Online으로 Exchange 2013 공용 폴더 마이그레이션: Exchange 2013 Help'
TOCTitle: 마이그레이션 일괄 처리를 사용 하 여 Exchange Online으로 Exchange 2013 공용 폴더 마이그레이션
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432741
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 마이그레이션 일괄 처리를 사용 하 여 Exchange Online으로 Exchange 2013 공용 폴더 마이그레이션

 

_**마지막으로 수정된 항목:** 2018-03-26_

**요약**:이 문서 Office 365에서 Exchange 2013 현대 공용 폴더를 이동 하는 방법을 설명 합니다.

Exchange Online 2013 Exchange 공용 폴더 마이그레이션 Exchange Server 2013 CU15 또는 온-프레미스 환경에서 이상을 실행 해야 합니다.


> [!NOTE]
> 조직에서 공용 폴더를 Exchange 2013와 Exchange 2016 있고 모든 Exchange Online으로 이동 하려면 <A href="https://go.microsoft.com/fwlink/p/?linkid=845314">이 문서의 Exchange 2016 버전</A> 을 사용 하 여 계획 하 고 마이그레이션을 실행. 2013 Exchange 서버 CU15가 필요 하거나 이상이 설치 되어 있습니다.



## 시작하기 전에 알아야 할 내용

  - 이상으로 2013 CU15 Exchange Server를 업그레이드 하면 Active Directory 준비도 해야 하거나 공용 폴더 마이그레이션을 실패 하 게 됩니다. 이러한 Active Directory 준비 하면 준비 하 고 실행 하 여 마이그레이션에 대 한 모든 관련 PowerShell cmdlet 및 매개 변수는 사용할 수 있습니다. 자세한 내용은 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md) 참조 하십시오.

  - Exchange Online에서 조직 관리 역할 그룹의 구성원이 될 필요. 이 역할 그룹은 Office 365 또는 Exchange Online에 등록할 때 사용자에 게 할당 된 사용 권한을 다릅니다. 조직 관리 역할 그룹을 사용 하는 방법에 대 한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조 하십시오.

  - Exchange Server에서 2013 해야 조직 관리 또는 서버 관리 RBAC 역할 그룹의 구성원 이어야 합니다. 자세한 내용은 [역할 그룹에 구성원 추가](https://go.microsoft.com/fwlink/?linkid=299212)참조 하십시오.

  - 권장 크기를 조정할 수 있는 해당 폴더에서 항목을 삭제 하거나 공용 폴더의 구분 하는 조직에는 단일 공용 폴더를 25 GB 보다 클 경우 공용 폴더 마이그레이션을 시작 하기 전에 콘텐츠를 여러 개의 작은 공용 폴더. 참고 25GB도 여기에 언급 된 적용 하도록 하 고 모든 자식 또는 하위 폴더에 없는 공용 폴더에 폴더에 있을 수 있습니다. 두 옵션 모두 가능한 경우 공용 폴더를 Exchange 온라인으로 이동 하지 마십시오 것이 좋습니다. 자세한 내용은 [Exchange 온라인 제한](https://go.microsoft.com/fwlink/p/?linkid=391188) 을 참조 하십시오.
    

    > [!NOTE]
    > Exchange Online의 현재 공용 폴더 할당량 25 GB 보다 작은 경우 DefaultPublicFolderIssueWarningQuota 및 DefaultPublicFolderProhibitPostQuota 매개 변수를 사용 하 여이 값을 늘릴 <A href="https://go.microsoft.com/fwlink/p/?linkid=844062">세트 OrganizationConfig cmdlet</A> 를 사용할 수 있습니다.



  - Office 365 및 Exchange Online에서 최대 1000 공용 폴더 사서함을 만들 수 있습니다.

  - Office 365로 사용자를 마이그레이션할 경우, 공용 폴더를 마이그레이션하기 전에 사용자 마이그레이션을 완료 해야 합니다. 자세한 내용은 [Office 365에 여러 전자 메일 계정을 마이그레이션하는 방법을](https://go.microsoft.com/fwlink/p/?linkid=842798)참조 하십시오.

  - 부인은 어 프록시를 또한 공용 폴더 사서함을 호스팅하는 서버 하나 이상의 Exchange 서버에서 사용할 수 있어야 합니다. 자세한 내용 은 [원격 이동에 대 한 MRS 프록시 끝점을 사용 하도록 설정](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md) 참조 하십시오.

  - 여기서에서 마이그레이션 절차를 수행 하려면 Exchange 관리 센터 (EAC)을 사용할 수 없습니다. 대신, 2013 Exchange 서버에서 Exchange 관리 셸을 사용 해야 합니다. Exchange Online에서 Exchange 온라인 PowerShell을 사용 해야 합니다. 자세한 내용은 [Exchange 온라인 PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=842801)을 참조 합니다.

  - 지운 편지함 마이그레이션 및 Exchange Online에 2013 Exchange에서에서 삭제 된 폴더는 지원 합니다. 마이그레이션을 시작 하기 전에 삭제 된 모든 폴더 및 폴더 항목을 검토 하 고 온라인 Exchange 필요 하지 모든 것을 영구적으로 삭제 하는 것이 좋습니다. 노트는 뭔가 영구적으로 삭제 되 면 복구할 수 없습니다.
    
    교환에 있는 삭제 된 공용 폴더를 나열 하려면 다음 명령을 사용할 수 있습니다 휴지통 (온-프레미스 Exchange 환경)에서:
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    특정 폴더를 영구히 삭제 하려면 ('Calendar2' 라는 폴더를 사용 하 여이 예제) 다음 명령을 사용 합니다.
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - 시작 하기 전에이 문서 전체에서를 읽어 보십시오. 몇 가지 단계는 작동 중단. 이 중단 시간 동안 공용 폴더는 모든 사용자가 액세스할 수 없습니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 1 단계: 마이그레이션 스크립트를 다운로드 합니다.

1.  [Exchange 2013/2016 공용 폴더 마이그레이션 스크립트](https://go.microsoft.com/fwlink/p/?linkid=844893)에서 모든 스크립트 및 지원 파일을 다운로드 합니다.

2.  PowerShell을 실행할 로컬 컴퓨터에서 C:\\PFScripts 등의 위치에 스크립트를 저장합니다. 모든 스크립트가 같은 위치에 저장되는지 확인합니다.

스크립트와 파일을 다운로드 하는.

  - `Sync-ModernMailPublicFolders.ps1` 이 스크립트는 Exchange 온-프레미스 환경과 Office 365 간에 공용 폴더 메일 사용 가능 개체를 동기화합니다. 2013 Exchange 서버에서이 스크립트를 실행 합니다.

  - `SyncModernMailPublicFolders.strings.psd1` 이 지원 ModernMailPublicFolders.ps1 동기화 스크립트에서 사용 하는 파일과 같은 위치에 다운로드 해야 합니다.

  - `Export-ModernPublicFolderStatistics.ps1` 이 스크립트는 폴더 이름-폴더 크기와 삭제 된 항목 크기가 매핑 파일을 만듭니다. 2013 Exchange 서버에서이 스크립트를 실행 합니다.

  - `Export-ModernPublicFolderStatistics.strings.psd1` 이 지원 ModernPublicFolderStatistics.ps1 내보내기 스크립트에서 사용 하는 파일과 같은 위치에 다운로드 해야 합니다.

  - `ModernPublicFolderToMailboxMapGenerator.ps1` 이 스크립트는 ModernPublicFolderStatistics.ps1 내보내기 스크립트의 출력을 사용 하 여 공용 폴더와 사서함-매핑 파일을 만듭니다. 2013 Exchange 서버에서이 스크립트를 실행 합니다.

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` 이 지원 ModernPublicFolderToMailboxMapGenerator.ps1 스크립트에서 사용 하는 파일과 같은 위치에 다운로드 해야 합니다.

  - `SetMailPublicFolderExternalAddress.ps1` 이 스크립트는 Exchange Online은 하드웨어의 온-프레미스 환경에서 메일 사용 가능 공용 폴더의 `ExternalEmailAddress` 업데이트합니다. 이렇게 하면, 마이그레이션 후 메일 사용이 가능한 공용 폴더로 주소가 지정 된 전자 메일 올바로 라우팅될 수 있도록 Exchange 온라인. 2013 Exchange 서버에서이 스크립트를 실행 해야 합니다.

  - `SetMailPublicFolderExternalAddress.strings.psd1` 이 지원 SetMailPublicFolderExternalAddress.ps1 스크립트에서 사용 하는 파일과 같은 위치에 다운로드 해야 합니다.

## 2단계: 마이그레이션 준비

공용 폴더 마이그레이션을 시작 하기 전에 다음 단원의 모든 필수 단계를 수행 합니다.

**일반적인 사전 요구 사항 단계**

성공 하려면 마이그레이션에 대해 다음 작업을 수행 해야 합니다.

  - 개가 없는 고아 공용 폴더 메일 개체 Active Directory에 있는지 확인 합니다. 이들은 해당 Exchange 개체는 Active Directory의 개체입니다.

  - SMTP 전자 메일 주소를 Active Directory의 공용 폴더에 대해 구성 된 Exchange 개체에서 SMTP 전자 메일 주소와 일치 하는지 확인 합니다.

  - Active Directory의 중복 된 공용 폴더 개체가 있는지 확인 합니다. 이것은 두는 것을 방지 하기 위해 필요 하거나 더 많은 Active Directory 개체를 가리키고 같은 메일 사용 가능 공용 폴더에.

**온-프레미스 Exchange 2013 서버 환경에서 필수 단계**

Exchange 관리 셸 (온-프레미스) 다음 단계를 수행 합니다.

1.  마이그레이션이 완료 되 면 걸립니다 DNS 캐시 시간 인터넷을 통해 메일 사용 가능 공용 폴더의 새 위치에 직접 메시지를 Exchange 온라인. 새로 마이그레이션한 메일 사용이 가능한 공용 폴더 메시지가이 DNS 전환 기간 동안 잘 알려진 이름을 사용 하 여 허용된 도메인을 만들어 확인할 수 있습니다. 이 위해 온-프레미스 Exchange 환경에서 다음 명령을 실행 합니다. 이 예제에서는 `target domain` 는 송신 커넥터에 이미 구성 되어 하이브리드 구성 마법사에서 Office 365 또는 온라인 Exchange 도메인입니다.
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **예**:
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    허용된 도메인은 온-프레미스 환경에 이미 있는 경우 이름을 `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` 로 변경 하 고 다른 속성을 그대로 둡니다.
    
    온-프레미스 환경에 이미 허용된 도메인 인지 확인 합니다.
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    허용된 도메인 `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`으로 바꾸려면 다음을 실행 합니다.
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    

    > [!NOTE]
    > 인터넷에서 외부 전자 메일을 받도록 Exchange Online에서 메일 사용이 가능한 공용 폴더를 기대 하는 경우 디렉터리 기반 Edge 차단 (DBEB) 온라인 Exchange 및 Exchange 온라인 보호 (EOP)를 사용 하지 않도록 설정 해야 합니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/dn600322(v=exchg.150)">디렉터리 기반 Edge 차단을 사용하여 잘못된 받는 사람에게 전송된 메시지 거부</A> 참조 하십시오.



2.  **\\** 백슬래시 또는 슬래시가 **/** 공용 폴더의 이름을 포함 하는 경우 그 수 마이그레이션되지 않는 지정 된 사서함의 마이그레이션 프로세스 동안. 를 마이그레이션하기 전에 이러한 문자를 제거 하려면 해당 폴더를 이름을 바꿀합니다
    
    1.  이름에 백슬래시 있는 공용 폴더를 찾으려면 다음 명령을 실행 합니다.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  공용 폴더가 반환되면 다음 명령을 실행하여 이름을 바꿀 수 있습니다.
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  다음 단계를 시킨 조직에 이전 하 고 성공적인 마이그레이션에 대 한 기록을 확인 합니다. 없을 경우, 해당 값을 `$false`으로 설정 해야 합니다.
    
    값을 변경 하기 전에 실수로 두 번째 마이그레이션 수행 하지 않도록 이전 마이그레이션 시도 취소할 수 있는지 확인 하십시오.
    
    1.  모든 이전 이주와 이러한 마이그레이션 상태를 확인 하려면 다음 명령을 실행 합니다.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        

        > [!NOTE]
        > <CODE>$true</CODE>는 <CODE>PublicFoldersLockedforMigration</CODE> 또는 <CODE>PublicFolderMigrationComplete</CODE> 매개 변수는 특정 시점 이전 공용 폴더를 마이그레이션한 것입니다. 3b 단계를 계속 하기 전에 모든 기존 공용 폴더 데이터베이스 역할이 해제 되었으면가지고 있는지 확인 하십시오.

    
    2.  위의 모든 `$true`로 설정 하는 값으로 반환 되 면 있도록 `$false` 를 실행 하 여:
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  완성 마이그레이션의 성공 여부를 확인 하기 위해 모든 적절 한 2013 Exchange 서버에서 다음 명령을 실행 하는 것이 좋습니다. 새로 마이그레이션된 공용 폴더와 함께 비교를 나중에 사용할 수 있는 사용자의 현재 공용 폴더 배포의 스냅샷을 걸립니다.
    

    > [!NOTE]
    > Exchange 조직 크기에 따라 이러한 명령을 실행 하려면 약간의 시간이 걸릴 수 있습니다.

    
      - 다음 명령을 실행하여 원래 원본 폴더 구조의 스냅숏을 만듭니다.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - 다음 명령을 실행하여 항목 수, 크기 및 소유자와 같은 공용 폴더 통계에 대한 스냅숏을 만듭니다.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - 공용 폴더 사용 권한 스냅숏 만들기 다음 명령을 실행 합니다.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - 메일 사용 가능 공용 폴더의 스냅샷을 다음 명령을 실행 합니다.
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - 마이그레이션 후에 비교 하기 위해 안전한 곳에 위의 명령에서 생성 된 파일을 저장 합니다.

5.  다음 작업을 수행 해야 Microsoft Azure Active Directory 연결 (광고 Azure Connect) Active Directory Azure와 온-프레미스 디렉터리 동기화를 사용할 경우 (Azure 광고 연결을 사용 하지 않는 경우 건너뛸 수 있습니다이 단계).
    
    1.  온-프레미스 컴퓨터에서는 Microsoft Azure Active Directory 연결을 열고 **구성** 을 선택 합니다.
    
    2.  **추가 작업** 화면에서 **사용자 지정 동기화 옵션** 을 선택한 후 **다음** 을 클릭 합니다.
    
    3.  **Azure 광고에 연결** 화면에서 적절 한 자격 증명을 입력 한 후 **다음** 을 클릭 합니다. 연결이 되 면 **다음** 때까지 계속 클릭 **선택적 기능** 화면에 연결 되어 있습니다.
    
    4.  **메일 공용 폴더** 선택 되지 않았는지 확인 하십시오. 을 선택 하지 않으면 *필수 단계 Exchange 온라인*, 다음 절을 계속 수 있습니다. 선택 되어 있으면 확인란을 선택 취소 하 고 을 클릭 합니다.
        

        > [!NOTE]
        > <STRONG>공용 폴더 메일기능 선택</STRONG> 화면에서 옵션으로 표시 되지 않으면, Microsoft Azure Active Directory 연결을 종료할 수 있으며 <EM>필수 Exchange 온라인 단계를</EM>다음 섹션으로 이동.

    
    5.  **메일 공용 폴더** 선택, 선택을 취소 한 후 **구성할 수** 있는 화면에 나타날 때까지 **다음** 을 클릭 하 두고 **구성** 을 클릭 합니다.

**Exchange 온라인의 필수 단계**

Exchange 온라인 PowerShell에서 다음을 수행 합니다.

1.  기존 공용 폴더 마이그레이션 요청이 없으면 선택 되어 있는지 확인 하십시오. 선택 취소 하거나 직접 마이그레이션 요청이 실패 합니다. 이 단계는만 실패 하는 등의 중단 하려면 파이프라인에서 기존 마이그레이션 요청 수 생각 하는 경우 필요 합니다.
    
    기존 마이그레이션 요청 두 가지 유형 중 하나일 수 있습니다: 마이그레이션 일괄 처리 또는 직렬 마이그레이션. 감지 및 제거, 각 유형의 요청에 대 한 주석은 다음과 같습니다.
    
    다음 예제에서는 기존 직렬 마이그레이션 요청 검색 합니다.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    다음 예제에서는 기존 직렬 마이그레이션 요청 공용 폴더를 제거합니다.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    다음 예제에서는 기존 마이그레이션 일괄 처리 요청을 검색 합니다.
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    다음 예제에서는 기존 공용 폴더 배치 마이그레이션 요청을 제거합니다.
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  마이그레이션 기능이 **PAW** 사용자 Office 365 테 넌 트에 대해 활성화 해야 합니다. Exchange 온라인 PowerShell에서 다음 명령을 실행 하 여이 확인할 수 있습니다.
    
        Get-MigrationConfig
    
    **PAW** **기능** 에서 출력 있으면 기능이 설정 되어 있는 하 고 단계를 계속할 수 있습니다.
    
    발은 아닙니다 아직 해당 테 넌 트를 사용 수 있습니다 일부 기존 마이그레이션 일괄 처리를 해야 하기 때문에 공용 폴더 배치 또는 사용자 일괄 처리. 이러한 일괄 처리 완료를 포함 하 여 모든 상태일에서 수 있습니다. 이런 경우 완료 하 고 `Get-MigrationBatch`를 실행 하면 반환 된 레코드가 없을 때까지 모든 마이그레이션 일괄 처리를 제거 하십시오. 기존의 모든 일괄 처리에서 제거 되 면 발 자동 활성화 얻을 합니다. 즉시 `Get-MigrationConfig` 에 있는 변경 내용을 반영 하지 못하는 것이 좋습니다. 이 단계가 완료 되 면 새 일괄 처리를 만드는 경우 사용자 마이그레이션을 계속할 수 있습니다.

3.  기존 공용 폴더나 공용 폴더 사서함에서 Exchange Online에 없는 있는지 확인 하십시오. Exchange 공용 폴더를 검색 않으면 단계 아래, 그의 존재는 왜 고 보고 조직에서 누가 시작 하기 전에 공용 폴더 계층 구조를 결정 해야 후 온라인 시작 공용 폴더 및 공용 폴더를 제거 합니다. 사서함입니다.
    
    1.  Office 365 또는 Exchange Online PowerShell에서 다음 명령을 실행하여 공용 폴더 사서함이 있는지 확인합니다.
        
            Get-Mailbox -PublicFolder
    
    2.  명령은 공용 폴더 사서함을 반환 하는 경우 계속 해 서 3 단계:.csv 파일을 생성. 명령에서 공용 폴더 사서함 반환 하 고, 모든 공용 폴더가 있는지 확인 하려면 다음 명령을 실행 합니다.
        
            Get-PublicFolder -Recurse
    
    3.  Office 365 또는 Exchange Online에서 모든 공용 폴더를 설정한 경우에 (필요 하지 않은 것을 확인) 한 후이 제거 하려면 다음 PowerShell 명령을 실행 합니다. 공용 폴더를 제거 하면 모든 정보가 영구적으로 삭제 되므로, 삭제 하기 전에이 공용 폴더에 있는 모든 정보를 저장 한 있는지 확인 하십시오.
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  공용 폴더가 제거 되는 모든 공용 폴더 사서함을 제거 하려면 다음 명령을 실행 합니다.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## .Csv 파일을 생성 하는 3 단계:

이전에 다운로드 된 스크립트를 사용 하 여 마이그레이션에 사용 될.csv 파일을 생성.

1.  (온-프레미스) Exchange 관리 셸에서 폴더 크기 폴더 이름에 매핑 파일을 만드는 `Export-ModernPublicFolderStatistics.ps1` 스크립트를 실행 합니다. 이 스크립트를 실행 하려면 로컬 관리자 권한이 있어야 합니다. 결과 파일 세 개의 열이 포함 되어: **폴더 이름**, **FolderSize** 및 **DeletedItemSize**. **FolderSize** 및 **DeletedItemSize** 열의 값을 바이트 단위로 표시 됩니다. 예를 들어, **\\PublicFolder01,10240, 100은** PublicFolder01 이라는 계층의 루트에 공용 폴더 10240 바이트 또는 10.240 MB 크기 이며 100 바이트의 복구할 수 있는 항목.
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **예**:
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  원본 공용 폴더 공용 폴더 대상 Exchange Online 사서함에 매핑하는.csv 파일을 만들려면 `ModernPublicFolderToMailboxMapGenerator.ps1` 스크립트를 실행 합니다. 이 파일이 올바른 Exchange Online의 공용 폴더 사서함 수를 계산 하는 데 사용 됩니다.
    

    > [!NOTE]
    > <CODE>ModernPublicFolderToMailboxMapGenerator.ps1</CODE> 에 의해 생성 되는 파일에는 조직의 모든 공용 폴더의 이름이 포함 되지 않습니다. 상위 폴더에 대 한 참조를 포함 합니다 큰 폴더 트리 또는 폴더 이름 자체가 상당히 큰. 상상할 수 있는이 파일의 특정 폴더 트리를 확인 하는 "예외" 파일을 사용 하 고 더 큰 폴더에 특정 공용 폴더 메일 배치상자입니다. 것은 정상 모든 중 공용 폴더가이 파일에 표시 되지 않도록입니다. 이 매핑 파일에 나열 된 폴더의 하위 폴더 마이그레이션됩니다 상위 폴더 같은 공용 폴더 사서함 (명시적인 언급이 다른 공용 폴더 사서함에 직접 연결 하는 매핑 파일에서 다른 줄에).

    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes` 는 하나의 공용 폴더 사서함에 Exchange 온라인 마이그레이션할 데이터의 최대 양입니다. 이 필드의 최대 크기는 현재 50GB 있지만 향후 성장을 위한 최대 크기의 50% 등의 더 작은 크기를 사용 하는 것이 좋습니다.
    
      - `Maximum mailbox recoverable items size in bytes` Exchange Online 사서함의 복구 가능한 항목 할당량입니다. 온라인 Exchange의 공용 폴더 사서함의 최대 크기는 50GB 현재. 15GB 이하인` RecoverableItemsQuota` 를 설정 하는 것이 좋습니다.
    
      - `Folder-to-size map path` `Export-ModernPublicFolderStatistics.ps1` 스크립트를 실행할 때 만든.csv 파일의 파일 경로입니다.
    
      - `Folder-to-mailbox map path` 는이 단계에서 만들고 있는 폴더-사서함.csv 파일의 파일 경로입니다. 파일 이름을 지정할 경우 로컬 컴퓨터에 현재 PowerShell 디렉터리에 파일이 생성 됩니다.

**예**:

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv


> [!NOTE]
> 우리 하면 Exchange Online에서 고유한 공용 폴더 사서함 수가 100 개 이상 이면 마이그레이션 공용 폴더를 Exchange 온라인으로 지원 하지 않습니다.



## 4 단계: 공용 폴더 사서함을 Exchange Online에서 만들기

이제 Exchange 온라인 PowerShell 마이그레이션된 공용 폴더에 있는 대상 공용 폴더 사서함을 만듭니다.

1.  대상 공용 폴더 사서함을 만들려면 다음 스크립트를 실행 합니다. 스크립트에서 이전에 생성 된.csv 파일에는 각 사서함에 대해 대상 사서함 만들어집니다 *3 단계:.csv 파일을 생성*`ModernPublicFoldertoMailboxMapGenerator.ps1` 스크립트를 실행 하는 경우.
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path` `ModernPublicFoldertoMailboxMapGenerator.ps1` 스크립트에 의해 생성 된 폴더에서 사서함.csv 파일의 파일 경로 *3 단계:.csv 파일을 생성*.

## 5 단계: 마이그레이션 요청 시작

여러 가지 명령 실행할 수 및 Exchange에서 Exchange 2013 온-프레미스 환경에서 온라인 해야 합니다.

1.  공용 폴더 사서함을 호스팅하는 2013 Exchange 서버에서 다음 스크립트를 실행 합니다. 이 스크립트는 메일 사용 가능 공용 폴더를 로컬 Active Directory를 Exchange 온라인으로 동기화 합니다. 이 스크립트의 최신 버전을 다운로드 하 고 실행 하는 것에서 Exchange 관리 셸을 있는지 확인 하십시오.
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential` Exchange Online 관리자가 사용자 이름과 암호입니다.
    
      - `CsvSummaryFile` 오류가 있는 동기화 작업의 로그 파일을 원하는 위치에 파일 경로입니다. .Csv 형식 로그가 됩니다.

2.  2013 Exchange 서버의 부인은 어 프록시 끝점 서버 찾아 기록 하기. 마이그레이션 요청을 실행 하려면이 정보가 필요 합니다. 3b 단계 아래에이 정보를 저장 합니다.

3.  Exchange 온라인 PowerShell에서 마이그레이션 요청에 사용할 변수를 cmdlet에 이전 단계의 부인은 어 정보와 자격 증명 정보를 전달 하기 위해 다음 명령을 실행 합니다.
    
    1.  2013 Exchange 온-프레미스 환경 변수 `$Source_Credential`에 대 한 관리자 권한이 있는 사용자의 자격 증명을 전달 합니다. 마이그레이션 요청을 실행 하는 Exchange Online Exchange Online에 콘텐츠를 통해 공용 폴더를 복사 하 여 온-프레미스 Exchange 2013 서버에 액세스 하 여이 자격 증명을 사용 합니다.
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  위의 2 단계에서 발견 하 고 변수로 전달 2013 Exchange 환경에서 부인은 어 프록시 서버 정보를 수행 합니다.
        
            $Source_RemoteServer = "<paste the value here>"

4.  온라인 PowerShell Exchange 공용 폴더 마이그레이션 끝점과 공용 폴더 마이그레이션 요청을 만들려면 다음 명령을 실행:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    

    > [!NOTE]
    > 여러 개의 이메일 주소를 쉼표로 구분 합니다.

    
    여기서 `folder_mapping.csv` 은 맵 파일에서 생성 된 *3 단계:.csv 파일 만들기*. 전체 파일 경로 제공 해야 합니다. 어떤 이유로 든 맵 파일이 이동 된 경우 새 위치를 사용 해야 합니다.

5.  마지막으로, Exchange 온라인 powershell에서 다음 명령을 사용 하 여 마이그레이션을 시작 합니다.
    
        Start-MigrationBatch PublicFolderMigration

마이그레이션 배치를 새로 MigrationBatch cmdlet를 사용 하 여 Exchange 온라인 powershell에서 해야 하는 동안 진행 상황 및 마이그레이션 완료 확인 및 수 EAC 또는 Get MigrationBatch cmdlet를 실행 하 여 관리. New MigrationBatch cmdlet는 각 공용 폴더 사서함에 대해 사서함 마이그레이션 요청을 시작 하 고 사서함 마이그레이션 페이지를 사용 하 여 이러한 요청의 상태를 볼 수 있습니다.

사서함 마이그레이션 페이지로 돌아갑니다.

1.  Exchange 온라인 로그온 및 EAC를 엽니다.

2.  **받는 사람** 게 이동한 다음 **마이그레이션** 을 선택 합니다.

3.  방금 만든 마이그레이션 요청을 선택한 다음 **세부 정보** 창에서 **자세히 보기를** 선택 합니다.

에 이동 하기 전에 *6 단계: 2013 Exchange 서버에 공용 폴더 잠금*, 모든 데이터가 복사 된 마이그레이션에 오류가 있는지 확인 하십시오. 일괄 처리에 **Synced** 의 상태로 옮겨졌는지 확인에서 설명한 명령을 실행 *2 단계: 마이그레이션을 위한 준비*, 최종 단계에서 **온-프레미스 Exchange 2013 서버 환경에서 필수 단계를**아래에 공용 폴더 온-프레미스의 스냅숏을 만듭니다. 이러한 명령을 실행 한 후 다음 단계로 진행할 수 있습니다. 이러한 명령은 있는 폴더 수에 따라 시간이 걸릴 수 있는지 note입니다.

## 6 단계: 최종 마이그레이션 (공용 폴더 작동 중단)에 대 한 2013 Exchange 환경에서 공용 폴더 잠금

마이그레이션 프로세스의이 시점까지 사용자가 온-프레미스 공용 폴더에 액세스할 수 없게 되었습니다. 다음 단계는 현재 사용자를 로그 오프 2013 Exchange 공용 폴더에서 되며 마이그레이션 프로세스는 마지막 동기화를 완료할 때마다 폴더를 잠글. 사용자가이 시간 동안 공용 폴더에 액세스할 수 없습니다 하 고 이러한 메일 사용 가능 공용 폴더에 전송 된 모든 메시지는 대기 공용 폴더 마이그레이션을 완료 될 때까지 배달 되지 않은.

아래와 같이 `PublicFolderMailboxesLockedForNewConnections` 명령을 실행 하기 전에 모든 작업 **Synced** 상태에 있는지 확인 하십시오. `Get-PublicFolderMailboxMigrationRequest` 명령을 실행 하 여이 수행할 수 있습니다. 모든 작업은 **Synced** 상태를 확인 한 후에이 단계를 계속 합니다.

온-프레미스 환경의 종료 2013 Exchange 공용 폴더를 잠그려면 다음 명령을 실행 합니다.

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true


> [!NOTE]
> <CODE>-PublicFolderMailboxesLockedForNewConnections</CODE> 매개 변수에 액세스할 수 없는 경우 이기 때문일 수 CU 업그레이드 하는 동안 Active Directory 준비 되지 않았습니다 위에 사전에 알고 있었던 것 처럼 <EM>를 시작 하기 전에 알고 하 시겠습니까?</EM> 자세한 내용은 <A href="prepare-active-directory-and-domains-exchange-2013-help.md">Active Directory 및 도메인 준비</A> 참조 하십시오.<BR>또한 모든 사용자에 게 공용 폴더에 액세스 해야 하는 <STRONG>전에</STRONG> 공용 폴더 자체를 마이그레이션하려면 먼저 마이그레이션됩니다.



조직에 여러 Exchange 2013 서버의 공용 폴더 사서함을 AD 복제가 완료 될 때까지 대기 해야 합니다. 완료 되 면 모든 공용 폴더 사서함 `PublicFolderMailboxesLockedForNewConnections` 플래그를 지정 하 고 모든 보류 중인 변경 내용을 조직 전체에 걸쳐 최근에 해당 공용 폴더의 내용을 사용자가 수렴 선택 되어 있는지 확인할 수 있습니다. 이 몇 시간이 걸릴 수 있습니다.

## 7 단계: 공용 폴더 마이그레이션 (공용 폴더 작동 중단) 완료

공용 폴더 마이그레이션을 완료 하려면, 이동 하는 다른 공용 폴더 사서함 또는 공용 폴더 이동 하는 것에서 온-프레미스 Exchange 환경에 이동 되는지 확인 해야 합니다. 이렇게 하려면 `Get-MoveRequest` 및 `Get-PublicFolderMoveRequest` cmdlet를 사용 하 여 기존 공용 폴더 목록으로 이동 합니다. 모든 이동 진행 중에서 또는 **완료** 상태에 있는 경우 제거 합니다.

다음으로 공용 폴더 마이그레이션을 완료 하는 데 Exchange 온라인 PowerShell에서 다음 명령을 실행 합니다.

    Complete-MigrationBatch PublicFolderMigration

이 명령을 실행 하면 Exchange Exchange 온-프레미스 조직 및 Exchange Online 사이의 마지막 동기화를 수행 합니다. 이 그러는 동안 마이그레이션 일괄 처리의 상태에서 **Synced** 으로 바뀝니다 **완료** 한 후 마지막으로 **완료 됨**. 마지막 동기화가 이루어지면 Exchange Online 공용 폴더 잠금이 됩니다.

일반적으로 마이그레이션 일괄 처리가 **완료Synced** 에서 상태 변경 하기 전에 몇 시간까지 걸릴, 나타나는데 최종 동기화가 시작 됩니다.

## 8 단계: 테스트 하 고 Exchange Online에서 공용 폴더를 잠금 해제

공용 폴더 마이그레이션을 완료 되 면 다음 단계 마이그레이션의 성공 여부를 테스트 하 고 공식적으로 완료를 확인할 수 있습니다. 이러한 최종 작업을 수행 하면 마이그레이션된 공용 폴더 계층 구조를 조직의 Exchange Online 공용 폴더를 영구적으로 전환 하기 전에 테스트할 수 있습니다.

1.  Exchange 온라인 PowerShell 할당 직원과 사용자 사서함의 기본 공용 폴더 사서함으로 새로 마이그레이션된 공용 폴더 사서함 중 하나를 사용 하 여.:
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    테스트 사용자가 공용 폴더를 만드는 데 필요한 권한이 있는지 확인 하십시오.

2.  이전 단계에서 지정 하 고 공용 폴더 다음 테스트를 수행할 테스트 사용자로 Outlook에 로그온 합니다. 노트 변경 사항이 적용 되려면 15 ~ 30 분 정도 걸릴 수 있습니다. Outlook에서 변경 사항을 인식 되 면 두 번 다시 시작 해야를 요청할 수 있습니다.
    
    1.  계층 구조를 확인합니다.
    
    2.  사용 권한을 확인합니다.
    
    3.  일부 공용 폴더를 만들고 삭제 합니다.
    
    4.  공용 폴더에서 삭제 콘텐츠와 콘텐츠를 게시 합니다.
    
    문제에 실행 하 고 조직의 공용 폴더를 Exchange Online으로 완전히 전환할 준비가 당신이 있는지 확인 [공용 폴더 마이그레이션 롤백 Exchange 2013에서 Exchange Online으로](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md)을 참조 하십시오.

3.  다음 명령을 Exchange 온라인 Exchange 공용 폴더를 잠금을 해제 하려면 PowerShell 온라인. 명령을 실행 한 후 변경 내용을 적용 하려면 약 15-30 분 정도 걸립니다. Outlook에서 변경 사항을 인식 되 면 다음 사용자가 프로그램을 여러 번 다시 시작 하도록 요청할 수 있습니다 것입니다.
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## 9 단계: 마이그레이션 온-프레미스 마무리

공용 폴더를 메일 사용이 가능한 온-프레미스 전자 메일을 사용 하려면 다음과이 같이 하십시오.

1.  온-프레미스 환경에서 메일 사용 가능 공용 폴더에 있는 모든 전자 메일 Exchange 온라인 올바르게 라우팅됩니다 되도록 다음 스크립트를 실행 합니다. 스크립트는 Exchange Online 상응 하는를 가리키는 `ExternalEmailAddress` 를 사용 하 여 메일 사용 가능 공용 폴더를 스탬프:
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  테스트에 성공 하면 온-프레미스 환경에서 공용 폴더 마이그레이션을 완료 되었음을 나타내기 위해 다음 명령을 실행 합니다.
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## 작동 여부는 어떻게 확인합니까?

2 단계: 마이그레이션을 위한 준비, 온-프레미스 공용 폴더 구조, 통계 및 사용 권한 스냅숏 찍은. 다음 단계는 온라인 Exchange 마이그레이션 후에 동일한 스냅숏을 사용 하 여 공용 폴더 마이그레이션을 제대로 되었는지 확인 하는 데 도움이 됩니다. 성공 여부를 확인 하려면 두 파일의 데이터를 비교 합니다.

1.  Exchange 온라인 PowerShell에서 스냅숏을 새 폴더 구조를 다음 명령을 실행 합니다.
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  Exchange 온라인 PowerShell에서 스냅숏을 항목 수, 크기 및 소유자를 비롯 하 여 공용 폴더 통계를 다음 명령을 실행:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  Exchange 온라인 PowerShell에서 스냅숏을 사용 권한을 다음 명령을 실행 합니다.
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  Exchange 온라인 PowerShell에서 메일 사용 가능 공용 폴더의 스냅숏을 다음 명령을 실행 합니다.
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## 알려진 문제

다음은 조직에서 발생할 수 있는 일반적인 공용 폴더 마이그레이션 문제입니다.

  - 우리 하면 Exchange Online에서 고유한 공용 폴더 사서함 수가 100 개 이상 이면 마이그레이션 공용 폴더를 Exchange 온라인으로 지원 하지 않습니다.

  - 사용 권한 EFORMS REGISTRY 폴더와 루트 공용 폴더는 마이그레이션되지 않습니다 Exchange Online을 수동으로 해야 합니다에 대 한 적용 한 Exchange 온라인 됩니다. 이렇게 하려면 Exchange 온라인 powershell에 다음 명령을 실행 합니다. 구내에 있는 각 사용 권한 항목에 대해 한 번씩 명령을 실행 하지만 없음 Exchange 온라인.
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - 일부 공용 폴더 사서함 공용 폴더 계층 구조를 제공 하지 않습니다 일부 공용 폴더 마이그레이션 실패 합니다. 즉, 하나 이상의 사서함에서 `IsExcludedFromServingHierarchy` 매개 변수를 `$true`로 설정 되어 있는지. 이 방지 하려면 계층을 처리 하기 위해 Exchange Online에서 모든 사서함을 설정 합니다.

  - **사람 이름으로 보내기** 및 **대신 보내기** 권한은 Exchange Online으로 마이그레이션되지 않는. 이 마이그레이션을 경우 이러한 권한이 있는 담당자를 온-프레미스 환경에서 다음 명령을 사용 합니다.
    
    공용 폴더 다른 사람 이름으로 보내기 권한을 확인 하려면 온-프레미스:
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    공용 폴더는 권한이 온-프레미스를 대신 하 여 보낼 수 있습니다.
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    Exchange 메일 사용 가능 공용 폴더에 다른 사람 이름으로 보내기 권한을 추가 하려면 온라인 Exchange 온라인 PowerShell을 입력.
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **예**:
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    Exchange 보내기 메일 사용 가능 공용 폴더를 대신 하 여 권한을 추가 하려면 온라인 Exchange 온라인 PowerShell을 입력.
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **예**:
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" 폴더 10000 개 이상의 폴더 마이그레이션이 실패 발생할 수 있습니다. 따라서 "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" 폴더 바로 아래 (직계 자식) 10, 000 개 이상의 폴더가 있는지를 확인 합니다. 이 위치에 있는 공용 폴더의 수를 찾으려면 다음 명령을 사용할 수 있습니다.
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online 지원 하지 않습니다 10000 개 이상의 하위 폴더 이기 때문에 10000 개 이상의 폴더 마이그레이션을 실패 하 게 됩니다. 이러한 구성의 차단을 해제 하는 스크립트를 현재 개발 중인 우리. 한편, 대기 공용 폴더를 마이그레이션하는 것이 좋습니다.

  - 마이그레이션 작업 진행 됩니다 또는 중단 됩니다. 이 너무 많은 작업이 병렬로 실행, 간헐적인 오류와 함께 실패 하는 작업이 발생 하는 경우 발생할 수 있습니다. `MaxConcurrentMigrations` 및 `MaxConcurrentIncrementalSyncs` 더 작은 수를 수정 하 여 동시 작업 수를 줄일 수 있습니다. 이러한 값을 설정 하려면 다음 예제를 사용 합니다.
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - 오류가 발생 하 여 마이그레이션 작업 실패 "오류: 휴지통 폴더의 휴지통." 이 오류가 표시 되 면 일괄 처리를 중지 한 다음 다시 시작 하는 경우 확인할 수 있어야.

  - 마이그레이션 작업 실패 하 고 생성 한 "요청이 다음 오류로 인해 격리 된: 지정한 키가 사전에 없습니다" 오류 메시지. 이 마이그레이션 작업을 복사할 수 없습니다 폴더에 손상된 된 항목이 있으면 발생 합니다. 이 문제를 해결 하려면
    
    1.  마이그레이션 일괄 처리를 중지 합니다.
    
    2.  잘못 된 항목이 들어 있는 폴더를 식별 합니다. 마이그레이션 보고서에 오류 발생 시 복사 된 폴더에 대 한 참조가 포함 되어야 합니다.
    
    3.  온-프레미스 환경에서 기본 공용 폴더 사서함에 폴더를 이동 합니다. 폴더를 이동 하려면 `New-PublicFolderMoveRequest` cmdlet를 사용할 수 있습니다.
    
    4.  폴더 이동이 완료 될 때까지 기다립니다. 완료 되 면 이동 요청을 제거 합니다. 마이그레이션 일괄 처리를 다시 시작 합니다.

## 공용 폴더 사서함을 온-프레미스 Exchange 환경에서 제거

마이그레이션이 완료 되 고 확인 온라인 Exchange에서 공용 폴더는 예상 대로 하 고 필요한 모든 데이터를 포함, 온-프레미스 공용 폴더 사서함을 제거할 수 있습니다.

삭제 된 공용 폴더 사서함은 복구할 수 없으므로이 단계는 되돌릴 수 있음을 주의 해야 합니다. 따라서, 여 마이그레이션의 성공 여부를 확인 하는 것 외에도 또한 모니터링 하 여 Exchange Online 공용 폴더 공용 폴더 온-프레미스 사서함을 제거 하기 전에 몇 주 동안 것이 좋습니다.

