---
title: '클라이언트 프로토콜 관리: Exchange 2013 Help'
TOCTitle: 클라이언트 프로토콜 관리
ms:assetid: 89ba6d24-d1d3-46d5-a0ae-61f0d4c6df21
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657727(v=EXCHG.150)
ms:contentKeyID: 50483603
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 클라이언트 프로토콜 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

서로 다른 세 영역에서 발생 하는 Exchange ActiveSync, Outlook Web App, POP3, IMAP4, 자동 검색 서비스, Exchange 웹 서비스 및 가용성 서비스의 클라이언트 프로토콜 관리: Exchange 관리 센터 (EAC), Exchange 관리 셸 및 인터넷 정보 서비스 (IIS) 관리자입니다. 각 위치에서 관리 되는 설정 클라이언트 프로토콜에 따라 다릅니다.

## Outlook Web App 설정 관리

대부분의 사용자에 게 제공 되는 Outlook Web App 기능에 영향을 주는 설정 Outlook Web App 가상 디렉터리에서 설정할 수 또는 Outlook Web App 사서함 정책에서 구성할 수 있습니다. Outlook Web App 사서함 정책을 사용 하 여 개별 사용자에 게 제공 되는 기능을 정의할 수 있습니다. 사서함 정책 설정에는 가상 디렉터리 설정을 무시합니다. Outlook Web App 관리에 대 한 자세한 내용은 [Outlook Web App](outlook-web-app-exchange-2013-help.md)을 참조 하십시오.

## Exchange ActiveSync 설정 관리

Exchange 2010 모든 클라이언트 액세스 프로토콜 된 구현 및 단일 서버 역할, 클라이언트 액세스 서버 역할에서 관리 합니다. IIS의 단일 인스턴스에서 프로토콜 관리 수행 된, 각 클라이언트 프로토콜에 대 한 단일 가상 디렉터리 개체를 Active Directory에서 했습니다 및 가상 디렉터리를 구성 하는 단일 일련의 cmdlet에 사용 된 합니다.

Exchange 2013 Exchange ActiveSync에 대 한 클라이언트 프로토콜 관리 클라이언트 액세스 서버와 사서함 서버 간에 분할 됩니다. 이 아키텍처 변경으로 인해 클라이언트 액세스 서버와 사서함 서버에서 가상 디렉터리를 다른 관리 작업을 실행할 수 있습니다. 이러한 두 서버 동일한 실제 컴퓨터에 설치 되지 않은 경우 cmdlet를 변경 하는 가상 디렉터리와 함께 사용 하는 매개 변수를을 실행 하는 서버 역할에 기반 합니다.

