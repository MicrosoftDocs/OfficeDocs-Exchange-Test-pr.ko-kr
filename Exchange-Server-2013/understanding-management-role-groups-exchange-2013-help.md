---
title: '관리 역할 그룹 이해 (영문): Exchange 2013 Help'
TOCTitle: 관리 역할 그룹 이해 (영문)
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 50482765
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 역할 그룹 이해 (영문)

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

*관리 역할 그룹*은 Microsoft Exchange Server 2013에서 RBAC(역할 기반 액세스 제어) 사용 권한 모델에 사용되는 USG(유니버설 보안 그룹)입니다. 관리 역할 그룹을 사용하여 관리 역할을 사용자 그룹에 간편하게 할당할 수 있습니다. 역할 그룹의 모든 구성원에게 동일한 역할 집합이 할당됩니다. 역할 그룹에는 조직 관리, 받는 사람 관리 및 기타 작업과 같은 Exchange 2013의 주요 관리 작업을 정의하는 관리자 및 전문가 역할이 할당됩니다. 역할 그룹을 사용하면 관리자 또는 전문가 사용자 그룹에 보다 광범위한 사용 권한 집합을 쉽게 할당할 수 있습니다.


> [!NOTE]  
> 이 항목에서는 고급 RBAC 기능에 대해 중점적으로 설명합니다. EAC(Exchange 2013 관리 센터)를 사용하여 구성원을 역할 그룹에 추가 및 역할 그룹에서 제거, 역할 그룹 생성과 수정 또는 역할 할당 정책 생성과 수정과 같은 기본 Exchange 권한을 관리하려면, <A href="permissions-exchange-2013-help.md">사용 권한</A>를 참조하세요.



**목차**

Role group layers

Role group management

Built-in role groups

Linked role groups

Role group delegation

Role group membership

Role group creation workflow


> [!NOTE]  
> 사용자에게 자신의 사서함이나 메일 그룹을 관리할 수 있는 권한을 할당하려면 <A href="understanding-management-role-assignment-policies-exchange-2013-help.md">관리 역할 할당 정책 이해 (영문)</A> 항목을 참조하십시오.



## 역할 그룹 계층

역할 그룹 모델을 구성하는 계층은 다음과 같습니다.

  - **역할 그룹 구성원**   *역할 그룹 구성원*은 역할 그룹의 구성원으로 추가할 수 있는 사서함, USG(유니버설 보안 그룹) 또는 다른 역할 그룹입니다. 사서함, USG 또는 다른 역할 그룹이 역할 그룹의 구성원으로 추가되면 관리 역할과 역할 그룹 간의 할당이 새 구성원에게 적용됩니다. 이렇게 하면 관리 역할에서 제공되는 모든 사용 권한이 새 구성원에게 부여됩니다.

  - **관리 역할 그룹**   *관리 역할 그룹*은 사서함, USG 및 역할 그룹의 구성원인 다른 역할 그룹이 포함된 특수 USG입니다. 이 그룹에 구성원을 추가 및 제거하며 관리 역할이 할당되는 것도 이 그룹입니다. 역할 그룹의 모든 역할이 조합되어 역할 그룹에 추가된 구성원이 Exchange 조직에서 관리할 수 있는 항목을 정의합니다.

  - **관리 역할 할당**   *관리 역할 할당*은 관리 역할과 역할 그룹을 연결합니다. 역할 그룹에 관리 역할을 할당하면 역할 그룹의 구성원에게 관리 역할에 정의된 cmdlet과 매개 변수를 사용할 수 있는 권한이 부여됩니다. 역할 할당에서 관리 범위를 사용하여 할당을 사용할 수 있는 영역을 제어할 수 있습니다. 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md) 항목을 참조하십시오.

  - **관리 역할 범위**   *관리 역할 범위*는 역할 할당에 미치는 영향의 범위입니다. 범위를 사용하여 역할 그룹에 역할을 할당하면 관리 범위가 할당에서 관리할 수 있는 대상 개체를 구체적으로 지정합니다. 할당과 할당 범위는 역할 그룹의 구성원에게 할당되어 구성원이 관리할 수 있는 항목을 제한합니다. 범위는 서버나 데이터베이스 목록, 조직 구성 단위 또는 서버나 데이터베이스나 받는 사람 개체에 대한 필터로 구성될 수 있습니다. 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md) 항목을 참조하십시오.

  - **관리 역할**   *관리 역할*은 관리 역할 항목 그룹에 대한 컨테이너입니다. 역할은 해당 역할이 할당된 역할 그룹의 구성원이 수행할 수 있는 특정 작업을 정의하는 데 사용됩니다. 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md) 항목을 참조하십시오.

  - **관리 역할 항목**   *관리 역할 항목*은 특정 작업을 수행할 수 있도록 하는 cmdlet, 스크립트 및 기타 특수 사용 권한에 대한 액세스를 제공하는 관리 역할의 개별 항목입니다. 대체로 역할 항목은 관리 역할에서 액세스할 수 있는 매개 변수와 하나의 cmdlet 또는 스크립트 및 역할이 할당되는 역할 그룹으로 구성됩니다.

