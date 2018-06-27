---
title: '관리자 감사 로깅: Exchange 2013 Help'
TOCTitle: 관리자 감사 로깅
ms:assetid: 22b17eb8-d8ee-4599-b202-d6a7928c20d9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335144(v=EXCHG.150)
ms:contentKeyID: 50555959
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리자 감사 로깅

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2018-03-05_

Microsoft Exchange Server 2013에서 관리자 감사 로깅을 사용하여 사용자 또는 관리자가 언제 조직에서 변경 작업을 수행하는지 기록할 수 있습니다. 변경 내용의 로그를 유지하면 변경을 수행한 사용자의 변경 내용을 추적하고, 변경 내용이 구현될 때 변경에 대한 상세 레코드가 포함된 변경 로그를 늘리고, 검색에 대한 규정 요구 사항 및 요청을 준수하는 등의 작업이 가능합니다.

기본적으로 Exchange 2013을 새로 설치하면 감사 로깅을 사용할 수 있습니다.

**목차**

What gets audited

Audit logging configuration

Audit logs

Manual audit log entries

Active Directory replication

Admin Audit Log agent

## 감사 대상

Exchange의 관리 셸에서 직접 실행되는 cmdlet에 대해 감사가 수행됩니다. 또한 EAC(Exchange 관리 센터)를 사용하여 수행되는 작업도 백그라운드에서 cmdlet을 실행하므로 기록됩니다.

Cmdlet은 실행 중인 위치에 관계 없이 감사 되는 cmdlet이 목록과 하나 감사 cmdlet에 또는 해당 cmdlet에서 더 많은 매개 변수는 매개 변수 감사 목록에 있는 경우. 감사 로깅은 Exchange 조직에서 개체를 수정 하려면 동작 수행한 표시 하기 위한 것이 아닌 개체의 종류를 본 합니다.


> [!IMPORTANT]
> cmdlet이 관리자 감사 로그 cmdlet 확장 에이전트를 호출하기 전에 오류가 발생할 경우에는 기록되지 않습니다. 관리 감사 로그 에이전트가 호출된 후 오류가 발생하면 관련 오류와 함께 cmdlet이 기록됩니다. 자세한 내용은 이 항목 뒷부분에 나오는 Admin Audit Log Agent 섹션을 참조하십시오.<BR>Microsoft Exchange Server 2010 관리 도구를 사용하여 변경한 내용은 기록되지만 Microsoft Exchange Server 2007 관리 도구를 사용하여 변경한 내용은 기록되지 않습니다.<BR>감사 로그 구성의 변경 내용은 구성 변경 시 셸이 열리는 컴퓨터에서 60분마다 새로 고쳐집니다. 변경 내용을 즉시 적용하려면 각 컴퓨터에서 셸을 닫은 후 다시 여십시오.<BR>실행된 명령이 감사 로그 검색 결과에 나타나려면 최대 15분까지 걸릴 수 있습니다. 감사 로그 항목은 인덱싱되어야 검색이 가능하기 때문입니다. 명령이 관리자 감사 로그에 표시되지 않으면 몇 분간 기다렸다가 검색을 다시 실행해 보십시오.



## 감사 로깅 구성

기본적으로 감사 로깅이 설정 되 면 로그 항목이 만들어집니다 할 때마다 모든 cmdlet을 실행 합니다. 모든 cmdlet을 실행 하는 감사 않으려면 cmdlet 및 매개 변수에 관심이 감사에 감사 로깅을 구성할 수 있습니다. **Set-AdminAuditLogConfig** cmdlet과 함께 감사 로깅을 구성합니다. 다음 섹션에서 참조 되는 매개 변수는이 cmdlet과 함께 사용 됩니다.


> [!IMPORTANT]
> 관리자 감사 로그 구성의 변경 내용은 <STRONG>Set-AdministratorAuditLog</STRONG> cmdlet이 감사되는 cmdlet 목록에 포함되어 있는지 여부 및 감사 로깅이 사용되는지 여부와 관계없이 항상 기록됩니다.



명령이 실행되면 Exchange는 사용된 cmdlet을 검사합니다. 실행된 cmdlet이 *AdminAuditLogConfigCmdlets* 매개 변수가 사용된 cmdlet과 일치하면 Exchange는 *AdminAuditLogConfigParameters* 매개 변수에 지정된 매개 변수를 확인합니다. 매개 변수 목록에서 하나 이상의 매개 변수가 일치하는 경우 Exchange는 *AdminAuditLogMailbox* 매개 변수를 사용하여 지정된 사서함에서 실행된 cmdlet을 기록합니다. 다음 섹션에서는 감사 로깅 구성의 각 측면에 대한 추가 정보를 소개합니다.

