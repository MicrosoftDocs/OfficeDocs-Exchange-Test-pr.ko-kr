---
title: '관리 역할 범위 이해 (영문): Exchange 2013 Help'
TOCTitle: 관리 역할 범위 이해 (영문)
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 50482737
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 역할 범위 이해 (영문)

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

*관리 역할 범위*를 이용하면 관리 역할 할당을 만들 때 관리 역할의 영향 범위를 정의할 수 있습니다. 범위를 적용하면 역할이 할당된 역할 담당자는 그 범위에 있는 개체만 수정할 수 있습니다. 역할 담당자는 관리 역할 그룹, 관리 역할, 관리 역할 할당 정책, 사용자 또는 USG(유니버설 보안 그룹)입니다. 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 이 항목에서는 고급 RBAC 기능에 대해 중점적으로 설명합니다. EAC(Exchange 2013 관리 센터)를 사용하여 구성원을 역할 그룹에 추가 및 역할 그룹에서 제거, 역할 그룹 생성과 수정 또는 역할 할당 정책 생성과 수정과 같은 기본 Exchange 권한을 관리하려면, <A href="permissions-exchange-2013-help.md">사용 권한</A>를 참조하세요.



모든 관리 역할에 있는지 여부는 기본 제공 역할 또는 사용자 지정 역할에는 것이 관리 범위입니다. 관리 범위는 다음 중 하나일 수 있습니다.

  - **일반**   *일반 범위*는 단독이 아닙니다. 이 범위는 Active Directory에서 관리 역할이 할당된 사용자가 보거나 수정할 수 있는 개체를 결정합니다. 일반적으로 관리 역할은 만들거나 수정할 수 있는 것을 나타내고 관리 역할 범위는 만들거나 수정할 수 있는 위치를 나타냅니다. 일반 범위는 명시적 또는 암시적 범위일 수 있습니다. 명시적 및 암시적 범위에 대해서는 이 항목의 뒷부분에서 설명합니다.

  - **단독**   *단독 범위*는 일반 범위와 거의 비슷합니다. 주된 차이는 단독 범위에 연결된 역할이 할당되지 않은 사용자에 대해 단독 범위 내의 개체 액세스를 거부할 수 있다는 것입니다. 모든 단독 범위는 명시적 범위입니다. 명시적 범위에 대해서는 이 항목의 뒷부분에서 설명합니다.
    
    단독 범위에 대한 자세한 내용은 [배타적 범위 이해 (영문)](understanding-exclusive-scopes-exchange-2013-help.md)를 참조하십시오.

범위는 관리 역할에서 상속하거나, 관리 역할 할당에서 미리 정의된 상대 범위로 지정하거나, 사용자 지정 필터로 만들어 관리 역할 할당에 추가할 수 있습니다. 관리 역할에서 상속한 범위를 *암시적 범위*라고 하고 미리 정의된 범위 및 사용자 지정 범위를 *명시적 범위*라고 합니다. 다음 섹션에서는 각 범위 유형에 대해 설명합니다.

  - Implicit Scopes

  - Explicit Scopes

  - Predefined Relative Scopes

  - Custom Scopes
    
      - Recipient Filter Scopes
    
      - Configuration Scopes

각 역할에는 다음과 같은 유형의 범위를 지정할 수 있습니다.

  - **받는 사람 읽기 범위**   암시적인 받는 사람 읽기 범위는 관리 역할이 할당된 사용자가 Active Directory에서 읽을 수 있는 받는 사람 개체를 결정합니다.

  - **받는 사람 쓰기 범위**   암시적인 받는 사람 쓰기 범위는 관리 역할이 할당된 사용자가 Active Directory에서 수정할 수 있는 받는 사람 개체를 결정합니다.

  - **구성 읽기 범위**   암시적인 구성 읽기 범위는 관리 역할이 할당된 사용자가 Active Directory에서 읽을 수 있는 구성 개체를 결정합니다.

  - **구성 쓰기 범위**    암시적 구성 쓰기 범위는 관리 역할이 할당된 사용자가 Active Directory에서 수정할 수 있는 조직, 데이터베이스 및 서버 개체를 결정합니다.

