---
title: '사서함 데이터베이스 복사본을 다시 시작 또는 일시 중단: Exchange 2013 Help'
TOCTitle: 사서함 데이터베이스 복사본을 다시 시작 또는 일시 중단
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 50483742
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 데이터베이스 복사본을 다시 시작 또는 일시 중단

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-11-02_

데이터베이스 복사본이 포함된 디스크에 대한 유지 관리 같은 다양한 이유로 데이터베이스 복사본을 일시 중단하거나 다시 시작해야 할 수도 있고, 재해 복구를 위해 개별 데이터베이스 복사본의 활성화를 일시 중단해야 할 수도 있습니다.

사서함 데이터베이스 복사본과 관련된 다른 관리 작업에 대한 자세한 내용은 [사서함 데이터베이스 복사본 관리](managing-mailbox-database-copies-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "사서함 데이터베이스 복사본" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사서함 데이터베이스 복사본 일시 중단

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  복사본을 일시 중단할 데이터베이스를 선택합니다.

3.  세부 정보 창의 **데이터베이스 복사본** 아래에서 일시 중단할 데이터베이스 복사본 아래에 있는 **일시 중단**을 클릭합니다.

4.  **설명** 필드에 일시 중단의 이유를 지정하는 설명(선택 사항)을 최대 512자로 추가합니다.

5.  데이터베이스 복사본의 자동 활성화를 일시 중단하려면 **이 복사본은 수동으로만 활성화할 수 있습니다.** 확인란을 선택합니다.

6.  **저장**을 클릭하여 데이터베이스 복사본을 일시 중단합니다.

## EAC를 사용하여 사서함 데이터베이스 복사본 다시 시작

1.  EAC에서 **서버** \> **데이터베이스**로 이동합니다.

2.  복사본을 다시 시작할 데이터베이스를 선택합니다.

3.  세부 정보 창의 **데이터베이스 복사본** 아래에서 다시 시작할 데이터베이스 복사본 아래에 있는 **다시 시작**을 클릭합니다.

4.  **예**를 클릭하여 데이터베이스 복사본을 다시 시작합니다.

## 셸을 사용하여 사서함 데이터베이스 복사 일시 중단

이 예에서는 서버 MBX1에서 호스트되는 데이터베이스 DB1의 복사본에 대해 연속 복제를 일시 중단합니다. 선택적인 설명도 지정되었습니다.

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False

이 예에서는 서버 MBX2에서 호스트되는 데이터베이스 DB2의 복사본에 대해 활성화를 일시 중단합니다.

    Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False

## 셸을 사용하여 사서함 데이터베이스 복사 다시 시작

이 예에서는 서버 MBX1에서 데이터베이스 DB1의 복사본을 다시 시작합니다.

    Resume-MailboxDatabaseCopy -Identity DB1\MBX1

이 예에서는 복제만을 위해 서버 MBX2에서 데이터베이스 DB2의 복사본을 다시 시작합니다.

    Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly

## 작동 여부는 어떻게 확인합니까?

사서함 데이터베이스 복사본을 성공적으로 일시 중단 또는 다시 시작했는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **서버** \> **데이터베이스**로 이동합니다. 적절한 데이터베이스를 선택하고 세부 정보 창에서 **세부 정보 보기**를 클릭하여 데이터베이스 복사 속성을 봅니다.

  - 셸에서 다음 명령을 실행하여 데이터베이스 복사본에 대한 상태 정보를 표시합니다.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