다음 그림에서는 앞의 목록에 있는 각 역할 그룹 계층과 각 계층이 서로 연결된 방식을 보여 줍니다.

**관리 역할 그룹 계층**

![관리 역할 그룹 계층](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "관리 역할 그룹 계층")

RBAC에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md) 항목을 참조하십시오.

맨 위로 이동

## 역할 그룹 관리

역할 그룹을 만드는 경우 역할 그룹의 구성원을 포함하는 USG를 만들고 역할 그룹과 지정한 관리 역할 간에 할당을 만들게 됩니다. 선택적으로 역할 할당에 적용할 관리 범위를 지정할 수도 있으며, 새 역할 그룹의 구성원이 될 사서함을 추가할 수 있습니다.

역할 그룹을 만든 후에는 각 계층이 독립적인 개체가 됩니다. 역할 그룹은 모든 계층이 결합되는 중앙 지점으로 계속 사용되지만 각 계층이 독립적으로 관리됩니다. 예를 들어 역할 그룹을 만들 때 적용한 관리 범위를 수정하려면 역할 그룹을 만든 후 개별 역할 할당의 범위를 변경해야 합니다. 역할 그룹 모델 관리는 역할 그룹 모델의 개별 계층을 관리하는 cmdlet을 사용하여 수행됩니다.

다음 표에서는 역할 그룹 계층 및 각 계층을 관리하는 데 사용할 수 있는 절차 항목을 보여 줍니다.

### 역할 그룹 관리 항목

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>역할 그룹 모델 계층</th>
<th>관리 항목</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>역할 그룹 구성원</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">역할 그룹 구성원 관리</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>역할 그룹</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>관리 역할 및 할당</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</a></p></td>
</tr>
<tr class="even">
<td><p>관리 역할 항목</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">역할에 역할 항목 추가</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">역할 항목 변경</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">역할에서 역할 항목을 제거 합니다.</a></p>

> [!NOTE]  
> 역할 그룹에서 관리 역할의 관리 역할 항목을 변경하는 것은 고급 작업이며 일반적으로 필요하지 않습니다. 대신 요구 사항에 맞는 기존 관리 역할을 사용할 수 있습니다. 자세한 내용은 <A href="built-in-role-groups-exchange-2013-help.md">기본 제공 역할 그룹</A> 항목을 참조하십시오.


</td>
</tr>
</tbody>
</table>


맨 위로 이동

## 기본 제공 역할 그룹

기본 제공 역할 그룹은 Exchange 2013에 포함되어 있는 역할로, 사용자 그룹에 여러 수준의 관리 권한을 제공하는 데 사용할 수 있는 역할 그룹 집합을 제공합니다. 기본 제공 역할 그룹에 사용자를 추가하거나 제거할 수 있습니다. 대부분의 역할 그룹에 역할 할당을 추가하거나 제거할 수도 있습니다. 유일한 예외는 다음과 같습니다.

  - 조직 관리 역할 그룹에서 위임 역할 할당을 제거할 수 없습니다.

  - 조직 관리 역할 그룹에서 역할 관리 역할을 제거할 수 없습니다.

다음 표에는 Exchange 2013에 포함된 기본 제공 역할 그룹이 모두 나와 있습니다. 기본 제공 역할 그룹에 대한 자세한 내용은 [기본 제공 역할 그룹](built-in-role-groups-exchange-2013-help.md) 항목을 참조하십시오.