감사 로깅 구성 관리에 대한 자세한 내용은 [관리자가 관리 감사 로깅](manage-administrator-audit-logging-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

## Cmdlet

기록할 cmdlet 및 매개 변수의 목록을 제공하여 감사할 cmdlet을 제어할 수 있습니다. 감사 로깅을 구성할 때 모든 cmdlet을 감사하도록 지정하거나, *AdminAuditLogConfigCmdlets* 매개 변수를 사용하여 원하는 cmdlet만 감사하도록 지정할 수 있습니다. **New-Mailbox**와 같이 전체 cmdlet 이름을 지정할 수도 있고, 또는 부분적인 cmdlet 이름을 지정하고 해당 이름을 별표(`*`) 등의 와일드카드 문자로 묶을 수 있습니다. 예를 들어 `Transport` 문자열이 포함된 cmdlet이 실행되면 로깅하려는 경우 `*Transport*`의 값을 지정할 수 있습니다. cmdlet 이름 전체와 cmdlet 이름 일부를 동시에 혼합 사용하여 필요에 맞게 감사 로깅 구성을 지정할 수 있습니다.

## 매개 변수

기록할 cmdlet을 지정하는 것뿐만 아니라 해당 cmdlet에 특정 매개 변수가 사용될 경우에만 cmdlet이 기록되도록 지정할 수도 있습니다. *AdminAuditLogConfigParameters* 매개 변수를 사용하여 로깅해야 할 매개 변수를 지정합니다. cmdlet과 마찬가지로 전체 매개 변수 이름(예: `Database`)을 지정하거나, `*Address*`와 같이 와일드카드 문자(`*`)로 묶은 부분적인 매개 변수 이름을 지정하거나, 또는 이 두 가지를 조합하여 지정할 수 있습니다.

## 감사 로그 보존 기간

기본적으로 감사 로깅은 감사 로그 항목을 90일 동안 저장하도록 구성되어 있습니다. 90일이 지나면 감사 로그 항목은 삭제됩니다. *AdminAuditLogAgeLimit* 매개 변수를 사용하여 감사 로그 보존 기간을 변경할 수 있습니다. 감사 로그 항목을 유지할 일수, 시간, 분 및 초를 지정할 수 있습니다. 값을 지정하려면 `dd.hh:mm:ss` 형식을 사용합니다. 여기서 각 항목은 다음을 나타냅니다.

  - **dd**   감사 로그 항목을 보존할 일수

  - **hh**   감사 로그 항목을 보존할 시간

  - **mm**   감사 로그 항목을 보존할 시간(분)

  - **ss**   감사 로그 항목을 보존할 시간(초)

여러 해는 `dd` 필드를 사용하여 지정해야 합니다. 예를 들어, 365일은 1년, 730일은 2년, 913일은 2년 6개월에 해당합니다. 예를 들어, 감사 로그 보존 기간을 2년 6개월로 설정하려면 `913.00:00:00` 구문을 사용합니다.


> [!WARNING]
> 감사 로그 보존 기간을 현재 보존 기간보다 작게 설정할 수 있습니다. 이 경우 보존 기간이 새 보존 기간을 초과하는 모든 감사 로그 항목이 삭제됩니다.<BR>보존 기간을 0으로 설정할 경우 Exchange는 감사 로그의 모든 항목을 삭제합니다.<BR>감사 로그 보존 기간을 구성할 수 있는 권한은 신뢰할 수 있는 사용자에게만 부여하는 것이 좋습니다.



## 자세한 정보 로깅

기본적으로 관리자 감사 로그는 cmdlet 이름, cmdlet 매개 변수(및 지정된 값), 수정된 개체, cmdlet을 실행한 사람, cmdlet이 실행된 시간, cmdlet이 실행된 서버만 기록합니다. 관리자 감사 로그는 어떤 개체 속성이 수정되었는지는 기록하지 않습니다. 감사 로그에 수정된 개체 속성을 포함하려면 *LogLevel* 매개 변수를 `Verbose`로 설정하여 자세한 정보 로깅을 사용할 수 있습니다. 기본적으로 기록되는 정보 이외에 자세한 정보 로깅을 사용할 경우 수정된 개체 속성과 이전 값 및 새 값이 감사 로그에 포함됩니다.

## 테스트 cmdlet

동사 **Test**로 시작하는 cmdlet은 기본적으로 기록되지 않습니다. *TestCmdletLoggingEnabled* 매개 변수를 `$true`로 설정하여 **Test** cmdlet을 기록하도록 지정할 수 있습니다. 테스트 cmdlet 로깅을 사용하도록 설정할 수 있지만 테스트 cmdlet이 대량의 정보를 생성할 수 있으므로 짧은 기간 동안만 로깅하는 것이 좋습니다.

## 감사 로그

cmdlet이 기록될 때마다 감사 로그 항목이 만들어집니다. 감사 로그는 EAC, **Search-AdminAuditLog** 또는 **New-AdminAuditLogSearch** cmdlet을 사용해서만 액세스할 수 있는 숨겨진 전용 중재 사서함에 저장됩니다. 이 로그는 Microsoft Outlook Web App 또는 Microsoft Outlook을 사용하여 열 수 없습니다. 다음 섹션에서는 다음에 대한 정보를 제공합니다.

  - 로그에 포함된 내용

  - EAC **감사** 페이지에서 사용할 수 있는 보고서

  - 감사 로그 검색 cmdlet

## 감사 로그 콘텐츠

각 감사 로그 항목에는 다음 표에 설명된 정보가 포함되어 있습니다. 감사 로그에는 하나 이상의 감사 로그 항목이 포함되어 있습니다. 감사 로그 항목 수는 **Set-AdminAuditLogConfig** cmdlet을 사용하여 지정된 감사 로그 보존 기간으로 제어됩니다. 보존 기간을 초과하는 모든 감사 로그 항목은 삭제됩니다.

### 감사 로그 항목 필드

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>필드</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>RunspaceId</code></p></td>
<td><p>이 필드는 Exchange에서 내부적으로 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>ObjectModified</code></p></td>
<td><p>이 필드에는 <code>CmdletName</code> 필드에 지정된 cmdlet이 수정한 개체가 포함되어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>CmdletName</code></p></td>
<td><p>이 필드에는 <code>Caller</code> 필드의 사용자가 실행한 cmdlet 이름이 포함되어 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletParameters</code></p></td>
<td><p>이 필드에는 <code>CmdletName</code> 필드의 cmdlet이 실행될 때 지정된 매개 변수가 포함되어 있습니다. 또한 이 매개 변수로 지정된 값(있는 경우)은 이 필드에 저장되지만 기본 출력에서 표시되지 않습니다. 이 필드의 추가 정보에 액세스하는 방법에 대한 자세한 내용은 <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">역할 그룹 변경 내용을 검색 또는 관리자 감사 로그</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><code>ModifiedProperties</code></p></td>
<td><p>이 필드에는 <code>ObjectModified</code> 필드의 개체에서 수정한 속성이 포함되어 있습니다. 또한 저장된 속성의 이전 값 및 새 값은 이 필드에 저장되지만 기본 출력에서 표시되지 않습니다. 이 필드의 추가 정보에 액세스하는 방법에 대한 자세한 내용은 <a href="search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md">역할 그룹 변경 내용을 검색 또는 관리자 감사 로그</a>을 참조하십시오.</p>

> [!IMPORTANT]
> 이 필드는 <STRONG>Set-AdminAuditLogConfig</STRONG> cmdlet의 <EM>LogLevel</EM> 매개 변수가 <CODE>Verbose</CODE>로 설정된 경우에만 채워집니다.


</td>
</tr>
<tr class="even">
<td><p><code>Caller</code></p></td>
<td><p>이 필드에는 <code>CmdletName</code> 필드의 cmdlet을 실행한 사용자의 사용자 계정이 포함되어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Succeeded</code></p></td>
<td><p>이 필드는 <code>CmdletName</code> 필드의 cmdlet이 성공적으로 실행되었는지 여부를 지정합니다. 값은 <code>True</code> 또는 <code>False</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Error</code></p></td>
<td><p>이 필드에는 <code>CmdletName</code> 필드의 cmdlet이 성공적으로 완료되지 않은 경우 생성된 오류 메시지가 포함되어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>RunDate</code></p></td>
<td><p>이 필드에는 <code>CmdletName</code> 필드의 cmdlet이 실행된 날짜 및 시간이 포함되어 있습니다. 날짜와 시간은 UTC(협정 세계시) 형식으로 저장됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>OriginatingServer</code></p></td>
<td><p>이 필드는 <code>CmdletName</code> 필드에 지정된 cmdlet이 실행된 서버를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>이 필드는 Exchange에서 내부적으로 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>IsValid</code></p></td>
<td><p>이 필드는 Exchange에서 내부적으로 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ObjectState</code></p></td>
<td><p>이 필드는 Exchange에서 내부적으로 사용합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## EAC 감사 보고서

EAC의 **감사** 페이지에는 다양한 유형의 준수 및 관리 구성 변경 내용에 대한 정보를 제공하는 여러 가지 보고서가 있습니다. 다음 보고서는 조직의 구성 변경 내용에 대한 정보를 제공합니다.

  - **관리자 역할 그룹 보고서**   이 보고서를 사용하면 지정된 시간대 내에서 지정하는 관리 역할 그룹에 대한 변경 내용을 검색할 수 있습니다. 반환되는 결과에는 변경된 역할 그룹, 변경한 사용자 및 변경 시간 및 내용이 포함되어 있습니다. 최대 3,000개의 항목이 반환될 수 있습니다. 검색이 3,000개를 초과하는 항목을 반환할 가능성이 있으면 경우 **관리자 감사 로그** 보고서 또는 **Search-AdminAuditLog** cmdlet을 사용합니다.

  - **관리자 감사 로그**   이 보고서를 사용하면 지정된 시간대 내에 기록된 감사 로그 항목을 XML 파일로 내보낸 다음 이 파일을 지정된 받는 사람에게 전자 메일로 보낼 수 있습니다. XML 파일의 콘텐츠에 대한 자세한 내용은 [관리자 감사 로그 구조](administrator-audit-log-structure-exchange-2013-help.md)를 참조하십시오.

이러한 보고서를 사용하는 방법에 대한 자세한 내용은 [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)을 참조하십시오.

**감사** 페이지에 포함된 다른 보고서에 대한 자세한 내용은 [감사 보고서를 교환 합니다.](exchange-auditing-reports-exchange-2013-help.md)를 참조하십시오.

## Search-AdminAuditLog cmdlet

**Search-AdminAuditLog** cmdlet을 실행하는 경우 지정하는 검색 조건과 일치하는 모든 감사 로그 항목이 반환됩니다. 다음과 같은 검색 조건을 지정할 수 있습니다.

  - **Cmdlet**   관리자 감사 로그에서 검색하려는 cmdlet을 지정합니다.

  - **매개 변수**   관리자 감사 로그에서 검색하려는 매개 변수를 쉼표로 구분하여 지정합니다. 검색할 cmdlet을 지정하는 경우 매개 변수만 검색할 수 있습니다.

  - **종료 날짜**   지정한 날짜 또는 그 이전에 발생한 로그 항목에 대한 관리자 감사 로그 결과의 범위를 지정합니다.

  - **시작 날짜**   지정한 날짜 또는 그 이후에 발생한 로그 항목에 대한 관리자 감사 로그 결과의 범위를 지정합니다.

  - **개체 ID**   지정한 변경된 개체를 포함하는 관리자 감사 로그 항목만 반환되어야 하는지 여부를 지정합니다.

  - **사용자 ID**   cmdlet을 실행한 사용자의 지정한 ID를 포함하는 관리자 감사 로그 항목만 반환되어야 하는지 여부를 지정합니다.

  - **성공적 완료**   성공 또는 실패를 나타내는 관리자 감사 로그 항목만 반환되어야 하는지 여부를 지정합니다.

각 감사 로그 항목에는 Audit Log Contents의 표에 설명된 정보가 포함되어 있습니다. 기본적으로 지정한 조건과 일치하는 처음 1,000개의 로그 항목이 반환됩니다. 하지만 이 기본값을 무시하고 *ResultSize* 매개 변수를 사용하여 더 많거나 적은 수의 항목을 반환할 수 있습니다. *ResultSize* 매개 변수로 `Unlimited` 값을 지정하여 조건과 일치하는 모든 로그 항목을 반환할 수 있습니다.

**Search-AdminAuditLog** cmdlet을 사용하는 방법에 대한 자세한 내용은 [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)을 참조하십시오.

## New-AdminAuditLogSearch cmdlet

**New-AdminAuditLogSearch** cmdlet은 **Search-AdminAuditLog** cmdlet과 동일하게 감사 로그를 검색합니다. 하지만 셸에서 감사 로그 검색 결과를 표시하는 대신 **New-AdminAuditLogSearch** cmdlet이 검색을 수행한 다음 이 검색 결과를 지정된 받는 사람에게 전자 메일 메시지로 보냅니다. 결과는 XML 첨부 파일로 전자 메일 메시지에 포함됩니다.

**Search-AdminAuditLog** cmdlet에서 사용되는 **New-AdminAuditLogSearch** cmdlet과 동일한 검색 조건을 사용할 수 있습니다. 검색 조건 목록은 Search-AdminAuditLog Cmdlet을 참조하십시오.

**New-AdminAuditLogSearch** cmdlet을 실행한 후 Exchange가 지정된 받는 사람에게 보고서를 배달하는 데 최대 15분까지 걸릴 수 있습니다. XML 파일 첨부 보고서의 최대 크기는 10MB입니다. XML 파일에는 Audit Log Contents의 표에 설명된 동일한 정보가 포함되어 있습니다. XML 파일의 구조에 대한 자세한 내용은 [관리자 감사 로그 구조](administrator-audit-log-structure-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> Outlook Web App은 기본적으로 XML 첨부 파일을 열지 못하도록 되어 있습니다. Exchange을 사용하여 XML 첨부 파일을 볼 수 있도록 Outlook Web App을 구성하거나 Microsoft Outlook과 같은 다른 전자 메일 클라이언트를 사용하여 첨부 파일을 볼 수 있습니다. Outlook Web App에서 XML 첨부 파일을 볼 수 있도록 구성하는 방법에 대한 자세한 내용은 <A href="view-or-configure-outlook-web-app-virtual-directories-exchange-2013-help.md">Outlook Web App 가상 디렉터리 보기 또는 구성</A>을 참조하세요.



**New-AdminAuditLogSearch** cmdlet을 사용하는 방법에 대한 자세한 내용은 [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

## 수동 감사 로그 항목

실행 시 Exchange cmdlet 기록뿐만 아니라 Exchange 2013을 사용하여 수동으로 감사 로그에 로그 항목을 기록할 수도 있습니다. Exchange 2013은 **Write-AdminAuditLog** cmdlet을 사용하여 이를 지원합니다. 수동 로그에 포함하려는 사항은 다음과 같습니다.

  - 사용자 지정 스크립트 입력 및 종료

  - 변경 제어 정보

  - 유지 관리 시작 및 종료 시간

**Write-AdminAuditLog** cmdlet에서 *Comment* 매개 변수를 사용하여 감사 로그에 포함할 텍스트 문자열을 지정합니다. *Comment* 매개 변수는 최대 500자의 영숫자 문자열을 허용합니다. Exchange cmdlet이 로그될 때 캡처된 모든 동일한 정보가 주석 문자열과 함께 수동 감사 로그 항목에 포함됩니다. 감사 로그에 포함된 각 필드에 대한 설명을 보려면 Audit Log Contents에 있는 표를 참조하십시오.

EAC **감사** 페이지, **Search-AdminAuditLog** 또는 **New-AdminAuditLogSearch** cmdlet을 사용하여 다른 로그 항목과 동일한 방식으로 수동 감사 로그 항목을 검색할 수 있습니다.

수동 감사 로그 항목에서 **Write-AdminAuditLog** cmdlet의 *Comment* 매개 변수 콘텐츠를 보려면 [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)을 참조하십시오.

## Active Directory 복제

관리자 감사 로깅 구성 설정을 지정 하면 조직에서 도메인 컨트롤러에 복제 하려면 복제 Active Directory 복제에 의존 합니다. 복제 설정에 따라 변경 사항을 하지 즉시에 적용할 수 조직에서 Exchange 2013 또는 Exchange 2010 를 실행 하는 모든 서버입니다.

## 관리 감사 로그 에이전트

기본 제공 cmdlet 확장 에이전트인 관리자 감사 로그 에이전트는 Exchange 2013에서 cmdlet 작업의 관리자 감사 로깅을 수행합니다. 이 에이전트는 감사 로그 구성을 읽은 후 조직에서 실행되는 각 cmdlet에 대한 평가를 수행합니다. 감사 로그 구성에 지정한 조건이 실행 중인 cmdlet과 일치하는 경우 에이전트에서 감사 로그를 생성합니다.

관리자 감사 로그 에이전트는 기본적으로 사용하도록 설정되어 있으며, 감사 로깅이 작동하는 데 필요합니다. 사용하지 않도록 설정할 수 없으며 해당 우선 순위를 변경할 수 없습니다. cmdlet 확장 에이전트에 대한 자세한 내용은 [cmdlet 확장 에이전트](cmdlet-extension-agents-exchange-2013-help.md)를 참조하십시오.

