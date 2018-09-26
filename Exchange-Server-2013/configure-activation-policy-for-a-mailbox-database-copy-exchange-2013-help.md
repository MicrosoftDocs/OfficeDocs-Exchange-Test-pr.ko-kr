---
title: '사서함 데이터베이스 복사본에 대 한 정품 인증 정책 구성: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본에 대 한 정품 인증 정책 구성
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 50483387
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본에 대 한 정품 인증 정책 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-02_

*정품 인증*은 사서함 데이터베이스 복사본을 수동 복사본에서 활성 복사본으로 변경하는 프로세스입니다. 정품 인증은 데이터베이스나 서버 장애 조치(failover) 작업의 일부로서 시스템에서 자동으로 발생하며, 데이터베이스나 서버 전환 작업의 일부로 관리자가 수동으로 수행할 수도 있습니다. 정품 인증을 위해 데이터베이스를 차단하면 데이터베이스 또는 서버 장애 조치(failover) 중 활성 복사본이 되지 않습니다.

사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 데이터베이스 복사본에 대한 활성화 정책 구성

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  구성할 데이터베이스를 선택합니다.

3.  세부 정보 창의 **데이터베이스 복사본**에서 구성할 데이터베이스 복사본을 찾고 **일시 중단**을 클릭합니다.

4.  선택적으로 설명을 추가하고 <strong>이 복사본은 수동 작업으로만 활성화할 수 있습니다.</strong>라는 확인란을 선택합니다.

5.  **저장**을 클릭하여 사서함 데이터베이스 복사본에 대한 구성 변경 내용을 저장합니다.

## 셸을 사용하여 정품 인증을 위해 데이터베이스 복사본 일시 중단 또는 다시 시작

이 예에서는 정품 인증을 위해 서버 MBX2에서 데이터베이스 DB1의 복사본을 차단합니다.

```powershell
Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly
```

이 예에서는 정품 인증을 위해 서버 MBX2에서 데이터베이스 DB1의 복사본을 다시 시작합니다.

```powershell
Resume-MailboxDatabaseCopy -Identity DB1\MBX2
```

구문과 매개 변수에 대한 자세한 내용은 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)) 또는 [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335220\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 서버에 대한 정품 인증 정책 구성

이 예에서는 정품 인증을 위해 MBX2 서버에서 데이터베이스 복사본을 차단된 상태로 구성합니다.

```powershell
Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked
```

이 예에서는 사이트 외부 정품 인증을 위해 MBX3 서버에서 데이터베이스 복사본을 차단된 상태로 구성합니다.

```powershell
Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly
```

이 예에서는 정품 인증을 위해 MBX4 서버에서 데이터베이스 복사본을 차단 해제된 상태로 구성합니다.

```powershell
Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted
```

구문과 매개 변수에 대한 자세한 내용은 [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd351074\(v=exchg.150\)), [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/ko-kr/library/dd335220\(v=exchg.150\)) 또는 [Set-MailboxServer](https://technet.microsoft.com/ko-kr/library/aa998651\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

활성화 정책이 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

  - 셸에서 다음 명령을 실행하여 데이터베이스 복사본에 대한 정품 인증 설정을 확인합니다.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended
    ```

  - 셸에서 다음 명령을 실행하여 DAG 구성원에 대한 정품 인증 설정을 확인합니다.
    
    ```powershell
    Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy
    ```