받는 사람 개체는 사서함, 메일 그룹, 메일 사용 가능 사용자 및 기타 개체를 포함 합니다. 구성 개체는 Microsoft Exchange Server 2013 및 Exchange 를 실행 하는 서버에 있는 데이터베이스를 실행 하는 서버를 포함 합니다. 각 유형의 범위는 암시적 범위 또는 명시적 범위 될 수 있습니다.

## 암시적 범위

암시적 범위는 관리 역할 유형에 적용되는 기본 범위입니다. 암시적 범위가 관리 역할 유형과 연결되므로 역할 유형이 동일한 모든 상위 및 하위 관리 역할은 같은 암시적 범위가 지정됩니다. 암시적 범위는 기본 제공 역할과 사용자 지정 관리 역할 모두에 적용됩니다. 관리 역할 및 관리 역할 유형에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

다음 표는 관리 역할에서 정의할 수 있는 모든 암시적 범위를 소개합니다.

### 관리 역할에 정의되는 암시적 범위

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>암시적 범위</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code>이 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 Exchange 조직 전체에서 받는 사람 개체를 만들거나 수정할 수 있습니다.</p>
<p><code>Organization</code>이 역할의 받는 사람 읽기 범위에 있는 경우 역할은 Exchange 조직 전체에서 받는 사람 개체를 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code>이 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 현재 사용자의 GAL(전체 주소 목록)에 있는 모든 받는 사람의 속성을 볼 수 있습니다.</p>
<p><code>MyGAL</code>이 역할의 받는 사람 읽기 범위에 있는 경우 역할은 현재 사용자의 GAL에 있는 모든 받는 사람의 속성을 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p><code>Self</code>가 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 현재 사용자의 사서함에 있는 속성만 수정할 수 있습니다.</p>
<p><code>Self</code>가 역할의 받는 사람 읽기 범위에 있는 경우 역할은 현재 사용자의 사서함에 있는 속성만 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyDistributionGroups</code>가 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 현재 사용자가 소유한 메일 그룹 개체를 만들거나 수정할 수 있습니다.</p>
<p><code>MyDistributionGroups</code>가 역할의 받는 사람 읽기 범위에 있는 경우 역할은 현재 사용자가 소유한 메일 그룹 개체를 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code>가 역할의 구성 쓰기 범위에 있는 경우 역할은 Exchange 조직 전체에서 모든 서버 또는 데이터베이스 구성 개체를 만들거나 수정할 수 있습니다.</p>
<p><code>OrganizationConfig</code>가 역할의 구성 읽기 범위에 있는 경우 역할은 Exchange 조직 전체에서 모든 서버 또는 데이터베이스 구성 개체를 볼 수 있습니다.</p>
<p>이 범위는 구성 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p><code>None</code>이 범위에 있으면 범위를 역할에 사용할 수 없습니다. 예를 들어 받는 사람 쓰기 범위에 <code>None</code>이 지정된 역할은 Exchange 조직에서 받는 사람 개체를 수정할 수 없습니다.</p></td>
</tr>
</tbody>
</table>


역할이 역할 담당자에게 할당되었지만 미리 정의된 범위나 사용자 지정 범위가 지정되지 않은 경우에는 역할에 정의된 암시적 범위를 사용하여 사용자가 보거나 수정할 수 있는 받는 사람 또는 조직 개체를 제어합니다.

역할의 암시적 쓰기 범위는 항상 암시적 읽기 범위보다 작거나 같습니다. 즉, 역할은 범위에서 볼 수 있는 개체만 수정할 수 있습니다.

관리 역할에 정의된 암시적 범위는 변경할 수 없습니다. 하지만 관리 역할에서 암시적 쓰기 범위 및 구성 범위를 재정의할 수는 있습니다. 미리 정의된 상대 범위 또는 사용자 지정 범위를 역할 할당에 사용하면 역할의 암시적 쓰기 범위가 재정의되고 새 범위가 우선적으로 적용됩니다. 역할의 암시적 읽기 범위는 재정의할 수 없으며 항상 적용됩니다. 자세한 내용은 Predefined Relative Scopes 및 Custom Scopes를 참조하십시오.

