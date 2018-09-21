---
title: '발신음 복구 수행: Exchange 2013 Help'
TOCTitle: 발신음 복구 수행
ms:assetid: 158817fa-4b17-4fa9-8341-a86609e6a388
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd979810(v=EXCHG.150)
ms:contentKeyID: 51407668
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 발신음 복구 수행

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-06-27_

발신음 이식성을 사용하면 사용자의 원래 사서함이 복원 또는 복구되는 동안 전자 메일을 보내고 받을 수 있는 임시 사서함을 사용할 수 있습니다. 임시 사서함은 조직 내에서 같은 Exchange 2013 사서함 서버나 다른 Exchange 2013 사서함 서버에 위치할 수 있습니다. 발신음 이식성을 사용하기 위한 과정을 발신음 복구라고 하며, 여기에는 오류가 발생한 데이터베이스를 대체하기 위해 사서함 서버에 빈 데이터베이스를 만드는 작업이 포함됩니다. 자세한 내용은 [발신음 이식성](dial-tone-portability-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 + 데이터 복원 및 이동에 소요되는 시간

  - 발신음 데이터베이스를 만들려면 배포된 데이터베이스의 수가 지원되는 최대 수보다 적어야 합니다. Exchange 2013 Standard Edition은 서버당 최대 5개의 데이터베이스를 지원하고, Exchange 2013 Enterprise Edition은 RTM 및 CU1에서 서버당 최대 50대의 데이터베이스를 지원하며 CU2 이상에서는 서버당 최대 100대의 데이터베이스를 지원합니다.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 복구" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 단일 서버에서 발신음 복구 수행


> [!NOTE]
> EMC를 사용하여 단일 서버에서 발신음 복구를 수행할 수는 없습니다.



1.  복구될 데이터베이스의 기존 파일은 나중에 추가 복구 작업에 필요할 경우에 대비하여 보존해야 합니다.

2.  다음 예에서와 같이, [New-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/aa997976\(v=exchg.150\)) cmdlet을 사용하여 발신음 데이터베이스를 만듭니다.
    
    ```powershell
New-MailboxDatabase -Name DTDB1 -EdbFilePath D:\DialTone\DTDB1.EDB
```

3.  다음 예에서와 같이, [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet을 사용하여 복구될 데이터베이스에서 호스트되는 사용자 사서함을 상주시킵니다.
    
    ```powershell
Get-Mailbox -Database DB1 | Set-Mailbox -Database DTDB1
```

4.  다음 예에서와 같이, [Mount-Database](https://technet.microsoft.com/ko-kr/library/aa998871\(v=exchg.150\)) cmdlet을 사용하여 클라이언트 컴퓨터가 데이터베이스에 액세스하고 메시지를 주고 받을 수 있도록 데이터베이스를 마운트합니다.
    
    ```powershell
Mount-Database -Identity DTDB1
```

5.  RDB(복구 데이터베이스)를 만들고 RDB로 복구할 데이터가 포함된 데이터베이스 및 로그 파일을 복원 또는 복사합니다. 자세한 단계는 [복구 데이터베이스 만들기](create-a-recovery-database-exchange-2013-help.md)를 참조하십시오.

6.  데이터가 RDB로 복사된 다음 복원된 데이터베이스를 탑재하기 전에, 복원된 데이터베이스에 대해 재생될 수 있도록 오류가 발생한 데이터베이스의 로그 파일을 복구 데이터베이스 로그 폴더로 복사합니다.

7.  다음 예에서와 같이, RDB를 탑재한 다음 [Dismount-Database](https://technet.microsoft.com/ko-kr/library/bb124936\(v=exchg.150\)) cmdlet을 사용하여 이를 분리합니다.
    
    ```powershell
Mount-Database -Identity RDB1
```
        Dismount-Database -Identity RDB1

8.  RDB가 분리되면 현재 데이터베이스와 RDB 폴더의 로그 파일을 안전한 위치로 이동합니다. 이로써 복구된 데이터베이스를 발신음 데이터베이스로 교체하기 위한 준비 단계가 끝났습니다.

9.  다음 예에서와 같이 발신음 데이터베이스를 분리합니다. 이 데이터베이스를 분리할 때 최종 사용자가 서비스 중단을 겪게 된다는 점에 유의하십시오.
    
    ```powershell
Dismount-Database -Identity DTDB1
```

10. 데이터베이스 및 발신음 데이터베이스 폴더의 로그 파일을 RDB 폴더로 이동합니다.

11. 다음 예에서와 같이, 복구된 데이터베이스가 있는 안전한 위치에서 데이터베이스와 로그 파일을 발신음 데이터베이스 폴더로 이동한 다음 데이터베이스를 탑재합니다.
    
    ```powershell
Mount-Database -Identity DTDB1
```
    
    이제 최종 사용자에 대해 중단되었던 서비스가 재개됩니다. 최종 사용자는 원래 프로덕션 데이터베이스에 액세스하고 메시지를 주고 받을 수 있습니다.

12. 다음 예에서와 같이 RDB를 탑재합니다.
    
    ```powershell
Mount-Database -Identity RDB1
```

13. 다음 예에서와 같이, [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 및 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\)) cmdlet을 사용하여 RDB에서 데이터를 내보내고 복구된 데이터베이스로 가져옵니다. 이렇게 하면 발신음 데이터베이스를 사용하여 주고 받은 모든 메시지를 프로덕션 데이터베이스로 가져옵니다.

    ```
```powershell
$mailboxes = Get-Mailbox -Database DTDB1
```
    ```

    ```
    $mailboxes | %{ New-MailboxRestoreRequest -SourceStoreMailbox $_.ExchangeGuid -SourceDatabase RDB1 -TargetMailbox $_ }
    ```

14. 복원 작업이 완료되면 다음 예에서와 같이 RDB를 분리하고 제거합니다.
    
        Dismount-Database -Identity RDB1
        Remove-MailboxDatabase -Identity RDB1

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [New-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/aa997976\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))

  - [Mount-Database](https://technet.microsoft.com/ko-kr/library/aa998871\(v=exchg.150\))

  - [Dismount-Database](https://technet.microsoft.com/ko-kr/library/bb124936\(v=exchg.150\))

  - [Remove-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/aa997931\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

사서함이 이동되었는지 확인하려면 다음을 수행합니다.

  - Microsoft Office Outlook Web App을 사용하여 사서함을 엽니다.

  - Microsoft Outlook을 사용하여 사서함을 엽니다.

