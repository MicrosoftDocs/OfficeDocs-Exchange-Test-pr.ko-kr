---
title: '메일 흐름 사용 권한: Exchange 2013 Help'
TOCTitle: 메일 흐름 사용 권한
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 50484546
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 흐름 사용 권한

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

메일 흐름과 관련된 작업을 수행하는 데 필요한 사용 권한은 수행하는 절차 또는 실행하려는 cmdlet에 따라 달라집니다. 전송 기능에 대한 자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md)을 참조하십시오.

이 항목에는 Microsoft Exchange Server 2013 에서 메일 흐름 기능을 관리 하는 데 필요한 권한을 보여줍니다. Exchange 권한을 Office 365 사용 권한 관련 되는 방법에 대 한 정보를 [Office 365의 사용 권한](https://go.microsoft.com/fwlink/p/?linkid=335814)을 참조 하십시오.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.


> [!NOTE]
> 관리하고자 하는 일부 기능은 Edge 전송 서버에 존재할 수 있습니다. Edge 전송 서버에서 기능을 관리하려면 관리할 Edge 전송 서버에서 로컬 관리자 그룹의 구성원이 되어야 합니다. Edge 전송 서버는 RBAC(역할 기반 액세스 제어)를 사용하지 않습니다. Edge 전송 서버에서 관리할 수 있는 기능은 아래 표의 "필요한 사용 권한" 열에 Edge 전송 로컬 관리자로 표시되어 있습니다.




> [!NOTE]
> 일부 기능의 경우 관리하려는 서버에 대한 로컬 관리자 권한이 필요할 수도 있습니다. 이러한 기능을 관리하려면 해당 서버에서 로컬 관리자 그룹의 구성원이어야 합니다.



## 메일 흐름 사용 권한

다음 표의 기능을 사용하여 클라이언트 액세스 서버의 프런트 엔드 전송 서비스, 사서함 서버의 전송 서비스, 사서함 서버의 사서함 전송 서비스 및 Edge 전송 서버의 사서함 전송 서비스에서 메일 흐름 설정을 구성할 수 있습니다. 각 기능을 구성하는 데 필요한 사용 권한이 나열되어 있습니다.

보기 전용 관리 역할 그룹이 할당된 사용자는 다음 표에 있는 기능의 구성을 볼 수 있습니다. 자세한 내용은 [보기 전용 조직 관리](view-only-organization-management-exchange-2013-help.md)를 참조하십시오.

**사서함 서버 및 클라이언트 액세스 서버**


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
<td><p>허용 도메인</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Active Directory 사이트 및 사이트 링크 관리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>스팸 방지 기능</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="even">
<td><p>스팸 방지 업데이트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="odd">
<td><p>인증서 관리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>배달 에이전트 커넥터</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>DSN</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>외부 커넥터</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>프런트 엔드 전송 서비스</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="odd">
<td><p>저널링</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 액세스</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 정크 메일 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 전송 서비스</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="odd">
<td><p>메일 설명</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>메시지 분류</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p>메시지 추적</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>중재된 전송</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>큐</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>수신 커넥터</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="odd">
<td><p>원격 도메인</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>수신 허용 목록 집계</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p>송신 커넥터</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>섀도 중복성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>메일 흐름 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>전송 규칙 처리 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>전송 에이전트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="even">
<td><p>전송 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>전송 로그</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>전송 규칙</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p>전송 서비스</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="even">
<td><p>X.400 도메인</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


**Edge 전송 서버**


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
<td><p>허용 도메인 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="even">
<td><p>주소 다시 쓰기 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="odd">
<td><p>Edge 전송 서버</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="odd">
<td><p>큐 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="even">
<td><p>수신 커넥터 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="odd">
<td><p>송신 커넥터 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="even">
<td><p>전송 구성 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="odd">
<td><p>전송 로그 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
<tr class="even">
<td><p>전송 규칙 - Edge 전송</p></td>
<td><p>Edge 전송 로컬 관리자</p></td>
</tr>
</tbody>
</table>

