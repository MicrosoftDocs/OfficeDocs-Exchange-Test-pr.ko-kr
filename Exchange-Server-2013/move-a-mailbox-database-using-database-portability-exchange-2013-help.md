---
title: '데이터베이스 이식성을 사용하여 사서함 데이터베이스 이동: Exchange 2013 Help'
TOCTitle: 데이터베이스 이식성을 사용하여 사서함 데이터베이스 이동
ms:assetid: a765ead1-43bc-4786-ae93-1835cacfc8fc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876926(v=EXCHG.150)
ms:contentKeyID: 51407727
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 이식성을 사용하여 사서함 데이터베이스 이동

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-06-16_

데이터베이스 이식성을 사용하여 같은 조직에 있는 Exchange Server 2013 사서함 서버 간에 Microsoft Exchange 2013 사서함 데이터베이스를 이동할 수 있습니다. 이 경우 일부 오류 시나리오에 대한 전체 복구 시간을 줄일 수 있습니다. 자세한 내용은 [데이터베이스 이식성](database-portability-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 + 데이터 복원, 데이터베이스 파일 이동 및 Active Directory 복제 완료 대기에 소요되는 시간

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 복구" 항목

  - EAC를 사용하여 데이터베이스 이식성을 통해 복구된 데이터베이스 또는 발신음 데이터베이스로 사용자 사서함을 이동할 수는 없습니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 데이터베이스 이식성을 통해 복구된 데이터베이스 또는 발신음 데이터베이스로 사용자 사서함 이동

1.  데이터베이스가 완전한 종료 상태로 전환되었는지 확인합니다. 데이터베이스가 완전한 종료 상태가 아니면 소프트 복구를 수행합니다.
    

    > [!NOTE]
    > 소프트 복구를 수행하면 커밋되지 않은 로그 파일이 모두 데이터베이스로 커밋됩니다. 필요한 로그 파일 중 일부가 없는 경우에는 소프트 복구 프로세스를 완료할 수 없습니다. 2단계를 계속 진행합니다.

    
    커밋되지 않은 로그 파일을 모두 데이터베이스로 커밋하려면 명령 프롬프트에서 다음 명령을 실행합니다.
    
    ```powershell
ESEUTIL /R <Enn>
```
    

    > [!NOTE]
    > &lt;E<EM>nn</EM>&gt;은 로그 파일을 재생할 데이터베이스의 로그 파일 접두사를 지정합니다. &lt;E<EM>nn</EM>&gt;을 사용하여 지정한 로그 파일 접두사는 Eseutil /r의 필수 매개 변수입니다.



2.  다음 구문을 사용하여 서버에 데이터베이스를 만듭니다.
    
        New-MailboxDatabase -Name <DatabaseName> -Server <ServerName> -EdbFilePath <DatabaseFileNameandPath> -LogFolderPath <LogFilesPath>

3.  다음 구문을 사용하여 *This database can be over written by restore* 특성을 설정합니다.
    
    ```powershell
Set-MailboxDatabase <DatabaseName> -AllowFileRestore $true
```

4.  위의 새 데이터베이스를 만들 때 원본 데이터베이스 파일(.edb 파일, 로그 파일 및 Exchange Search 카탈로그)을 지정한 데이터베이스 폴더로 이동합니다.

5.  다음 구문을 사용하여 데이터베이스를 탑재합니다.
    
    ```powershell
Mount-Database <DatabaseName>
```

6.  데이터베이스가 탑재된 후에는 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet을 사용하여 사용자 계정이 새 사서함 서버의 사서함을 가리키도록 계정 설정을 수정합니다. 이전 데이터베이스의 모든 사용자를 새 데이터베이스로 이동하려면 다음 구문을 사용합니다.
    
        Get-Mailbox -Database <SourceDatabase> |where {$_.ObjectClass -NotMatch '(SystemAttendantMailbox|ExOleDbSystemMailbox)'}| Set-Mailbox -Database <TargetDatabase>

7.  다음 구문을 사용하여 큐에 남아 있는 모든 메시지가 전달되도록 합니다.
    
    ```powershell
Get-Queue <QueueName> | Retry-Queue -Resubmit $true
```

Active Directory 복제가 완료되면 모든 사용자가 새 Exchange 서버의 사서함에 액세스할 수 있습니다. 대부분의 클라이언트는 자동 검색을 통해 리디렉션됩니다. Microsoft Office Outlook Web App 사용자도 자동으로 리디렉션됩니다.

## 작동 여부는 어떻게 확인합니까?

사서함이 이동되었는지 확인하려면 다음을 수행합니다.

  - Outlook Web App을 사용하여 사서함을 엽니다.

  - Microsoft Outlook을 사용하여 사서함을 엽니다.

