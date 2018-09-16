---
title: '관리 역할 할당 정책 이해 (영문): Exchange 2013 Help'
TOCTitle: 관리 역할 할당 정책 이해 (영문)
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 50482667
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 역할 할당 정책 이해 (영문)

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

*관리 역할 할당 정책*은 최종 사용자가 자신의 Microsoft Exchange Server 2013 사서함과 메일 그룹 구성을 관리할 수 있도록 하는 하나 이상의 최종 사용자 관리 역할 모음입니다. Exchange 2013의 RBAC(역할 기반 액세스 제어) 권한 모델의 일부인 역할 할당 정책을 통해 최종 사용자가 수정할 수 있는 특정 사서함 및 메일 그룹 구성 설정을 제어할 수 있습니다. 사용자 그룹에 따라 특수한 역할 할당 정책이 있을 수 있습니다.


> [!NOTE]  
> 이 항목에서는 고급 RBAC 기능에 대해 중점적으로 설명합니다. EAC(Exchange 2013 관리 센터)를 사용하여 구성원을 역할 그룹에 추가 및 역할 그룹에서 제거, 역할 그룹 생성과 수정 또는 역할 할당 정책 생성과 수정과 같은 기본 Exchange 권한을 관리하려면, <A href="permissions-exchange-2013-help.md">사용 권한</A>를 참조하세요.



RBAC에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md) 항목을 참조하십시오.

**목차**

Role assignment policy layers

Default and explicit role assignment policies

Using role assignment policies

Role assignment policy management

## 역할 할당 정책 계층

다음은 역할 할당 정책 모델을 구성하는 계층을 설명하는 목록입니다.

  - **사서함**   사서함에는 하나의 역할 할당 정책이 할당됩니다. 사서함에 역할 할당 정책을 할당하면 사서함 역할과 역할 할당 정책 간의 할당이 사서함에 적용됩니다. 이렇게 하면 관리 역할에서 제공되는 모든 사용 권한이 사서함에 부여됩니다.

  - **관리 역할 할당 정책**   *관리 역할 할당 정책*은 Exchange 2013의 특수 개체입니다. 사서함이 만들어지거나 사서함의 역할 할당 정책을 변경하면 사용자가 역할 할당 정책과 연결됩니다. 최종 사용자 관리 역할도 이 정책에 할당합니다. 역할 할당 정책의 모든 역할이 조합되어 사용자가 자신의 사서함이나 메일 그룹에서 관리할 수 있는 항목을 정의합니다.

  - **관리 역할 할당**   *관리 역할 할당*은 관리 역할과 역할 할당 정책 간의 연결입니다. 역할 할당 정책에 관리 역할을 할당하면 관리 역할에 정의된 cmdlet과 매개 변수를 사용할 수 있는 권한이 부여됩니다. 역할 할당 정책과 관리 역할 간에 역할 할당을 만드는 경우 범위를 지정할 수 없습니다. 할당에 의해 적용되는 범위는 관리 역할을 기준으로 하며 `Self` 또는 `MyGAL`입니다. 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md) 항목을 참조하십시오.

  - **관리 역할**   *관리 역할*은 관리 역할 항목 그룹에 대한 컨테이너입니다. 역할은 사용자가 자신의 사서함이나 메일 그룹에 대해 수행할 수 있는 특정 작업을 정의하는 데 사용됩니다. *관리 역할 항목*은 관리 역할의 각 특정 작업을 수행할 수 있도록 하는 cmdlet, 스크립트 또는 특수 사용 권한입니다. 역할 할당 정책에만 최종 사용자 관리 역할을 사용할 수 있습니다. 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md) 항목을 참조하십시오.

  - **관리 역할 항목**   관리 역할 항목은 관리 역할과 역할 그룹에서 사용할 수 있는 cmdlet과 매개 변수를 결정하는 관리 역할의 개별 항목입니다. 각 역할 항목은 관리 역할에서 액세스할 수 있는 매개 변수와 하나의 cmdlet으로 구성됩니다.

다음 그림에서는 앞의 목록에 있는 각 역할 할당 정책 계층과 각 계층이 서로 연결된 방식을 보여 줍니다.

**관리 역할 할당 정책 모델**

![역할 할당 모델 관계](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "역할 할당 모델 관계")

관리 역할, 역할 할당 및 범위에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md) 항목을 참조하십시오.

## 기본 및 명시적 역할 할당 정책

다음 섹션에서는 Exchange 2013의 두 가지 역할 할당 정책 유형에 대해 설명합니다.

## 기본 역할 할당 정책

기본 역할 할당 정책은 **New-Mailbox** 또는 **Enable-Mailbox** cmdlet의 *RoleAssignmentPolicy* 매개 변수를 사용하여 역할 할당 정책이 제공되지 않은 경우 사서함이 만들어지거나 Exchange 2013을 실행하는 서버로 이동될 때 사서함에 할당되는 정책입니다.

