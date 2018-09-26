---
title: '조직 관리: Exchange 2013 Help'
TOCTitle: 조직 관리
ms:assetid: 0bfd21c1-86ac-4369-86b7-aeba386741c8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335087(v=EXCHG.150)
ms:contentKeyID: 50482485
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

조직 관리 관리 역할 그룹은 Microsoft Exchange Server 2013의 RBAC(역할 기반 액세스 제어) 권한 모델을 구성하는 몇 가지 기본 제공 역할 그룹 중 하나입니다. 역할 그룹에는 지정된 작업 집합을 수행하기 위해 필요한 사용 권한을 포함하는 관리 역할이 하나 이상 할당됩니다. 역할 그룹 구성원은 역할 그룹에 할당된 관리 역할에 액세스할 수 있습니다. 역할 그룹에 대한 자세한 내용은 [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)를 참조하세요.

조직 관리 역할 그룹의 구성원인 관리자는 전체 Exchange 2013 조직에 대한 관리 액세스 권한을 가지며, 몇 가지 예외는 있지만 모든 Exchange 2013 개체에 대해 거의 모든 작업을 수행할 수 있습니다. 기본적으로 이 역할 그룹의 구성원은 사서함 검색 및 범위가 지정되지 않은 최상위 관리 역할 관리를 수행할 수 없습니다. 자세한 내용은 이 항목의 뒷부분에 있는 "역할 할당만 위임" 섹션을 참조하십시오.


> [!IMPORTANT]
> 조직 관리&nbsp;역할 그룹은 매우 강력한 역할이므로 전체 Exchange&nbsp;조직에 영향을 줄 수 있는 조직 수준의 관리 작업을 수행하는 사용자나 USG(유니버설 보안 그룹)만 이 역할 그룹의 구성원이어야 합니다.



이 역할 그룹은 Exchange Server 2007의 Exchange 조직 관리자 역할에 해당합니다.

RBAC에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.

## 역할 그룹 구성원

기본적으로 조직에 Exchange 2013을 설치하는 데 사용되는 계정은 조직 관리 역할 그룹의 구성원으로 추가됩니다. 그런 다음 이 계정에서 필요에 따라 다른 구성원을 역할 그룹에 추가할 수 있습니다.

이 역할 그룹에서 구성원을 추가 또는 제거하려면 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)를 참조하세요.

기본적으로 Organization Management 역할 그룹의 구성원만 이 역할 그룹에서 구성원을 추가 또는 제거할 수 있습니다. 역할 그룹 대리인을 추가하는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)의 "역할 그룹 대리인 추가 또는 제거" 섹션을 참조하세요.

다음 명령을 사용하여 이 역할 그룹의 구성원인 사용자 또는 USG 목록을 볼 수 있습니다.

```powershell
Get-RoleGroupMember "Organization Management"
```

역할 그룹 구성원에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조하십시오.

## 역할 그룹 사용자 지정

이 역할 그룹에는 기본적으로 관리 역할이 할당됩니다. 포함되는 역할은 "이 역할 그룹에 할당된 관리 역할" 섹션에 나열되어 있습니다. 조직의 필요에 맞게 이 역할 그룹에서 역할 할당을 추가 또는 제거할 수 있습니다.

Exchange 2013에서 제공하는 역할 그룹은 더 세부적인 작업에 맞게 설계되었습니다. 역할 그룹에 역할을 할당하여 역할 그룹 구성원이 역할과 관련된 작업을 수행하도록 설정할 수 있습니다. 예를 들어 저널링 역할을 사용하면 저널링 에이전트 및 저널링 규칙을 관리할 수 있습니다. 역할 그룹에 역할을 할당하는 방법에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참고하세요.

이 역할 그룹에 할당된 역할에는 기본 관리 범위가 지정됩니다. 관리 범위는 역할 그룹 구성원이 보거나 수정할 수 있는 Exchange 개체를 결정합니다. 역할과 역할 그룹 사이의 할당과 관련된 범위를 변경할 수 있습니다. 예를 들어 역할 그룹 구성원이 특정 조직 구성 단위나 특정 위치에 있는 받는 사람만 변경할 수 있도록 하려는 경우 이 기능을 사용할 수 있습니다. 관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참고하세요.

