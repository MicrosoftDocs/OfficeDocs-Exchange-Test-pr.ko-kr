---
title: '클라이언트 및 모바일 장치 사용 권한: Exchange 2013 Help'
TOCTitle: 클라이언트 및 모바일 장치 사용 권한
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 50483163
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 및 모바일 장치 사용 권한

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-11-10_

클라이언트 및 모바일 장치에 대한 작업을 수행하는 데 필요한 사용 권한은 수행하는 절차 또는 실행하려는 cmdlet에 따라 달라집니다. 클라이언트 및 모바일 장치 기능에 대한 자세한 내용은 [클라이언트 및 모바일](clients-and-mobile-exchange-2013-help.md) 항목을 참조하십시오.

절차를 수행하거나 cmdlet을 실행하기 위해 필요한 사용 권한을 찾으려면 다음을 수행합니다.

1.  아래 표에서 수행할 절차나 실행할 cmdlet과 가장 관련이 깊은 기능을 찾습니다.

2.  그런 다음 기능에 필요한 사용 권한을 확인합니다. 역할 그룹 중 하나, 동등한 사용자 지정 역할 그룹 또는 동등한 관리 역할을 할당받아야 합니다. 역할 그룹을 클릭하여 관리 역할을 볼 수도 있습니다. 둘 이상의 역할 그룹이 표시될 경우 기능을 사용하려면 해당 역할 그룹 중 하나에만 지정되어야 합니다. 역할 그룹 및 관리 역할에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참고하세요.

3.  이제 **Get-ManagementRoleAssignment** cmdlet을 실행하여 자신에게 할당된 역할 그룹이나 관리 역할을 보고 기능 관리에 필요한 사용 권한이 있는지 확인합니다.
    

    > [!NOTE]
    > <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Role Management 관리 역할을 할당받아야 합니다. <STRONG>Get-ManagementRoleAssignment</STRONG> cmdlet을 실행할 사용 권한이 없는 경우에는 Exchange 관리자에게 문의하여 자신에게 할당된 역할 그룹이나 관리 역할을 검색합니다.



기능 관리를 다른 사용자에게 위임하려는 경우에는 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참고하세요.


> [!NOTE]
> 일부 기능의 경우 관리하려는 서버에 대한 로컬 관리자 권한이 필요할 수도 있습니다. 이러한 기능을 관리하려면 해당 서버에서 로컬 관리자 그룹의 구성원이어야 합니다.



## 클라이언트 액세스 서버 권한

클라이언트 액세스 서버에 대한 다음 기능을 구성할 수 있습니다.

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
<td><p>클라이언트 액세스 서버 배열 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 서버 설정</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 액세스 서비스 전자 메일 채널 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 사용자 설정</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 액세스 가상 디렉터리 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>RPC 클라이언트 액세스 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>푸시 알림 프록시 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>OAuth 인증 리디렉션 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


## Exchange ActiveSync 권한

Exchange ActiveSync에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>Exchange ActiveSync Autoblock 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 사서함 정책 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync 서버 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange ActiveSync 사용자 설정</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange ActiveSync 가상 디렉터리 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>모바일 장치 사서함 정책 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>모바일 장치 사용자 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
</tbody>
</table>


## 자동 검색 권한

자동 검색 서비스에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>자동 검색 서비스 구성 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">위임 설치</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="even">
<td><p>자동 검색 가상 디렉터리 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
</tbody>
</table>


## 가용성 서비스 권한

가용성 서비스에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>가용성 서비스 주소 공간 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>가용성 서비스 구성 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
</tbody>
</table>


## 클라이언트 스로틀 권한

클라이언트 스로틀에 대해 다음 항목을 구성할 수 있습니다.

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
<td><p>클라이언트 스로틀 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
</tbody>
</table>


## Exchange 웹 서비스 권한

웹 서비스 가상 디렉터리에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>Exchange 웹 서비스 가상 디렉터리 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 웹 서비스 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook 웹 서비스 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


## Outlook Anywhere 권한

외부에서 Outlook 사용에 대한 다음 설정을 구성하고 관리할 수 있습니다.

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
<td><p>외부에서 Outlook 사용 구성(활성화, 비활성화, 변경, 보기)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">위임 설치</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
<tr class="even">
<td><p>RPC over HTTP 프록시 구성 요소</p></td>
<td><p>로컬 서버 관리자</p></td>
</tr>
<tr class="odd">
<td><p>외부에서 Outlook 사용 연결 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
</tbody>
</table>


## Outlook Web App 권한

다음 기능을 사용하여 Outlook Web App 설정을 보고 Outlook Web App에 대한 사용자 액세스 및 보안을 제어하고 Outlook Web App 연결을 테스트할 수 있습니다.

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
<td><p>그래픽 편집기</p></td>
<td><p>로컬 서버 관리자</p></td>
</tr>
<tr class="even">
<td><p>IIS 관리자</p></td>
<td><p>로컬 서버 관리자</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>ISA Server 엔터프라이즈 관리자</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App 사서함 정책</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App 가상 디렉터리</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p></td>
</tr>
<tr class="even">
<td><p>레지스트리 편집기</p></td>
<td><p>로컬 서버 관리자</p></td>
</tr>
<tr class="odd">
<td><p>S/MIME 구성</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>텍스트 편집기</p></td>
<td><p>로컬 서버 관리자</p></td>
</tr>
<tr class="odd">
<td><p>Outlook Web App 사서함 정책 보기</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">위임 설치</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Hygiene Management</a></p></td>
</tr>
</tbody>
</table>


## POP3 및 IMAP4 권한

POP3 및 IMAP4에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>IMAP4 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="odd">
<td><p>IMAP4 설정 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>POP3 설정 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p>
<p><a href="server-management-exchange-2013-help.md">Server 관리</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">보기 전용 조직 관리</a></p></td>
</tr>
</tbody>
</table>


## Windows PowerShell 가상 디렉터리 권한

Windows PowerShell에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>Windows PowerShell 테스트</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
<tr class="even">
<td><p>Windows PowerShell 설정</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">조직 관리</a></p></td>
</tr>
</tbody>
</table>


## 텍스트 메시징 권한

텍스트 메시징에 대한 다음 항목을 구성할 수 있습니다.

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
<td><p>텍스트 메시징 알림 설정</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="even">
<td><p>텍스트 메시징 설정</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Recipient Management</a></p></td>
</tr>
<tr class="odd">
<td><p>텍스트 메시징 사용자 설정</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 역할</a></p>
<p>사용자가 자신의 사서함에 텍스트 메시징 설정을 구성할 수 있습니다. 관리자가 텍스트 메시징 다른 사용자의 사서함에 대 한 설정을 구성할 수 없습니다.</p></td>
</tr>
</tbody>
</table>