다음 표를 확장하면 기본 제공되는 관리 역할과 해당되는 암시적 범위가 모두 나타납니다. 기본 제공되는 개별 역할에 대한 자세한 내용은 [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)을 참조하십시오.

## 기본 제공 관리 역할 암시적 범위


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할</th>
<th>받는 사람 읽기 범위</th>
<th>받는 사람 쓰기 범위</th>
<th>구성 읽기 범위</th>
<th>구성 쓰기 범위</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## 명시적 범위

명시적 범위는 관리되는 역할에서 수정할 수 있는 개체를 제어하기 위해 직접 설정한 범위입니다. 암시적 범위는 관리 역할에 정의되지만, 명시적 범위는 관리 역할 할당에서 정의됩니다. 그렇기 때문에 재정의하는 명시적 범위를 사용하지 않는 경우에는 모든 관리 역할에서 일관성 있게 암시적 범위를 적용할 수 있습니다. 관리 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

명시적 범위는 관리 역할의 암시적인 쓰기 및 구성 범위를 재정의합니다. 관리 역할의 암시적인 읽기 범위는 재정의하지 않습니다. 암시적 읽기 범위는 계속해서 관리 역할이 읽을 수 있는 개체를 정의합니다.

명시적 범위는 관리 역할의 암시적 쓰기 범위가 비즈니스 요구에 맞지 않는 경우에 유용합니다. 새로운 범위가 암시적 읽기 범위의 경계를 넘지 않는 한 원하는 것은 무엇이든 명시적 범위에 추가할 수 있습니다. 관리 역할에 속한 cmdlet이 개체를 만들거나 수정하려면 개체나 개체를 포함한 컨테이너에 대한 정보를 읽을 수 있어야 합니다. 예를 들어, 관리 역할의 암시적 읽기 범위가 `Self`로 설정되어 있을 경우 명시적 쓰기 범위 `Organization`을 추가하면 쓰기 범위가 암시적 읽기 범위의 경계를 넘기 때문에 추가할 수 없습니다.

자세한 내용은 다음 섹션을 참조하십시오.

  - Predefined Relative Scopes

  - Custom Scopes

## 미리 정의된 상대 범위

Exchange 2013 여러 미리 정의 된 상대 쓰기 관리 역할의 범위를 수정 하는데 사용할 수 있는 범위를 제공 합니다. 미리 정의 된 상대 범위를 사용자 지정 범위를 수동으로 만들 필요 없이 비즈니스 요구를 더 가깝게 일치 하는 간편한 방법을 제공 합니다. 연결 된 역할 할당 할당 된 역할 담당자를 기준으로 이기 때문에 상대 범위 라고 합니다. 예, `Self` 미리 정의 된 상대 범위만 현재 사용자에 게 해당 쓰기 범위를 제한합니다. 미리 정의 된 `MyDistributionGroups` 상대 범위는 현재 사용자만 소유 하 고 메일 그룹에 쓰기 범위를 제한 합니다. 미리 정의 된 상대 범위 받는 사람 개체의 범위에 사용할 수 있습니다. 미리 정의 된 상대 범위 범위 구성 개체에 사용할 수 없습니다. 다음 표에서 사용할 수 있는 미리 정의 된 상대 범위를 보여줍니다.

### 미리 정의된 상대 범위

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>암시적 범위</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code>이 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 Exchange 조직 전체에서 받는 사람 개체를 만들거나 수정할 수 있습니다.</p>
<p><code>Organization</code>이 역할의 받는 사람 읽기 범위에 있는 경우 역할은 Exchange 조직 전체에서 받는 사람 개체를 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p><code>Self</code>가 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 현재 사용자의 사서함에 있는 속성만 수정할 수 있습니다.</p>
<p><code>Self</code>가 역할의 받는 사람 읽기 범위에 있는 경우 역할은 현재 사용자의 사서함에 있는 속성만 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyDistributionGroups</code>가 역할의 받는 사람 쓰기 범위에 있는 경우 역할은 현재 사용자가 소유한 메일 그룹 개체를 만들거나 수정할 수 있습니다.</p>
<p><code>MyDistributionGroups</code>가 역할의 받는 사람 읽기 범위에 있는 경우 역할은 현재 사용자가 소유한 메일 그룹 개체를 볼 수 있습니다.</p>
<p>이 범위는 받는 사람 읽기 및 쓰기 범위에만 사용됩니다.</p></td>
</tr>
</tbody>
</table>


