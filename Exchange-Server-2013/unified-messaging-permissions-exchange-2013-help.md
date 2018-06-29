---
title: '통합된 메시징 사용 권한: Exchange 2013 Help'
TOCTitle: 통합된 메시징 사용 권한
ms:assetid: d326c3bc-8f33-434a-bf02-a83cc26a5498
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638193(v=EXCHG.150)
ms:contentKeyID: 50484220
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 통합된 메시징 사용 권한

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

실행 하려는 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 하는 클라이언트 액세스 서버와 Microsoft Exchange 통합 메시징 서비스 수행 하는 절차에 따라 다를 실행 하는 사서함 서버 또는 cmdlet에서 작업을 수행 하는 데 필요한 사용 권한입니다.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.

## UM 구성 요소 사용 권한

다음 표에 UM 구성 요소와 기능에 대 한 설정을 구성할 수 있습니다.

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
<td><p>UM 자동 전화 교환</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>UM 전화 응답 규칙</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="odd">
<td><p>UM 호출 데이터 및 요약 보고서</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 서버 (UM 호출 라우터 서비스)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="odd">
<td><p>UM 다이얼 플랜</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>UM 헌트 그룹</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="odd">
<td><p>UM IP 게이트웨이</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>UM 사서함 정책</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="odd">
<td><p>UM 사서함</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>UM 음성 안내</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 서버 (UM 서비스)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
</tbody>
</table>

