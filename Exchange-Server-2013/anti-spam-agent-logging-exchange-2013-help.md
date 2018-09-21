---
title: '스팸 방지 에이전트 로깅: Exchange 2013 Help'
TOCTitle: 스팸 방지 에이전트 로깅
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 50484292
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스팸 방지 에이전트 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

에이전트 로그 메시지에 특정 스팸 방지 에이전트 Microsoft Exchange Server 2013 에 의해 수행 되는 작업을 기록 합니다. 다음 에이전트에만 에이전트 로그에 정보를 작성할 수 있습니다.

  - 연결 필터링 에이전트

  - 콘텐츠 필터 에이전트

  - 에 지 규칙 에이전트

  - 받는 사람 필터 에이전트

  - 보낸 사람 필터 에이전트

  - 보낸 사람 ID 에이전트


> [!NOTE]
> 연결 필터링 에이전트 및에 지 규칙 에이전트에는 사서함 서버에서 사용할 수 없습니다.



에이전트 로그에 기록 하는 정보는 에이전트, SMTP 이벤트 및 메시지에서 수행 되는 작업에 따라 다릅니다.

Exchange 관리 셸에서 **Set-TransportService** cmdlet를 사용 하 여 모든 에이전트 로그 구성 작업을 수행 합니다. 다음 옵션 에이전트 로그에 대해 사용할 수 있습니다.

  - 사용 하도록 설정 하거나 로깅 에이전트를 사용 하지 않도록 설정 합니다. 기본값은 사용할 수 있습니다.

  - 에이전트 로그 파일의 위치를 지정 합니다. 기본값은 ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog %입니다.

  - 개별 에이전트 로그 파일에 대 한 최대 크기를 지정 합니다. 기본 크기는 10mb (MB)입니다.

  - 에이전트 로그 파일이 포함 된 디렉터리에 대 한 최대 크기를 지정 합니다. 다음은 기본 크기는 250MB입니다.

  - 에이전트 로그 파일에 대 한 최대 사용 기간을 지정 합니다. 기본 기간 7 일입니다.

Exchange 사용 하 여 순환 로깅을 제한 파일 크기 및 제어 하는 하드 디스크 공간 사용을 위해 파일 보존 기간에 따라 에이전트 로그에서 로그 파일입니다.

**목차**

전송 에이전트의 개요 (영문)

에이전트 로그 파일의 구조

에이전트 로그에 기록 되는 정보

에이전트 로그를 검색 합니다.

## 전송 에이전트의 개요 (영문)

에이전트는 메시지 전송 서비스에서 사서함 서버 또는 Edge 전송 서버를 통해 메시지를 전송 하기 위해 사용 되는 SMTP 명령 시퀀스에 특정 시점에 따라만 작동할 수 있습니다. SMTP 명령 시퀀스에 이러한 액세스 포인트에 *SMTP 이벤트*라고 합니다. 각 에이전트에 할당 될 수 있는 우선순위 값입니다. 그러나 SMTP 이벤트 해야 항상 특정 순서로 수행 됩니다. 따라서 에이전트 우선순위 SMTP 이벤트에 따라 달라 집니다. 두 에이전트는 동일한 SMTP 이벤트를 사용 하는 동안 메시지에 작용 수, 여 가장 높은 우선순위를 지정 하는 에이전트의 메시지에 먼저 작동 합니다.

다음 표에서 발생 하 고 각 SMTP 이벤트에 대해 내림차순 우선순위에 따라에서 에이전트 로그에 정보를 기록 하는 에이전트의 순서에서 SMTP 이벤트를 보여줍니다.

### 각 SMTP 이벤트에 대 한 우선순위에 따라 발생 하 고 에이전트에 게 정보를 기록 하는 에이전트의 순서에서 SMTP 이벤트 로그

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>SMTP 이벤트</th>
<th>에이전트</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>연결 필터링 에이전트</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>연결 필터링 에이전트</p>
<p>보낸 사람 필터 에이전트</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>연결 필터링 에이전트</p>
<p>받는 사람 필터 에이전트</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>연결 필터링 에이전트</p>
<p>보낸 사람 ID 에이전트</p>
<p>보낸 사람 필터 에이전트</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>에 지 규칙 에이전트</p>
<p>콘텐츠 필터링 에이전트</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 연결 필터링 에이전트 및에 지 규칙 에이전트에는 사서함 서버에서 사용할 수 없습니다.