미리 정의된 상대 범위는 새 관리 역할 할당을 만들 때 적용됩니다. **New-ManagementRoleAssignment** cmdlet을 사용하여 역할 할당을 만드는 동안 *RecipientRelativeWriteScope* 매개 변수를 사용하여 미리 정의된 상대 범위를 지정할 수 있습니다. 새 역할 할당을 만들면 새 미리 정의된 역할이 관리 역할의 암시적 쓰기 범위를 재정의합니다. 미리 정의된 상대 범위로 역할 할당을 만들 때는 사용자 지정 받는 사람 범위를 지정할 수 없습니다. 그러나 필요한 경우 사용자 지정 구성 범위를 지정할 수 있습니다.

미리 정의된 상대 범위가 할당된 관리 역할을 추가하는 방법에 대한 자세한 내용은 [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)를 참조하십시오.

## 사용자 지정 범위

사용자 지정 범위 암시적 쓰기 범위 아니고 미리 정의 된 상대 범위 비즈니스 요구를 충족 하는 경우 필요 합니다. 사용자 지정 범위를 사용 하는 세분화 된 수준 관리 역할을 적용할 범위에서 정의할 수 있습니다. 예, 다음 특정 조직 구성 단위 (OU), 특정 유형의 받는 사람을 또는 둘 모두 대상으로 지정 하는 것이 좋습니다. 또는 사서함 데이터베이스의 특정 집합을 관리할 수 있도록 관리자의 그룹을 허용 하려면만 될 수 있습니다.

미리 정의된 상대 범위와 마찬가지로 사용자 지정 범위도 관리 역할에 정의된 암시적 쓰기 및 조직 구성 범위를 재정의합니다. 관리 역할의 암시적 읽기 범위는 계속 적용되며 결과적인 사용자 지정 범위는 암시적 읽기 범위의 경계를 넘을 수 없습니다. 다음과 같은 세 가지 유형의 사용자 지정 범위를 만들 수 있습니다.

  - **OU 범위**   가장 간단한 사용자 지정 범위인 OU 범위는 **New-ManagementRoleAssignment** cmdlet에서 *RecipientOrganizationalUnitScope* 매개 변수를 사용하여 만듭니다. 역할을 할당할 때 OU 범위를 지정하면 역할이 할당된 역할 담당자는 해당 OU 내의 받는 사람 개체만 수정할 수 있습니다. OU 범위가 할당된 관리 역할을 추가하는 방법에 대한 자세한 내용은 [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)를 참조하십시오.

  - **받는 사람 필터 범위**   받는 사람 필터 범위는 필터를 사용하여 받는 사람 유형이나 부서, 관리자, 위치 등의 기타 받는 사람 속성에 따라 특정 받는 사람을 대상으로 지정합니다. 자세한 내용은 Recipient Filter Scopes 섹션을 참조하십시오.

  - **구성 범위**   구성 범위 필터 또는 대상 서버 목록 또는 Active Directory 사이트 또는 서버 역할 등의 서버에서 정의할 수 있는 필터링 할 수 있는 속성을 기반으로 특정 서버 목록을 사용 합니다. 구성 범위는 데이터베이스 목록 또는 필터링 할 수 있는 데이터베이스 속성에 따라 특정 데이터베이스를 대상으로 데이터베이스 범위를 사용할 수도 수 있습니다. 자세한 내용은 구성 범위 섹션을 참조 하십시오.

