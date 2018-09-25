---
title: '일시 삭제 된 사서함 복원: Exchange 2013 Help'
TOCTitle: 일시 삭제 된 사서함 복원
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50555989
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 일시 삭제 된 사서함 복원

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-29_

셸을 사용하여 일시 삭제된 사서함을 Active Directory 사용자 계정에 연결 사서함을 다른 사서함 데이터베이스로 이동하면 이 사서함은 원본 사서함 데이터베이스에서 *일시 삭제*됩니다. Exchange는 이동이 완료되더라도 원본 사서함 데이터베이스에서 사서함을 완전히 삭제하지 않습니다. 대신, 원본 사서함 데이터베이스의 사서함이 일시 삭제 상태로 전환됩니다. 따라서 대상 데이터베이스의 사서함에 오류나 손상을 일으키는 문제가 이동 중에 발생할 경우 원본 사서함을 복원할 수 있습니다. 이러한 경우 원본 사서함을 복원하고 다시 이동을 수행할 수 있습니다.

일시 삭제된 사서함은 삭제된 사서함 보존 기간이 만료되거나 **Remove-StoreMailbox** cmdlet을 사용하여 일시 삭제된 사서함을 제거할 때까지 원본 데이터베이스에 보존됩니다. 일시 삭제된 사서함이 Exchange 사서함 데이터베이스에서 영구적으로 삭제되기 전에는 셸을 사용하여 일시 삭제된 사서함의 내용을 기존 사서함 또는 보관 사서함에 복원할 수 있습니다.

일시 삭제된 사서함에 대한 자세한 정보를 보고 다른 관련 관리 작업을 수행하려면 다음 항목을 참조하십시오.

  - [연결이 끊어진 사서함](disconnected-mailboxes-exchange-2013-help.md)

  - [삭제 된 사서함을 복원 또는 연결](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [사서함 복원 요청 관리](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션.

  - 이 항목의 프로시저만 셸에서 수행할 수 있습니다. 일시 삭제된 사서함을 복원하는 데 EAC를 사용할 수 없습니다.

  - 다음 명령을 실행하여 사용자 계정을 연결할 일시 삭제된 사서함이 사서함 데이터베이스에 그대로 있고 사용하지 않는 사서함이 아님을 확인합니다.
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    ```
    
    일시 삭제된 사서함은 사서함 데이터베이스에 있어야 하고 *DisconnectReason* 속성의 값은 `SoftDeleted`여야 합니다. 사서함이 데이터베이스에서 제거된 경우 명령은 결과를 반환하지 않습니다.
    
    또는 다음 명령을 실행하여 조직의 일시 삭제된 사서함을 모두 표시합니다.
    
    ```powershell
    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate
    ```
  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

  - 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## 셸을 사용하여 일시 삭제된 사서함 복원

셸에서 **New-MailboxRestoreRequest** cmdlet을 사용하여 일시 삭제된 사서함을 기존 사서함에 복원할 수 있습니다. 일시 삭제된 사서함을 복원할 경우 사서함의 내용이 *대상 사서함*이라는 기존 사서함에 복사됩니다. 사서함 복원 요청이 성공적으로 완료되면 요청은 30일(기본값) 동안 보존된 후 제거됩니다. **Remove-MailboxRestoreRequest** cmdlet을 사용하면 더 빨리 제거할 수 있습니다.

일시 삭제된 사서함이 복원된 후 해당 사서함은 관리자가 영구적으로 삭제하거나 삭제된 사서함 보존 기간이 만료되어 제거될 때까지 사서함 데이터베이스에 보존됩니다.

사서함 복원 요청을 만들려면 일시 삭제된 사서함의 표시 이름, 사서함 GUID 또는 레거시 DN(고유 이름)을 사용해야 합니다. **Get-MailboxStatistics** cmdlet을 사용하여 복원할 일시 삭제된 사서함에 대한 **DisplayName**, **MailboxGuid** 및 **LegacyDN** 속성의 값을 표시합니다. 예를 들면, 다음 명령을 사용하여 조직에서 사용하지 않는 사서함과 일시 삭제된 사서함 모두에 대해 이 정보를 반환합니다.

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database
```

이 예에서는 *SourceStoreMailbox* 매개 변수에서 표시 이름으로 식별되고 MBXDB01 사서함 데이터베이스에 있는 일시 삭제된 사서함을 Debra Garcia라는 대상 사서함에 복원합니다. *AllowLegacyDNMismatch* 매개 변수는 원본 사서함이 일시 삭제된 사서함과 동일한 레거시 DN 값을 갖지 않는 사서함에 복원될 수 있도록 하기 위해 사용됩니다.

```powershell
New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch
```

이 예에서는 Pilar Pinilla의 일시 삭제된 보관 사서함(사서함 GUID로 식별됨)을 현재 보관 사서함에 복원합니다. 기본 사서함과 해당 보관 사서함이 동일한 레거시 DN을 가지므로 *AllowLegacyDNMismatch* 매개 변수는 필요하지 않습니다.

```powershell
New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive
```

구문과 매개 변수에 대한 자세한 내용은 [New-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829875\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

일시 삭제된 사서함이 대상 사서함에 성공적으로 복원되었는지 확인하려면 **Get-MailboxRestoreRequest** cmdlet 또는 **Get-MailboxRestoreRequestStatistics** cmdlet을 실행하여 복원 요청에 대한 정보를 표시하십시오. 복원 요청이 성공적으로 만들어졌으면 *Status* 속성이 **Queued**, **InProgress** 또는 **Completed** 값을 갖게 됩니다. 복원 요청이 완료되면 일시 삭제된 사서함의 내용이 대상 사서함에 표시됩니다.

자세한 내용은 다음을 참조하십시오.

  - [사서함 복원 요청 관리](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ko-kr/library/ff829912\(v=exchg.150\))