에이전트, SMTP 이벤트 및 에이전트 우선 하는 방법에 대 한 자세한 내용은 [전송 에이전트](transport-agents-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

## 에이전트 로그 파일의 구조

에이전트 로그 %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog에서 존재 합니다.

에이전트 로그 파일에 대 한 명명 규칙은 AGENTLOG*yyyymmdd-nnnn*. 로그 합니다. 자리 표시자는 다음 정보를 나타냅니다.

  - 자리 표시자 *yyyymmdd*는 로그 파일이 생성된 UTC(협정 세계시) 날짜입니다. 이 자리 표시자에서 *yyyy*는 연도, *mm*는 월, *dd*는 일입니다.

  - 자리 표시자 *nnnn*은 각 날짜에 대해 값 1부터 시작하는 인스턴스 번호입니다.

파일 크기가 최대 지정 된 값을 증가 인스턴스 수를 갖는 새 로그 파일을 열 때까지 정보가 로그 파일에 기록 됩니다. 하루 동안이 프로세스가 반복 됩니다. 순환 로깅 에이전트 로그 디렉터리의 최대 지정 된 크기에 도달 하거나 로그 파일의 최대 지정 된 시간에 도달 하면 가장 오래 된 로그 파일을 삭제 합니다.

에이전트 로그 파일은 쉼표로 구분 된 값 (CSV) 파일 형식으로 데이터를에서 포함 하는 텍스트 파일입니다. 각 에이전트 로그 파일에 다음 정보를 포함 하는 헤더:

  - **\#Software**   에이전트 로그 파일을 만든 소프트웨어의 이름입니다. 일반적으로 값은 Microsoft Exchange 서버입니다.

  - **\#Version**   에이전트 로그 파일을 만든 소프트웨어의 버전 번호입니다. 현재 값이 15.0.0.0 합니다.

  - **\#Log 유형**   에이전트 로그 하는 로그 형식 값입니다.

  - **\#Date**   로그 파일이 만들어진 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. *yyyy-mm-dd*T*hh:mm:ss.fff*Z, 여기서 위치 *yyyy* = 년, *mm* = 월, *dd* = 일, T는 시간 구성 요소의 시작을 나타내며 *hh* = 시간, *mm* = 분, *ss* = 초, *fff* = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.

  - **\#Fields**   쉼표로 구분 에이전트 로그 파일에 사용 되는 필드 이름입니다.

맨 위로 이동

## 에이전트 로그에 기록 되는 정보

각 에이전트 트랜잭션 로그에 한 줄에 저장 하는 에이전트 로그 합니다. 각 줄에 저장 된 정보는 필드에 의해 구성 됩니다. 이러한 필드를 쉼표로 구분 하 여 합니다. 필드 이름은 일반적으로 알기 쉽게 포함 된 정보의 형식을 결정 합니다. 그러나 필드 중 일부만 비어 있을 수 있습니다. 또는 필드에 저장 된 정보의 유형을 에이전트 또는 메시지에는 에이전트에 의해 수행 되는 작업에 따라 변경 될 수 있습니다. 다음 표에서 각 에이전트 트랜잭션 분류에 사용 되는 필드에 설명 합니다.

### 각 에이전트 트랜잭션 분류에 사용 되는 필드

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>필드 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Timestamp</strong></p></td>
<td><p>UTC 날짜 및 시간 에이전트 이벤트입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, 여기서 위치 <em>yyyy</em> = 년, <em>mm</em> = 월, <em>dd</em> = 일, T는 시간 구성 요소의 시작을 나타내며 <em>hh</em> = 시간, <em>mm</em> = 분, <em>ss</em> = 초, <em>fff</em> = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>고유 SMTP 세션 식별자입니다. 이 식별자는 16 자리 16 진수 숫자로 표현 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>메시지를 허용 하는 로컬 IP 주소와 포트 번호입니다. SMTP 세션은 일반적으로 포트 25를 사용 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>메시지를 제공 하기 위해이 서버에 연결 하는 이전 SMTP 서버의 IP 주소와 포트 번호입니다. 경계 네트워크의 Edge 전송 서버를 통해 인터넷 메일 흐름, 사서함 서버에 있는 에이전트 로그에서 <strong>RemoteEndpoint</strong> 값 Edge 전송 서버의 IP 주소 됩니다. SMTP 하 여 메시지를 전송할 경우에 보내는 서버에서 사용 하는 포트 번호는 1, 024 보다 큰 난수가 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>먼저 메시지를 제공 하기 위해 Exchange 조직에 연결 하는 원격 SMTP 서버의 IP 주소입니다. Edge 전송 서버의 <strong>RemoteEndpoint</strong> 및 <strong>EnteredOrgFromIP</strong> 값 동일 합니다. 스팸 방지 에이전트 <strong>EnteredOrgFromIP</strong> 에서 IP 주소를 사용 하 여 메시지를 검사 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p><code>MessageID</code> 헤더 필드의 값입니다. 이 값이 비어 메시지를 수락 하는 경우 Exchange 전송 서버에만 표시 되는 임의의 값을 할당 합니다. 값을 할당 한 후 메시지의 수명 동안 <code>MessageID</code> 값이 상수입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>메시지 봉투의 <code>MAIL FROM</code> 지정 된 보낸 전자 메일 주소입니다. 이 값은 SMTP 메시징 서버 간에 메시지를 전송 하기 위해 사용 됩니다. 이 값은 메시지 헤더에서 보낸사람 주소는 위조 여부를 확인 하려면 <strong>P2FromAddresses</strong> 값에 비교 역할도 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>보낸 전자 메일 주소를 <code>From</code> 헤더 필드에서 또는 메시지 헤더에서 <code>Sender</code> 헤더 필드에 지정 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>받는 사람 전자 메일 주소입니다. 원본 메시지에는 여러 받는 사람에 게 포함 될 수 있습니다, 있지만 에이전트 로그에서 줄 당 하나만 받는 사람 표시 됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>원본 메시지의 받는 사람에 게의 총 수입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>작업을 작성 하는 에이전트의 이름입니다. 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p>콘텐츠 필터 에이전트</p></li>
<li><p>받는 사람 필터 에이전트</p></li>
<li><p>보낸 사람 필터 에이전트</p></li>
<li><p>보낸 사람 ID 에이전트</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>에이전트에 의해 작업이 있는 SMTP 이벤트입니다. <strong>Event</strong> 의 값은 에이전트에 따라 다릅니다. 각 에이전트에 게 사용할 수 있는 SMTP 이벤트는이 항목의 앞부분에서 표 1에 설명 되어있습니다. <strong>Event</strong> 에 대 한 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>에이전트에 의해 메시지에서 동작이 수행 됩니다. <strong>Action</strong> 에 대 한 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>연결 끊기</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>RFC 2034에 정의 된 SMTP 응답을 확장 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>에이전트에 의해 제공 되는 작업에 대 한 설명입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>에이전트에 의해 제공 되는 작업에 대 한 정보를 설명 합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 에이전트 로그를 검색 합니다.

에이전트 로그를 검색 하려면 **Get-AgentLog** cmdlet 및 **Get-AntiSpamFilteringReport.ps1** 스크립트를 사용할 수 있습니다.

**Get-AntiSpamFilteringReport.ps1** 스크립트는 `%ExchangeInstallPath%Scripts`에 있습니다. 셸에서 Scripts 폴더에서 스크립트를 실행 해야 합니다. 셸에서 위치 Scripts 폴더를 변경 하려면 다음 명령을 실행 합니다.

```powershell
Cd $env:ExchangeInstallPath\Scripts
```

스크립트 폴더에 스크립트를 실행 하려면 다음 구문을 사용 합니다.

    .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]

스크립트를 사용 하는 방법에 대 한 자세한 내용은, 다음 명령을 실행 합니다.

```powershell
Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1
```

맨 위로 이동