**New-ManagementScope** cmdlet을 사용하면 단순하고 광범위하거나 복잡하고 세분화된 받는 사람 및 구성 사용자 지정 범위를 만들 수 있습니다. 받는 사람 또는 구성 범위를 만들면 해당 범위와 일치하는 받는 사람, 서버 또는 데이터베이스 개체만 반환됩니다. **New-ManagementRoleAssignment** 또는 **Set-ManagementRoleAssignment** cmdlet을 사용한 역할 할당에 이러한 범위를 적용할 경우 역할이 할당된 역할 담당자는 범위와 일치하는 개체만 수정할 수 있습니다. 사용자 지정 범위를 만들고 나면 범위 유형을 변경할 수 없습니다. 받는 사람 범위는 항상 받는 사람 범위이고 구성 범위는 항상 구성 범위입니다.

기본적으로 사용자 지정 범위를 정의 하는 범위와 일치 하는 개체의 집합에 액세스 하는 역할 담당자를 수 있습니다. 그러나 다른 역할 임무 책임자에 게 동일한 또는 해당 범위에도 할당 되지 않은 사용자에 대 한 액세스를 제외 적극적으로 하지 않습니다. 모든 사용자 지정 범위는 동일한 개체를 목록 또는 해당 범위에 대 한 필터와 일치 하는 경우 동일한 개체에 액세스할 수 있습니다. 여기에서이 동작 되어있지는 이와 더불어, 등 경영진의 경우 개체가 있을 수 있습니다. 이러한 개체에 대 한 배타적 범위를 정의할 수 있습니다. 배타적 범위 필터 또는 목록을 사용 하 여 일반 범위 일반 범위와는 달리는 동일한 방식에서, 동일한 또는 해당 하는 배타적 범위의 일부가 아닌 다른 사람에 게 범위에 포함 된 개체에 대 한 액세스를 거부 합니다. 배타적 범위에 대 한 자세한 내용은 [배타적 범위 이해 (영문)](understanding-exclusive-scopes-exchange-2013-help.md)을 참조 하십시오.

## 받는 사람 필터 범위

받는 사람 필터 범위를 사용하면 필터 문에서 지정한 값을 기준으로 받는 사람 개체에 대한 속성 하나 이상을 평가하는 방법으로 역할 담당자가 관리할 수 있는 받는 사람 개체를 제어할 수 있습니다. 받는 사람 범위에 포함되는 받는 사람은 사서함, 메일 사용이 가능한 사용자, 메일 그룹 및 메일 연락처 등입니다. 지정한 필터와 일치하는 받는 사람만 해당 역할이 할당된 역할 담당자가 관리할 수 있습니다. 필터 문의 예는 `{ Name -Eq "David" }`입니다. 여기서 **Name**은 평가할 받는 사람 개체의 속성이며 **David**은 속성을 기준으로 평가할 값입니다. **-Eq** 비교 연산자 속성에 저장된 값이 필터가 참이 되도록 지정된 값과 동일해야 함을 나타냅니다. 필터가 참이면 받는 사람이 범위에 포함됩니다.

받는 사람 필터 범위는 **New-ManagementScope** cmdlet에서 *RecipientRestrictionFilter* 매개 변수를 적용하여 받는 사람 필터를 지정하는 방법으로 만듭니다. 기본적으로 **New-ManagementScope** cmdlet은 일반 범위를 만듭니다. 단독 범위를 만들려면 *Exclusive* 스위치를 *RecipientRestrictionFilter* 매개 변수와 함께 포함합니다.

받는 사람 제한 필터를 만들면 Exchange는 기본적으로 조직 내의 모든 받는 사람 개체를 기준으로 사용자가 제공한 필터를 평가합니다. 범위에서 평가되는 받는 사람을 제한하려면 *RecipientRoot* 매개 변수를 *RecipientRestrictionFilter* 매개 변수와 함께 사용하면 됩니다. *RecipientRoot* 매개 변수는 OU를 허용합니다. *RecipientRoot* 매개 변수를 사용하면 Exchange에서는 사용자가 제공한 필터를 기준으로 지정 OU에 포함된 받는 사람만 평가합니다.

받는 사람 필터 범위를 역할 할당에 추가할 때 새로운 역할 할당을 만드는 경우에는 **New-ManagementRoleAssignment**의 *CustomRecipientWriteScope* 매개 변수에 받는 사람 범위의 이름을 지정하고, 기존 역할 할당을 업데이트하는 경우에는 **Set-ManagementRoleAssignment** cmdlet을 지정합니다. 각 역할 할당은 미리 정의된 상대 범위를 포함하여 받는 사람 범위를 하나씩 가질 수 있습니다. 받는 사람 범위를 추가한 역할 할당에 구성 범위 하나를 추가할 수 있습니다.