Exchange 2013에는 최종 사용자에게 자주 사용하는 권한을 제공하는 기본 역할 할당 정책이 포함되어 있습니다. 기본 역할 할당 정책에 관리 역할을 추가하거나 제거하여 기본 사용 권한을 변경할 수 있습니다.

기본 제공 역할 할당 정책을 고유한 기본 역할 할당 정책으로 바꾸려는 경우 **Set-RoleAssignmentPolicy** cmdlet을 사용하여 새 기본값을 선택할 수 있습니다. 이 작업을 수행하면 역할 할당 정책을 명시적으로 지정하지 않은 경우 기본적으로 지정한 역할 할당 정책이 모든 새 사서함에 할당됩니다.

기본 역할 할당 정책을 변경하는 경우 기본 역할 할당 정책이 할당된 사서함에 자동으로 새 기본 역할 할당 정책이 할당되지 않습니다. 이전에 만든 사서함이 기본값으로 설정한 역할 할당 정책을 사용하도록 업데이트하려면 **Set-Mailbox** cmdlet을 사용해야 합니다.

## 명시적 역할 할당 정책

명시적 역할 할당 정책은 **New-Mailbox**, **Set-Mailbox** 또는 **Enable-Mailbox** cmdlet에 *RoleAssignmentPolicy* 매개 변수를 사용하여 사서함에 수동으로 할당하는 정책입니다. 명시적 역할 할당 정책을 할당하면 새 정책이 즉시 적용되고 이전에 할당한 명시적 역할 할당 정책을 바꿉니다.

## 역할 할당 정책 사용

역할 할당 정책을 사용하면 회사의 사용자가 구성할 수 있어야 하는 항목을 기준으로 사용 권한을 부여할 수 있습니다. 기본 역할 할당 정책이 요구에 맞는 경우에는 사용자 지정할 필요가 없습니다. 그러나 특수한 요구를 가진 여러 사용자 그룹이 있는 경우 각 그룹에 대해 역할 할당 정책을 만들 수 있습니다.

사용하는 기본 역할 할당 정책에는 가장 광범위한 사용자 집합에 적용되는 사용 권한이 포함되어야 합니다. 그런 다음 각 특수 사용자 그룹에 대한 역할 할당 정책을 만들고 이러한 역할 할당 정책을 사용자 지정하여 더 제한적이거나 덜 제한적인 사용 권한을 부여합니다. 이런 방식으로 역할 할당 정책을 구성하면 특수 사용자에게만 명시적으로 역할 할당 정책을 할당하고 대부분의 사용자는 기본 역할 할당 정책이 제공하는 보다 일반적인 사용 권한을 받기 때문에 복잡성이 줄어듭니다.

각 사서함에 하나의 역할 할당 정책만 지정할 수 있습니다. 관리자와 전문가 사용자를 비롯한 모든 사용자에게 하나의 역할 할당 정책이 할당됩니다. 사용자에게 서로 다른 사용 권한 집합을 제공하려면 해당 사용자의 사서함에 필요한 사용 권한이 있는 다른 역할 할당 정책을 할당해야 합니다.

## 역할 할당 정책 관리

새 역할 할당 정책을 추가하려면 먼저 역할 할당 정책을 만들고 기본 역할 할당 정책으로 지정할지 여부를 결정합니다. 역할 할당 정책을 만든 후 역할 할당 정책에 관리 역할을 할당하고 사서함에 역할 할당 정책을 할당합니다. 나중에 관리 역할을 추가 또는 제거하거나 다른 역할 할당 정책을 기본값으로 선택할 수 있습니다.

다음 표에서는 역할 할당 정책 계층 및 각 계층을 관리하는 데 사용할 수 있는 절차 항목을 보여 줍니다.

### 역할 할당 정책 관리 항목

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>역할 할당 정책 모델 계층</th>
<th>관리 항목</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>사서함</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes">사용자 사서함 관리</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">사서함에 할당 정책 변경</a></p></td>
</tr>
<tr class="even">
<td><p>역할 할당 정책</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">역할 할당 정책 관리</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>관리 역할 및 할당</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">역할 할당 정책 관리</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>관리 역할 항목</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">역할에 역할 항목 추가</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">역할 항목 변경</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">역할에서 역할 항목을 제거 합니다.</a></p>

> [!NOTE]  
> 역할 할당 정책에서 관리 역할의 관리 역할 항목을 변경하는 것은 고급 작업이며 일반적으로 필요하지 않습니다. 대신 요구 사항에 맞는 기존 관리 역할을 사용할 수 있습니다. 자세한 내용은 <A href="built-in-role-groups-exchange-2013-help.md">기본 제공 역할 그룹</A> 항목을 참조하십시오.


</td>
</tr>
</tbody>
</table>

