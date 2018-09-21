---
title: '사서함 데이터베이스 복사본에 대한 사서함 데이터베이스 이동: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본에 대한 사서함 데이터베이스 이동
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 50482798
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본에 대한 사서함 데이터베이스 이동

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-05-07_

사서함 데이터베이스를 만든 후 EAC나 셸을 사용하여 다른 볼륨, 폴더, 위치 또는 경로로 이동할 수 있습니다. 복제되지 않은 사서함 데이터베이스의 데이터베이스 경로를 이동하는 방법에 대한 단계별 지침은 [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) 항목을 참조하십시오.

이동할 사서함 데이터베이스가 하나 이상의 사서함 데이터베이스 복사본에 복제된 경우에는 이 항목에 나오는 절차를 따라 사서함 데이터베이스 경로를 이동해야 합니다. 사서함 데이터베이스의 모든 복사본은 복사본을 호스트하는 각 서버에서 같은 경로에 있어야 합니다. 예를 들어 DB1이 서버 EX1의 C:\\mountpoints\\DB1에 있으면 서버 EX2, EX3 등에서 DB1의 복사본도 C:\\mountpoints\\DB1에 있어야 합니다.

사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 2분. 데이터를 이동하는 시간 추가(이 시간은 데이터베이스 크기, 속도, 사용 가능한 대역폭, 네트워크의 대기 시간, 저장소 속도 등의 다양한 요소에 따라 달라짐).

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 이동 작업을 수행하려면 데이터베이스를 일시적으로 분리하여 모든 사용자가 액세스할 수 없도록 해야 합니다. 현재 데이터베이스가 분리된 경우 완료 시 다시 탑재되지 않습니다.

  - 이동 작업을 수행하려면 모든 복사본에 대해 데이터베이스의 복제를 비활성화해야 합니다. 복제를 일시 중단하는 것으로는 충분하지 않습니다. 데이터베이스 복사본을 제거하는 [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335119\(v=exchg.150\)) cmdlet을 사용하여 복제를 비활성화해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 복제된 사서함 데이터베이스를 새 경로로 이동


> [!NOTE]
> EAC를 사용하여 복제된 사서함 데이터베이스를 새 경로로 이동할 수는 없습니다.



1.  사서함 데이터베이스의 모든 복사본에 대한 재생 지연 또는 자르기 지연 설정도 이동된다는 점에 주의하십시오. 다음 예에 나오는 대로, [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\)) cmdlet을 사용하여 이 정보를 가져올 수 있습니다.
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  데이터베이스에서 순환 로깅을 사용하도록 설정되어 있을 경우 단계를 진행하기 전에 이 설정을 해제합니다. 다음 예에 나오는 대로, [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\)) cmdlet을 사용하여 사서함 데이터베이스에 대한 순환 로깅을 사용하지 않도록 설정할 수 있습니다.
    
    ```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $false
```

3.  이동할 데이터베이스의 사서함 데이터베이스 복사본을 모두 제거합니다. 자세한 단계는 [사서함 데이터베이스 복사본을 제거 합니다.](remove-a-mailbox-database-copy-exchange-2013-help.md)를 참조하십시오. 모든 복사본을 제거한 후 이들 복사본을 다른 위치로 이동하여 데이터베이스 복사본이 제거되는 각 서버로부터 데이터베이스 및 트랜잭션 로그 파일을 보존합니다. 이 파일을 보존하는 이유는 데이터베이스 복사본을 다시 추가한 후 다시 시드할 필요가 없도록 하기 위해서입니다.

4.  사서함 데이터베이스 경로를 새 위치로 이동합니다. 자세한 단계는 [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.
    

    > [!IMPORTANT]
    > 이동 작업이 수행되는 동안, 이동 중인 데이터베이스를 분리해야 합니다. 이동이 완료될 때까지 이동 중인 데이터베이스에 사서함이 있는 모든 사용자는 서비스 중단을 겪게 됩니다. 이동 작업이 완료되면 데이터베이스가 자동으로 탑재됩니다.



5.  이동한 사서함 데이터베이스의 수동 복사본을 포함하고 있었던 각 사서함 서버에 필요한 폴더 구조를 만듭니다. 예를 들어 데이터베이스를 C:\\mountpoints\\DB1로 이동했으면 사서함 데이터베이스 복사본을 호스트할 각 사서함 서버에 이와 동일한 경로를 만들어야 합니다.

6.  폴더 구조를 만든 후 사서함 데이터베이스의 수동 복사본과 로그 스트림을 새 위치로 이동합니다. 이는 3단계에서 제거하고 보존한 파일입니다. 3단계에서 제거된 데이터베이스 복사본마다 이 프로세스를 반복합니다.

7.  3단계에서 제거했던 데이터베이스 복사본을 모두 추가합니다. 자세한 단계는 [사서함 데이터베이스 복사본을 추가 합니다.](add-a-mailbox-database-copy-exchange-2013-help.md)를 참조하십시오.

8.  이동 중인 사서함 데이터베이스의 복사본을 포함하는 각 서버에서 다음 명령을 실행하여 콘텐츠 인덱스 서비스를 중지했다가 다시 시작합니다.
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  필요에 따라 다음 예에 나오는 대로, [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\)) cmdlet을 사용하여 순환 로깅을 사용하도록 설정합니다.
    
    ```powershell
Set-MailboxDatabase DB1 -CircularLoggingEnabled $true
```

10. 다음 예에 나오는 대로, [Set-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298104\(v=exchg.150\)) cmdlet을 사용하여 이전에 재생 지연 시간 및 자르기 지연 시간에 설정했던 값을 다시 구성합니다.
    
    ```powershell
Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00
```

11. 각 복사본을 추가할 때 다음 복사본을 추가하기 전에 해당 복사본의 상태를 확인하는 것이 좋습니다. 다음과 같은 방법으로 상태를 확인할 수 있습니다.
    
    1.  데이터베이스 또는 데이터베이스 복사본과 관련된 오류나 경고 이벤트에 대한 이벤트 로그를 검사합니다.
    
    2.  [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\)) cmdlet을 사용하여 데이터베이스 복사본에 대한 연속 복제의 상태를 확인합니다.
    
    3.  [Test-ReplicationHealth](https://technet.microsoft.com/ko-kr/library/bb691314\(v=exchg.150\)) cmdlet을 사용하여 데이터베이스 가용성 그룹 및 연속 복제의 상태를 확인합니다.

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/ko-kr/library/bb691314\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본의 경로가 성공적으로 이동했는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **서버** \> **데이터베이스**로 이동합니다. 복사된 데이터베이스를 선택합니다. 세부 정보 창에 데이터베이스 복사본의 상태 및 해당 콘텐츠 인덱스와 함께 현재 복사 큐 길이가 표시됩니다. 상태가 정상인지 확인합니다.

  - 셸에서 다음 명령을 실행하여 사서함 데이터베이스 복사본이 작성되어 있고 정상 상태인지 확인합니다.
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
```
    
    상태 및 콘텐츠 인덱스 상태가 모두 정상이어야 합니다.