필터 구문에 대한 자세한 내용 및 받는 사람에 대한 필터링 가능한 받는 사람 속성의 전체 목록은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

## 구성 범위

다음은 두 유형의 Exchange 2013 에서 제공 하는 구성 범위:

  - **서버 범위**   서버 범위, 서버 필터 범위 및 서버 목록 범위는 다음과 같은 두가지 유형이 있습니다. 서버 개체는 서버 범위에 포함 하는 경우에 수신 커넥터, 전송 큐, 서버 인증서, 가상 디렉터리와 등을 비롯 하 여 서버 구성을 관리할 수 있습니다.
    
      - **서버 필터 범위**   서버 필터 범위를 사용하면 필터 문에서 지정한 값을 기준으로 서버 개체에 대한 속성 하나 이상을 평가하는 방법으로 역할 담당자가 관리할 수 있는 서버 개체를 제어할 수 있습니다. 서버 필터 범위를 만들려면 **New-ManagementScope** cmdlet에 *ServerRestrictionFilter* 매개 변수를 사용합니다.
    
      - **서버 목록 범위**   서버 목록 범위를 사용하면 역할 담당자가 액세스할 수 있는 서버 목록을 정의하여 역할 담당자가 관리할 수 있는 서버 개체를 제어할 수 있습니다. 서버 목록 범위를 만들려면 **New-ManagementScope** cmdlet에 *ServerList* 매개 변수를 사용합니다.

  - **데이터베이스 범위**   데이터베이스 범위, 데이터베이스 필터 범위 및 데이터베이스 목록 범위는 다음과 같은 두가지 유형이 있습니다. 데이터베이스 개체는 데이터베이스 범위에 포함 하는 경우에 관리 될 수 있는 데이터베이스 구성에는 데이터베이스 할당량 제한을, 데이터베이스 유지 관리, 공용 폴더 복제 데이터베이스가 탑재 되 여부 등입니다. 데이터베이스 구성 외에도 데이터베이스 받는 사람에 만들 수 있는 컨트롤에 데이터베이스 범위도 사용할 수 있습니다. 조직에서 사전Exchange 2010 SP1 서버를 포함 하는 경우이 항목 뒷부분에 나오는 데이터베이스 범위 및 이전 버전의 Exchange 섹션을 참조 합니다.
    
      - **데이터베이스 필터 범위**   데이터베이스 필터 범위를 사용하면 필터 문에서 지정한 값을 기준으로 데이터베이스 개체에 대한 속성 하나 이상을 평가하는 방법으로 역할 담당자가 관리할 수 있는 데이터베이스 개체를 제어할 수 있습니다. 데이터베이스 필터 범위를 만들려면 **New-ManagementScope** cmdlet에 *DatabaseRestrictionFilter* 매개 변수를 사용합니다.
    
      - **데이터베이스 목록 범위**   데이터베이스 목록 범위를 사용하면 역할 담당자가 액세스할 수 있는 데이터베이스 목록을 정의하여 역할 담당자가 관리할 수 있는 데이터베이스 개체를 제어할 수 있습니다. 데이터베이스 목록 범위를 만들려면 **New-ManagementScope** cmdlet에 *DatabaseList* 매개 변수를 사용합니다.

필터 구문에 대한 자세한 내용 및 필터링 가능한 서버와 데이터베이스 속성의 전체 목록은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

서버 및 데이터베이스 목록은 각 범위에 포함할 서버와 데이터베이스를 지정하는 방법으로 정의할 수 있습니다. 서버와 데이터베이스 이름을 쉼표로 구분하여 여러 서버 또는 데이터베이스를 각 범위에 지정할 수 있습니다.

