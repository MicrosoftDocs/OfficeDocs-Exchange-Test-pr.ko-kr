---
title: '복구 데이터베이스를 사용하여 데이터 복원: Exchange 2013 Help'
TOCTitle: 복구 데이터베이스를 사용하여 데이터 복원
ms:assetid: d64c18e7-16af-4bd8-a5c5-01206984d4d1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee332351(v=EXCHG.150)
ms:contentKeyID: 50484296
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 복구 데이터베이스를 사용하여 데이터 복원

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-10-01_

RDB(복구 데이터베이스)는 복구 작업 단계에서 복원된 사서함 데이터베이스를 탑재하고 복원된 사서함 데이터베이스에서 데이터를 추출하도록 지원되는 특별한 종류의 사서함 데이터베이스입니다. RDB를 사용하는 경우 현재 데이터에 대한 사용자 액세스를 방해하지 않고 데이터베이스의 백업 또는 복사본에서 데이터를 복구할 수 있습니다.

RDB를 만든 후 백업 응용 프로그램을 사용하거나 데이터베이스와 해당 로그 파일을 RDB 폴더 구조로 복사하여 사서함 데이터베이스를 RDB로 복원할 수 있습니다. 그런 다음 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\)) cmdlet을 사용하여 복구된 데이터베이스에서 데이터를 추출할 수 있습니다. 추출이 끝나면 데이터를 폴더로 내보내거나 기존 사서함에 병합할 수 있습니다.

RDB와 관련된 추가 관리 작업에 대한 자세한 내용은 [복구 데이터베이스](recovery-databases-exchange-2013-help.md)을 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분, 그리고 데이터베이스를 완전한 종료 상태가 되게 하여 데이터를 추출할 추가 시간

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 복구" 항목

  - 일부 백업 응용 프로그램에는 복구 데이터베이스에 직접 Exchange 데이터를 복원할 수 있는 기능이 있습니다. Windows Server 백업은 파일 수준 백업만 복구 데이터베이스로 복원할 수 있습니다. 응용 프로그램 수준 백업을 복구 데이터베이스로 복원하는 데는 사용할 수 없습니다.

  - 복구된 데이터가 포함된 데이터베이스와 로그 파일은 RDB 폴더 구조로 복원하거나 복사해야 합니다.

  - 데이터베이스가 완전 종료 상태여야 합니다. RDB는 모든 데이터베이스의 대체 복원 위치이므로 복원되는 모든 데이터베이스는 완전하게 종료된 상태가 아닙니다. 복원된 데이터베이스를 완전하게 종료된 상태로 만들려면 **Eseutil /R**을 사용해야 합니다.

## 복구 데이터베이스를 사용하여 데이터를 복구하기 위해 셸 사용

1.  복구된 데이터베이스나 해당 로그 파일을 복사하거나 데이터베이스 및 해당 로그 파일을 복구 데이터베이스에 사용할 위치로 복원합니다.

2.  Eseutil을 사용하여 데이터베이스를 완전히 종료된 상태로 전환합니다. 다음 예제에서 EXX는 데이터베이스의 로그 생성 접두사(예: E00, E01, E02 등)입니다.
    
        Eseutil /R EXX /l <RDBLogFilePath> /d <RDBEdbFolder>
    
    다음 예제에서는 로그 생성 접두사 E01과 복구 데이터베이스 및 로그 파일 경로 E:\\Databases\\RDB1을 보여 줍니다.
    
        Eseutil /R E01 /l E:\Databases\RDB1 /d E:\Databases\RDB1

3.  복구 데이터베이스를 만듭니다. 복구 데이터베이스에 고유한 이름을 지정하되 EdbFilePath 매개 변수에 데이터베이스 파일의 이름과 경로를 사용하고, LogFolderPath 매개 변수에 복구된 로그 파일의 위치를 사용합니다.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath <RDBPathandFileName> -LogFolderPath <LogFilePath>
    
    다음 예제에서는 E:\\Databases\\RDB1에 있는 DB1.edb 및 해당 로그 파일을 복구하는 데 사용되는 복구 데이터베이스를 만드는 방법을 보여 줍니다.
    
        New-MailboxDatabase -Recovery -Name <RDBName> -Server <ServerName> -EdbFilePath "E:\Databases\RDB1\DB1.EDB" -LogFolderPath "E:\Databases\RDB1"

4.  Microsoft Exchange 정보 저장소 서비스를 다시 시작합니다.
    
        Restart-Service MSExchangeIS

5.  복구 데이터베이스를 탑재합니다.
    
        Mount-database <RDBName>

6.  탑재된 데이터베이스에 복원할 사서함이 들어 있는지 확인합니다.
    
        Get-MailboxStatistics -Database <RDBName> | ft -auto

7.  New-MailboxRestoreRequest cmdlet을 사용하여 사서함 또는 복구 데이터베이스의 항목을 프로덕션 사서함으로 복원합니다.
    
    다음 예제에서는 Morris 별칭을 사용 하 여 대상 사서함에 사서함 데이터베이스 d b 1에서 MailboxGUID 1d20855f-fd54-4681-98e6-e249f7326ddd 있는 원본 사서함을 복원 합니다.
    
        New-MailboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox 1d20855f-fd54-4681-98e6-e249f7326ddd -TargetMailbox Morris
    
    다음 예제에서는 보관 사서함으로 사서함 데이터베이스 d b 1에 표시 이름 Morris Cornejo Morris@contoso.com가 있는 원본 사서함의 콘텐츠를 복원 합니다.
    
        New-MaiboxRestoreRequest -SourceDatabase DB1 -SourceStoreMailbox "Morris Cornejo" -TargetMailbox Morris@contoso.com -TargetIsArchive

8.  [Get-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829907\(v=exchg.150\))를 사용하여 사서함 복원 요청의 상태를 주기적으로 확인합니다.
    
    복원의 상태가 완료됨이면 [Remove-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829910\(v=exchg.150\))를 사용하여 복원 요청을 제거합니다. 예를 들면 다음과 같습니다.
    
        Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

## 작동 여부는 어떻게 확인합니까?

사서함 데이터가 성공적으로 복구되었는지 확인하려면 Outlook 또는 Outlook Web App를 사용하여 대상 사서함을 열고 복구된 데이터가 있는지 알아봅니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