이 역할 그룹의 사용자 지정 방법에 대한 자세한 내용은 다음 항목을 참고하세요.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)

역할 그룹을 만들고 이 역할 그룹에 할당된 일부 역할을 새 역할 그룹에 할당하려는 경우 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)의 "역할 그룹 만들기" 섹션을 참조하세요.

이 역할을 사용자 지정할 수 있는 몇 가지 방법은 다음과 같습니다.

  - **사용 권한 소유자**   Exchange 관리자가 아닌 특정 그룹에서 조직의 사용 권한을 제어하는 경우 역할 그룹을 만들고 역할 관리 역할의 일반 및 위임 역할 할당을 새 역할 그룹으로 이동할 수 있습니다. 이 작업을 수행하면 조직 관리 역할 그룹의 구성원이 RBAC 권한을 관리할 수 없습니다.

  - **Active Directory 사용 권한 분할**   Exchange 관리자가 아닌 특정 그룹에서 사용자 계정 등 조직의 보안 주체 만들기를 제어하는 경우 역할 그룹을 만들고 메일 받는 사람 만들기 역할 및 보안 그룹 만들기 및 구성원 역할의 일반 및 위임 역할 할당을 새 역할 그룹으로 이동할 수 있습니다. 이 작업을 수행하면 조직 관리 역할 그룹의 구성원이 Active Directory 개체를 만들 수 없습니다. 하지만 새로운 Active Directory 개체는 계속 메일을 사용할 수 있습니다. 사용 권한 분할에 대한 자세한 내용은 [분할 권한 이해](understanding-split-permissions-exchange-2013-help.md)를 참조하십시오.

## 사용자 지정 제한

이 역할 그룹에 모든 역할을 추가하거나 제거할 수 있지만 다음과 같은 제한 사항이 있습니다.

  - 이 역할 그룹에서 위임 역할 할당을 제거하려면 모든 역할에 역할 그룹이나 USG에 대한 위임 역할 할당이 하나 이상 있어야 합니다.

  - 이 역할 그룹에서 일반 역할 할당을 제거하려면 모든 역할 관리 역할에 역할 그룹이나 USG에 대한 일반 역할 할당이 하나 이상 있어야 합니다.

이러한 제한은 실수로 자신을 시스템에서 잠글 수 없도록 방지하기 위한 것입니다. 모든 역할과 하나 이상의 역할 그룹 또는 USG 간에 위임 역할 할당이 하나 이상 있어야 하므로 항상 역할 담당자에게 역할을 할당할 수 있습니다. 또한 모든 역할 관리 역할과 하나 이상의 역할 그룹 또는 USG 간에 일반 역할 할당이 하나 이상 있어야 하므로 항상 역할 그룹과 역할 할당을 구성할 수 있습니다.


> [!IMPORTANT]
> 이러한 제한 때문에 역할 그룹이나 USG가 위임 및 일반 역할 할당의 대상이어야 합니다. 관리 역할의 일반 할당이나 위임 역할 할당이 사용자에 대해 남아 있는 마지막 역할 할당이 경우에는 제거할 수 없습니다.



## 위임 전용 역할 할당

조직 관리 역할 그룹과 관리 역할(예: 사서함 검색, 범위가 지정되지 않은 역할 관리) 간의 일부 역할 할당은 위임 전용 역할 할당입니다. 이러한 역할을 사용하면 사서함 콘텐츠 같은 중요한 정보 또는 개인 정보에 액세스하거나 범위가 지정되지 않은 강력한 관리 역할을 만들 수 있습니다.

위임 전용 역할 할당을 사용하면 조직 관리 역할 그룹의 구성원이 연결된 역할을 다른 역할 그룹, 관리 역할 할당 정책, 사용자 또는 USG에 할당할 수만 있습니다. 기본적으로 조직 관리 역할 그룹의 구성원에게 역할이 제공하는 권한은 부여되지 않습니다. 이렇게 하면 실수로 인한 개인 정보 노출이나 권한 상승을 방지할 수 있습니다.

그러나 조직 관리 역할 그룹의 구성원은 자신에게 모든 역할을 할당하여 사실상 모든 작업을 수행할 수 있습니다. 예를 들어 조직 관리 역할 그룹의 구성원이 조직 관리 역할 그룹에 사서함 검색 역할을 할당할 수 있습니다. 이 역할을 할당하면 조직 관리 역할 그룹의 구성원이 사서함 검색 역할에서 허용하는 작업을 수행할 수 있습니다.