Exchange 2013 의 아키텍처 변경 사항에 대 한 자세한 내용은 [Exchange 2013의 새로운 기능](what-s-new-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

Exchange ActiveSync 가상 디렉터리에 적용할 수 있는 설정의 두가지 유형이 있습니다.

  - 사서함 세션에 적용할 수 있는 설정

  - 서버 및 가상 디렉터리에 적용할 수 있는 설정

사서함 세션에 적용할 수 있는 설정이 사용자 세션 설정 합니다. 사용자는 클라이언트 액세스 서버에 연결할 때 연결은 사용자의 사서함이 포함 된 사서함 서버에 프록시 됩니다. 가상 디렉터리의 고유 식별자를 프록시 된 요청이 포함 됩니다. 사서함 서버는 다음 Active Directory에서 가상 디렉터리 설정을 검색 하 고 세션에 적용 합니다. 가상 디렉터리 설정 성능을 향상 시키기 위해 사서함 서버에 캐시 됩니다.

다른 Active Directory 사이트도 프록시 연결의 경우 가상 디렉터리 설정 하지 연결 시작 된 클라이언트 액세스 서버에서에서 사서함 서버와 동일한 사이트에 대 한 클라이언트 액세스 서버에서 로드 됩니다.

다음 표에서 각 서버에서 가상 디렉터리 설정을 관리할 수 있음을 나타냅니다. 적용할 수 없는 하는 서버에서 특정 설정을 관리 하는 경우에서 작동 하는 서버에 대 한 읽기 전용으로 설정 하려는 속성 임을 나타내는 오류 메시지가 나타납니다.

**클라이언트 액세스 서버에서 Exchange ActiveSync 가상 디렉터리 설정**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BadItemReportingEnabled</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>BasicAuthEnabled</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>ClientCertAuth</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>CompressionEnabled</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthenticationMethods</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>ExternalURL</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>InternalAuthenticationMethods</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>InternalURL</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertificateAuthorityURL</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>MobileClientCertificateProvisioningEnabled</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>MobileClientCertTemplateName</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsActionForUnknownServers</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsAllowedServers</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>RemoteDocumentsBlockedServers</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>RemoteDocumentsInternalDomainSuffixList</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>SendWatsonReport</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
</tbody>
</table>


**클라이언트 액세스 및 사서함 서버에서 Exchange ActiveSync 가상 디렉터리 설정**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ApplicationRoot</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>AppPoolID</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>MetabasePath</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>이름</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>경로</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>ProxySubVdir</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>VirtualDirectoryName</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>WebsiteName</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
</tbody>
</table>


## POP3 및 IMAP4 설정 관리

구현 하는 POP3 및 IMAP4 프로토콜 Exchange 2013 클라이언트 액세스 및 사서함 서버 역할 간에 분할 된도 했습니다. 새로운 구현으로 인해 POP3 및 IMAP4 연결은 각 관리 되는 사서함 서버에서 서비스에 따라서도 클라이언트 액세스 서버에서 서비스. 클라이언트 액세스 서버에서 실행 되는 서비스의 이름은 Exchange 2010에서 제공 하는 이름으로 동일: Microsoft Exchange IMAP4 서비스 및 Microsoft Exchange POP3 서비스입니다. 사서함 서버에서 실행 되는 두 새로운 서비스의 이름에는 Microsoft Exchange IMAP4 백엔드 서비스 및 Microsoft Exchange POP3 백엔드 서비스입니다.

조직에서 POP3 및 IMAP4 연결을 관리할 때 다음 사항을 고려 합니다.

  - 동일한 컴퓨터에 클라이언트 액세스 서버 역할 및 사서함 서버 역할을 실행 하는 경우, 하는 경우 POP3 또는 IMAP4 설정을 변경한 내용을 올바른 POP3 및 IMAP4 서비스에 자동으로 적용 됩니다.

  - 별도 컴퓨터에 클라이언트 액세스 서버 역할 및 사서함 서버 역할을 실행 하는 경우, 설정을 변경 하려면 설정을 관리 하는 컴퓨터에서 관리 해야 합니다.

사용 하 여 다음 표에 표시 POP/IMAP 설정은 각 서버 역할을 수행 하는 합니다.

**클라이언트 액세스 서버에서 POP3 및 IMAP4 설정**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AuthenticatedConnectionTimeout</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>배너</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>ExternalConnectionSettings</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>InternalConnectionSettings</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>MaxCommandSize</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionFromSingleIP</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>MaxConnections</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>MaxConnectionsPerUser</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="odd">
<td><p>PreAuthenticatedConnectionTimeout</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
<tr class="even">
<td><p>UnencryptedOrTLSBindings</p></td>
<td><p>클라이언트 액세스</p></td>
</tr>
</tbody>
</table>


**사서함 서버에서 POP3 및 IMAP4 설정**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CalendarItemRetrivalOption</p></td>
<td><p>사서함</p></td>
</tr>
<tr class="even">
<td><p>EnableExactRFC822Size</p></td>
<td><p>사서함</p></td>
</tr>
<tr class="odd">
<td><p>MessageRetrievalSortOrder</p></td>
<td><p>사서함</p></td>
</tr>
<tr class="even">
<td><p>OWAServerURL</p></td>
<td><p>사서함</p></td>
</tr>
<tr class="odd">
<td><p>ProxyTargetPort</p></td>
<td><p>사서함</p></td>
</tr>
<tr class="even">
<td><p>ShowHiddenFoldersEnabled</p></td>
<td><p>사서함</p></td>
</tr>
<tr class="odd">
<td><p>SuppressReadReceipt</p></td>
<td><p>사서함</p></td>
</tr>
</tbody>
</table>


**클라이언트 액세스 및 사서함 서버에서 POP3 및 IMAP4 설정**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>설정</th>
<th>서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>EnforceCertificateErrors</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>LogFileLocation</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>LogFileRolloverSettings</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>LoginType</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>LogPerFileSizeQuota</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>ProotocolLogEnabled</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="even">
<td><p>서버</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
<tr class="odd">
<td><p>X509CertificateName</p></td>
<td><p>클라이언트 액세스 및 사서함</p></td>
</tr>
</tbody>
</table>