### 기본 제공 역할 그룹

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>역할 그룹</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
<td><p>조직 관리 역할 그룹의 구성원인 관리자는 전체 Microsoft Exchange 2013 조직에 대한 관리 액세스 권한을 가지며, 몇 가지 예외는 있지만 모든 Exchange 2013 개체에 대해 거의 모든 작업을 수행할 수 있습니다. 기본적으로 이 역할 그룹의 구성원은 사서함 검색 및 범위가 지정되지 않은 최상위 관리 역할 관리를 수행할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
<td><p>Organization Management만 보기 역할 그룹의 구성원인 관리자는 Exchange 조직에 있는 모든 개체의 속성을 볼 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
<td><p>Recipient Management 역할 그룹의 구성원인 관리자는 Exchange 2013 조직 내에서 Exchange 2013 받는 사람을 만들거나 수정할 수 있는 관리 액세스 권한이 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
<td><p>UM Management 역할 그룹의 구성원인 관리자는 UM(통합 메시징) 서버 구성, 사서함의 UM 속성, UM 프롬프트 및 UM 자동 전화 교환 구성과 같은 Exchange 조직의 기능을 관리할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">검색 관리</a></p></td>
<td><p>검색 관리 역할 그룹의 구성원인 사용자나 관리자는 Exchange 조직의 사서함에서 특정 기준을 충족하는 데이터를 검색할 수 있으며, 사서함에 대해 소송 보존을 구성할 수도 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
<td><p>Records Management 역할 그룹의 구성원인 사용자는 보존 정책 태그, 메시지 분류, 전송 규칙 등의 준수 기능을 구성할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
<td><p>이 역할 그룹의 구성원인 관리자는 전송, 클라이언트 액세스 및 사서함 기능(예: 데이터베이스 복사본, 인증서, 전송 큐 및 송신 커넥터, 가상 디렉터리, 클라이언트 액세스 프로토콜)의 서버별 구성을 구성할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
<td><p>기술 지원팀 역할 그룹의 구성원인 사용자는 Exchange 2013 받는 사람에 대해 제한된 받는 사람 관리를 수행할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
<td><p>방역 관리 역할 그룹의 구성원인 사용자는 Exchange 2013의 스팸 방지 및 맬웨어 방지 기능을 구성할 수 있습니다. Exchange 2013과 통합되는 타사 프로그램은 이 역할 그룹에 서비스 계정을 추가하여 Exchange 구성의 검색 및 구성에 필요한 cmdlet에 대한 액세스 권한을 해당 프로그램에 부여할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p></td>
<td><p>규정 준수 관리 역할 그룹의 구성원인 사용자는 Exchange 규정 준수 구성을 정책에 따라 구성하고 관리할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">공용 폴더 관리</a></p></td>
<td><p>공용 폴더 관리 역할 그룹의 구성원인 관리자는 Exchange 2013을 실행하는 서버의 공용 폴더를 관리할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">위임 설치</a></p></td>
<td><p>위임 설치 역할 그룹의 구성원인 관리자는 Exchange 2013 역할 그룹 구성원에 의해 이전에 제공된 조직 관리을 실행하는 서버를 배포할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 연결된 역할 그룹

연결된 역할 그룹은 전용 리소스 포리스트에 Exchange 2013을 설치하고 다른 신뢰할 수 있는 외부 포리스트에 사용자를 배치하는 조직에서 사용됩니다. 이름에서 알 수 있듯이 연결된 역할 그룹은 Exchange 포리스트의 역할 그룹과 외부 포리스트의 USG 간에 연결을 만듭니다. 연결된 역할 그룹은 Exchange를 관리하도록 하려는 관리자의 AD DS(Active Directory 도메인 서비스) 사용자 계정이 Exchange와 동일한 리소스 포리스트에 없는 경우에 유용합니다. 연결된 역할 그룹은 외부 USG 하나에만 연결할 수 있습니다. 또한 Exchange 포리스트와 외부 포리스트 간에 양방향 트러스트를 만들 필요가 없습니다. Exchange 포리스트는 외부 포리스트를 트러스트해야 하지만 외부 포리스트는 Exchange 포리스트를 트러스트하지 않아도 됩니다.

다중 포리스트 토폴로지의 사용 권한에 대한 자세한 내용은 [다중 포리스트 사용 권한을 이해 (영문)](understanding-multiple-forest-permissions-exchange-2013-help.md) 항목을 참조하십시오.