위임 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

## 추가 사용 권한

조직 관리 역할 그룹의 구성원에게 부여되는 사용 권한은 주로 역할 그룹에 할당된 관리 역할에 의해 결정됩니다. 하지만 수행해야 할 작업 중 일부가 관리 역할에 포함되지 않습니다. 일부 작업은 Exchange 관리 도구 외부에서 수행되므로 RBAC 권한 모델이 적용되지 않습니다. 이러한 작업의 경우 특정 조직 관리 개체의 ACL(액세스 제어 목록)에 Active Directory 역할 그룹을 추가하여 사용 권한을 제공합니다.

다음 작업은 Active Directory 역할 그룹에 할당된 관리 역할이 아니라 조직 관리 개체의 ACL을 통해 사용 권한이 부여됩니다.

  - Setup.exe를 사용하여 DomainPrep 및 ForestPrep 실행

  - 조직에 추가 서버 배포

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
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Active Directory 권한 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="address-lists-role-exchange-2013-help.md">주소 목록 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="audit-logs-role-exchange-2013-help.md">감사 로그 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Cmdlet 확장 에이전트 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">데이터 손실 방지 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">데이터베이스 가용성 그룹 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="database-copies-role-exchange-2013-help.md">데이터베이스 복사본 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="databases-role-exchange-2013-help.md">데이터베이스 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">재해 복구 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="distribution-groups-role-exchange-2013-help.md">메일 그룹 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Edge 구독 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">전자 메일 주소 정책 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Exchange 커넥터 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Exchange 서버 인증서 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange 서버 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Exchange 가상 디렉터리 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="federated-sharing-role-exchange-2013-help.md">페더레이션된 공유 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="information-rights-management-role-exchange-2013-help.md">정보 권한 관리 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="journaling-role-exchange-2013-help.md">저널링 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="legal-hold-role-exchange-2013-help.md">법적 보존 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="legalholdapplication-role-exchange-2013-help.md">LegalHoldApplication 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">메일 사용 가능 공용 폴더 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mail-recipients-role-exchange-2013-help.md">메일 받는 사람에 게 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mail-tips-role-exchange-2013-help.md">메일 팁 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Mailbox Import Export 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mailbox-search-role-exchange-2013-help.md">사서함 검색 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="message-tracking-role-exchange-2013-help.md">메시지 추적 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="migration-role-exchange-2013-help.md">마이그레이션 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="monitoring-role-exchange-2013-help.md">역할을 모니터링</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">사서함 역할 이동</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-client-access-role-exchange-2013-help.md">조직의 클라이언트 액세스 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="organization-configuration-role-exchange-2013-help.md">조직 구성 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">조직 전송 설정 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">POP3 및 IMAP4 프로토콜 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="public-folders-role-exchange-2013-help.md">공용 폴더 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="receive-connectors-role-exchange-2013-help.md">수신 커넥터 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="recipient-policies-role-exchange-2013-help.md">받는 사람 정책 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">원격 및 허용 도메인 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="reset-password-role-exchange-2013-help.md">암호 역할을 다시 설정</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="retention-management-role-exchange-2013-help.md">보존 관리 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="role-management-role-exchange-2013-help.md">역할 관리 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">보안 그룹 만들기 및 멤버 자격 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="send-connectors-role-exchange-2013-help.md">커넥터 역할을 보내기</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Support Diagnostics 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-agents-role-exchange-2013-help.md">전송 에이전트 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">전송 방역 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="transport-queues-role-exchange-2013-help.md">전송 큐 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="transport-rules-role-exchange-2013-help.md">전송 규칙 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">UM 사서함 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="um-prompts-role-exchange-2013-help.md">UM 음성 안내 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">범위가 지정 되지 않은 역할 관리 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="unified-messaging-role-exchange-2013-help.md">통합된 메시징 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="user-options-role-exchange-2013-help.md">사용자 옵션 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">보기 전용 감사 로그 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">보기 전용 구성 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">보기 전용 받는 사람에 게 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 역할</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">사용자 지정 앱의 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">내 마켓플레이스 앱 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 역할</a></p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

