---
title: '공유 및 공동 작업 사용 권한: Exchange 2013 Help'
TOCTitle: 공유 및 공동 작업 사용 권한
ms:assetid: b7fa4b7c-1266-45bd-a14b-f66be0459cc5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150556(v=EXCHG.150)
ms:contentKeyID: 50483988
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공유 및 공동 작업 사용 권한

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

공유 및 공동 작업 기능을 구성 하는 데 필요한 사용 권한은 수행 하는 절차 또는 실행 하려는 cmdlet에 따라 다릅니다. 공유 및 공동 작업 하는 방법에 대 한 자세한 내용은 [공동 작업](collaboration-exchange-2013-help.md) 및 [공유](sharing-exchange-2013-help.md)를 참조 하십시오.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.

## 공유 및 공동 작업 기능 사용 권한

공유 및 공동 작업 기능을 구성 하는 다음 표에 기능을 사용할 수 있습니다. 각 기능을 구성 하는 데 필요한 역할 그룹이 나열 됩니다.

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
<td><p>파트너 응용 프로그램-구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더, 메일 사용 가능</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="public-folder-management-exchange-2013-help.md">공용 폴더 관리</a></p></td>
</tr>
<tr class="even">
<td><p>사이트 사서함</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>사이트 사서함 프로 비전 정책</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
</tbody>
</table>