연결된 역할 그룹은 다음 두 부분으로 구성됩니다.

  - **연결된 역할 그룹**   연결된 역할 그룹은 외부 USG를 역할 그룹에 할당된 관리 역할 할당에 연결하는 컨테이너 개체입니다.

  - **외부 USG**   외부 USG에는 연결된 역할 그룹이 제공하는 사용 권한을 부여해야 하는 구성원이 들어 있습니다.

연결된 역할 그룹을 만드는 경우 Exchange 포리스트를 관리하도록 할 사용자가 포함된 외부 포리스트에 도메인 컨트롤러를 제공하고 이러한 사용자를 구성원으로 포함하는 USG, 외부 USG 이름 및 외부 포리스트에 액세스하는 데 필요한 자격 증명을 제공합니다. Exchange는 연결된 역할 그룹에 외부 USG의 SID(보안 식별자)를 추가합니다. USG SID는 외부 USG의 유일한 ID이므로 외부 포리스트가 여러 개 있는 경우 역할 그룹의 이름에 외부 포리스트를 지정하는 것이 좋습니다.

연결된 역할 그룹에는 구성원이 포함되어 있지 않습니다. 해당 역할 그룹의 모든 구성원은 외부 USG를 사용하여 관리됩니다. 따라서 **Update-RoleGroupMember**, **Add-RoleGroupMember** 또는 **Remove-RoleGroupMember** cmdlet을 사용하여 역할 그룹 구성원을 추가하거나 제거할 수는 없습니다. 외부 USG에 구성원을 추가하면 연결된 역할 그룹이 제공하는 사용 권한이 부여됩니다.

자체 구성원이 포함된 표준 역할 그룹을 연결된 역할 그룹으로 변경할 수 없으며 그 반대의 경우도 마찬가지입니다. 역할 그룹을 표준 역할 그룹에서 연결된 역할 그룹으로 변경하려면 새 연결된 역할 그룹을 만들고 표준 역할 그룹에 있는 관리 역할 할당을 연결된 역할 그룹에 복제해야 합니다. 기본 제공 역할 그룹도 표준 역할 그룹이기 때문에 동일한 제한이 적용됩니다. 외부 포리스트에서 Exchange 포리스트의 모든 관리 작업을 수행하려면 새 연결된 역할 그룹을 만들고 기본 제공 역할 그룹에 있는 관리 역할을 새 연결된 역할 그룹에 추가해야 합니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 [기본 제공 역할 그룹을 미러링 하는 연결 된 역할 그룹 만들기](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md) 항목을 참조하십시오.

맨 위로 이동

## 역할 그룹 위임

기본적으로 조직 관리 역할 그룹의 구성원은 역할 그룹에 구성원을 추가 및 제거할 수 있습니다. 그러나 조직 관리 역할 그룹의 구성원이 아닌 사용자가 역할 그룹 구성원을 추가 및 제거할 수 있도록 설정할 수도 있습니다. 이 경우 역할 그룹 위임을 사용합니다.

역할 그룹 위임은 각 역할 그룹의 **ManagedBy** 속성에 의해 제어됩니다. **ManagedBy** 속성에는 역할 그룹에 구성원을 추가 및 제거하고 역할 그룹의 구성을 변경할 수 있는 사용자 목록이 포함되어 있습니다. 사용자가 역할 그룹의 구성원이 아닌 경우 역할 그룹이 제공하는 사용 권한은 할당되지 않습니다.

역할 그룹에 **ManagedBy** 속성을 설정하면 기본적으로 해당 속성에 역할 그룹 관리자로 표시된 사용자만 역할 그룹 또는 역할 그룹의 구성원을 수정할 수 있습니다. 그러나 역할 그룹 또는 역할 그룹 구성원을 수정하는 cmdlet의 선택적 매개 변수를 통해 이 제한을 재정의할 수 있습니다. 조직 관리 역할의 구성원이거나 직접 또는 간접적으로 역할 관리 관리 역할이 할당된 사용자는 *BypassSecurityGroupManagerCheck* 스위치를 사용할 수 있습니다. 이 스위치를 사용하면 **ManagedBy** 속성이 무시되고 사용자가 역할 그룹 또는 역할 그룹 구성원을 수정할 수 있습니다.

