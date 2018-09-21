---
title: '사서함 데이터베이스 복사본을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본을 제거 합니다.
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 50483733
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본을 제거 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-06_

이 절차에서는 사서함 데이터베이스 복사본을 제거하는 방법을 보여 줍니다. 이 절차를 따라 사서함 데이터베이스의 마지막 복사본을 제거할 수는 없습니다. 사서함 데이터베이스의 마지막 복사본을 제거하는 방법에 대한 자세한 내용은 [Remove a mailbox database](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) 또는 [Remove-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/aa997931\(v=exchg.150\)) 항목을 참조하십시오.

사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 사서함 데이터베이스 복사본은 정상적인 DAG(데이터베이스 가용성 그룹)에서만 제거할 수 있습니다. DAG가 정상이 아니면(예: 쿼럼이 손실되어 DAG의 기본 클러스터가 작동 중지된 경우) 사서함 데이터베이스 복사본을 제거할 수 없습니다.

  - 데이터베이스의 마지막 수동 복사본을 제거하는 경우 지정된 사서함 데이터베이스에 대해 CRCL(연속 복제 순환 로깅)을 설정하지 않아야 합니다. CRCL이 사용하도록 설정된 경우 먼저 사용하지 않도록 설정해야 합니다. 사서함 데이터베이스 복사본을 제거한 후 순환 로깅을 사용하도록 설정할 수 있습니다. 복제되지 않은 사서함 데이터베이스에 대해 JET 순환 로깅을 사용하도록 설정하면 CRCL 대신 JET 순환 로깅이 사용됩니다. 데이터베이스의 마지막 수동 복사본을 제거하는 경우 CRCL을 사용할 수 있게 설정한 상태로 둘 수 있습니다.

  - 데이터베이스 복사본을 제거한 후에는 데이터베이스 복사본을 제거하고 있는 서버에서 모든 데이터베이스 및 트랜잭션 로그 파일을 수동으로 삭제해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 데이터베이스 복사본 제거

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  복사본을 제거할 사서함 데이터베이스를 선택합니다.

3.  세부 정보 창에서 제거할 수동 복사본을 선택한 다음 **제거**를 클릭합니다.

4.  경고 대화 상자에서 **예**를 클릭하여 제거를 확인합니다.

5.  모든 메시지를 검토한 후 **확인**을 클릭하여 제거를 확인합니다.

6.  데이터베이스 복사본을 제거 중인 서버에서 모든 데이터베이스 및 트랜잭션 로그 파일을 수동으로 삭제합니다.

## 셸을 사용하여 사서함 데이터베이스 복사본 제거

이 예에서는 사서함 서버 MBX1에서 사서함 데이터베이스 DB1의 복사본을 제거합니다.

```powershell
Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False
```

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본이 제거되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **서버** \> **데이터베이스**로 이동합니다. 해당 데이터베이스를 선택하면 제거된 수동 복사본이 더 이상 세부 정보 창에 나열되지 않습니다.

  - 셸에서 다음 명령을 실행하여 복사본이 제거되었는지 확인합니다.
    
    ```powershell
Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
```
    
    제거된 수동 복사본이 더 이상 나열되지 않습니다.

