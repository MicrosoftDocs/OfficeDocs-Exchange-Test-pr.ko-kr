---
title: '전송 큐 역할: Exchange 2013 Help'
TOCTitle: 전송 큐 역할
ms:assetid: f663005a-4cb0-4c52-9c95-58681fc5eaab
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876955(v=EXCHG.150)
ms:contentKeyID: 50484515
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 큐 역할

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

`Transport Queues` 관리 역할에는 관리자가 개별 전송 서버에 메시지 큐 관리를 수 있습니다.

이 관리 역할은 Microsoft Exchange Server 2013의 RBAC(역할 기반 액세스 제어) 사용 권한 모델에 있는 몇 가지 기본 제공 역할 중 하나입니다. 하나 이상의 관리 역할 그룹, 관리 역할 할당 정책, 사용자 또는 USG(유니버설 보안 그룹)에 할당되는 관리 역할은 사서함 데이터베이스, 전송 규칙, 받는 사람과 같은 Exchange 2013 구성 요소의 구성을 보거나 구성하기 위한 액세스 권한을 제공하기 위해 결합되는 cmdlet 및 스크립트의 논리적 그룹 기능을 수행합니다. cmdlet 또는 스크립트와 해당 매개 변수(이 모두를 관리 역할 항목이라고 함)가 역할에 포함되어 있으면 역할을 할당받은 사람이 그러한 cmdlet 또는 스크립트와 매개 변수를 실행할 수 있습니다. 관리 역할 및 관리 역할 항목에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하세요.

관리 역할, 관리 역할 그룹 및 기타 RBAC 구성 요소에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

## 관리 역할 할당

이 역할이 사용 권한을 부여할 수 있으려면 역할 그룹, 사용자 또는 USG(유니버설 보안 그룹) 등의 역할 담당자에게 이 역할을 할당해야 합니다. 이러한 할당은 관리 역할 할당을 사용하여 수행됩니다. 역할 할당은 역할 담당자와 역할을 서로 연결합니다. 한 역할 담당자에게 둘 이상의 역할이 할당되면, 할당된 모든 역할에서 부여하는 모든 사용 권한이 역할 담당자에게 부여됩니다.

역할 할당은 역할 담당자를 역할에 연결할 뿐만 아니라 사용자 지정 또는 기본 제공 관리 범위도 적용할 수 있습니다. 관리 범위는 역할 담당자가 수정할 수 있는 받는 사람, 서버 및 데이터베이스 개체를 제어합니다. 이 역할이 역할 담당자에게 할당되었지만 관리 범위에서 역할 담당자에게 정의된 범위를 기반으로 일부 개체만 관리하도록 허용하는 경우, 역할 담당자는 이 역할에 의해 그러한 특정 개체에 부여되는 사용 권한만 사용할 수 있습니다. 이 역할에서 제공하는 사용 권한은 역할 할당에 정의된 범위 외부의 개체에 적용할 수 없습니다. 역할 할당 및 범위에 대한 자세한 내용은 다음 항목을 참고하세요.

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

이 역할은 기본적으로 하나 이상의 역할 그룹에 할당됩니다. 자세한 내용은 이 항목의 뒷부분에 있는 "기본 관리 역할 할당" 섹션을 참고하세요.

이 역할에 할당된 역할 그룹, 사용자 또는 USG를 보려면 다음 명령을 사용합니다.

    Get-ManagementRoleAssignment -Role "<role name>"

## 일반 및 위임 역할 할당

일반 또는 위임 역할 할당을 사용하여 역할 담당자에게 이 역할을 할당할 수 있습니다. 일반 역할 할당은 역할에서 제공하는 권한을 역할 담당자에게 부여합니다. 위임 역할 할당은 다른 역할 담당자에게 역할을 할당하는 기능을 역할 담당자에게 부여합니다. 일반 및 위임 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)을 참조하세요.

## 역할 할당 추가 또는 제거

이 역할을 할당받을 역할 담당자를 변경할 수 있습니다. 이 역할을 할당받을 역할 담당자를 변경하면 이 사용 권한이 부여되는 대상이 변경됩니다. 이 역할을 다른 기본 제공 역할 그룹에 할당할 수도 있고, 역할 그룹을 만들어서 이 역할을 할당할 수도 있습니다. 사용자 또는 USG에 이 역할을 할당할 수도 있습니다. 하지만 사용 권한 모델이 지나치게 복잡해지지 않도록 역할 할당을 사용자 및 USG로 제한하는 것이 좋습니다.