역할 그룹에 **ManagedBy** 속성을 설정하지 않으면 조직 관리 역할의 구성원이거나 직접 또는 간접적으로 역할 관리 관리 역할이 할당된 사용자만 역할 그룹 또는 역할 그룹 구성원을 수정할 수 있습니다.


> [!NOTE]  
> 역할 그룹에 할당되는 역할을 위임 역할 할당으로 할당할 수도 있습니다. 위임 역할 할당을 사용하면 위임 역할이 할당된 역할 그룹의 구성원이 해당 역할을 다른 역할 그룹, 할당 정책, 사용자 또는 USG에 할당할 수 있습니다. 역할 그룹의 구성원은 <STRONG>ManagedBy</STRONG> 속성에도 추가되어 있는 경우가 아니면 해당 역할만 할당할 수 있고 역할 그룹을 위임할 수는 없습니다. 위임 역할 할당에 대한 자세한 내용은 <A href="understanding-management-role-assignments-exchange-2013-help.md">관리 역할 할당 이해 (영문)</A> 항목을 참조하십시오.



역할 그룹 위임을 관리하는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목을 참조하십시오.

맨 위로 이동

## 역할 그룹 구성원

사용자가 역할 그룹의 구성원이 되면 역할 그룹에 할당된 관리 역할이 사용자에게 할당됩니다. 사용자가 여러 역할 그룹의 구성원인 경우 각 역할 그룹의 관리 역할이 집계되어 사용자에게 할당됩니다. 사용자, USG 및 기타 역할 그룹이 역할 그룹의 구성원이 될 수 있습니다.

조직 관리 또는 역할 관리 역할 그룹의 구성원인 사용자와 역할 그룹에 사용자를 추가 및 제거할 수 있는 권한이 위임된 사용자만 역할 그룹 구성원을 관리할 수 있습니다.

역할 그룹 구성원을 관리하는 방법에 대한 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md) 항목을 참조하십시오.

## 역할 그룹 만들기 워크플로

앞에서 설명한 것처럼 역할 그룹은 여러 계층으로 이루어져 있습니다. 역할 그룹을 만들 때 나타나는 결과를 이해하려면 새 역할 그룹을 만드는 다음 예를 고려해 보십시오.

  ```powershell
  New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"
  ```

앞의 명령을 실행하면 다음과 같은 결과가 나타납니다.

1.  특수 USG인 Seattle Recipient Management라는 새 역할 그룹 개체가 만들어집니다.

2.  Ray, Jenn, Maria, Chris, Maija, Carter, Jenny, Sam, Lukas, Isabel 및 Katie의 사서함이 역할 그룹의 구성원으로 추가됩니다. 이러한 사용자는 이 역할 그룹이 제공하는 사용 권한을 받습니다.

3.  사용자 Brian과 David가 역할 그룹의 **ManagedBy** 속성에 추가됩니다. 두 사용자는 역할 그룹에 구성원을 추가 및 제거할 수 있지만 구성원이 아니기 때문에 역할 그룹이 제공하는 사용 권한을 받지 못합니다. Katie도 역할 그룹의 **ManagedBy** 속성에 추가됩니다. Katie는 **ManagedBy** 속성에 추가되었으며 역할 그룹의 구성원이기 때문에 역할 그룹에 구성원을 추가하거나 제거할 수 있을 뿐 아니라 역할 그룹이 제공하는 사용 권한도 받습니다.

4.  다음과 같은 관리 역할 할당이 만들어집니다. 역할 할당은 명령에 지정된 각 관리 역할을 역할 그룹에 할당합니다. 관리 범위 Seattle Users가 각 역할 할당에 추가됩니다. 각 역할 할당의 이름은 할당되는 관리 역할과 역할 그룹 이름의 조합입니다.
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

이 명령의 결과를 이 항목의 앞부분 있는 관리 역할 그룹 계층 그림과 비교하면 각 단계가 역할 그룹 계층에 상호 관련되는 위치를 확인할 수 있습니다. 그런 다음 이 항목의 앞부분에 있는 "역할 그룹 관리"에 표시된 관리 역할 그룹 관리 항목을 참조하여 각 역할 그룹 계층을 관리할 수 있습니다.

맨 위로 이동

