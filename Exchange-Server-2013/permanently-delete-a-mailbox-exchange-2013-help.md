---
title: '사서함을 영구적으로 삭제: Exchange 2013 Help'
TOCTitle: 사서함을 영구적으로 삭제
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50556095
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함을 영구적으로 삭제

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-16_

활성 사서함 및 연결이 끊긴된 사서함을 영구적으로 삭제할 때 Exchange 사서함 데이터베이스에서 모든 사서함 내용을 비워집니다 하 고 데이터 손실은 영구적입니다. 활성 사서함을 영구적으로 삭제 하는 경우 연결 된 Active Directory 사용자 계정이 삭제 됩니다.

사서함을 영구적으로 삭제 하는 대신 연결을 끊으려면 것은입니다. 기본적으로는 사서함을 끊으면 30 일 동안 보존 사서함 데이터베이스에 됩니다. 이렇게 하면 기회를 다시 연결 하거나 데이터베이스에서 제거 되기 전에 사서함을 복원 합니다.

연결이 끊어진 사서함에 대해 자세히 알아보고 관련 관리 작업을 수행하려면 다음 항목을 참조하십시오.

  - [연결이 끊어진 사서함](disconnected-mailboxes-exchange-2013-help.md)

  - [사용 하지 않거나 사서함 삭제](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [비활성화 된 사서함에 연결](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [삭제 된 사서함을 복원 또는 연결](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)


> [!NOTE]
> EAC를 사용 하 여 활성 사서함이 있는 또는 연결이 끊긴된 사서함을 영구적으로 삭제 하려면 수는 없습니다.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 활성 사서함 영구 삭제

## 셸을 사용 하 여 활성 사서함을 영구적으로 삭제

활성 사서함과 관련된 된 Active Directory 사용자 계정 영구적으로 삭제 하려면 다음 명령을 실행 합니다.

```powershell
Remove-Mailbox -Identity <identity> -Permanent $true
```


> [!NOTE]
> <EM>Permanent</EM> 매개 변수를 포함 하지 않으면 하는 경우 삭제 된 사서함 전에 보존 되 사서함 데이터베이스에 30 일 동안 기본적으로 영구적으로 삭제 됩니다.



자세한 구문 및 매개 변수 정보에 대 한 [Remove-Mailbox](https://technet.microsoft.com/ko-kr/library/aa995948\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

활성 사서함을 영구적으로 삭제 했는지를 확인 하려면 다음을 수행 합니다.

1.  EAC에서 더이상 사서함이 나타나는지 확인 합니다.

2.  연결 된 사용자 계정을 Active Directory 사용자 및 컴퓨터에서 더이상 표시 되는지 확인 합니다.

3.  Exchange 사서함 데이터베이스에서 사서함을 제거 된 성공적으로 확인 하려면 다음 명령을 실행 합니다.
    
    ```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {         Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```
    
    사서함을 성공적으로 제거 하는 경우 명령은 모든 결과가 반환 되지 않습니다. 사서함 삭제 되지 않은 경우 명령은 사서함에 대 한 정보를 반환 합니다.

## 연결이 끊긴된 사서함을 영구적으로 삭제

## 셸을 사용하여 연결이 끊어진 사서함을 영구적으로 삭제

연결이 끊긴된 사서함의 두가지 유형이 있습니다: 사용 하지 않도록 설정 하 고 일시 삭제 합니다. 사서함을 영구적으로 삭제 하려면 cmdlet을 실행 하는 경우 이러한 형식 중 하나를 지정 해야 합니다. 형식을 지정 하는 연결이 끊어진된 사서함의 실제 유형과 일치 하지 않으면, 명령이 실패 합니다.

연결이 끊긴된 사서함 사용 하지 않도록 설정 되었거나 일시 삭제 여부를 확인 하려면 다음 명령을 실행 합니다.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

연결이 끊긴된 사서함에 대 한 *DisconnectReason* 속성에 대 한 값 중 하나 `Disabled` 또는 `SoftDeleted`됩니다.

조직에서 연결이 끊긴된 모든 사서함에 대 한 종류를 표시 하려면 다음 명령을 실행할 수 있습니다.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason

> [!CAUTION]
> <strong>Remove-StoreMailbox</strong> cmdlet을 사용 하 여 연결이 끊긴된 사서함을 영구적으로 삭제 사서함 데이터베이스에서 모든 내용을 비워집니다 하 고 데이터 손실은 영구적입니다.


이 예에서는 사서함 데이터베이스 MBD01에서 GUID가 2ab32ce3-fae1-4402-9489-c67e3ae173d3인 사용되지 않는 사서함을 영구적으로 삭제합니다.

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

이 예에서는 일시 삭제 된 사서함 Dan 점프에 대 한 사서함 데이터베이스 m b d 01에서에서 영구적으로 삭제합니다.

```powershell
Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted
```

이 예에서는 사서함 데이터베이스 MBD01에서 일시 삭제된 모든 사서함을 영구적으로 삭제합니다.

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

구문과 매개 변수에 대한 자세한 내용은 [Remove-StoreMailbox](https://technet.microsoft.com/ko-kr/library/ff829913\(v=exchg.150\)) 및 [Get-MailboxStatistics](https://technet.microsoft.com/ko-kr/library/bb124612\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

연결이 끊긴된 사서함을 영구적으로 삭제 했을 때 하 고 Exchange 사서함 데이터베이스에서 성공적으로 제거 된를 확인 하려면 다음 명령을 실행 합니다.

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {     Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```

사서함을 성공적으로 제거 하는 경우 명령은 모든 결과가 반환 되지 않습니다. 사서함 삭제 되지 않은 경우 명령은 사서함에 대 한 정보를 반환 합니다.

