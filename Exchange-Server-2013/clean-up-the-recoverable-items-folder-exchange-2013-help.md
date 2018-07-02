---
title: '복구 가능한 항목 폴더를 정리: Exchange 2013 Help'
TOCTitle: 복구 가능한 항목 폴더를 정리
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50556025
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 복구 가능한 항목 폴더를 정리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-09-30_

(이 항목은 관리자를 위한 Exchange.)

복구 가능한 항목 폴더 (이전 버전으로 Exchange 알려진 *는 휴지통*)을 실수로 또는 악의적 삭제를 방지 하 고 일반적으로 이전 또는 소송 보존 또는 조사 하는 동안 작업을 수행 하는 검색 작업을 원활 하 게 존재 합니다. 복구 가능한 항목 폴더에 대 한 자세한 내용은, [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조 하십시오.

사용자의 사서함에서 복구 가능한 항목 폴더를 정리 하는 방법에 따라 달라 집니다 또는 단일 항목 복구가 사용 여부는 사서함의 원본 위치 유지 또는 소송 보존에 배치 됩니다.

  - 사서함의 원본 위치 유지 또는 소송 보존에 배치 되지 않거나 단일 항목 복구를 사용할 수 없으면, 복구 가능한 항목 폴더에서 항목을 간단히 삭제할 수 있습니다. 삭제 되 고 후의 항목을 복구 하려면 단일 항목 복구를 사용할 수 없습니다.

  - 사서함 원본 위치 유지 또는 소송 보존에 배치 또는 단일 항목 복구를 사용 하는 경우에 보존이 제거 또는 단일 항목 복구를 사용 하지 않도록 설정 될 때까지 사서함 데이터를 보존 하는 것이 중요 합니다. 이 경우의 복구 가능한 항목 폴더를 정리 하는 더 자세한 단계를 수행 해야 합니다.

원본 위치 유지 및 소송 보존으로 설정 하는 방법에 대 한 자세한 내용은, [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md)를 참조 하십시오. 단일 항목 복구 하는 방법에 대 한 자세한 내용은, [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)에서 "단일 항목 복구"를 참조 하십시오.

복구 가능한 항목 폴더에 대 한 자세한 내용은, [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)를 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상이 절차를 완료 시간: 30 분입니다. 복구 가능한 항목 폴더의 크기에 따라 다를 수 있습니다.

  - 검색 하 여 사용자의 사서함에서 메시지를 삭제 하려면 **Search-Mailbox** cmdlet을 사용 하려면 다음 관리 역할을 할당 해야 합니다.
    
      - **사서함 검색**   이 역할을 통해 사용자는 조직의 여러 사서함에 있는 메시지를 검색할 수 있습니다. 관리자에게는 기본적으로 이 역할이 할당되지 않습니다. 사서함을 검색할 수 있도록 이 역할을 자신에게 할당하려면 자신을 검색 관리 역할 그룹의 구성원으로 추가합니다. [Exchange eDiscovery 사용 권한 할당](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)를 참조하세요.
    
      - **사서함 가져오기 내보내기**   이 역할을 사용 하면 사용자의 사서함에서 메시지를 삭제할 수 있습니다. 기본적으로이 역할은 모든 역할 그룹에 할당 되지 않습니다. 사용자의 사서함에서 메시지를 삭제 하려면 조직 관리 역할 그룹에는 사서함 가져오기 내보내기 역할을 추가할 수 있습니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 의 "역할을 역할 그룹에 게 추가" 섹션을 참조 하십시오.

  - 있기 때문에 복구 가능한 항목 폴더 올바르게 정리 데이터 손실이 발생할 수 있습니다, 복구 가능한 항목 폴더 및 해당 내용을 제거의 영향을 익숙한 것이 중요 합니다. 이 절차를 수행 하기 전에 [복구 가능한 항목 폴더](recoverable-items-folder-exchange-2013-help.md)에 대 한 정보를 검토 하는 것이 좋습니다.

  - 이러한 절차를 수행 하려면 Exchange 관리 센터 (EAC)를 사용할 수 없습니다. 셸을 사용 해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 셸을 사용 하 여 보류에 추가 되지 않은 되었거나 구성 되지 않은 단일 항목 복구를 사용 하는 사서함에 대 한 복구 가능한 항목 폴더에서 항목을 삭제 하려면

이 예에서는 Gurinder Singh의 복구 가능한 항목 폴더에서 항목을 영구적으로 삭제 하 고도 검색 사서함 ( Exchange 설치 하 여 만든 검색 사서함)에서 GurinderSingh RecoverableItems 폴더에 항목을 복사 합니다.

    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent


> [!NOTE]
> 사서함에서 다른 사서함으로 복사 하지 않고 항목을 삭제 하려면 <EM>TargetMailbox</EM> 및 <EM>TargetFolder</EM> 매개 변수 없이 앞의 명령을 사용 합니다.



구문과 매개 변수에 대한 자세한 내용은 [Search-Mailbox](https://technet.microsoft.com/ko-kr/library/dd298173\(v=exchg.150\))를 참조하십시오.

## 셸을 사용 하 여 단일 항목 복구를 사용 하거나 보류에 배치 되는 사서함에 대 한 복구 가능한 항목 폴더를 정리

사서함 복구 가능한 항목 할당량에 도달 하는 경우 할당량 발생 하 고 폴더에서 항목을 삭제 하지는 것이 좋습니다. 복구 가능한 항목 경고 보내기 할당량와 관련 된 응용 프로그램 로그에 이벤트를 모니터링 하 고 (예: 할당량을 발생 시키는 또는 경고 보내기 할당량에 도달 하는 사서함에 대 한 복구 가능한 항목 폴더의 증가 조사) 필요한 작업을 수행할 수도 있습니다.

저장소 제약 조건 또는 유사한 문제로 인해 하면에서 복구 가능한 항목 할당량 발생 하 고 원본 위치 유지 또는 소송 보존으로 설정 된 사서함의 복구 가능한 항목 폴더에서 메시지를 삭제 해야 하거나가 단일 항목 복구를 사용 하는 경우에 먼저을 복사 하는 데이터는 사용자의 복구 가능한 항목 폴더에서 다른 사서함 하는 것이 좋습니다. 한 볼륨에 저장소 제약 조건으로 인해 항목을 삭제 하는 경우에 적절 한 저장소를 포함 된 볼륨에 있는 사서함에 항목을 복사할 수 있습니다.

이 절차를 사용 하면 Gurinder Singh의 복구 가능한 항목 폴더에서 항목을 복사 하는 사서함 검색에서에서 GurinderSingh RecoverableItems 폴더로 합니다. 복사 및 복구 가능한 항목 폴더에서 항목을 삭제 하기 전에 먼저 항목이 복구 가능한 항목 폴더에서 삭제 되지 않은 있는지 확인 하려면 여러 단계를 수행 해야 합니다. 검색 또는 백업 사서함에 항목을 복사 하 고 폴더를 정리 후에 사서함의 이전 설정으로 되돌릴 수 있습니다.

1.  다음 할당량 설정을 검색 합니다. 복구 가능한 항목 폴더를 정리 하 고 후 이러한 설정으로 되돌릴 수 있도록 값을 확인 해야 합니다.
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    

    > [!NOTE]
    > <EM>UseDatabaseQuotaDefaults</EM> 매개 변수는 <CODE>$true</CODE>로설정하면 이전 할당량 설정 적용 되지 않습니다. 사서함 데이터베이스에 구성 된 해당 할당량 설정은 개별 사서함 설정 채워져 하는 경우에 적용 됩니다.

    
        Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults

2.  사서함에 대 한 사서함 액세스 설정을 검색 합니다. 나중에 대 한 이러한 설정에 유의 해야 합니다.
    
        Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled

3.  복구 가능한 항목 폴더의 현재 크기를 검색 합니다. 6 단계에서에서 할당량을 발생 시킬 수 있도록 크기를 note 합니다.
    
        Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize

4.  현재 관리 되는 폴더 도우미가 작업 주기 구성을 검색 합니다. 나중에 대 한 설정을 확인 해야 합니다.
    
        Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle

5.  이 절차의 기간에 대 한 변경 된 내용이 없습니다를 사서함 데이터를 설정할 수 있는지 확인 하는 사서함에 대 한 클라이언트 액세스를 사용 하지 않도록 설정 합니다.
    
        Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false

6.  항목이 없는 복구 가능한 항목 폴더에서 삭제 하려면 복구 가능한 항목 할당량을 늘릴 수, 복구 가능한 항목 경고 할당량을 늘릴 수 및 사용자의 복구 가능한 항목 폴더의 현재 크기 보다 큰 값으로 삭제 된 항목 보존 기간을 설정 합니다. 이 원본 위치 유지 또는 소송 보존 상태인 사서함에 대 한 메시지를 유지 하기 위한 특히 중요 합니다. 이러한 설정의을 두번 현재 크기를 발생 시키는 것이 좋습니다.
    
        Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false

7.  관리 되는 폴더 도우미가 사서함 서버에서을 사용 하지 않도록 설정 합니다.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    

    > [!IMPORTANT]
    > 사서함 데이터베이스 가용성 그룹 (DAG)에서 사서함 데이터베이스에 있는 하는 경우에 관리 되는 폴더 도우미가 데이터베이스의 복사본을 호스팅하는 각 DAG 구성원에서을 비활성화 해야 합니다. 데이터베이스를 다른 서버로 장애 조치 하는 경우이 수 없도록는 관리 되는 폴더 도우미가 해당 서버에서 사서함 데이터를 삭제 합니다.



8.  단일 항목 복구를 사용 하지 않도록 설정 하 고 소송 보존으로 설정에서 사서함을 제거 합니다.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    

    > [!IMPORTANT]
    > 이 명령을 실행 하면 단일 항목 복구 또는 소송 보존으로 설정 하지 않으려면 1 시간까지 걸릴 수 있습니다. 이 기간이 경과한 후에 다음 단계를 수행 하는 것이 좋습니다.



9.  검색 검색 사서함의 폴더를 복구할 수 있는 항목 폴더에서 항목을 복사 하 고 원본 사서함에서 콘텐츠를 삭제 합니다.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    지정 된 조건에 맞는 메시지에만 삭제 해야하는 경우 조건을 지정 하려면 *SearchQuery* 매개 변수를 사용 합니다. **제목** 필드에 문자열 "Your bank statement"를 포함 하는 메시지를 삭제 하는이 예제입니다.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    

    > [!NOTE]
    > 사서함 검색에 항목을 복사할 필요가 없습니다. 모든 사서함에 메시지를 복사할 수 있습니다. 그러나 잠재적으로 중요 한 사서함 데이터에 대 한 액세스를 방지 하려면 메시지 권한이 부여 된 레코드 관리자에 게 제한 된 액세스 권한이 있는 사서함에 복사 하는 것이 좋습니다. 기본적으로 기본 검색 사서함에 대 한 액세스는 검색 관리 역할 그룹의 구성원으로 제한 합니다. 자세한 내용은 <A href="in-place-ediscovery-exchange-2013-help.md">원본 위치 eDiscovery</A>를 참조 합니다.



10. 사서함을 소송 보존에 배치 명 하는 경우 단일 항목 복구가 사용 이전, 이러한 기능을 다시 사용 합니다.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    

    > [!IMPORTANT]
    > 이 명령을 실행 하면 단일 항목 복구 또는 소송 보존을 사용 하도록 설정 하려면 1 시간까지 걸릴 수 있습니다. 후에이 관리 되는 폴더 도우미를 사용 하도록 설정 하 고 클라이언트 액세스 (11 단계 및 단계 12)를 허용 하는 권장 시간이 경과 했습니다.



11. 1 단계에서에서 기록한 값을 다음 할당량 되돌리기:
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    이 예제에서는 사서함을 보존 보류에서 제거 하 고 삭제 된 항목 보존 기간을 14 일의 기본값으로 다시 설정 됩니다 복구 가능한 항목 할당량 사서함 데이터베이스와 동일한 값을 사용 하도록 구성 된 합니다. 1 단계에서에서 적어둔 값이 다르면 하는 경우에 각 값을 지정 하 고 `$false`*UseDatabaseQuotaDefaults* 매개 변수를 설정 하려면 위의 매개 변수를 사용 해야 합니다. 이전에 *RetainDeletedItemsForand UseDatabaseRetentionDefaults* 매개 변수를 다른 값으로 설정 된, 1 단계에서에서 기록한 값도 돌아갈 해야 있습니다.
    
        Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true

12. 4 단계에서에서 적어둔 값으로 다시 작업 주기를 설정 하 여 관리 되는 폴더 도우미를 사용 합니다. 1 일 작업 주기를 설정 하는이 예제입니다.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

13. 클라이언트 액세스를 사용 하도록 설정 합니다.
    
        Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하세요.

  - [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/ko-kr/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/ko-kr/library/dd298173\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

사서함의 복구 가능한 항목 폴더를 정리 성공적으로 포함을 확인 하려면 [Get-MailboxFolderStatistics](https://technet.microsoft.com/ko-kr/library/aa996762\(v=exchg.150\)) cmdlet 검사 복구 가능한 항목 폴더의 크기를 사용 합니다.

복구 가능한 항목 폴더의 크기를 검색 하는이 예제 및 폴더 및 각 하위 폴더에 하위 폴더와 항목 개수입니다.

    Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto

