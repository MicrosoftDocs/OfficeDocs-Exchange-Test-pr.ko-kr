---
title: '사서함 감사 로깅: Exchange 2013 Help'
TOCTitle: 사서함 감사 로깅
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 50482689
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 사서함 감사 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

사서함에는 중요한 HBI(높은 업무상의 영향) 정보 및 PII(개인 식별이 가능한 정보)가 포함될 수 있으므로 조직의 사서함에 로그온하는 사람과 수행되는 작업을 추적해야 합니다. 사서함 소유자가 아닌 사용자의 사서함 액세스를 추적하는 것이 특히 중요합니다. 이러한 사용자를 *위임 사용자*라고 합니다.

*사서함 감사 로깅*을 사용하면 사서함 소유자, 대리인(모든 사서함에 대한 액세스 권한이 있는 관리자 포함) 및 관리자의 사서함 액세스를 로깅할 수 있습니다.

사서함에 감사 로깅을 사용하도록 설정할 때 로그온 유형(관리자, 위임 사용자 또는 소유자)에 따라 로깅할 사용자 작업(예: 메시지 액세스, 이동 또는 삭제)을 지정할 수 있습니다. 감사 로그 항목에는 클라이언트 IP 주소, 호스트 이름, 사서함 액세스에 사용된 프로세스 또는 클라이언트 등의 중요한 정보도 포함됩니다. 이동한 항목의 경우 대상 폴더의 이름도 항목에 포함됩니다.

## 사서함 감사 로그

사서함 감사 로그는 사서함 감사 로깅을 사용할 수 있는 각 사서함에 대해 생성됩니다. 로그 항목은 감사 대상 사서함의 복구 가능한 항목 폴더에 있는 감사 하위 폴더에 저장됩니다. 이렇게 하면 사서함 액세스에 사용된 클라이언트 액세스 방법이나 관리자가 사서함 감사 로그에 액세스하는 데 사용한 서버 또는 워크스테이션에 관계없이 단일 위치에서 모든 감사 로그 항목을 사용할 수 있습니다. 사서함을 다른 사서함 서버로 이동하면 해당 사서함의 사서함 감사 로그도 이동됩니다. 사서함 감사 로그는 사서함에 있기 때문입니다.

기본적으로 사서함 감사 로그 항목은 사서함에 90일 동안 보존된 다음 삭제됩니다. [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet과 함께 *AuditLogAgeLimit* 매개 변수를 사용하여 이 보존 기간을 수정할 수 있습니다. 사서함이 원본 위치 유지 또는 소송 보존 상태인 경우 감사 로그 항목은 사서함의 감사 로그 보존 기간에 도달할 때까지만 보존됩니다. 감사 로그 항목을 더 오랫동안 보존하려면 *AuditLogAgeLimit* 매개 변수의 값을 변경하여 보존 기간을 늘려야 합니다. 보존 기간에 도달하기 전에 감사 로그 항목을 내보낼 수도 있습니다. 자세한 내용은

  - [사서함 감사 로그 내보내기](export-mailbox-audit-logs-exchange-2013-help.md)

  - [사서함 감사 로그 검색 만들기](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## 사서함 감사 로깅 사용

사서함 감사 로깅은 사서함별로 사용하도록 설정됩니다. **Set-Mailbox** cmdlet을 사용하여 사서함 감사 로깅을 사용하거나 사용하지 않도록 설정할 수 있습니다. 자세한 내용은 [사서함 감사 사서함에 대해 로깅을 사용 하지 않도록 설정 하거나 사용](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md) 항목을 참조하십시오.

사서함에 대해 사서함 감사 로깅을 사용하도록 설정하면 기본적으로 사서함 액세스와 특정 관리자 및 대리인 작업이 로깅됩니다. 사서함 소유자가 수행한 작업을 로깅하려면 감사할 소유자 작업을 지정해야 합니다.

## 사서함 감사 로깅으로 로깅되는 사서함 작업

다음 표에는 작업이 로깅될 수 있는 로그온 유형을 비롯하여 사서함 감사 로깅으로 로깅되는 작업이 나와 있습니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>작업</th>
<th>설명</th>
<th>관리자</th>
<th>대리인</th>
<th>소유자</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>복사</p></td>
<td><p>항목이 다른 폴더에 복사되었습니다.</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>만들기</p></td>
<td><p>항목이 사서함의 일정, 연락처, 메모 또는 작업 폴더에 만들어집니다. 예를 들면 새 모임 요청이 만들어집니다. 메시지나 폴더 만들기는 감사되지 않습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>사서함 폴더가 액세스되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예**</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>항목이 복구 가능한 항목 폴더에서 영구적으로 삭제되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>항목이 읽기 창에서 액세스되었거나 열렸습니다.</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>Move</p></td>
<td><p>항목이 다른 폴더로 이동되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>항목이 지운 편지함 폴더로 이동되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>메시지가 다른 사람 이름으로 보내기 권한을 사용하여 전송되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>메시지가 대신 보내기 권한을 사용하여 전송되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>항목이 지운 편지함 폴더에서 삭제되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>업데이트</p></td>
<td><p>항목의 속성이 업데이트되었습니다.</p></td>
<td><p>예*</p></td>
<td><p>예*</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


\* 사서함에 대해 감사가 사용되는 경우 기본적으로 감사됩니다.

\*\* 대리인이 수행한 폴더 바인딩 작업에 대한 항목이 통합됩니다. 24시간 내에 개별 폴더 액세스에 대한 하나의 로그 항목이 생성됩니다.

특정 유형의 사서함 작업을 더 이상 감사할 필요가 없는 경우 사서함의 감사 로깅 구성을 수정하여 해당 작업을 사용하지 않도록 설정해야 합니다. 기존 로그 항목은 감사 로그 항목의 기간 제한에 도달할 때까지 제거되지 않습니다.

## 사서함 감사 로그 항목 검색

다음 방법을 사용하여 사서함 감사 로그 항목을 검색할 수 있습니다.

  - **동기적으로 단일 사서함 검색**   [Search-MailboxAuditLog](https://technet.microsoft.com/ko-kr/library/ff522360\(v=exchg.150\)) cmdlet을 사용하여 단일 사서함에 대한 사서함 감사 로그 항목을 동기적으로 검색할 수 있습니다. 이 cmdlet은 Exchange 관리 셸 창에 검색 결과를 표시합니다. 자세한 내용은 [사서함에 대 한 사서함 감사 로그를 검색 합니다.](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md) 항목을 참조하십시오.

  - **비동기적으로 하나 이상의 사서함 검색**   사서함 감사 로그 검색을 만들어 하나 이상의 사서함에 대한 사서함 감사 로그를 비동기적으로 검색한 다음 검색 결과를 특정 전자 메일 주소로 보낼 수 있습니다. 검색 결과는 XML 첨부 파일로 전송됩니다. 검색을 만들려면 [New-MailboxAuditLogSearch](https://technet.microsoft.com/ko-kr/library/ff522362\(v=exchg.150\)) cmdlet을 사용합니다. 자세한 내용은 [사서함 감사 로그 검색 만들기](create-a-mailbox-audit-log-search-exchange-2013-help.md) 항목을 참조하십시오.

  - **EAC(Exchange 관리 센터)에서 감사 보고서 사용**   EAC의 **감사** 탭을 사용하여 비소유자 사서함 액세스 보고서를 실행하거나 사서함 감사 로그에서 항목을 내보낼 수 있습니다. 자세한 내용은
    
      - [비 소유자 사서함 액세스 보고서 실행](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [사서함 감사 로그 내보내기](export-mailbox-audit-logs-exchange-2013-help.md)를 참조하세요.

## 사서함 감사 로그 항목

다음 표에서는 사서함 감사 로그 항목에 로깅되는 필드에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>필드</th>
<th>채워지는 값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>다음 작업 중 하나</p>
<ul>
<li><p>복사</p></li>
<li><p>만들기</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>이동</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>업데이트</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>다음 결과 중 하나</p>
<ul>
<li><p>Failed</p></li>
<li><p>PartiallySucceeded</p></li>
<li><p>Succeeded</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>작업을 수행한 사용자의 로그온 유형. 로그온 유형에는 다음이 포함됩니다.</p>
<ul>
<li><p>소유자</p></li>
<li><p>대리인</p></li>
<li><p>관리</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>이동 작업의 대상 폴더 GUID</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>이동 작업의 대상 폴더 경로</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>폴더 GUID</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>폴더 경로</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>작업을 수행한 클라이언트 또는 Exchange 구성 요소를 식별하는 세부 정보</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>클라이언트 컴퓨터 IP 주소</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>클라이언트 컴퓨터 이름</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>클라이언트 응용 프로그램 프로세스의 이름</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>클라이언트 응용 프로그램 버전</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>작업을 수행한 사용자의 로그온 유형. 로그온 유형에는 다음이 포함됩니다.</p>
<ul>
<li><p>소유자</p></li>
<li><p>대리인</p></li>
<li><p>관리</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>사서함 소유자 UPN(사용자 계정 이름)</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>사서함 소유자 SID(보안 식별자)</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>사서함 간 작업에 대해 로깅된 대상 사서함 소유자 UPN</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>사서함 간 작업에 대해 로깅된 대상 사서함 소유자 SID</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>대상 사서함 소유자 GUID</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>로깅된 작업이 사서함 간 작업(예: 사서함 간 메시지 복사 또는 이동)인지 여부에 대한 정보</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>로그온한 사용자의 표시 이름</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>위임 사용자 표시 이름</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>로그온한 사용자의 SID</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>로깅된 작업(예: 이동 또는 삭제)이 수행된 사서함 항목의 ItemID. 많은 항목에 대해 수행된 작업의 경우 이 필드가 항목 모음으로 반환됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>원본 폴더 GUID</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>항목 ID</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>항목 제목</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>사서함 GUID</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p><em>DOMAIN</em>\<em>SamAccountName</em> 형식의 사서함 사용자 확인 이름</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>작업이 수행된 시간</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>감사 로그 항목 ID</p></td>
</tr>
</tbody>
</table>


## 추가 정보

  - **관리자의 사서함 액세스**   다음 시나리오에서는 관리자만 사서함에 액세스한다고 간주합니다.
    
      - [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)를 사용하여 사서함을 검색합니다.
    
      - [New-MailboxExportRequest](https://technet.microsoft.com/ko-kr/library/ff607299\(v=exchg.150\)) cmdlet을 사용하여 사서함을 내보냅니다.
    
      - [Microsoft Exchange Server MAPI 편집기](https://go.microsoft.com/fwlink/p/?linkid=204086)를 사용하여 사서함에 액세스합니다.

  - **사서함 감사 로깅 무시**   타사 도구로 사용하는 계정이나 합법적인 모니터링에 사용되는 계정 등의 승인된 자동 프로세스에 의한 사서함 액세스는 많은 양의 사서함 감사 로그 항목을 생성할 수 있지만 조직에 중요하지 않을 수 있습니다. 사서함 감사 로깅을 무시하도록 해당 계정을 구성할 수 있습니다. 자세한 내용은 [프로그램에서 사용자 계정을 사서함 감사 로깅 바이패스](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md) 항목을 참조하십시오.

  - **사서함 소유자 작업 로깅**   검색 사서함과 같이 보다 중요한 정보가 포함될 수 있는 사서함의 경우 메시지 삭제 등의 사서함 소유자 작업에 대해 사서함 감사 로깅을 사용하도록 설정하는 것이 좋습니다.

사서함 감사 로그

