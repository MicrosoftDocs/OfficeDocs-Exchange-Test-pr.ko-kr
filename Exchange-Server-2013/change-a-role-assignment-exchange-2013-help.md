---
title: '역할 할당을 변경: Exchange 2013 Help'
TOCTitle: 역할 할당을 변경
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 50482521
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 할당을 변경

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

관리 역할 할당에서는 역할 담당자에 관리 역할을 할당합니다. 역할 할당을 변경하면 역할이 할당된 역할 담당자가 변경할 수 있는 개체를 제어할 수 있습니다. 역할 할당에 적용되는 관리 역할 범위는 역할의 암시적 쓰기 범위를 재정의합니다. 하지만 역할의 암시적 읽기 범위가 계속 적용됩니다. 적용하는 범위는 역할의 암시적 읽기 범위를 벗어난 개체를 반환할 수 없습니다.

Microsoft Exchange Server 2013의 관리 역할 범위 및 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

역할 할당과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 "역할 할당" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 역할 할당을 사용하거나 사용하지 않도록 설정

역할 할당은 기본적으로 사용하도록 설정되므로 역할이 할당된 역할 담당자에게 연결된 역할이 적용됩니다. 역할 할당을 사용하지 않도록 설정하면 역할 담당자에게 연결된 역할이 적용되지 않습니다.

역할 할당을 사용하도록 설정하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $true
```

역할 할당을 사용하지 않도록 설정하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $false
```

이 예에서는 Help Desk Assignment 역할 할당을 사용하지 않도록 설정합니다.

```powershell
Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 역할 할당의 관리 역할 또는 역할 담당자 변경

역할 할당에 지정된 관리 역할이나 역할 담당자는 변경할 수 없습니다. 역할 할당을 다른 역할이나 역할 담당자와 연결하려면 새 역할 할당을 만든 다음 이전 역할 할당을 삭제해야 합니다. 역할 할당을 추가 및 제거하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [사용자 또는 USG에서 역할을 제거 합니다.](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

사용자 또는 USG(유니버설 보안 그룹)에 대해 직접 할당을 만든 경우 관리 역할 그룹과 관리 역할 할당 정책을 사용하는 것이 좋습니다. 역할 그룹과 할당 정책을 사용하면 사용 권한 모델을 간소화하고 관리해야 하는 역할 할당 수를 줄일 수 있습니다. 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md) 항목을 참조하십시오.

## 셸을 사용하여 역할 할당에 미리 정의된 상대 범위 변경

역할 할당에 미리 정의된 상대 범위를 변경하거나 추가할 수 있습니다. 미리 정의된 범위를 추가하거나 변경하면 이전에 지정한 받는 사람 범위가 역할 할당에서 제거됩니다. 미리 정의된 범위와 그 설명에 대한 목록은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md) 항목을 참조하십시오.

역할 할당에 미리 정의된 범위를 변경하거나 추가하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >
```
이 예에서는 John의 Assignment 역할 할당에 미리 정의된 범위를 MyDistributionGroups로 변경합니다.

```powershell
Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 역할 할당의 받는 사람 필터 범위 변경

새 받는 사람 필터 기반 범위를 지정하거나 역할 할당에 이미 적용된 받는 사람 필터 기반 범위를 변경할 수 있습니다. 받는 사람 필터 범위를 추가하면 이전에 정의한 받는 사람 범위가 역할 할당에서 제거됩니다.

새 받는 사람 필터 기반 범위를 지정하거나 기존 범위를 바꾸려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>
```

이 예에서는 받는 사람 필터 기반 범위를 추가하거나 Redmond Recipients로 변경합니다.

```powershell
Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"
```

역할 할당에 적용된 것과 동일한 받는 사람 필터 기반 범위를 유지하지만 받는 사람 개체를 일치시키는 데 사용되는 받는 사람 필터를 변경하려는 경우 범위의 받는 사람 필터 자체를 변경해야 합니다. 범위를 변경하는 방법에 대한 자세한 내용은 [역할 범위를 변경 합니다.](change-a-role-scope-exchange-2013-help.md) 항목을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 역할 할당의 서버 필터 또는 목록 기반 구성 범위 변경

