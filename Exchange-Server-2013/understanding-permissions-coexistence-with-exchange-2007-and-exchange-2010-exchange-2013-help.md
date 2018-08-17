---
title: 'Exchange 2007 및 Exchange 2010 동시 사용 권한이 해: Exchange 2013 Help'
TOCTitle: Exchange 2007 및 Exchange 2010 동시 사용 권한이 해
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54915193
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2007 및 Exchange 2010 동시 사용 권한이 해

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

기존 Exchange Server 2010 또는 Microsoft Exchange Server 2007 조직에 Microsoft Exchange Server 2013을 설치할 때는 새 조직에서 사용 권한이 작동하는 방식을 이해해야 합니다. 아래에서 사용자의 조직에 해당하는 섹션을 읽어 보십시오.

  - Installing Exchange 2013 into an existing Exchange 2010 organization

  - Installing Exchange 2013 into an existing Exchange 2007 organization

## 기존 Exchange 2010 조직에 Exchange 2013 설치

Exchange 2013 Exchange 2010 에 사용 되는 동일한 액세스 제어 RBAC (역할 기반) 사용 권한 모델을 사용 합니다. 기존 Exchange 2010 조직에 Exchange 2013 를 설치 하는 경우 동일한 관리 역할 그룹, 관리 역할 및 관리 범위 Exchange 2013 및 Exchange 2010 서버와 받는 사람 모두에 적용 됩니다. 역할 그룹 또는 역할에 할당 된 사용자 그룹의 구성원은 모든 Exchange 2013 또는 Exchange 2013 서버 또는 역할 그룹 또는 역할의 범위에 포함 된 받는 사람 관리할 수 있습니다. 조직에서 범위를 사용 하지 않는 받는 사람 및 Exchange 2010과 Exchange 2013 서버를 관리 하 여 기존 역할 그룹의 구성원을 사용할 경우에 다른 작업을 수행할 필요가 없습니다. 이러한 관리자가 조직에 추가 되는 받는 사람 및 Exchange 2013 서버를 관리할 수 없게 됩니다. 권한 작동 방법 Exchange 2010과 Exchange 2013에 대 한 미리 알림을 필요 하면 [사용 권한](permissions-exchange-2013-help.md)를 참조 하십시오.

새 조직에서는 Exchange 2010 및 Exchange 2013 서버와 받는 사람 관리를 분리할 수 있습니다. 즉, Exchange 2010 서버 및 받는 사람을 관리하는 관리자 그룹은 Exchange 2013 서버 및 받는 사람을 관리하지 못할 수도 있고 Exchange 2013 관리자 그룹은 Exchange 2010 서버 및 받는 사람을 관리하지 못할 수도 있습니다. 이 경우에는 관리 범위를 사용하여 각 관리자 그룹이 관리할 수 있는 서버와 받는 사람을 정의할 수 있습니다. 원하는 범위를 만든 후에는 기존 역할 그룹을 복사하고 각 그룹의 구성원으로 포함할 관리자를 추가한 다음 해당 역할 그룹에 범위를 추가할 수 있습니다. 작업을 완료하면 각 역할 그룹의 구성원은 해당 범위와 일치하는 서버와 받는 사람만 관리할 수 있습니다.

역할 그룹, 범위, 역할 그룹 복사 및 역할 그룹에 범위를 추가하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

## 기존 Exchange 2007 조직에 Exchange 2013 설치

Exchange 2013에는 Microsoft Exchange Server 2007에서 사용된 Active Directory ACE(액세스 제어 항목) 기반 권한 부여 모델을 대체하는 RBAC(역할 기반 액세스 제어) 권한이 포함되어 있습니다. RBAC는 대부분의 Exchange 2013 관리에 사용되는 권한 부여 메커니즘입니다. 이 메커니즘에는 다음과 같은 관리 영역이 포함됩니다.

  - Exchange 관리 셸

  - EAC(Exchange 관리 센터)

  - Exchange 웹 서비스

Exchange 2013과 Exchange 2007 간 동시 사용을 계획하는 방법에 대한 자세한 내용은 [Exchange 2007에서 Exchange 2013으로 업그레이드](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)를 참조하십시오.

사용 권한과 관련된 관리 작업에 대한 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md)을 참조하십시오.

## Exchange 2013 사용 권한

