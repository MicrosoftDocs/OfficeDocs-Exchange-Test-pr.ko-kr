---
title: '메시징 정책 및 규정 준수 권한: Exchange 2013 Help'
TOCTitle: 메시징 정책 및 규정 준수 권한
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 50484439
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시징 정책 및 규정 준수 권한

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

메시징 정책 및 규정 준수를 구성하는 데 필요한 권한은 수행하는 절차 또는 실행하려는 cmdlet에 따라 달라집니다. 메시징 정책 및 규정 준수에 대한 자세한 내용은 [메시징 정책 및 규정 준수](messaging-policy-and-compliance-exchange-2013-help.md)를 참조하십시오.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.


> [!NOTE]
> 관리하고자 하는 일부 기능은 Edge 전송 서버에 존재할 수 있습니다. Edge 전송 서버에서 기능을 관리하려면 관리할 Edge 전송 서버에서 로컬 관리자 그룹의 구성원이 되어야 합니다. Edge 전송 서버는 RBAC(역할 기반 액세스 제어)를 사용하지 않습니다. Edge 전송 서버에서 관리할 수 있는 기능은 아래 표의 "필요한 사용 권한" 열에 Edge 전송 로컬 관리자로 표시되어 있습니다.



## 메시징 정책 및 규정 준수 권한

다음 표의 기능을 사용하여 메시징 정책 및 규정 준수 기능을 구성할 수 있습니다. 각 기능을 구성하는 데 필요한 역할 그룹이 나열되어 있습니다.

View-Only Management 역할 그룹이 할당된 사용자는 다음 표에 있는 기능의 구성을 볼 수 있습니다. 자세한 내용은 [보기 전용 조직 관리](view-only-organization-management-exchange-2013-help.md)를 참조하십시오.


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
<td><p>DLP(데이터 손실 방지)</p></td>
<td><p>Office 365를 사용하는 경우:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 전역 관리자</a>, 자동으로 Exchange <a href="organization-management-exchange-2013-help.md">조직 관리</a> 를 포함 하는</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 서비스 관리자</a>, Exchange의 <a href="organization-management-exchange-2013-help.md">조직 관리</a> 관리 역할 그룹 plus</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Office 365 암호 관리자</a></p></li>
</ul>
<p>Exchange Server 2013 또는 Exchange Online만 사용하는 경우:</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>사서함 콘텐츠 삭제(<a href="https://technet.microsoft.com/ko-kr/library/dd298173(v=exchg.150)">Search-Mailbox</a> cmdlet을 <em>DeleteContent</em> 스위치와 함께 사용하여)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">검색 관리</a> <strong>및</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">Mailbox Import Export 역할</a></p>

> [!NOTE]
> 기본적으로 사서함 가져오기 내보내기 역할이 역할 그룹에 할당되어 있지 않습니다. 기본 제공 또는 사용자 지정 역할 그룹, 사용자 또는 유니버설 보안 그룹에 관리 역할을 할당할 수 있습니다. 역할 그룹에 역할을 할당하는 것이 좋습니다. 자세한 내용은 <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">사용자 또는 USG에는 역할을 추가 합니다.</A>를 참조하십시오.


</td>
</tr>
<tr class="odd">
<td><p>검색 사서함 - 만들기</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>저널링</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 감사 로깅</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>메시지 분류</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>메시징 레코드 관리</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p>
<p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>원본 위치 eDiscovery</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">검색 관리</a></p>

> [!NOTE]
> 기본적으로 Discovery Management 역할 그룹에는 구성원이 없습니다. 관리자를 포함한 사용자에게 사서함을 검색하는 데 필요한 권한이 없습니다. 자세한 내용은 <A href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions">Exchange eDiscovery 사용 권한 할당</A>를 참조하십시오.


</td>
</tr>
<tr class="odd">
<td><p>원본 위치 유지</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">검색 관리</a></p>
<p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>

> [!IMPORTANT]
> 쿼리 기반 원본 위치 유지를 만들려면 사용자에게 사서함 검색 및 소송 보존 역할이 이러한 두 역할이 할당된 역할 그룹의 구성원을 통해 또는 직접 할당되어야 합니다. 쿼리를 사용하지 않고 모든 사서함을 보류 상태로 유지하는 원본 위치 유지를 만들려면 소송 보존 역할이 할당되어야 합니다. Discovery Management 역할 그룹에는 두 역할이 모두 할당됩니다.<BR>Organization Management 역할 그룹에는 소송 보존 역할이 할당됩니다. Organization Management 역할 그룹의 구성원은 사서함의 모든 항목에 원본 위치 유지를 적용할 수 있지만 쿼리 기반 원본 위치 유지를 만들 수는 없습니다.


</td>
</tr>
<tr class="even">
<td><p>원본 위치 보관</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>원본 위치 보관 - 연결 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>IRM(정보 권한 관리) 구성</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p>
<p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>보존 정책 - 적용</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>보존 정책 - 만들기</p></td>
<td><p>메시징 레코드 관리 항목 참조</p></td>
</tr>
<tr class="odd">
<td><p>전송 규칙</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
</tbody>
</table>