이 역할을 역할 담당자에게 할당하려면 위임 역할 할당을 사용하여 역할을 자신이 속해 있는 역할 그룹에 할당하거나, 자기 자신에게 직접 할당하거나, 자신이 속해 있는 USG에 할당해야 합니다. 위임 역할 할당에 대한 자세한 내용은 "일반 및 위임 역할 할당" 섹션을 참고하세요.

기본 제공 역할 그룹, 자신이 만드는 역할 그룹, 사용자 및 USG에서 이 역할을 제거할 수도 있습니다. 하지만 이 역할과 역할 그룹 또는 USG 사이에 항상 위임 역할 할당이 적어도 하나는 있어야 합니다. 마지막 위임 역할 할당은 삭제할 수 없습니다. 이러한 제한 기능을 통해 시스템에서 자신이 잠기는 것을 방지할 수 있습니다.


> [!IMPORTANT]
> 이 역할과 역할 그룹 또는 USG 사이에 위임 역할 할당이 적어도 하나는 있어야 합니다. 마지막으로 사용자에게 할당되는 경우 이 역할과 연결된 마지막 위임 역할 할당은 제거할 수 없습니다.



이 역할과 역할 그룹, 사용자 및 USG 사이에서 할당을 추가 또는 제거하는 방법에 대한 자세한 내용은 다음 항목을 참고하세요.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [사용자 또는 USG에서 역할을 제거 합니다.](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## 역할 할당의 관리 범위 변경

이 역할과 역할 담당자 사이에서 기존 역할 할당의 관리 범위를 변경할 수도 있습니다. 역할 할당의 범위를 변경하면 이 역할이 제공하는 사용 권한을 사용하여 관리할 수 있는 개체를 제어할 수 있습니다. 역할 할당의 범위를 변경하는 방법에는 여러 가지가 있습니다. 다음 중 하나를 수행할 수 있습니다.

  - **Set-ManagementRoleAssignment** cmdlet을 사용하여 새 사용자 지정 범위를 추가합니다. 자세한 내용은 다음 항목을 참고하세요.
    
      - [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)
    
      - [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)

  - **Set-ManagementRoleAssignment** cmdlet을 사용하여 조직 구성 단위 범위를 추가 또는 변경합니다. 자세한 내용은 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참고하세요.

  - **Set-ManagementRoleAssignment** cmdlet을 사용하여 미리 정의된 범위를 추가 또는 변경합니다. 자세한 내용은 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참고하세요.

  - **Set-ManagementScope** cmdlet을 사용하여 역할 할당과 연결된 사용자 지정 범위에서 받는 사람, 서버 또는 데이터베이스 범위를 변경합니다. 자세한 내용은 [역할 범위를 변경 합니다.](change-a-role-scope-exchange-2013-help.md)을 참고하세요.

## 역할 할당 사용 또는 사용 안 함

역할 할당을 사용하거나 사용하지 않도록 설정함으로써 역할 할당의 적용 여부를 제어할 수 있습니다. 역할 할당을 사용하지 않도록 설정한 경우에는 연결된 역할에서 부여하는 사용 권한이 역할 담당자에게 적용되지 않습니다. 이 기능은 역할 할당을 삭제하지 않고 일시적으로 사용 권한을 제거하려는 경우에 편리합니다. 자세한 내용은 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참조하세요.

## 기본 관리 역할 할당

이 역할에는 하나 이상의 역할 담당자에 대한 역할 할당이 있습니다. 다음 표는 역할 할당이 일반인지 위임인지와 각 할당에 적용되는 관리 범위를 나타냅니다. 다음 목록에서는 각 열에 대해 설명합니다.

  - **일반 할당**   역할 담당자는 일반 역할 할당을 사용하여 이 역할에 대한 관리 역할 항목에 의해 제공되는 사용 권한에 액세스할 수 있습니다.

  - **위임 할당**   역할 담당자는 위임 역할 할당을 사용하여 역할 그룹, 사용자 또는 USG에 이 역할을 할당할 수 있습니다.

  - **받는 사람 읽기 범위**   받는 사람 읽기 범위는 역할 담당자가 Active Directory에서 읽을 수 있는 받는 사람 개체를 결정합니다.

  - **받는 사람 쓰기 범위**   받는 사람 쓰기 범위는 역할 담당자가 Active Directory에서 수정할 수 있는 받는 사람 개체를 결정합니다.

  - **구성 읽기 범위**   구성 읽기 범위는 역할 담당자가 Active Directory에서 읽을 수 있는 구성 및 서버 개체를 결정합니다.

  - **구성 쓰기 범위**   구성 쓰기 범위는 역할 담당자가 Active Directory에서 수정할 수 있는 조직 및 서버 개체를 결정합니다.

### 이 역할에 대한 기본 관리 역할 할당

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>역할 그룹</th>
<th>일반 할당</th>
<th>위임 할당</th>
<th>받는 사람 읽기 범위</th>
<th>받는 사람 쓰기 범위</th>
<th>구성 읽기 범위</th>
<th>구성 쓰기 범위</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 관리 역할 사용자 지정

이 역할은 이 항목의 시작 부분에 나열된 기능과 구성 요소를 관리하는 데 필요한 모든 cmdlet과 해당 매개 변수를 역할 담당자에게 제공하도록 구성되었습니다. 다른 기능을 관리할 수 있는 다른 역할도 제공되었습니다. 역할 그룹에서 역할을 추가 및 제거하면 개별 관리 역할을 사용자 지정하지 않고도 사용자 지정된 사용 권한 모델을 만들 수 있습니다. 전체 역할 목록을 보려면 [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)을 참조하세요. 역할 그룹 사용자 지정에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조하세요.

이 역할의 사용자 지정 버전을 만들어야 하는 경우에는 이 역할의 자식으로서의 역할을 만들고 새 역할을 사용자 지정해야 합니다.


> [!WARNING]
> 다음 정보를 활용하면 사용 권한의 고급 관리를 수행할 수 있습니다. 관리 역할을 사용자 지정하면 사용 권한 모델이 매우 복잡해질 수 있습니다. 기본 제공 관리 역할을 잘못 구성된 사용자 지정 역할로 바꾸면 특정 기능이 더 이상 작동하지 않을 수도 있습니다.



다음은 사용자 지정된 역할을 만들어 역할 담당자에게 할당하는 가장 일반적인 단계입니다.

1.  이 역할의 복사본을 만듭니다. 자세한 내용은 [역할 만들기](create-a-role-exchange-2013-help.md)를 참조하세요.

2.  **Set-ManagementRoleEntry** 및 **Remove-ManagementRoleEntry** cmdlet을 사용하여 새 역할에서 역할 항목을 변경하거나 제거합니다. 새 역할은 부모 기본 제공 역할에 있는 역할 항목만 포함할 수 있으므로 새 역할에 역할 항목을 추가할 수 없습니다. 자세한 내용은 다음 항목을 참고하세요.
    
      - [역할 항목 변경](change-a-role-entry-exchange-2013-help.md)
    
      - [역할에서 역할 항목을 제거 합니다.](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  기본 제공 역할을 사용자 지정된 새 역할로 바꾸려면 기본 제공 역할과 연결된 모든 역할 할당을 제거합니다. 자세한 내용은 다음 항목을 참조하세요.
    
      - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)의 "역할 그룹에 역할 추가 또는 역할 그룹에서 역할 제거" 섹션
    
      - [사용자 또는 USG에서 역할을 제거 합니다.](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  사용자 지정된 새 역할을 필요한 역할 담당자에게 추가합니다. 자세한 내용은 다음 항목을 참조하세요.
    
      - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)의 "역할 그룹에 역할 추가 또는 역할 그룹에서 역할 제거" 섹션
    
      - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        

        > [!IMPORTANT]
        > 역할을 만든 사용자 외에 다른 사용자도 사용자 지정된 새 역할을 할당할 수 있게 만들려면 한 명 이상의 역할 담당자에게 위임 역할 할당을 추가해야 합니다. 자세한 내용은 <A href="delegate-role-assignments-exchange-2013-help.md">대리인 역할 할당</A>을 참고하세요.