Exchange 2013 RBAC 권한 모델은 여러 관리 역할 중 하나가 할당된 관리 역할 그룹으로 구성됩니다. 관리 역할에는 Exchange 조직에서 관리자가 작업을 수행할 수 있는 권한이 포함되어 있습니다. 관리자는 역할 그룹의 구성원으로 추가되고 해당 역할이 제공하는 모든 사용 권한을 부여받습니다. 다음 표에서는 역할 그룹의 예, 역할 그룹에 할당된 몇 가지 역할, 역할 그룹의 구성원이 될 수 있는 사용자 유형에 대한 설명을 제공합니다.

### Exchange 2013의 역할 그룹 및 역할의 예

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할 그룹</th>
<th>관리 역할</th>
<th>이 역할 그룹의 구성원</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직 관리</p></td>
<td><p>이 역할 그룹에 할당된 역할 중 일부는 다음과 같습니다.</p>
<ul>
<li><p>주소 목록</p></li>
<li><p>Exchange Servers</p></li>
<li><p>저널링</p></li>
<li><p>메일 받는 사람</p></li>
<li><p>공용 폴더</p></li>
</ul></td>
<td><p>전체 Exchange 2013 조직을 관리하는 사용자는 이 역할 그룹의 구성원이어야 합니다. 몇 가지 예외를 제외하면 이 역할 그룹의 구성원은 Exchange 2013 조직의 거의 모든 측면을 관리할 수 있습니다.</p>
<p>기본적으로 Exchange 2013용 Active Directory를 준비하는 데 사용되는 사용자 계정은 이 역할 그룹의 구성원입니다.</p>
<p>이 역할 그룹에 대한 자세한 내용과 이 역할 그룹에 할당된 역할의 전체 목록은 <a href="organization-management-exchange-2013-help.md">조직 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>Organization Management만 보기</p></td>
<td><p>이 역할 그룹에 할당된 역할은 다음과 같습니다.</p>
<ul>
<li><p>모니터링</p></li>
<li><p>보기 전용 구성</p></li>
<li><p>보기 전용 받는 사람</p></li>
</ul></td>
<td><p>전체 Exchange 2013 조직의 구성을 확인하는 사용자는 이 역할 그룹의 구성원이어야 합니다. 이러한 사용자는 서버 구성, 받는 사람 정보를 보고 조직 또는 받는 사람 구성을 변경할 수 있는 기능 없이도 모니터링 기능을 수행할 수 있어야 합니다.</p>
<p>이 역할 그룹에 대한 자세한 내용은 <a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>Recipient Management</p></td>
<td><p>이 역할 그룹에 할당된 역할은 다음과 같습니다.</p>
<ul>
<li><p>메일 그룹</p></li>
<li><p>메일 사용 가능 공용 폴더</p></li>
<li><p>메일 받는 사람 만들기</p></li>
<li><p>메일 받는 사람</p></li>
<li><p>메시지 추적</p></li>
<li><p>마이그레이션</p></li>
<li><p>사서함 이동</p></li>
<li><p>받는 사람 정책</p></li>
</ul></td>
<td><p>Exchange 2013 조직에서 사서함, 연락처, 메일 그룹과 같은 받는 사람을 관리하는 사용자는 이 역할 그룹의 구성원이어야 합니다. 이러한 사용자는 받는 사람을 만들거나, 기존의 받는 사람을 수정 또는 삭제하거나 사서함을 이동할 수 있습니다.</p>
<p>이 역할 그룹에 대한 자세한 내용과 이 역할 그룹에 할당된 역할의 전체 목록은 <a href="recipient-management-exchange-2013-help.md">Recipient Management</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>서버 관리</p></td>
<td><p>이 역할 그룹에 할당된 역할 중 일부는 다음과 같습니다.</p>
<ul>
<li><p>데이터베이스</p></li>
<li><p>Exchange 커넥터</p></li>
<li><p>Exchange Server</p></li>
<li><p>수신 커넥터</p></li>
<li><p>전송 큐</p></li>
</ul></td>
<td><p>수신 커넥터, 인증서, 데이터베이스, 가상 디렉터리와 같은 Exchange 서버 구성을 관리하는 사용자는 이 역할 그룹의 구성원이어야 합니다. 이러한 사용자는 Exchange 서버 구성을 수정하고, 데이터베이스를 만들고, 전송 큐를 다시 시작 및 조작할 수 있습니다.</p>
<p>이 역할 그룹에 대한 자세한 내용과 이 역할 그룹에 할당된 역할의 전체 목록은 <a href="server-management-exchange-2013-help.md">Server 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>검색 관리</p></td>
<td><p>이 역할 그룹에 할당된 역할은 다음과 같습니다.</p>
<ul>
<li><p>법적 보유</p></li>
<li><p>사서함 검색</p></li>
</ul></td>
<td><p>법적 절차를 지원하거나 법적 보유를 구성하기 위해 사서함 검색을 수행하는 사용자는 이 역할 그룹의 구성원이어야 합니다.</p>
<p>다음은 법률 부서 직원과 같은 비 Exchange 관리자를 포함할 수 있는 역할 그룹의 예입니다. 법률 담당자가 Exchange 관리자의 개입 없이 작업을 수행할 수 있습니다.</p>
<p>이 역할 그룹에 대한 자세한 내용과 이 역할 그룹에 할당된 역할의 전체 목록은 <a href="discovery-management-exchange-2013-help.md">검색 관리</a>를 참조하십시오.</p></td>
</tr>
</tbody>
</table>


이 표에서는 Exchange 2013이 관리자에게 부여된 사용 권한을 세부적으로 제어할 수 있는 기능을 제공함을 보여줍니다. Exchange 2013의 12개 역할 그룹 중에서 선택할 수 있습니다. 역할 그룹과 역할 그룹이 제공하는 사용 권한의 전체 목록은 [기본 제공 역할 그룹](built-in-role-groups-exchange-2013-help.md)을 참조하십시오.

Exchange 2013 많은 역할 그룹을 제공 하 고 Active Directory 개체에 대 한 액세스 제어 조작 목록 (Acl) 이기 때문에 추가로 사용자 지정 가능한 다른 역할을 함께 포함 하는 역할 그룹을 만들어 때문에 더이상 필요 하지 하 고 영향을 주지 않습니다. Acl 더이상 개별 관리자 또는 Exchange 2013 의 그룹에 사용 권한을 적용할 사용 합니다. 사서함을 만들거나 사용자는 사서함에 액세스 하는 관리자와 같은 모든 작업을 RBAC에 의해 관리 됩니다. RBAC 작업 권한을 부여 하 고 Exchange 허용 되는 경우 사용자를 대신 하 여 작업을 수행 하는 다음 합니다. Exchange (USG) Exchange 신뢰할 수 있는 하위 시스템 유니버설 보안 그룹에서 작업을 수행 합니다. 일부 예외 사항과 함께 Active Directory 의 개체에 대 한 모든 Acl 해당 Exchange 2010 에 대 한 액세스 Exchange 신뢰할 수 있는 하위 시스템 USG 부여 됩니다. 이것이 Exchange 2007 에서 사용 권한을 처리 되는 방식에서 근본적으로 변경 합니다.

Active Directory의 사용자에게 부여된 사용 권한은 사용자가 Exchange 2013 관리 도구를 사용할 때 RBAC에서 사용자에게 부여한 사용 권한과는 별개입니다.

RBAC에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.

## Exchange 2007 사용 권한

Exchange 2007 관리 모델은 Active Directory 포리스트를 활용하여 보안 경계를 정의합니다. 특정 포리스트 내에는 보안 사용 권한 격리가 없습니다. 포리스트 소유자 및 엔터프라이즈 관리자는 도메인의 모든 리소스에 대한 액세스 권한을 항상 얻을 수 있습니다. Exchange 2007에서는 일시적으로만 엔터프라이즈 관리자 권한 및 최상위 도메인 관리자 권한을 부여해야 할 수 있습니다.

Exchange 2007은 다음과 같은 미리 정의된 관리자 역할을 제공합니다.

  - **Exchange 조직 관리자 역할**   이 역할은 Exchange 2007 조직의 모든 측면을 제어할 수 있는 사용 권한을 부여합니다. 또한 이 역할이 있는 관리자는 다른 Exchange 관리자에게 사용 권한을 부여할 수 있습니다. 이 역할은 Exchange 2007을 설치하는 데 사용하는 계정에 부여됩니다.

  - **보기 권한만 있는 Exchange 관리자 역할**   이 역할은 Exchange 구성을 볼 수 있는 사용 권한을 부여합니다. 하지만 이 역할이 있는 관리자는 Exchange 2007 조직의 개체를 수정할 수 없습니다.

  - **Exchange 받는 사람 관리자 역할**   이 역할은 전자 메일 받는 사람을 관리할 수 있는 사용 권한을 부여합니다. 이 역할이 있는 관리자는 사용자, 그룹, 연락처 및 메일 그룹에 대한 Exchange 관련 항목을 수정할 수 있습니다.

  - **Exchange Server 관리자 역할**   이 역할은 특정 서버를 관리할 수 있는 사용 권한을 부여합니다. 하지만 이 역할은 Exchange 2007 조직 전체에 영향을 주는 작업을 수행할 수 있는 사용 권한을 부여하지 않습니다.

  - **Exchange 공용 폴더 관리자 역할**   이 역할은 Exchange 2007 서비스 팩 1에 추가되었습니다**.** 이 역할은 Exchange 2007 조직의 공용 폴더를 관리할 수 있는 사용 권한을 부여합니다.

이 권한 모델은 Exchange Server 관리자 역할을 제외한 모든 역할에 USG를 사용합니다. Exchange 2007**Setup /PrepareAD** 명령을 실행하면 설치 프로그램이 루트 도메인에서 USG를 만들고 USG에 포리스트 전체 범위를 제공합니다. USG에는 Active Directory에서 Exchange 개체를 관리할 수 있는 ACL이 할당됩니다.

Exchange 2007에서는 관리자에게 여러 역할을 할당하여 관리자를 구분할 수 있습니다. 사용 권한이 사용자 또는 해당 사용자가 구성원인 USG에 직접 할당됩니다. 사용자가 수행한 작업이 사용자의 Active Directory 계정의 컨텍스트에서 수행됩니다. 다음 표에서는 Exchange 2007 관리자 역할 및 Exchange 관련 사용 권한의 목록을 함께 보여줍니다.

### Exchange 2007 관리자 역할

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>관리자 역할</th>
<th>구성원</th>
<th>소속 그룹</th>
<th>Exchange 사용 권한</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 조직 관리자</p></td>
<td><p>처음 Exchange 2007 서버를 설치하는 데 사용한 계정 또는 관리자 계정</p></td>
<td><p>Exchange 받는 사람 관리자</p>
<p><em>&lt;서버 이름&gt;</em>에 대한 관리자 로컬 그룹</p></td>
<td><p>Active Directory의 Microsoft Exchange 컨테이너에 대한 전체 사용 권한</p></td>
</tr>
<tr class="even">
<td><p>Exchange 보기 권한만 있는 관리자</p></td>
<td><p>Exchange 받는 사람 관리자</p>
<p>Exchange Server 관리자(<em>&lt;서버 이름</em>&gt;)</p></td>
<td><p>Exchange Recipient Administrators</p>
<p>Exchange Server 관리자</p></td>
<td><p>Active Directory의 Microsoft Exchange 컨테이너에 대한 읽기 권한</p>
<p>Exchange 받는 사람이 있는 모든 Windows 도메인에 대한 읽기 권한</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Recipient Administrator</p></td>
<td><p>Exchange 조직 관리자</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>Active Directory 사용자 개체의 Exchange 속성에 대한 권한</p></td>
</tr>
<tr class="even">
<td><p>Exchange 서버 관리자</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Exchange View-Only Administrators</p>
<p><em>&lt;서버 이름</em>&gt;에 대한 관리자 로컬 그룹</p></td>
<td><p>Exchange <em>&lt;서버 이름</em>&gt;에 대한 모든 권한</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>각 Exchange 2007 컴퓨터 계정</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>특별 권한</p></td>
</tr>
<tr class="even">
<td><p>Exchange 공용 폴더 관리자</p></td>
<td><p>Exchange Organization Administrators</p></td>
<td><p>Exchange View-Only Administrators</p></td>
<td><p>모든 공용 폴더를 관리할 수 있는 모든 권한(최상위 공용 폴더 만들기 확장 권한이 부여됨)</p></td>
</tr>
</tbody>
</table>


보다 세분화된 사용 권한을 할당해야 하는 경우 주소 목록 또는 데이터베이스 등의 개별 Exchange 2007 개체에서 ACL을 수정할 수 있습니다. 사용자 또는 사용자가 속해 있는 보안 그룹을 ACL에 직접 추가해야 합니다. 그러면 특정 사용자의 컨텍스트에서 작업이 수행됩니다.

Exchange 2007에서 사용 권한을 관리하는 방법에 대한 자세한 내용은 [Exchange Server 2007에서 사용 권한 구성](http://go.microsoft.com/fwlink/p/?linkid=90671)을 참조하십시오.

## Exchange 2013과 Exchange 2007의 동시 사용 권한

Exchange 2013에 대한 권한 모델과 Exchange 2007에 대한 권한 모델은 서로 다르므로 Exchange 2013 사용 권한 할당은 Exchange 2007 사용 권한 할당과 다릅니다. 두 버전의 Exchange를 동일한 포리스트에 설치한 경우에도 마찬가지입니다. 추가 구성을 하지 않으면 Exchange 2013 관리자에게는 Exchange 2007 기반 서버를 관리하는 데 필요한 사용 권한이 없으며 Exchange 2007 관리자에게는 Exchange 2013 기반 서버를 관리하는 데 필요한 사용 권한이 없습니다. 다음 질문을 고려해야 합니다.

  - Exchange 2013 관리자에게 Exchange 2007 서버를 관리할 수 있는 액세스 권한을 부여하시겠습니까?

  - Exchange 2007 관리자에게 Exchange 2013 서버를 관리할 수 있는 액세스 권한을 부여하시겠습니까?

  - Exchange 2007 ACL에 적용된 모든 사용자 지정과 일치되도록 Exchange 2013 사용 권한을 사용자 지정하시겠습니까?

## Exchange 2007 관리자에게 Exchange 2013 사용 권한 부여

Exchange 2007 관리자가 Exchange 2013 서버를 관리하도록 하려면 Exchange 2007 관리자가 하나 이상의 Exchange 2013 역할 그룹에 구성원으로 추가되어야 합니다. 사용자 또는 USG를 역할 그룹에 추가할 수 있습니다. 역할 그룹에 부여된 사용 권한은 구성원으로 추가한 사용자 또는 USG에 적용됩니다.


> [!IMPORTANT]
> 도메인 로컬 또는 글로벌 Active Directory 보안 그룹을 사용하는 경우 이 그룹을 Exchange 2013 역할 그룹의 구성원으로 추가하려면 USG로 변경해야 합니다. Exchange 2013은 USG만 지원합니다.



다음 표에서는 Exchange 2007 관리자 역할과 Exchange 2013 역할 그룹 간의 매핑을 설명합니다.

### Exchange 2007 관리자 역할 및 Exchange 2010 역할 그룹

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 2007 관리자 역할</th>
<th>Exchange 2013 역할 그룹</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Organization Administrator</p></td>
<td><p>조직 관리</p></td>
</tr>
<tr class="even">
<td><p>Exchange Recipient Administrator</p></td>
<td><p>Recipient Management</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server Administrator</p></td>
<td><p>Server Management</p></td>
</tr>
<tr class="even">
<td><p>Exchange View-Only Administrator</p></td>
<td><p>Organization Management만 보기</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Exchange 2013에 해당 역할 그룹 없음</p>
<p>사용자 지정 역할 그룹을 만드는 방법에 대한 자세한 내용은 <a href="manage-role-groups-exchange-2013-help.md">역할 그룹 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>Exchange Public Folder Administrator</p></td>
<td><p>공용 폴더 관리</p></td>
</tr>
</tbody>
</table>


모든 Exchange 2007 관리자가 Exchange 2007 관리 역할 중 하나의 구성원인 경우 각 관리 그룹의 구성원을 해당 Exchange 2013 역할 그룹에 추가할 수 있습니다. 예를 들어 모든 Exchange 2007 조직 관리자에게 Exchange 2013 개체에 대한 모든 권한을 부여하려는 경우 Exchange 조직 관리자 USG를 조직 관리 역할 그룹에 추가합니다.

사용자와 USG를 역할 그룹에 추가하는 방법에 대한 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)를 참조하십시오.

Exchange 2007 관리자에게 보다 세분화된 사용 권한을 부여하기 위해 Exchange 2007 개체의 ACL을 수정하는 경우 해당 관리자에게 Exchange 2013 서버와 유사한 사용 권한을 할당하려면 다음 단계를 수행합니다.

1.  Exchange 2007 개체에 지정한 ACL 사용자 지정을 검토하고 각 개체에 대한 사용 권한을 부여받은 관리자를 찾습니다.

2.  각 Exchange 2007 개체를 분류합니다. 예를 들어 개체가 데이터베이스, 서버 또는 받는 사람 개체인지 결정합니다.

3.  개체를 해당 Exchange 2013 역할 그룹에 매핑합니다. 기본 제공 역할 그룹 목록을 보려면 [기본 제공 역할 그룹](built-in-role-groups-exchange-2013-help.md)을 참조하십시오.

4.  각 개체 유형의 USG 또는 사용자를 해당 Exchange 2013 역할 그룹에 추가합니다. 사용자와 USG를 역할 그룹에 추가하는 방법에 대한 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)를 참조하십시오.

해당 단계를 완료하면 Exchange 2007 관리자는 해당 Exchange 2013 개체에 매핑되는 특정 역할 그룹의 구성원이 됩니다. Exchange 2007 관리자는 Exchange 2013 관리 도구를 사용하여 Exchange 2013 서버와 받는 사람을 관리할 수 있습니다.


> [!IMPORTANT]
> 일반적으로 Exchange 2007 서버와 받는 사람은 Exchange 2007 관리 도구를 사용하여 관리하고, Exchange 2013 서버와 받는 사람은 Exchange 2013 관리 도구를 사용하여 관리해야 합니다.



기본 제공 역할 그룹에서 제공하지 않는 특정 권한 집합을 몇몇 관리자에게 부여하려는 경우 사용자 지정 역할 그룹을 만들 수 있습니다. 사용자 지정 역할 그룹을 만들면 역할 그룹에 추가할 역할을 선택할 수 있습니다. 역할 그룹의 구성원에게 관리하도록 할 특정 기능을 정의할 수 있습니다. 예를 들어, 관리자가 메일 그룹만 관리하도록 하려면 사용자 지정 역할 그룹을 만들고 메일 그룹 역할을 선택하면 됩니다. 이렇게 하면 해당 사용자 지정 역할 그룹의 구성원은 메일 그룹만 관리할 수 있습니다. 사용자 지정 역할 그룹을 만드는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조하십시오.

관리자에게 특정 데이터베이스만 관리하도록 허용하는 등 특정 Exchange 2007 개체에 선택적 사용 권한을 부여하는 경우 동일한 구성을 Exchange 2013 서버에 적용하려면 이 항목의 뒷부분에 나오는 "Exchange 2013의 관리 범위를 사용하여 Exchange 2007 ACL 사용자 지정 다시 만들기"를 참조하십시오.

## Exchange 2013 관리자에게 Exchange 2007 사용 권한 부여

Exchange 2013 관리자가 Exchange 2007 서버를 관리하도록 하려면 Exchange 2013 관리자를 USG 또는 특정 Exchange 2007 관리자 역할에 해당하는 보안 그룹에 추가합니다. 또는 사용자 지정된 ACL 설정이 있는 경우 관리자를 해당 ACL에 추가합니다. 역할 그룹은 USG이므로 역할 그룹은 Exchange 2007 관리자 역할 USG에 직접 추가할 수 있습니다.

완료 후 Exchange 2013 관리자는 해당 Exchange 2007 관리자 역할의 구성원이 됩니다. Exchange 2013 관리자는 Exchange 2007 관리 도구를 사용하여 Exchange 2007 서버와 받는 사람을 관리할 수 있습니다.

## Exchange 2013의 관리 범위를 사용하여 Exchange 2007 ACL 사용자 지정 다시 만들기

Exchange 2007에서는 특정 사서함 저장소 또는 특정 사용자를 관리하거나 사서함이 만들어지는 사서함 저장소를 제어할 수 있는 사람을 제한하려면 제한할 개체의 ACL을 수정해야 합니다. Exchange 2013은 동일한 기능을 제공하지만 ACL을 수정할 필요가 없습니다. RBAC의 구성 요소인 관리 범위를 사용하여 이 작업을 수행할 수 있습니다.

관리 범위는 관리자가 관리할 수 있는 개체를 정의하기 위한 기본 제공 범위와 사용자 지정 범위를 제공합니다. 관리 범위를 적용하여 관리 가능한 받는 사람, 사서함을 만들 수 있는 사서함 데이터베이스, 소규모 관리자 그룹이 관리하거나 아무도 관리해서는 안 되는 받는 사람 또는 서버를 정의할 수 있습니다.

다음과 같은 유형의 관리 범위를 만들 수 있습니다.

  - **미리 정의된 상대**   미리 정의된 상대 범위가 Exchange 2013에 포함되어 있습니다. 사용자가 보고 수정할 수 있는 항목을 제어할 수 있습니다. 예를 들어, 미리 정의된 상대 범위를 통해 사용자에게 본인에 대한 정보만 표시할지 또는 전체 조직에 대한 정보를 표시할지를 제어할 수 있습니다.

  - **받는 사람**   받는 사람 범위는 관리자가 생성, 수정 또는 삭제할 수 있는 받는 사람을 제어합니다. 이러한 선택 항목은 OU(조직 구성 단위), 받는 사람 필터 또는 둘 다를 기준으로 할 수 있습니다. 받는 사람 필터는 받는 사람이 범위에 포함되려면 일치해야 하는 기준을 지정합니다. 예를 들어, 특정 위치 또는 특정 부서의 모든 사용자를 포함하는 받는 사람 필터 범위를 만들 수 있습니다. OU와 받는 사람 필터를 결합하여 특정 OU 내의 사용자와 특정 관리자에게 보고하는 사용자만 일치시킬 수 있습니다.

  - **서버**   서버 범위는 관리자가 관리할 수 있는 서버를 제어합니다. 서버 목록 또는 서버 필터를 지정할 수 있습니다. 서버 목록에 대한 관리할 수 있는 서버의 정적 목록을 정의합니다. 서버 필터는 일치시켜야 하는 조건을 지정할 수 있다는 점에서 받는 사람 필터와 같은 방식으로 작동합니다. 예를 들어, 특정 Active Directory 사이트 내의 모든 서버를 일치시키는 서버 범위를 만들 수 있습니다.

  - **데이터베이스**   데이터베이스 범위는 관리자가 관리할 수 있는 데이터베이스를 제어합니다. 또한 만들 수 있는 데이터베이스 사서함이나 이동할 수 있는 데이터베이스 사서함을 제어할 수 있습니다. 서버 범위와 마찬가지로 목록 또는 필터로 정의될 수 있습니다. 예를 들어, 관리자가 특정 지사에 의해 관리되는 특정 사서함 데이터베이스에 사서함을 만들거나 이동할 수 있도록 하는 목록 또는 필터를 만들 수 있습니다.

  - **배타적**   받는 사람, 서버 및 데이터베이스 범위를 배타적 범위로 만들 수도 있습니다. 배타적 범위는 ACL의 액세스 거부 ACE와 동일한 방식으로 작동합니다. 배타적 범위와 일치하는 모든 항목은 배타적 범위가 할당된 관리자만 해당 개체를 관리할 수 있습니다. 배타적이지 않은 다른 범위가 동일한 개체와 일치하는 경우도 마찬가지입니다. 이 기능은 신뢰할 수 있는 몇몇 개인에게만 임원의 사서함을 관리할 수 있게 하려는 경우 특히 유용합니다. 다른 일반 받는 사람 범위가 더 넓고 임원의 사서함이 이 범위에 포함된 경우에도 배타적 범위에 할당되지 않는 한 더 넓은 일반 받는 사람 범위에 할당된 관리자가 임원의 사서함을 관리할 수 없습니다.

관리 범위는 관리 역할, 관리 역할 할당, 관리 역할 그룹과 함께 사용하여 누가 어떤 개체를 관리할 수 있는지와 해당 개체를 관리할 수 있는 방식을 제어합니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [배타적 범위 이해 (영문)](understanding-exclusive-scopes-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

  - [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)

  - [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)

사용자 지정된 ACL을 사용하여 정의한 관리 범위를 사용해 Exchange 2013에 동일한 권한 모델을 만들려면 사용자 지정한 ACL 목록을 만들고 이와 일치하는 관리 범위를 만들어야 합니다. 받는 사람, 서버, 데이터베이스 개체에 사용 가능한 필터링할 수 있는 속성을 이용해 각 관리 범위에서 액세스를 제어할 개체를 포함하는 관리 범위를 만들 수 있습니다. 관리 범위 필터와 함께 사용할 수 있는 속성에 대한 자세한 내용은 [관리 역할 범위 필터 이해 (영문)](understanding-management-role-scope-filters-exchange-2013-help.md)를 참조하십시오.

관리 범위를 만드는 방법에 대한 자세한 내용은 [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)를 참조하십시오.

