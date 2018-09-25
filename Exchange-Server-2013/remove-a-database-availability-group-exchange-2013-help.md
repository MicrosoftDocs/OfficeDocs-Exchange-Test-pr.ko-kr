---
title: '데이터베이스 가용성 그룹을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 데이터베이스 가용성 그룹을 제거 합니다.
ms:assetid: 071296e9-31b0-40f4-9a02-177d97486ebd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335069(v=EXCHG.150)
ms:contentKeyID: 50482426
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 가용성 그룹을 제거 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-16_

DAG(데이터베이스 가용성 그룹) 제거는 빠르고 쉬운 작업입니다. EAC 또는 셸을 사용하여 DAG를 제거할 수 있습니다.

DAG와 관련된 다른 관리 작업에 대한 자세한 내용은 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [높은 가용성 및 사이트 복원 력 사용 권한](high-availability-and-site-resilience-permissions-exchange-2013-help.md)의 "데이터베이스 가용성 그룹" 항목

  - DAG가 비어 있어야 DAG를 제거할 수 있습니다. 제거하려는 DAG에 사서함 서버가 포함되어 있는 경우 먼저 DAG에서 이러한 서버를 제거해야 합니다. DAG에서 사서함 서버를 제거하는 방법에 대한 자세한 단계는 [데이터베이스 가용성 그룹 구성원 관리](manage-database-availability-group-membership-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 데이터베이스 가용성 그룹 제거

1.  **서버** \> **데이터베이스 가용성 그룹**으로 이동합니다.

2.  제거하려는 DAG를 선택하고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

3.  **예**를 클릭하여 경고를 확인하고 DAG를 제거합니다.

## 셸을 사용하여 데이터베이스 가용성 그룹 제거

이 예에서는 DAG1이라는 DAG를 제거합니다.

```powershell
Remove-DatabaseAvailabilityGroup -Identity DAG1
```

## 작동 여부는 어떻게 확인합니까?

DAG가 성공적으로 제거되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서 **서버** \> **데이터베이스 사용 가능 그룹**으로 이동하여 DAG가 아직도 표시되는지 확인합니다.

  - 셸에서 다음 명령을 실행하여 DAG가 여전히 존재하는지 확인합니다.
    
    ```powershell
    Get-DatabaseAvailabilityGroup <DAGName>
    ```
    
    DAG가 성공적으로 삭제된 경우 위의 명령을 실행하면 개체를 찾을 수 없다는 오류 메시지가 나타납니다.