서버 또는 데이터베이스 구성 범위를 역할 할당에 추가할 때 새로운 역할 할당을 만드는 경우에는 **New-ManagementRoleAssignment**의 *CustomConfigWriteScope* 매개 변수에 서버 또는 데이터베이스 구성 범위의 이름을 지정하고, 기존 역할 할당을 업데이트하는 경우에는 **Set-ManagementRoleAssignment** cmdlet을 지정합니다. 각 역할 할당은 구성 범위를 하나씩만 가질 수 있습니다.

데이터베이스 범위를 사용하면 역할 담당자가 관리할 데이터베이스를 제어할 수 있을 뿐 아니라 역할 담당자가 사서함을 만들 데이터베이스도 제어할 수 있습니다. 이는 역할 담당자가 관리할 수 있는 받는 사람을 제어하는 기능과는 별개입니다. 역할 담당자에게 새 사서함을 만들거나 기존 사용자를 메일 사용이 가능한 사용자로 만들거나 사서함을 이동할 권한이 있는 경우, 권한을 더욱 구체화하여 데이터베이스 범위를 사용하여 사서함을 만들 데이터베이스 또는 사서함을 이동할 데이터베이스를 제어할 수 있습니다. 역할 담당자가 관리할 수 있는 받는 사람을 제어하려면 **New-ManagementRoleAssignment** 또는 **Set-ManagementRoleAssignment** cmdlet의 *CustomRecipientWriteScope* 매개 변수에 지정된 받는 사람 범위를 사용합니다. 사서함을 만들거나 이동할 데이터베이스를 제어하려면 동일한 cmdlet의 *CustomConfigurationWriteScope* 매개 변수에 지정된 데이터베이스 범위를 사용합니다.


> [!NOTE]
> 데이터베이스 범위를 사용 하 여 자동 사서함 배포를 제어할 수 있습니다.



서버 범위, 데이터베이스 범위 또는 모두를 관리할 수 Exchange 기능이 필요할 수 있습니다. 서버와 데이터베이스 범위를 관리할 수 있어야 하는 한 기능을 하는 경우 두 역할 할당을 생성 하 고 기능 관리에 액세스할 수 있어야 하는 역할 담당자에 게 할당 해야 합니다. 하나의 역할 할당 서버 범위와 연결 하며 하나의 역할 할당 데이터베이스 범위와 연결 해야 합니다.

일부 cmdlet은 명확하지 않은 구성 범위를 사용할 수 있습니다. 다음 표는 사용을 제어하는 데 사용할 수 있는 cmdlet 목록과 구성 범위를 제공합니다. 받는 사람 기능 영역에 포함된 cmdlet의 경우 구성 범위를 사용하여 받는 사람을 만들 데이터베이스를 제어할 수 있습니다. 받는 사람 중 누구를 관리할지는 제어하지 않습니다. **필요한 범위** 열에 다음을 포함할 수 있습니다.

  - **데이터베이스**   cmdlet을 실행하려면 관리할 데이터베이스를 포함한 데이터베이스 범위와 함께 역할 할당을 역할 담당자에게 할당하거나 역할의 암시적 구성 쓰기 범위에 관리할 데이터베이스를 포함해야 합니다.

  - **서버**   cmdlet을 실행하려면 관리할 서버를 포함한 서버 범위와 함께 역할 할당을 역할 담당자에게 할당하거나 역할의 암시적 구성 쓰기 범위에 관리할 서버를 포함해야 합니다.

  - **서버 또는 데이터베이스**   cmdlet을 실행하려면 데이터베이스 범위에 관리할 데이터베이스가 포함되거나 또는 서버 범위에 데이터베이스가 위치한 서버가 포함되는 역할 할당을 역할 담당자에게 할당해야 합니다. 또는 역할의 암시적 구성 쓰기 범위에 관리할 데이터베이스를 포함하거나 데이터베이스가 위치한 서버를 포함해야 합니다. 역할 할당은 사용자 지정 쓰기 범위를 가질 수 없습니다.

  - **서버 및 데이터베이스**   이 cmdlet을 실행하려면 역할 담당자에게 두 가지 역할을 할당해야 합니다. 첫 번째 역할 할당에는 관리할 데이터베이스를 포함하는 데이터베이스 범위가 포함되어야 합니다. 두 번째 역할 할당에는 데이터베이스가 위치한 서버를 포함하는 서버 범위가 포함되어야 합니다. 역할 할당에서는 사용자 지정 구성 범위를 정의할 수도 있고 역할 할당이 역할로부터 암시적 구성 쓰기 범위를 상속할 수도 있습니다. 역할로부터 암시적 쓰기 범위를 상속하려면 역할 할당이 사용자 지정 쓰기 범위를 가질 수 없습니다.

