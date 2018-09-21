---
title: '사용자 또는 USG에서 역할을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 사용자 또는 USG에서 역할을 제거 합니다.
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 50484378
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 또는 USG에서 역할을 제거 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-02_

관리 역할 할당을 사용자 또는 유니버설 USG (보안 그룹)에 관리 역할을 할당합니다. 역할 할당을 제거 하는 경우 역할이 할당 된 사용자는 해당 역할에서 사용할 수 있는 cmdlet에 액세스할을 수 더이상 됩니다. Microsoft Exchange Server 2013 의 관리 역할 할당에 대 한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)을 참조 하십시오.

역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상이 절차를 완료 시간: 5 분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 할당" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 관리 역할 할당을 제거 합니다.

제거 하려는 역할 할당의 이름을 알고 있는 경우에 다음 구문을 사용 합니다.

```powershell
Remove-ManagementRoleAssignment <assignment name>
```

예, "계층 2 Help Desk 배정" 역할 할당을 제거 하려면 다음 명령을 사용 합니다.

```powershell
Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"
```

역할 할당의 이름을 모르는 경우에 다음 구문을 사용할 수 있습니다.

    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 

예: 사용자에서 편지 병합 받는 사람 일반 역할 할당을 제거 하려는 경우 davids, 다음 명령을 사용 합니다.

    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment

