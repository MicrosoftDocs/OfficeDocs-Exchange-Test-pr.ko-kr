---
title: 'Exchange 및 셸 인프라 권한: Exchange 2013 Help'
TOCTitle: Exchange 및 셸 인프라 권한
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 50482844
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 및 셸 인프라 권한

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Microsoft Exchange Server 2013의 여러 구성 요소에 대해 구성 작업을 수행하는 데 필요한 권한은 수행되는 절차나 실행하려는 cmdlet에 따라 달라집니다. 해당 기능에 대한 자세한 내용은 이 항목의 각 섹션을 참조하십시오.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.


> [!NOTE]
> 일부 기능의 경우 관리하려는 서버에 대한 로컬 관리자 권한이 필요할 수도 있습니다. 이러한 기능을 관리하려면 해당 서버에서 로컬 관리자 그룹의 구성원이어야 합니다.



## Exchange 인프라 권한

다음 표에서는 일반적인 Exchange 2013 설정의 구성 작업을 수행하는 데 필요한 권한을 보여 줍니다.

보기 전용 관리 역할 그룹이 할당된 사용자는 다음 표에 있는 기능의 구성을 볼 수 있습니다. 자세한 내용은 [보기 전용 조직 관리](view-only-organization-management-exchange-2013-help.md)를 참조하세요.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>필요한 권한</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>관리자 감사 로깅</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 관리 센터 구성 설정</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 관리 센터 연결</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 서버 구성 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 도움말 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>메시지 범주</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>제품 키</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>시스템 상태 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>보기 전용 관리자 감사 로깅</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p>

> [!NOTE]
> 보기 전용 감사 로그 관리 역할을 관리 역할 그룹에 수동으로 할당할 수도 있습니다. 자세한 내용은 <A href="view-only-audit-logs-role-exchange-2013-help.md">보기 전용 감사 로그 역할</A>를 참조하십시오.


</td>
</tr>
<tr class="even">
<td><p>감사 로그에 쓰기</p></td>
<td><p>역할 그룹 구성원이거나 관리 역할이 할당된 사용자는 관리자 감사 로그에 쓸 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 셸 인프라 권한

다음 표에서는 Exchange 관리 셸이 실행되는 방식을 제어하는 기능의 구성 작업을 수행하는 데 필요한 권한을 보여 줍니다.

보기 전용 관리 역할 그룹이 할당된 사용자는 다음 표에 있는 기능의 구성을 볼 수 있습니다. 자세한 내용은 [보기 전용 조직 관리](view-only-organization-management-exchange-2013-help.md)를 참조하세요.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>필요한 권한</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Active Directory 도메인 서비스 서버 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>cmdlet 확장 에이전트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>PowerShell 가상 디렉터리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>PowerShell 및 WinRM 설치</p></td>
<td><p>로컬 서버 관리자</p></td>
</tr>
<tr class="odd">
<td><p>원격 셸</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


## 페더레이션 및 인증서 권한

다음 표에서는 페더레이션 트러스트, OAuth 구성, 인증서 관리 및 하이브리드 배포 구성과 관련된 작업 수행에 필요한 권한을 보여 줍니다.

보기 전용 관리 역할 그룹이 할당된 사용자는 다음 표에 있는 기능의 구성을 볼 수 있습니다. 자세한 내용은 [보기 전용 조직 관리](view-only-organization-management-exchange-2013-help.md)를 참조하세요.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>필요한 권한</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인증서 관리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>페더레이션 트러스트, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>페더레이션 트러스트 테스트, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>하이브리드 배포 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>조직 내 커넥터</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
</tbody>
</table>