### 기능 영역 및 해당 데이터베이스와 서버 범위

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>기능 영역</th>
<th>cmdlet</th>
<th>필요한 범위</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>데이터베이스</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>데이터베이스</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>데이터베이스</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>서버 및 데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>데이터베이스</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>서버 또는 데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>데이터베이스</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>고가용성</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p>고가용성</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>서버</p></td>
</tr>
<tr class="even">
<td><p>고가용성</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p>고가용성</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>서버</p></td>
</tr>
<tr class="even">
<td><p>고가용성</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>서버 또는 데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>고가용성</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>서버 또는 데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>고가용성</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>서버 또는 데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>고가용성</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>서버 또는 데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>고가용성</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>서버 또는 데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>받는 사람</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>받는 사람</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>받는 사람</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="even">
<td><p>받는 사람</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
<tr class="odd">
<td><p>문제 해결</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>데이터베이스</p></td>
</tr>
</tbody>
</table>


## 데이터베이스 범위 및 이전 버전의 Exchange

데이터베이스 범위 Microsoft Exchange 2010 서비스 팩 1 (SP1)에서 처음으로 도입 하 고 계속 Exchange 2013 에서 지원 됩니다. 버전 Exchange 2010 SP1 하기 전에 Exchange 받는 사람 범위 및 서버 구성 범위를 지원 합니다. Exchange 2010 SP1 또는 이상 서버에 새 데이터베이스 범위를 만들 때 다음과 같은 경고가 표시 됩니다.

```powershell
WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.
```

데이터베이스 범위를 만들 때만 Exchange 2010 s p 1을 실행 하는 서버에 연결 하는 사용자에 게 적용 되 이상입니다. 사전Exchange 2010 SP1 서버에 연결 하는 사용자는 자신에 게 적용 되는 데이터베이스 범위와 관련 된 모든 역할 할당을이 없습니다. 즉, 이러한 역할 할당에서 제공 하는 사용 권한을 모두 서버 사전Exchange 2010 s p 1에 연결할 때 사용자에 게 부여 되지 않습니다. 데이터베이스 범위 없습니다 수, 제거, 수정, 만들거나 사전Exchange 2010 SP1 서버에서 볼 합니다.

데이터베이스 범위 Exchange 조직에서 모든 데이터베이스를 포함할 수 있습니다. 이 Exchange Server 2007, Exchange 2010 및 Exchange 2013 서버를 포함합니다. 이 옵션을 사용 하면 사용자가 관리할 수 있는 Exchange 버전에 관계 없이 어떤 데이터베이스를 제어할 수 있습니다. 으로 다른 데이터베이스 범위와 Exchange 2007 및 Exchange 2010 데이터베이스를 포함 하는 데이터베이스 범위와 관련 된 역할 할당만 적용 됩니다 사용자에 게 Exchange 2010 SP1 이상의 서버에 연결할 때.

SP1 서버 사전에Exchange 2010 에 연결 하는 사용자를 볼 수 있으며 데이터베이스 범위와 관련 된 역할 할당을 수정할 수 있습니다. 데이터베이스 범위와 연결 된 현재가 하는 경우 서버 범위에 기존 역할 할당에 구성 범위를 변경 하는입니다. 그러나 서버 범위에 구성 범위는 역할 할당에 변경 되 고 사용자가 나중에 다시 데이터베이스 범위를 변경 하려는 경우 또는 사용자가 다른 데이터베이스 범위에 구성 범위를 변경 하려면 사용자 Exchange 2010 SP1 이상의 서버에 연결 하는 동안 변경을 수행 해야 합니다. 만 사용자 셰이프가 SP1 서버 사전에Exchange 2010 에 연결 된 경우 역할 할당에 구성 범위를 변경 될 때 서버 범위를 지정할 수 있습니다.