새 서버 필터 또는 목록 기반 구성 범위를 지정하거나 역할 할당에 이미 적용된 범위를 변경할 수 있습니다. 구성 범위를 추가하거나 변경하면 이전에 지정한 구성 범위가 역할 할당에서 제거됩니다.

새 구성 범위를 지정하거나 기존 범위를 바꾸려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

이 예에서는 구성 범위를 추가하거나 Redmond Servers로 변경합니다.

```powershell
Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"
```

역할 할당에 적용된 것과 동일한 구성 범위를 유지하지만 범위의 서버 필터 또는 서버 목록을 변경하려는 경우 구성 범위 자체를 변경해야 합니다. 범위를 변경하는 방법에 대한 자세한 내용은 [역할 범위를 변경 합니다.](change-a-role-scope-exchange-2013-help.md) 항목을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 역할 할당의 데이터베이스 필터 또는 목록 기반 구성 범위 변경

새 데이터베이스 필터 또는 목록 기반 구성 범위를 지정하거나 역할 할당에 이미 적용된 범위를 변경할 수 있습니다. 구성 범위를 추가하거나 변경하면 이전에 지정한 구성 범위가 역할 할당에서 제거됩니다.

새 구성 범위를 지정하거나 기존 범위를 바꾸려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

이 예에서는 구성 범위를 추가하거나 Redmond Databases로 변경합니다.

```powershell
Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"
```

역할 할당에 적용된 것과 동일한 구성 범위를 유지하지만 범위의 데이터베이스 필터 또는 데이터베이스 목록을 변경하려는 경우 구성 범위 자체를 변경해야 합니다. 범위를 변경하는 방법에 대한 자세한 내용은 [역할 범위를 변경 합니다.](change-a-role-scope-exchange-2013-help.md) 항목을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 역할 할당의 조직 구성 단위 변경

새 OU를 추가하거나 역할 할당에 이미 적용된 OU를 변경할 수 있습니다. 새 OU를 지정하면 이전에 지정한 받는 사람 범위가 역할 할당에서 제거됩니다.

역할 할당의 새 OU를 변경하거나 추가하려면 다음 구문을 사용합니다.

```powershell
Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>
```

이 예에서는 contoso.com 도메인의 Engineering\\Users OU를 Engineering Help Desk 역할 할당에 추가합니다.

```powershell
Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 배타적 받는 사람 또는 구성 범위 변경

배타적 받는 사람 또는 배타적 구성 범위를 변경하려면 이 항목 앞부분의 "셸을 사용하여 역할 할당의 받는 사람 필터 범위 변경", "셸을 사용하여 역할 할당의 서버 필터 또는 목록 기반 구성 범위 변경" 및 "셸을 사용하여 역할 할당의 데이터베이스 필터 또는 목록 기반 구성 범위 변경" 섹션에 제공된 절차를 사용할 수 있습니다. 유일한 차이점은 배타적 범위를 변경하는 경우 배타적 받는 사람 범위를 변경하는지 또는 배타적 구성 범위를 변경하는지에 따라 다음과 같은 배타적 매개 변수를 지정해야 한다는 것입니다.

  - **받는 사람의 배타적 범위**   *CustomRecipientWriteScope* 매개 변수 대신 *ExclusiveRecipientWriteScope* 매개 변수를 사용합니다.

  - **배타적 서버 및 데이터베이스 구성 범위**   *CustomConfigWriteScope* 매개 변수 대신 *ExclusiveConfigWriteScope* 매개 변수를 사용합니다.

일반 받는 사람 및 구성 범위와 마찬가지로 배타적 범위를 추가하거나 변경하면 이전에 정의한 받는 사람 또는 구성 범위가 모두 바뀝니다.

이 예에서는 배타적 받는 사람 쓰기 범위를 변경합니다.

```powershell
Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\)) 항목을 참조하십시오.

