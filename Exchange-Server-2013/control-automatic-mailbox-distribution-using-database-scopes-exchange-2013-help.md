---
title: '데이터베이스 범위를 사용 하 여 자동 사서함 배포 제어: Exchange 2013 Help'
TOCTitle: 데이터베이스 범위를 사용 하 여 자동 사서함 배포 제어
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 50483636
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 범위를 사용 하 여 자동 사서함 배포 제어

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

자동 사서함 배포는 Microsoft Exchange Server 2013의 기능으로 데이터베이스를 명시적으로 지정하지 않는 경우 사서함 데이터베이스를 임의로 선택하여 새로운 또는 이동한 사서함을 저장합니다. 신참 관리자나 기술 지원 직원이 사서함이 만들어지는 사서함 데이터베이스를 몰라도 사서함을 만들 수 있도록 하는 경우에 유용한 기능입니다.

데이터베이스 관리 범위를 사용하여 자동 사서함 배포를 통해 선택할 수 있는 사서함 데이터베이스를 제어할 수 있습니다. 데이터베이스 범위를 관리자에게 적용하는 경우에는 관리자는 정의한 데이터베이스 범위와 일치하는 데이터베이스만 사용 가능합니다. 자동 사서함 배포는 현재 사용자의 컨텍스트를 사용하므로 관리자에게 적용되는 데이터베이스 범위로 제한됩니다.

자동 사서함 배포, 데이터베이스 범위 및 역할 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [자동 사서함 배포](automatic-mailbox-distribution-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

범위와 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 범위" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: 데이터베이스 범위 만들기

이 단계에서는 데이터베이스 범위에 포함하려는 데이터베이스를 지정합니다. 또한, 데이터베이스의 정적 목록을 지정할지 또는 지정한 조건과 일치하는 데이터베이스만을 포함하는 데이터베이스 필터를 만들지를 판단합니다.


> [!IMPORTANT]
> 데이터베이스 범위와 관련 된 역할 할당 Microsoft Exchange Server 2010 서비스 팩 1 (SP1)을 실행 하는 서버에 연결 하는 사용자 에게만 적용 됩니다 이상 또는 Exchange 2013 합니다. 데이터베이스 범위와 관련 된 역할 할당을 할당 된 사용자가 사전Exchange 2010 SP1 서버에 연결 하는 경우에 역할 할당 사용자에 게 적용 되지 않습니다 및 사용자 역할 할당에서 제공 하는 모든 권한을 부여 되지 않습니다.



## 데이터베이스 목록 범위 사용

이 범위에 포함되어야 하는 사서함 데이터베이스의 정적 목록을 정의하려는 경우에는 데이터베이스 목록을 사용합니다. 데이터베이스 목록 범위를 만들려면 다음 구문을 사용합니다.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

이 예에서는 데이터베이스 Database 1, Database 2 및 Database 3에만 적용되는 범위를 만듭니다.

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 데이터베이스 필터 범위 사용

지정한 조건과 일치하는 데이터베이스만을 포함하는 동적 데이터베이스 범위를 만들려는 경우에는 데이터베이스 필터를 사용합니다. 이는 데이터베이스 범위를 만들고 사서함 데이터베이스의 특정 설정을 확인할 수 있는 조직에 대해 표준 값을 정의한 후 해당 데이터베이스 범위를 관리하지 않으려는 경우에 유용할 수 있습니다.

필터링할 수 있는 데이터베이스 속성 목록은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

데이터베이스 필터 범위를 만들려면 다음 구문을 사용합니다.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

이 예에서는 데이터베이스의 **Name** 속성에 "ACCT"라는 문자열이 있는 모든 데이터베이스를 포함하는 범위를 만듭니다.

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))를 참조하십시오.

## 2단계: 관리 역할 할당에 데이터베이스 범위 추가

범위를 만든 후에는 이를 새로운 또는 기존 관리 역할 할당에 추가해야 합니다. 관리 역할 그룹을 사용하여 관리 권한을 제어하는 것이 좋습니다. 그러므로 이 단계의 예에서는 Accounting Administrator라는 역할 그룹 예를 사용합니다. 역할 그룹을 만드는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조하십시오.

해당 역할을 데이터베이스 범위의 역할 그룹에 할당한 후에는 역할 그룹 구성원만이 해당 범위에 포함되는 데이터베이스에서 사서함을 만들어서 이동할 수 있습니다.

역할 그룹에 할당할 수 있는 기본 제공 역할 목록은 [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)을 참조하십시오.

## 새 역할 할당 추가

역할 그룹을 만들어서 이에 역할을 추가해야 하는 경우에 이 절차를 사용합니다.

다음 구문을 사용하여 할당하려는 관리 역할과 새 역할 그룹 간에 역할 할당을 새로운 데이터베이스 범위를 통해 만듭니다.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

이 예에서는 Mail Recipient와 Mail Recipient Creation 역할 간에 역할 할당을 만들고 Accounting Databases 데이터베이스 범위를 이용하여 Accounting Administrators 역할 그룹을 만듭니다.

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 기존 역할 할당 수정

기존 역할 그룹이 있고 해당 역할 그룹과 새 데이터베이스를 적용하려는 역할 간에 이미 역할 할당이 있는 경우 이 절차를 사용합니다.

이 절차에서는 파이프라이닝을 사용합니다. 자세한 내용은 [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))을 참조하십시오.

다음 구문을 사용해서 기존 역할 그룹과 데이터베이스 범위를 적용하려는 관리 역할 간에 역할 할당을 수정할 수 있습니다.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

이 예에서는 Accounting Administrators 역할 그룹에 할당된 Mail Recipients 및 Mail Recipient Creation 역할에 Accounting Databases 데이터베이스 범위를 추가합니다.

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\)) 또는 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\))를 참조하십시오.

## 3단계: 역할 그룹에 구성원 추가(적용할 수 있는 경우)

역할 그룹에 구성원을 추가하는 경우 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> 이 역할 그룹에 구성원을 추가하여 사용자를 만들거나 사서함을 이동할 수 있는 데이터베이스에 대해 제한하는 경우 해당 구성원은 추가적인 사용 권한을 부여할 수 있는 다른 역할 그룹의 구성원이어서는 안 됩니다.



## 4단계: 역할 그룹에서 구성원 제거(적용할 수 있는 경우)

사서함을 만들거나 사서함을 이동할 수 있는 데이터베이스에 대해 제한하는 새 역할 그룹에 구성원을 추가하였고 그 구성원이 추가적인 사용 권한이 있는 다른 역할 그룹의 구성원인 경우에는 해당 구성원을 기존 역할 그룹에서 제거합니다. 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md) 항목을 참조하십시오.

