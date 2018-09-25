---
title: '역할 그룹 관리: Exchange 2013 Help'
TOCTitle: 역할 그룹 관리
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 50483845
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 그룹 관리

 

_<strong>적용 대상:</strong> Exchange Online, Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2012-10-08_

이 항목에서는 Microsoft Exchange Server 2013에서 관리 역할 그룹을 추가, 제거, 복사하고 보는 방법을 설명합니다. 또한 역할 그룹에서 관리 역할을 추가, 제거 및 나열하는 방법과 역할 그룹에서 관리 범위와 대리자를 변경하는 방법에 대해서도 설명합니다. Exchange 2013의 역할 그룹에 대한 자세한 내용은 [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)를 참조하십시오.

역할 그룹에 관련된 추가 관리 작업은 [사용 권한](permissions-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5~10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 그룹" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]   
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 역할 그룹 만들기

사용자 그룹에 할당할 수 있는 사용 권한을 사용자 지정하려는 경우 새 사용자 지정 관리 역할 그룹을 만들 수 있습니다.

## EAC를 사용하여 역할 그룹 만들기

1.  EAC(Exchange 관리 센터)에서 <strong>사용 권한</strong> \> <strong>관리자 역할</strong>로 이동한 다음 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  <strong>새 역할 그룹</strong> 창에서 새 역할 그룹의 이름을 제공합니다.

3.  지금 역할 그룹에 할당할 역할 및 역할 그룹에 추가할 구성원을 선택하거나, 나중에 이 작업을 수행할 수 있습니다.

4.  새 역할 그룹에 적용할 쓰기 범위를 선택합니다.

5.  <strong>저장</strong>을 클릭하여 역할 그룹을 만듭니다.

## 셸을 사용하여 역할 그룹 만들기

역할 그룹을 만들려면 [New-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638181\(v=exchg.150\))에서 [Examples](https://technet.microsoft.com/ko-kr/dd638181\(exchg.150\)#examples) 섹션을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹이 성공적으로 만들어졌는지 확인하려면 다음을 수행하십시오.

1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  새 역할 그룹이 역할 그룹 목록에 나타나는지 확인한 다음 해당 역할 그룹을 선택합니다.

3.  새 역할 그룹에 지정한 구성원, 할당된 역할, 범위가 역할 그룹 세부 정보 창에 표시되는지 확인합니다.

## 역할 그룹 복사

## EAC를 사용하여 역할 그룹 복사

사용자에게 부여할 사용 권한이 포함된 관리 역할 그룹을 보유하고 있지만 다른 관리 범위를 적용하려는 경우 또는 그 밖의 모든 역할을 수동으로 추가하지 않으면서 하나 또는 두 개의 관리 역할을 제거하거나 추가하려는 경우, 기존 역할 그룹을 복사할 수 있습니다.


> [!IMPORTANT]  
> Exchange 관리 셸을 사용하여 역할 그룹에서 다중 관리 역할 범위나 단독 범위를 구성한 경우에는 EAC를 사용하여 역할 그룹을 복사할 수 없습니다. 역할 그룹에 대해 여러 범위나 단독 범위를 구성한 경우에는 이 항목 후반부에 나오는 셸 프로시저를 사용하여 역할 그룹을 복사해야 합니다. 관리 역할 범위에 대한 자세한 내용은 <A href="understanding-management-role-scopes-exchange-2013-help.md">관리 역할 범위 이해 (영문)</A>를 참조하십시오.



1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  복사할 역할 그룹을 선택한 다음 <strong>복사</strong>![복사 아이콘](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "복사 아이콘")을 클릭합니다.

3.  <strong>새 역할 그룹</strong> 창에서 새 역할 그룹의 이름을 제공합니다.

4.  새 역할 그룹에 복사된 역할을 검토합니다. 필요에 따라 역할을 추가 또는 제거합니다.

5.  쓰기 범위를 검토하고 필요에 따라 변경합니다.

6.  새 역할 그룹에 복사된 구성원을 검토합니다. 필요에 따라 구성원을 추가 또는 제거합니다.

7.  <strong>저장</strong>을 클릭하여 역할 그룹을 만듭니다.

## 셸을 사용하여 범위 없는 역할 그룹 복사

1.  다음 구문을 사용하여 복사할 역할 그룹을 변수에 저장합니다.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  새 역할 그룹을 만든 후, 다음 구문을 사용하여 역할 그룹에 구성원을 추가하고 새 역할 그룹을 다른 사용자에게 위임할 수 있는 사용자를 지정합니다.
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>
    ```
예를 들어 다음 명령으로 Organization Management 역할 그룹을 복사하고 새 역할 그룹의 이름을 "Limited Organization Management"로 지정합니다. 이를 통해 Isabelle, Carter 및 Lukas라는 구성원이 추가되며 이는 Jenny 및 Katie에게서 위임될 수 있습니다.

```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie
```
새 역할 그룹을 만든 후, 역할을 추가 또는 제거하고 이 역할에 대한 역할 할당 범위를 변경하는 등의 작업을 수행할 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638115\(v=exchg.150\)) 및 [New-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638181\(v=exchg.150\))을 참조하십시오.

## 셸을 사용하여 사용자 지정 범위의 역할 그룹 복사

1.  다음 구문을 사용하여 복사할 역할 그룹을 변수에 저장합니다.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  다음 구문을 사용하여 사용자 지정 범위의 새 역할 그룹을 만듭니다.
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>
    ```

예를 들어 다음 명령으로 Organization Management 역할 그룹을 복사하고 Vancouver Users 받는 사람 범위와 Vancouver Servers 구성 범위의 Vancouver Organization Management라는 새 역할 그룹을 만듭니다.

```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"
```

이 항목의 전반부에 있는 Use the Shell to copy a role group with no scope에 표시된 것처럼 *Members* 매개 변수를 사용하여 그룹을 만드는 경우 역할 그룹에 구성원을 추가할 수도 있습니다. 관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

새 역할 그룹을 만든 후, 역할을 추가하거나 제거하고 이 역할에 대한 역할 할당 범위를 변경하며 그 외의 다른 작업을 수행할 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638115\(v=exchg.150\)) 및 [New-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638181\(v=exchg.150\))을 참조하십시오.

## 셸을 사용하여 OU 범위의 역할 그룹 복사

1.  다음 구문을 사용하여 복사할 역할 그룹을 변수에 저장합니다.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  다음 구문을 사용하여 사용자 지정 범위의 새 역할 그룹을 만듭니다.
    
    ```powershell
    New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>
    ```

예를 들어 다음 명령으로 Recipient Management 역할 그룹을 복사하고 Toronto Users OU의 사용자만 관리할 수 있도록 하는 Toronto Recipient Management라는 새 역할 그룹을 만듭니다.

```powershell
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"
```

이 항목의 전반부에 있는 Use the Shell to copy a role group with no scope에 표시된 것처럼 *Members* 매개 변수를 사용하여 그룹을 만드는 경우 역할 그룹에 구성원을 추가할 수도 있습니다. 관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

새 역할 그룹을 만든 후, 역할을 추가 또는 제거하고 이 역할에 대한 역할 할당 범위를 변경하는 등의 작업을 수행할 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638115\(v=exchg.150\)) 및 [New-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638181\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹이 성공적으로 복사되었는지 확인하려면 다음을 수행하십시오.

1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  복사된 역할 그룹이 역할 그룹 목록에 나타나는지 확인한 다음 해당 역할 그룹을 선택합니다.

3.  복사된 역할 그룹에 지정한 구성원, 할당된 역할, 범위가 역할 그룹 세부 정보 창에 표시되는지 확인합니다.

## 역할 그룹 제거

직접 만든 역할 그룹이 더 이상 필요하지 않은 경우 제거할 수 있습니다. 역할 그룹을 제거하면 역할 그룹과 관리 역할 사이의 관리 역할 할당이 삭제됩니다. 관리 역할은 삭제되지 않습니다. 역할 그룹을 통해 기능에 액세스하는 사용자는 더 이상 해당 기능에 액세스할 수 없습니다. 기본 제공 역할 그룹은 제거할 수 없습니다.

## EAC를 사용하여 역할 그룹 제거

1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  제거할 역할 그룹을 선택한 다음 <strong>삭제</strong>![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")을 클릭합니다.

3.  선택한 역할 그룹을 제거하려는 것이 확실하면 경고에 <strong>예</strong>로 응답합니다.

## 셸을 사용하여 역할 그룹 제거

역할 그룹을 제거하려면 [Remove-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638141\(v=exchg.150\))에서 [Examples](https://technet.microsoft.com/ko-kr/dd638141\(exchg.150\)#examples) 섹션을 참조하십시오.

## 역할 그룹 보기

조직의 역할 그룹 목록 또는 특정 역할 그룹에 대한 세부적인 정보를 볼 수 있습니다.

## EAC를 사용하여 역할 그룹 목록 및 역할 그룹 세부 정보 보기

1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다. 조직의 모든 역할 그룹이 여기에 나열됩니다.

2.  역할 그룹에 구성된 구성원, 할당된 역할, 범위를 보려면 역할 그룹을 선택합니다.

## 셸을 사용하여 역할 그룹 목록 및 역할 그룹 세부 정보 보기

역할 그룹의 목록을 보려면 [Get-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638115\(v=exchg.150\))에서 [Examples](https://technet.microsoft.com/ko-kr/dd638115\(exchg.150\)#examples) 섹션을 참조하십시오.

## 역할 그룹에 역할 추가

관리 역할을 역할 그룹에 추가하는 것은 관리자 또는 전문가 사용자 그룹에 사용 권한을 부여할 수 있는 가장 효과적이고도 간단한 방법입니다. 역할 그룹의 구성원인 사용자에게 기능 관리 권한을 부여하려면 기능을 관리하는 관리 역할을 해당 역할 그룹에 추가해야 합니다. 해당 역할이 추가되면 역할 그룹의 구성원에게는 해당 역할에서 제공한 사용 권한이 부여됩니다.

## EAC를 사용하여 관리 역할을 역할 그룹에 추가


> [!IMPORTANT]  
> 셸을 사용하여 역할 그룹에서 다중 관리 역할 범위나 단독 범위를 구성한 경우에는 EAC를 사용하여 역할 그룹에 역할을 추가할 수 없습니다. 여러 범위나 단독 범위를 역할 그룹에 구성한 경우 이 항목의 뒷부분에 나오는 셸 절차를 사용하여 역할을 역할 그룹에 추가해야 합니다. 관리 역할 범위에 대한 자세한 내용은 <A href="understanding-management-role-scopes-exchange-2013-help.md">관리 역할 범위 이해 (영문)</A>를 참조하십시오.



1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  역할을 추가할 역할 그룹을 선택한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  <strong>역할</strong> 섹션에서 역할 그룹에 추가할 역할을 선택합니다.

4.  역할 그룹에 역할을 추가했으면 <strong>저장</strong>을 클릭합니다.

## 셸을 사용하여 범위가 없는 역할 할당 만들기

범위가 없는 역할 할당 역할과 역할 그룹 간에 만들 수 있습니다. 이 때 역할의 암시적인 읽기 범위 및 암시적인 쓰기 범위가 적용됩니다.

역할 그룹에 범위 없는 역할을 할당하려면 다음 구문을 사용합니다. 역할 할당 이름은 지정하지 않은 경우 자동으로 만들어집니다.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>
```

이 예에서는 Seattle Compliance 역할 그룹에 Transport Rules 관리 역할을 할당합니다.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 미리 정의된 범위가 있는 역할 할당 만들기

미리 정의된 범위가 업무 요구 사항에 맞는 경우 새 범위를 만들지 않고 해당 범위를 역할 할당에 적용할 수 있습니다. 미리 정의된 범위와 그 설명에 대한 목록은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

미리 정의된 범위를 사용하여 역할 그룹에 역할을 할당하려면 다음 구문을 사용합니다. 역할 할당 이름은 지정하지 않은 경우 자동으로 만들어집니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >
```

이 예에서는 Enterprise Support 역할 그룹에 Message Tracking 역할을 할당하고 미리 정의된 범위 Organization을 적용합니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 받는 사람 필터 기반 범위가 있는 역할 할당 만들기

받는 사람 필터 기반 범위를 만든 경우 역할 그룹에 역할을 할당하는 데 사용되는 명령에 *CustomRecipientWriteScope* 매개 변수를 사용하여 범위를 포함해야 합니다.

또한 받는 사람 쓰기 범위가 있는 역할 할당을 만드는 경우 구성 쓰기 범위도 포함할 수 있습니다.

역할 할당 및 범위에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

받는 사람 필터 기반 범위를 사용하여 역할 그룹에 역할을 할당하려면 다음 구문을 사용합니다. 역할 할당 이름은 지정하지 않은 경우 자동으로 만들어집니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>
```
이 예에서는 Seattle Recipient Admins 역할 그룹에 Message Tracking 역할을 할당하고 Seattle Recipients 범위를 적용합니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 구성 범위가 있는 역할 할당 만들기

서버나 데이터베이스 구성 필터 또는 목록 기반 범위를 만든 경우, *CustomConfigWriteScope* 매개 변수를 사용하여 역할을 역할 그룹에 할당하는 데 사용되는 명령에 해당 범위를 포함해야 합니다.

또한 구성 쓰기 범위가 있는 역할 할당을 만드는 경우 받는 사람 쓰기 범위도 포함할 수 있습니다.

역할 할당 및 관리 범위에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

구성 범위를 사용하여 역할 그룹에 역할을 할당하려면 다음 구문을 사용합니다. 역할 할당 이름은 지정하지 않은 경우 자동으로 만들어집니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>
```
이 예에서는 Seattle Server Admins 역할 그룹에 Databases 역할을 할당하고 Seattle Servers 범위를 적용합니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"
```
구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 OU 범위가 있는 역할 할당 만들기

OU(조직 단위)에 역할의 쓰기 범위를 적용하려는 경우 *RecipientOrganizationalUnitScope* 매개 변수에 직접 OU를 지정할 수 있습니다.

역할 할당 및 관리 범위에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

역할 그룹에 역할을 할당하고 역할의 쓰기 범위를 특정 OU로 제한하려면 다음 명령을 사용합니다. 역할 할당 이름은 지정하지 않은 경우 자동으로 만들어집니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>
```

이 예에서는 Seattle Recipient Admins 역할 그룹에 Mail Recipients 역할을 할당하고 Contoso.com 도메인의 Sales\\Users OU에 할당 범위를 적용합니다.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users
```

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹에 역할이 성공적으로 추가되었는지 확인하려면 다음을 수행하십시오.

1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  역할을 추가한 역할 그룹을 선택합니다. 역할 그룹 세부 정보 창에서 추가한 역할이 표시되는지 확인합니다.

## 역할 그룹에서 역할 제거

관리 역할 그룹에서 역할을 제거하는 것은 관리자 또는 전문가 사용자 그룹에 부여된 권한을 해지할 수 있는 가장 효과적이고도 간단한 방법입니다. 관리자 또는 전문가 사용자에게 기능을 관리할 수 있는 권한을 부여하지 않으려면 해당 권한을 관리하는 관리 역할 그룹에서 관리 역할을 제거하십시오. 역할이 제거되면 역할 그룹의 구성원이 더 이상 기능을 관리할 수 있는 권한을 보유하지 않게 됩니다.


> [!NOTE]  
> 조직 관리 역할 그룹과 같은 일부 역할 그룹은 특정 역할 그룹에서 제거할 수 있는 역할을 제한합니다. 자세한 내용은 <A href="understanding-management-role-groups-exchange-2013-help.md">관리 역할 그룹 이해 (영문)</A>을 참조하십시오.<BR>관리자가 기능 관리 권한을 부여하는 관리 역할이 포함된 다른 역할 그룹의 구성원인 경우 다른 역할 그룹에서 관리자를 제거하거나 다른 역할 그룹에서 기능 관리 권한을 부여하는 역할을 제거하십시오.



## EAC를 사용하여 역할 그룹에서 관리 역할 제거


> [!IMPORTANT]  
> 셸을 사용하여 역할 그룹에서 다중 범위나 단독 범위를 구성한 경우에는 EAC를 사용하여 역할 그룹에서 역할을 제거할 수 없습니다. 여러 범위나 단독 범위를 역할 그룹에 구성한 경우 이 항목의 뒷부분에 나오는 셸 절차를 사용하여 역할을 역할 그룹에서 제거해야 합니다. 관리 역할 범위에 대한 자세한 내용은 <A href="understanding-management-role-scopes-exchange-2013-help.md">관리 역할 범위 이해 (영문)</A>를 참조하십시오.



1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  역할을 제거할 역할 그룹을 선택한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  <strong>역할</strong> 섹션에서 역할 그룹에서 제거할 역할을 선택합니다.

4.  역할 그룹에서 역할을 제거했으면 <strong>저장</strong>을 클릭합니다.

## 셸을 사용하여 역할 그룹에서 역할 제거

<strong>Get-ManagementRoleAssignment</strong> cmdlet을 사용하여 관련된 관리 역할 할당을 검색한 다음 <strong>Remove-ManagementRoleAssignment</strong> cmdlet에 반환된 역할 할당을 파이프하여 역할 그룹에서 역할을 제거할 수 있습니다. 위임과 일반 역할 할당을 동시에 제거하지 않으려면 *Delegating* 매개 변수를 지정하여 일반 역할 할당을 제거할지, 또는 위임 역할 할당을 제거할지를 지정합니다.

일반 및 위임 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

이 절차에서는 파이프라이닝을 사용합니다. 파이프라이닝에 대한 자세한 내용은 [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))을 참조하십시오.

역할 그룹에서 역할을 제거하려면 다음 구문을 사용합니다.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment
```

이 예에서는 Seattle Recipient Administrators 역할 그룹에서 관리자에게 메일 그룹을 관리하도록 허용하는 메일 그룹 역할을 제거합니다. 메일 그룹을 관리하는 권한을 부여하는 역할 할당을 제거할 것이므로 *Delegating* 매개 변수를 `$False`로 설정하여 일반 역할 할당만 반환되도록 합니다.

```powershell
   Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment
```

구문과 매개 변수에 대한 자세한 내용은 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351205\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹에서 역할이 성공적으로 제거되었는지 확인하려면 다음을 수행하십시오.

1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  역할을 제거한 역할 그룹을 선택합니다. 역할 그룹 세부 정보 창에서 제거한 역할이 더 이상 표시되지 않음을 확인합니다.

## 역할 그룹의 범위 변경

역할 그룹과 역할 간 관리 역할 할당에는 관리 범위가 포함되어 있는데, 이 범위에 따라 해당 역할 그룹의 구성원이 사용할 수 있는 개체가 결정됩니다. 역할 그룹에서 쓰기 범위를 변경하면 역할 그룹 구성원이 만들거나 변경하거나 제거할 수 있는 개체를 변경할 수 있습니다. 역할 그룹에서 읽기 범위를 변경할 수는 없습니다.

Exchange 2013에는 사용자 지정 범위가 만들어지지 않은 경우 역할 할당에 기본적으로 적용되는 범위가 포함됩니다. 역할 그룹에 대한 역할 할당이 포함된 사용자 지정 범위를 사용하려면 우선 범위를 하나 만들어야 합니다. 고급 작업인 사용자 지정 범위 만들기에 대한 자세한 내용은 [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)를 참조하십시오.

Exchange 2013의 관리 역할 범위 및 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

## EAC를 사용하여 역할 그룹에서 범위 변경

EAC를 사용하여 역할 그룹에서 범위를 변경하면 실제로는 역할 그룹과 그 역할 그룹에 할당되는 각 관리 역할 사이의 모든 역할 할당에 대한 범위가 변경됩니다. 특정 역할 할당에 대한 범위를 변경하려면 이 항목 후반부에 나오는 셸 프로시저를 사용해야 합니다.


> [!IMPORTANT]  
> 셸을 사용하여 역할 할당에 대해 다중 범위나 단독 범위를 구성한 경우에는 EAC를 사용하여 역할과 역할 그룹 사이에서 역할 할당에 대한 범위를 관리할 수 없습니다. 이러한 역할 할당에 대해 여러 범위나 단독 범위를 구성한 경우에는 이 항목 후반부에 나오는 셸 프로시저를 사용하여 범위를 관리해야 합니다. 관리 역할 범위에 대한 자세한 내용은 <A href="understanding-management-role-scopes-exchange-2013-help.md">관리 역할 범위 이해 (영문)</A>를 참조하십시오.



1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리 역할</strong>로 이동합니다.

2.  범위를 변경할 역할 그룹을 선택한 다음 <strong>편집</strong>![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  다음 두 가지 <strong>쓰기 범위</strong> 옵션 중 하나를 선택합니다.
    
      - 드롭다운 상자의 쓰기 범위에서 기본 쓰기 범위 또는 사용자 지정 쓰기 범위를 선택할 수 있습니다.
    
      - <strong>조직 구성 단위</strong>   이 역할 그룹의 범위를 OU(조직 구성 단위)로 지정하려면 이 옵션을 선택하고 OU를 입력합니다.

4.  <strong>저장</strong>을 클릭하여 역할 그룹에 대한 변경 내용을 저장합니다.

## 셸을 사용하여 역할 그룹에서 모든 역할 할당 범위를 동시에 변경

역할 그룹과 그 그룹에 할당된 역할 할당 사이의 역할 할당에서는 역할 자체, 동일한 사용자 지정 범위 또는 다른 사용자 지정 범위에서 가져온 암시적 범위를 사용할 수 있습니다. 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

역할 할당의 범위는 <strong>Set-ManagementRoleAssignment</strong> cmdlet을 사용하여 관리됩니다. 범위를 관리하는 데 <strong>Set-RoleGroup</strong> cmdlet을 사용할 수는 없습니다.

역할 그룹과 관리 역할 집합 간 모든 역할 할당 범위를 동시에 변경하려면 먼저 역할 그룹에서 역할 할당을 검색한 다음 각 할당에서 새 범위를 설정해야 합니다. 이 작업은 <strong>Get-ManagementRoleAssignment</strong> cmdlet을 사용하여 역할 할당을 검색한 다음 <strong>Set-ManagementRoleAssignment</strong> cmdlet에 파이프하여 수행할 수 있습니다.

이 절차에서는 파이프라이닝의 개념과 *WhatIf* 스위치를 사용합니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [WhatIf, Confirm 및 ValidateOnly 스위치](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

역할 그룹에서 모든 역할 할당 범위를 동시에 설정하려면 다음 구문을 사용합니다.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
```
사용할 범위를 구성하는 데 필요한 매개 변수만 사용합니다. 예를 들어 Sales Recipient Management 역할 그룹에서 모든 역할 할당에 대한 받는 사람 범위를 Direct Sales Employees로 변경하려면 다음 명령을 사용합니다.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"
```


> [!NOTE]  
> 변경하고자 하는 역할 할당만 변경되었는지 확인하려면 <EM>WhatIf</EM> 스위치를 사용할 수 있습니다. <EM>WhatIf</EM> 스위치와 함께 위의 명령을 실행하여 결과를 확인한 다음 <EM>WhatIf</EM> 스위치를 제거하여 변경 내용을 적용합니다.



관리 역할 할당 변경에 대한 자세한 내용은 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 역할 그룹에서 개별 역할 할당 범위 변경

역할 그룹과 그 그룹에 할당된 역할 할당 사이의 역할 할당에서는 역할 자체, 동일한 사용자 지정 범위 또는 다른 사용자 지정 범위에서 가져온 암시적 범위를 사용할 수 있습니다. 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

역할 할당의 범위는 <strong>Set-ManagementRoleAssignment</strong> cmdlet을 사용하여 관리됩니다. 범위를 관리하는 데 <strong>Set-RoleGroup</strong> cmdlet을 사용할 수는 없습니다.

이 절차에서는 파이프라이닝의 개념과 <strong>Format-List</strong> cmdlet을 사용합니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

역할 그룹과 관리 역할 집합 간에 역할 할당 범위를 변경하려면 먼저 역할 할당 이름을 찾은 다음 역할 할당에서 범위를 설정합니다.

1.  역할 그룹에서 모든 역할 할당 이름을 찾으려면 다음 명령을 사용합니다. <strong>Format-List</strong> cmdlet으로 관리 역할 할당을 파이프하면 할당의 전체 이름을 볼 수 있습니다.
    
    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name
    ```

2.  변경할 역할 할당의 이름을 찾습니다. 역할 할당의 이름은 다음 단계에서 사용합니다.

3.  개별 할당에서 범위를 설정하려면 다음 구문을 사용합니다.
    
    ```powershell
        Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
    ```

사용할 범위를 구성하는 데 필요한 매개 변수만 사용합니다. 예를 들어 Mail Recipients\_Sales Recipient Management 역할 할당에 대한 받는 사람 범위를 All Sales Employees로 변경하려면 다음 명령을 사용합니다.

```powershell
    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"
```

관리 역할 할당 변경에 대한 자세한 내용은 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹에서 역할 할당의 범위를 성공적으로 변경했는지 확인하려면 다음을 수행하십시오.

  - EAC를 사용하여 역할 그룹에 범위를 구성했으면 다음을 수행합니다.
    
    1.  EAC에서 <strong>사용 권한</strong> \> <strong>관리자 역할</strong>로 이동합니다. 조직의 모든 역할 그룹이 여기에 나열됩니다.
    
    2.  역할 그룹에 구성된 범위를 보려면 역할 그룹을 선택합니다.

  - 셸을 사용하여 역할 그룹에 범위를 구성했으면 다음을 수행합니다.
    
    1.  셸에서 다음 명령을 실행합니다.
        
        ```powershell
            Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
        ```
    
    2.  역할 할당의 쓰기 범위가 지정한 범위로 변경되었는지 확인합니다.

## 역할 그룹 대리인 추가 또는 제거

역할 그룹 대리인은 역할 그룹에서 구성원을 추가 또는 제거하거나 역할 그룹의 속성을 변경할 수 있는 사용자 또는 USG(유니버설 보안 그룹)입니다. 역할 그룹 대리인을 추가하거나 제거하여 역할 그룹을 관리할 수 있는 사용자를 제어할 수 있습니다.


> [!IMPORTANT]   
> 역할 그룹에 대리인을 추가하면 역할 그룹의 대리인 또는 직접적이든 간접적이든 Role Management 관리 역할이 할당된 사용자만 해당 역할 그룹을 관리할 수 있습니다.<BR>직접적이든 간접적이든 사용자가 Role Management 역할을 할당받았지만 역할 그룹의 대리인으로 추가되지 않는 경우 사용자는 <STRONG>Add-RoleGroupMember</STRONG>, <STRONG>Remove-RoleGroupMember</STRONG>, <STRONG>Update-RoleGroupMember</STRONG> 및 <STRONG>Set-RoleGroup</STRONG> cmdlet에서 <EM>BypassSecurityGroupManagerCheck</EM> 스위치를 사용하여 역할 그룹을 관리해야 합니다.


> [!NOTE]
> 역할 그룹에 대리인을 추가하는 데 EAC를 사용할 수 없습니다.

## 셸을 사용하여 역할 그룹에 대리인 추가

역할 그룹에서 대리인 목록을 변경하려면 <strong>Set-RoleGroup</strong> cmdlet에서 *ManagedBy* 매개 변수를 사용합니다. *ManagedBy* 매개 변수는 역할 그룹에 있는 전체 대리인 목록을 덮어씁니다. 전체 대리인 목록을 교체하지 않고 역할 그룹에 대리인을 추가하려면 다음 단계를 사용합니다.

1.  다음 명령을 사용하여 역할 그룹을 변수에 저장합니다.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  다음 명령을 사용하여 변수에 저장된 역할 그룹에 대리인을 추가합니다.
    
    ```powershell
    $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    ```   

    > [!NOTE]
    > USG를 추가하려면 <STRONG>Get-Group</STRONG> cmdlet을 사용합니다.


3.  추가할 각 대리인에 대해 2단계를 반복합니다.

4.  다음 명령을 사용하여 새 대리인 목록을 실제 역할 그룹에 적용합니다.
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

이 예에서는 조직 관리 역할 그룹의 대리인으로서 사용자 David Strome을 추가합니다.

   ```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy += (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
   ```

구문과 매개 변수에 대한 자세한 내용은 [Set-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638182\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 역할 그룹에서 대리인 제거

역할 그룹에서 대리인 목록을 변경하려면 <strong>Set-RoleGroup</strong> cmdlet에서 *ManagedBy* 매개 변수를 사용합니다. *ManagedBy* 매개 변수는 역할 그룹에 있는 전체 대리인 목록을 덮어씁니다. 전체 대리인 목록을 교체하지 않고 역할 그룹에서 대리인을 제거하려면 다음 단계를 사용합니다.

1.  다음 명령을 사용하여 역할 그룹을 변수에 저장합니다.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  다음 명령을 사용하여 변수에 저장된 역할 그룹에서 대리인을 제거합니다.
    
    ```powershell
    $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    ```   

    > [!NOTE]  
    > USG를 제거하려면 <STRONG>Get-Group</STRONG> cmdlet을 사용합니다.

3.  제거할 각 대리인에 대해 2단계를 반복합니다.

4.  다음 명령을 사용하여 새 대리인 목록을 실제 역할 그룹에 적용합니다.
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

이 예에서는 조직 관리 역할 그룹의 대리인으로서 사용자 David Strome을 제거합니다.

   ```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
   ```

구문과 매개 변수에 대한 자세한 내용은 [Set-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638182\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

역할 그룹에서 대리자 목록이 성공적으로 변경되었는지 확인하려면 다음을 수행하십시오.

1.  셸에서 다음 명령을 실행합니다.
    
    ```powershell
    Get-RoleGroup <role group name> | Format-List ManagedBy
    ```

2.  *ManagedBy* 속성에 나열된 대리자에 역할 그룹을 관리할 수 있는 대리자만 포함되어 있는지 확인합니다.

