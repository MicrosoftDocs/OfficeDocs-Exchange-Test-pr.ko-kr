---
title: '검색 관리: Exchange 2013 Help'
TOCTitle: 검색 관리
ms:assetid: b8bc5922-a8c9-4707-906d-fa38bb87da8f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351080(v=EXCHG.150)
ms:contentKeyID: 50483992
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검색 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

검색 관리 관리 역할 그룹은 Microsoft Exchange Server 2013의 RBAC(역할 기반 액세스 제어) 권한 모델을 구성하는 몇 가지 기본 제공 역할 그룹 중 하나입니다. 역할 그룹에는 지정된 작업 집합을 수행하기 위해 필요한 사용 권한을 포함하는 관리 역할이 하나 이상 할당됩니다. 역할 그룹 구성원은 역할 그룹에 할당된 관리 역할에 액세스할 수 있습니다. 역할 그룹에 대한 자세한 내용은 [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)를 참조하세요.

검색 관리 역할 그룹의 구성원인 사용자나 관리자는 Exchange 조직의 사서함에서 특정 기준을 충족하는 데이터를 검색할 수 있으며, 사서함에 대해 소송 보존을 구성할 수도 있습니다. 자세한 내용은 [원본 위치 eDiscovery](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery)를 참조하십시오.


> [!IMPORTANT]
> 기본적으로 조직 관리 역할 그룹을 통해 해당 역할 그룹의 구성원인 USG(유니버설 보안 그룹) 또는 사용자에 대한 검색 기능을 사용할 수 있는 것은 아닙니다. 조직 관리&nbsp;역할 그룹의 구성원이 이 역할 그룹의 구성원이 되거나 이 항목 뒷부분에 나오는 사서함 검색 역할을 수동으로 조직 관리&nbsp;역할 그룹에 할당해야 합니다. 역할 그룹에 역할을 할당하는 방법에 대한 자세한 내용은 <A href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</A>를 참조하십시오.



RBAC에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.

## 역할 그룹 구성원

이 역할 그룹에서 구성원을 추가 또는 제거하려면 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)를 참조하세요.

기본적으로 Organization Management 역할 그룹의 구성원만 이 역할 그룹에서 구성원을 추가 또는 제거할 수 있습니다. 역할 그룹 대리인을 추가하는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)의 "역할 그룹 대리인 추가 또는 제거" 섹션을 참조하세요.

다음 명령을 사용하여 이 역할 그룹의 구성원인 사용자 또는 USG 목록을 볼 수 있습니다.

    Get-RoleGroupMember "Discovery Management"

역할 그룹 구성원에 대한 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)의 [View the members of a role group](manage-role-group-members-exchange-2013-help.md)를 참조하십시오.

## 역할 그룹 사용자 지정

이 역할 그룹에는 기본적으로 관리 역할이 할당됩니다. 포함되는 역할은 "이 역할 그룹에 할당된 관리 역할" 섹션에 나열되어 있습니다. 조직의 필요에 맞게 이 역할 그룹에서 역할 할당을 추가 또는 제거할 수 있습니다.

Exchange 2013에서 제공하는 역할 그룹은 더 세부적인 작업에 맞게 설계되었습니다. 역할 그룹에 역할을 할당하여 역할 그룹 구성원이 역할과 관련된 작업을 수행하도록 설정할 수 있습니다. 예를 들어 저널링 역할을 사용하면 저널링 에이전트 및 저널링 규칙을 관리할 수 있습니다. 역할 그룹에 역할을 할당하는 방법에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참고하세요.

이 역할 그룹에 할당된 역할에는 기본 관리 범위가 지정됩니다. 관리 범위는 역할 그룹 구성원이 보거나 수정할 수 있는 Exchange 개체를 결정합니다. 역할과 역할 그룹 사이의 할당과 관련된 범위를 변경할 수 있습니다. 예를 들어 역할 그룹 구성원이 특정 조직 구성 단위나 특정 위치에 있는 받는 사람만 변경할 수 있도록 하려는 경우 이 기능을 사용할 수 있습니다. 관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참고하세요.

이 역할 그룹의 사용자 지정 방법에 대한 자세한 내용은 다음 항목을 참고하세요.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)

역할 그룹을 만들고 이 역할 그룹에 할당된 일부 역할을 새 역할 그룹에 할당하려는 경우 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)의 "역할 그룹 만들기" 섹션을 참조하세요.

## 이 역할 그룹에 할당된 관리 역할

다음 표에는 이 역할 그룹에 할당된 모든 관리 역할 및 각 역할 할당의 특성이 나타나 있습니다.

  - **일반 할당**   역할 그룹의 구성원이 연결된 관리 역할에서 사용할 수 있는 관리 역할 항목에 액세스할 수 있게 합니다.

  - **위임 할당**   역할 그룹 구성원이 지정된 역할을 다른 역할 그룹, 역할 할당 정책, 사용자 또는 USG에 할당할 수 있게 합니다.

  - **받는 사람 읽기 범위**   역할 그룹 구성원이 Active Directory에서 읽을 수 있는 받는 사람 개체를 결정합니다.

  - **받는 사람 쓰기 범위**   역할 그룹 구성원이 Active Directory에서 수정할 수 있는 받는 사람 개체를 결정합니다.

  - **구성 읽기 범위**   역할 그룹 구성원이 Active Directory에서 읽을 수 있는 구성 및 서버 개체를 결정합니다.

  - **구성 쓰기 범위**   역할 그룹 구성원이 Active Directory에서 수정할 수 있는 조직 및 서버 개체를 결정합니다.

역할 할당 및 관리 범위에 대한 자세한 내용은 다음 항목을 참고하세요.

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

### 이 역할 그룹에 할당된 관리 역할

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
<th>관리 역할</th>
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
<td><p><a href="legal-hold-role-exchange-2013-help.md">법적 보존 역할</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailbox-search-role-exchange-2013-help.md">사서함 검색 역할</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
</tbody>
</table>

