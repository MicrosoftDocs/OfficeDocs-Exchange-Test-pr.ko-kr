---
title: '연결 로깅: Exchange 2013 Help'
TOCTitle: 연결 로깅
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 50484088
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 연결 로깅

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

연결 로깅은 Exchange 서버의 전송 서비스에서 메시지를 전송하는 데 사용되는 아웃바운드 연결 활동을 기록합니다. 연결 로그는 개별 전자 메일 메시지의 전송을 추적하기 위한 것이 아니며, 전송되는 메시지의 수에 상관없이 원본에서 대상으로의 연결 활동을 추적합니다. 연결 로깅은 클라이언트 액세스 서버의 프런트 엔드 전송 서비스, 사서함 서버의 전송 서비스 및 사서함 서버의 사서함 전송 서비스에서 사용할 수 있습니다. 다음 목록에서는 연결 로그에 기록된 정보 유형에 대해 설명합니다.

  - 원본

  - Destination

  - DNS 확인 정보

  - 연결 실패에 대한 자세한 정보

  - 전송된 메시지 및 바이트 수

Exchange 관리 셸에서 **Set-TransportService**, **Set-FrontEndTransportService** 및 **Set-MailboxTransportService** cmdlet을 사용하면 모든 연결 로그 구성 작업을 수행할 수 있습니다. 연결 로그에 사용할 수 있는 옵션은 다음과 같습니다.

  - 연결 로깅을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 사용하도록 설정되어 있습니다.

  - 연결 로그 파일의 위치를 지정합니다.

  - 개별 연결 로그 파일의 최대 크기를 지정합니다. 기본 크기는 10MB입니다.

  - 연결 로그 파일이 있는 디렉터리의 최대 크기를 지정합니다. 기본 크기는 1000MB입니다.

  - 연결 로그 파일의 최대 보존 기간을 지정합니다. 기본 보존 기간은 30일입니다.

기본적으로 Exchange는 순환 로깅을 사용하여 파일 크기와 파일 보존 기간을 기준으로 연결 로그를 제한함으로써 연결 로그 파일에서 사용하는 하드 디스크 공간을 제어합니다.

**목차**

Structure of the connectivity log files

Information written to the connectivity log

## 연결 로그 파일의 구조

기본적으로 연결 로그 파일은 다음 위치에 있습니다.

  - **Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

연결 로그 파일의 명명 규칙은 CONNECTLOG*yyymmdd-nnnn*.log입니다. 자리 표시자는 다음 정보를 표시합니다.

  - 자리 표시자 *yyyymmdd*는 로그 파일이 생성된 UTC(협정 세계시) 날짜입니다. 이 자리 표시자에서 *yyyy*는 연도, *mm*는 월, *dd*는 일입니다.

  - 자리 표시자 *nnnn*은 각 날짜에 대해 값 1부터 시작하는 인스턴스 번호입니다.

파일 크기가 지정된 최대 값에 도달할 때까지 로그 파일에 정보가 기록되며, 인스턴스 번호가 증가된 새 로그 파일이 열립니다. 이 프로세스는 하루 종일 반복됩니다. 연결 로그 디렉터리가 지정된 최대 크기에 도달하거나 로그 파일이 지정된 최대 보존 기간에 도달하면 순환 로깅은 가장 오래된 로그 파일을 삭제합니다.

연결 로그 파일은 CSV(쉼표로 분리된 값) 파일 형식의 데이터가 포함된 텍스트 파일입니다. 각 연결 로그 파일에는 다음과 같은 정보가 들어 있는 헤더가 있습니다.

  - **\#Software**   해당 연결 로그 파일을 만든 소프트웨어의 이름입니다. 일반적으로 이 값은 Microsoft Exchange Server입니다.

  - **\#Version**   해당 연결 로그 파일을 만든 소프트웨어의 버전 번호입니다. 현재 이 값은 15.0.0.0입니다.

  - **\#Log-Type**   로그 유형 값으로, Transport Connectivity Log입니다.

  - **\#Date**   로그 파일이 만들어진 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. *yyyy-mm-dd*T*hh:mm:ss.fff*Z, 여기서 위치 *yyyy* = 년, *mm* = 월, *dd* = 일, T는 시간 구성 요소의 시작을 나타내며 *hh* = 시간, *mm* = 분, *ss* = 초, *fff* = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.

  - **\#Fields**   해당 연결 로그 파일에서 사용되는 쉼표로 분리된 필드 이름입니다.

맨 위로 이동

## 연결 로그에 기록되는 정보

연결 로그는 각 아웃바운드 전송 서비스 연결 이벤트를 한 줄로 저장합니다. 각 줄에 저장된 정보는 필드로 구성되고 이러한 필드는 쉼표로 분리됩니다. 다음 표에서는 각 보내는 연결 이벤트를 분류하는 데 사용되는 필드를 설명합니다.

### 각 연결 이벤트를 분류하는 데 사용되는 필드

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
<td><p><strong>date-time</strong></p></td>
<td><p>연결 이벤트의 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, 여기서 위치 <em>yyyy</em> = 년, <em>mm</em> = 월, <em>dd</em> = 일, T는 시간 구성 요소의 시작을 나타내며 <em>hh</em> = 시간, <em>mm</em> = 분, <em>ss</em> = 초, <em>fff</em> = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>각 SMTP 세션에 대해서는 고유하지만 해당 SMTP 세션과 연결된 각 이벤트에 대해서는 동일한 GUID입니다. 사서함 전송 서비스의 MAPI 세션의 경우 세션 필드가 비어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p>SMTP 연결의 경우 <strong>SMTP</strong>, 로컬 사서함 데이터베이스에 대한 사서함 전송 서비스 연결의 경우 <strong>MAPI</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>대상 이름입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>연결의 시작, 중간 또는 끝을 나타내는 단일 문자입니다. direction 필드에 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p><strong>+</strong>   Connect</p></li>
<li><p><strong>-</strong>   Disconnect</p></li>
<li><p><strong>&gt;</strong>   Send</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>연결 이벤트와 연결된 텍스트 정보입니다. description 필드에 다음과 같은 값을 사용할 수 있습니다.</p>
<ul>
<li><p>전송된 메시지의 수 및 크기</p></li>
<li><p>대상 도메인에 대한 DNS MX 리소스 레코드 확인 정보</p></li>
<li><p>대상 사서함 서버에 대한 DNS 확인 정보</p></li>
<li><p>연결 설정 메시지</p></li>
<li><p>연결 실패 메시지</p></li>
</ul></td>
</tr>
</tbody>
</table>


전송 서비스가 대상에 대한 연결을 설정하면 전송 서비스는 메시지 하나 또는 메시지 여러 개를 보낼 준비가 된 것입니다. 연결 및 메시지 전송 프로세스는 연결 로그의 여러 줄에 기록되는 여러 개의 이벤트를 생성합니다. 여러 대상에 동시에 연결하면 인터레이스되는 여러 대상에 관련된 연결 로그 항목이 만들어집니다. 그러나 date-time, session, source 및 direction 필드를 사용하여 시작될 때부터 완료될 때까지 각각의 별도 연결에 대해 연결 로그 항목을 정렬할 수 있습니다.

맨 위로 이동

