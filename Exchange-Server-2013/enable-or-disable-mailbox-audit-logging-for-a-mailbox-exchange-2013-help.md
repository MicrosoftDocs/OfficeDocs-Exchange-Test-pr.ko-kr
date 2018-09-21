---
title: '사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용
ms:assetid: c4bbfd52-6196-49c7-8c31-777fbbee11f2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff461937(v=EXCHG.150)
ms:contentKeyID: 50484108
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-09-30_

사서함 감사 로깅을 사용하여 사서함 로그온과 사용자가 로그온한 상태에서 수행한 작업을 추적할 수 있습니다. 사서함에 대해 사서함 감사 로깅을 사용하도록 설정하면 기본적으로 관리자와 대리인이 수행한 일부 작업이 기록됩니다. 사서함 소유자가 수행한 작업은 기록되지 않습니다. 사서함 감사 로깅에 대한 자세한 내용은 [사서함 감사 로깅](mailbox-audit-logging-exchange-2013-help.md)를 참조하십시오.


> [!WARNING]
> 사서함 소유자 작업 감사는 많은 사서함 감사 로그 항목을 생성할 수 있으므로 기본적으로 사용하지 않도록 설정됩니다. 비즈니스 또는 보안 요구 사항을 충족하는 데 필요한 특정 소유자 작업 감사만 사용하도록 설정하는 것이 좋습니다.



사서함 감사 로깅과 관련된 추가 작업에 대한 자세한 내용은 [사서함 감사 로깅 절차](mailbox-audit-logging-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "사서함 감사 로깅" 항목

  - 사서함을 사용할지 여부를 Exchange 관리 센터 (EAC)를 사용할 수 없습니다 감사 로깅. 셸을 사용 해야 합니다.

  - 사용자의 사서함에 대해 모든 액세스 권한이 할당된 관리자는 대리인으로 간주됩니다.

  - 사서함은 관리자가 다음과 같은 경우에만 액세스할 수 있다고 간주 됩니다.
    
      - In-Place eDiscovery를 사용하여 사서함을 검색합니다.
    
      - **New-MailboxExportRequest** cmdlet을 사용하여 사서함을 내보냅니다.
    
      - Microsoft Exchange Server MAPI 편집기는 사서함에 액세스 하는데 사용 됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 사서함 감사 로깅을 사용하거나 사용하지 않도록 설정

셸을 사용하여 사서함에 대한 사서함 감사 로깅을 사용하거나 사용하지 않도록 설정할 수 있습니다. 이는 관리자, 대리인 및 사서함 소유자에게 지정된 모든 작업의 로깅을 사용하거나 사용하지 않도록 하는 설정입니다.

이 예에서는 Ben Smith의 사서함에 대해 사서함 감사 로깅을 사용하도록 설정합니다.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $true
```

이 예에서는 Ben Smith의 사서함에 대해 사서함 감사 로깅을 사용하지 않도록 설정합니다.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditEnabled $false
```

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 관리자, 대리인 및 소유자 액세스에 대한 사서함 감사 로깅 설정 구성

사서함에 대해 사서함 감사 로깅을 사용하는 경우 사서함의 감사 로깅 구성에 지정된 관리자, 대리인 및 소유자 작업만 로깅됩니다.

이 예에서는 위임된 사용자가 Ben Smith의 사서함에 대해 수행한 `SendAs` 또는 `SendOnBehalf` 작업이 기록되도록 지정합니다.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditDelegate SendAs,SendOnBehalf -AuditEnabled $true
```

이 예에서는 관리자가 Ben Smith의 사서함에 대해 수행한 `MessageBind` 및 `FolderBind` 작업이 기록되도록 지정합니다.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditAdmin MessageBind,FolderBind -AuditEnabled $true
```

이 예에서는 사서함 소유자가 Ben Smith의 사서함에 대해 수행한 `HardDelete` 작업이 기록되도록 지정합니다.

```powershell
Set-Mailbox -Identity "Ben Smith" -AuditOwner HardDelete -AuditEnabled $true
```

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함에 대한 사서함 감사 로깅을 사용하도록 설정하고 관리자, 대리인 또는 소유자 액세스에 대한 올바른 로깅 설정을 성공적으로 지정했는지 확인하려면 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) cmdlet을 사용하여 해당 사서함의 사서함 감사 로깅 설정을 검색합니다.

이 예에서는 Ben Smith의 사서함 설정을 검색하고 감사 로그 기간 제한을 비롯한 지정된 감사 설정을 **Format-List** cmdlet에 파이프합니다.

    Get-Mailbox "Ben Smith" | Format-List *audit*

