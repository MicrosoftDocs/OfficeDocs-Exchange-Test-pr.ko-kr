---
title: '받는 사람에 게 사용 권한: Exchange 2013 Help'
TOCTitle: 받는 사람에 게 사용 권한
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 50483205
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람에 게 사용 권한

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

받는 사람을 관리하기 위한 작업을 수행하는 데 필요한 사용 권한은 수행하는 절차 또는 실행하려는 cmdlet에 따라 달라집니다.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.

## 사서함 서버 사용 권한

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
<td><p>일정 복구, 서버 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 서버 위임</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>전자 메일 주소 정책</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 검색</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 검색 – 진단</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p>Support Diagnostics 역할</p>

> [!NOTE]
> Support Diagnostics 역할은 역할 그룹에 할당되지 않습니다. 자세한 내용은 <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">사용자 또는 USG에는 역할을 추가 합니다.</A>를 참조하십시오.


</td>
</tr>
<tr class="even">
<td><p>그룹 메트릭</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>가져오기 내보내기</p></td>
<td><p>Mailbox Import Export 역할</p>

> [!NOTE]
> Mailbox Import Export 역할은 역할 그룹에 할당되지 않습니다. 자세한 내용은 <A href="mailbox-import-export-role-exchange-2013-help.md">Mailbox Import Export 역할</A>을 참조하십시오.


</td>
</tr>
<tr class="even">
<td><p>사서함 도우미</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 이동</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 복구</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 복구 요청</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 복원 요청</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 서버 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 서버의 Exchange Search Indexer 서비스 관리</p></td>
<td><p>사서함 서버의 로컬 관리자</p></td>
</tr>
<tr class="odd">
<td><p>MAPI 연결</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>OAB 가상 디렉터리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>저장소 사서함 제거</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
</tbody>
</table>


## 일정 및 공유 권한

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
<td><p>일정 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="even">
<td><p>일정 진단</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p>
<p><a href="compliance-management-exchange-2013-help.md">Compliance Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>일정 처리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="even">
<td><p>알림</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>조직 관계</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>공유 정책</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


## 리소스 사서함 구성 권한

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
<td><p>예약 정책</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="even">
<td><p>위임</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>리소스 사서함 스키마 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


## 사서함 데이터베이스 권한

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
<td><p>사서함 데이터베이스</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
</tbody>
</table>


## 받는 사람 프로비전 권한

이 표에는 받는 사람을 관리하는 데 필요한 다양한 권한이 포함되어 있습니다.

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
<td><p>주소 목록, GAL</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>스팸 방지</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook용 앱</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="even">
<td><p>공유 정책 적용</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>중재</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>보관 연결</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>오프라인 주소록 할당</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>자동 회신</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>일정 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>일정 복구</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>연락처 집계 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>연결이 끊어진 사서함</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>메일 그룹</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>동적 메일 그룹</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>전자 메일 주소</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>받은 편지함 규칙</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>메일 연락처</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>메일 설명</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>메일 사용자</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 폴더 권한</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>사서함 폴더</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>MAPI 연결</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>메시지 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="even">
<td><p>메시지 할당량</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>조절</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>사용 권한 및 위임</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>보관 사서함</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>받는 사람 데이터 속성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>원격 사서함</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>보존 및 법적 보유</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="records-management-exchange-2013-help.md">Records Management</a></p></td>
</tr>
<tr class="odd">
<td><p>다른 사람 이름으로 보내기</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>맞춤법 검사 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
<tr class="odd">
<td><p>통합 메시징</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="um-management-exchange-2013-help.md">UM Management</a></p></td>
</tr>
<tr class="even">
<td><p>사용자 사서함</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>사용자 사진</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="help-desk-exchange-2013-help.md">지원 센터</a></p></td>
</tr>
</tbody>
</table>


## 사서함 이동 및 마이그레이션 권한

다음 표에서는 온-프레미스 사서함을 다른 도메인 또는 포리스트로 이동하고 온-프레미스 사서함을 클라우드 기반 조직에서 또는 조직으로 마이그레이션하는 데 필요한 사용 권한을 보여줍니다.


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
<td><p>사서함 이동(로컬 또는 포리스트 간)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>사서함 이동(하이브리드 배포)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>마이그레이션(클라우드에 온보드/오프보드)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
</tbody>
</table>

