---
title: '메시지 추적: Exchange 2013 Help'
TOCTitle: 메시지 추적
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51407739
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 메시지 추적

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013에서 메시지 추적 로그는 사서함 서버의 전송 서비스, 사서함 서버의 사서함 및 Edge 전송 서버를 오고가는 메시지 전송 시 수행되는 모든 메시지 작업에 대한 상세 레코드입니다. 메시지 정보 분석, 메일 흐름 분석, 보고 및 문제 해결을 위해 메시지 추적 로그를 사용할 수 있습니다.

Exchange 2013에서는 모든 메시지 추적 구성 작업에 **Set-TransportService** cmdlet 또는 **Set-MailboxServer** cmdlet을 사용할 수 있습니다. Exchange 2013 사서함 서버에 Transport Service와 사서함이 있기 때문입니다. 이 두 cmdlet 중 하나를 사용하여 다음 메시지 추적 구성을 변경할 수 있습니다.

  - 메시지 추적을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 사용하도록 설정되어 있습니다.

  - 메시지 추적 로그 파일의 위치를 지정합니다.

  - 개별 메시지 추적 로그 파일의 최대 크기를 지정합니다. 기본값은 10MB입니다.

  - 메시지 추적 로그 파일이 있는 디렉터리의 최대 크기를 지정합니다. 기본값은 1,000 MB입니다.

  - 메시지 추적 로그 파일의 최대 보존 기간을 지정합니다. 기본값은 30일입니다.

  - 메시지 추적 로그에서 메시지 제목 로깅을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 사용하도록 설정되어 있습니다.


> [!NOTE]
> EAC(Exchange 관리 센터)를 사용하여 메시지 추적을 사용하거나 사용하지 않도록 설정하고 메시지 추적 로그 파일의 위치를 지정할 수도 있습니다.



기본적으로 Exchange는 순환 로깅을 사용하여 파일 크기와 파일 보존 기간을 기준으로 메시지 추적 로그를 제한함으로써 메시지 추적 로그 파일에서 사용하는 하드 디스크 공간을 제어합니다.

**목차**

메시지 추적 로그 검색

메시지 추적 로그 파일의 구조

메시지 추적 로그 파일의 필드

메시지 추적 로그의 이벤트 유형

메시지 추적 로그의 원본 값

메시지 추적 로그의 항목 예

메시지 추적 로그에 대한 보안 문제

## 메시지 추적 로그 검색

메시지가 Exchange 2013 사서함 서버를 통해 이동할 때는 메시지 추적 로그에 많은 데이터가 포함됩니다. 메시지 추적 로그는 다양한 옵션을 통해 검색할 수 있습니다.

  - **Get-MessageTrackingLog**   관리자는 이 cmdlet을 사용하여 광범위한 필터 조건을 통해 메시지 추적 로그에서 메시지에 대한 정보를 검색할 수 있습니다. 자세한 내용은 [메시지 추적 로그 검색](search-message-tracking-logs-exchange-2013-help.md)을 참조하십시오.

  - **관리자용 배달 보고서**   관리자는 EAC(Exchange 관리 센터)의 **배달 보고서** 탭 또는 기본 **Search-MessageTrackingReport** 및 **Get-MesageTrackingReport** cmdlet을 사용하여 메시지 추적 로그에서 조직의 특정 사서함이 보내거나 받은 메시지에 대한 정보를 검색할 수 있습니다. 자세한 내용은 [관리자에 대 한 배달 보고서](delivery-reports-for-administrators-exchange-2013-help.md)를 참조하십시오.

  - **사용자용 배달 보고서**   사용자는 Outlook Web App의 **배달 보고서** 탭을 사용하여 메시지 추적 로그에서 자신의 사서함으로 보내거나 사서함에서 보낸 메시지에 대한 정보를 검색할 수 있습니다. 자세한 내용은 [배달 보고서](https://go.microsoft.com/fwlink/?linkid=279920)를 참조하세요.

맨 위로 이동

## 메시지 추적 로그 파일의 구조

기본적으로 메시지 추적 로그 파일은 %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking에 있습니다.

메시지 추적 로그 디렉터리에서 로그 파일의 명명 규칙은 `MSGTRK`*yyyymmdd-nnnn*`.log`, `MSGTRKMA`*yyyymmdd-nnnn*`.log`, `MSGTRKMD`*yyyymmdd-nnnn*`.log` 및 `MSGTRKMS`*yyyymmdd-nnnn*`.log`입니다. 다음 서비스에서는 서로 다른 로그를 사용합니다.

  - **MSGTRK**   Transport Service와 연관된 로그입니다.

  - **MSGTRKMA**   중재된 전송에서 사용하는 승인 및 거부와 연관된 로그입니다. 자세한 내용은 [메시지 승인 관리](manage-message-approval-exchange-2013-help.md)을 참조하십시오.

  - **MSGTRKMD**   사서함 전송 배달 서비스에 의해 사서함으로 배달되는 메시지와 연관된 로그입니다.

  - **MSGTRKMS**   사서함 전송 제출 서비스에 의해 사서함에서 보내는 메시지와 연관된 로그입니다.

로그 파일 이름의 자리 표시자는 다음 정보를 나타냅니다.

  - 자리 표시자 *yyyymmdd*는 로그 파일이 만들어진 UTC(Coordinated Universal Time) 날짜입니다. 여기서 *yyyy*는 년, *mm*은 월, *dd*는 일을 표시합니다.

  - 자리 표시자 *nnnn*은 각 메시지 추적 로그 파일 이름 접두사에 대해 매일 값 1에서 시작하는 인스턴스 번호입니다.

파일 크기가 각 로그 파일에 대해 지정된 최대값에 도달할 때까지 각 로그 파일에 정보가 기록됩니다. 그런 다음 인스턴스 번호가 증가된 상태로 새 로그 파일이 열립니다. 이 프로세스는 하루 종일 반복됩니다. 로그 파일 순환 기능은 다음 조건 중 하나가 만족될 때 가장 오래된 로그 파일을 삭제합니다.

  - 로그 파일이 지정된 최대 보존 기간에 도달합니다.

  - 메시지 추적 로그 디렉터리가 지정된 최대 크기에 도달합니다.
    

    > [!IMPORTANT]
    > 메시지 추적 로그 디렉터리의 최대 크기는 이름 접두사가 같은 모든 로그 파일의 전체 크기로 계산됩니다. 이름 접두사 규칙을 따르지 않는 다른 파일은 전체 디렉터리 크기를 계산할 때 합산되지 않습니다. 이전 로그 파일의 이름을 바꾸거나 다른 파일을 메시지 추적 로그 디렉터리로 복사하면 디렉터리의 지정된 최대 크기를 초과할 수 있습니다.<BR>Exchange 2013 사서함 서버에서 메시지 추적 로그 디렉터리의 최대 크기는 지정된 값의 세 배입니다. 서로 다른 네 가지 서비스에서 생성되는 메시지 추적 로그 파일의 이름 접두사는 모두 다르지만, <STRONG>MSGTRKMA</STRONG> 로그 파일에 기록되는 데이터의 양과 빈도는 나머지 3개 로그 파일 접두사에 비해 매우 적습니다.



메시지 추적 로그 파일은 CSV(쉼표로 분리된 값) 형식의 데이터가 포함되어 있는 텍스트 파일입니다. 각 메시지 추적 로그 파일에는 다음과 같은 정보가 포함된 헤더가 있습니다.

  - **\#Software:**   해당 메시지 추적 로그 파일을 만든 소프트웨어의 이름입니다. 일반적으로 이 값은 Microsoft Exchange Server입니다.

  - **\#Version:**   해당 메시지 추적 로그 파일을 만든 소프트웨어의 버전 번호입니다. 현재 이 값은 15.0.0.0입니다.

  - **\#Log-Type**   로그 유형 값으로, Message Tracking Log입니다.

  - **\#Date:**   로그 파일이 만들어진 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. *yyyy-mm-dd*T*hh:mm:ss.fff*Z, 여기서 위치 *yyyy* = 년, *mm* = 월, *dd* = 일, T는 시간 구성 요소의 시작을 나타내며 *hh* = 시간, *mm* = 분, *ss* = 초, *fff* = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.

  - **\#Fields:**   메시지 추적 로그 파일에서 사용되는 쉼표로 분리된 필드 이름입니다.

맨 위로 이동

## 메시지 추적 로그 파일의 필드

메시지 추적 로그는 로그의 한 줄에 각 메시지 이벤트를 저장합니다. 메시지 이벤트 정보는 필드로 구성되며 이러한 필드는 쉼표로 구분됩니다. 필드 이름은 일반적으로 필드에 포함된 정보 유형을 판단할 수 있는 설명 형식입니다. 그러나 필드 중 일부가 비어 있거나 필드에 저장된 정보 유형이 메시지 이벤트 유형 및 이벤트가 기록된 메시지 추적 로그 파일의 유형에 따라 바뀔 수 있습니다. 각 메시지 추적 이벤트를 분류하는 데 사용되는 필드에 대한 일반적인 설명은 다음 표에 나와 있습니다.


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
<td><p>메시지 추적 이벤트의 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, 여기서 위치 <em>yyyy</em> = 년, <em>mm</em> = 월, <em>dd</em> = 일, T는 시간 구성 요소의 시작을 나타내며 <em>hh</em> = 시간, <em>mm</em> = 분, <em>ss</em> = 초, <em>fff</em> = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>메시지를 전송한 메시징 서버 또는 메시징 클라이언트의 IPv4 또는 IPv6 주소입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>메시지를 전송한 메시징 서버 또는 메시징 클라이언트의 호스트 이름 또는 FQDN입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>원본 또는 대상 Exchange 서버의 IPv4 또는 IPv6 주소입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>대상 서버의 호스트 이름 또는 FQDN입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p><strong>source</strong> 필드와 관련된 추가 정보입니다. 전송 에이전트 정보를 예로 들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>원본 또는 대상 송신 커넥터나 수신 커넥터의 이름입니다. 예를 들어 <em>ServerName</em>\<em>ConnectorName</em> 또는 <em>ConnectorName</em>입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>메시지 추적 이벤트를 담당하는 Exchange 전송 구성 요소입니다. 이 필드의 값에 대한 설명은 이 항목 뒷부분의 메시지 추적 로그의 원본 값 섹션에 나와 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>메시지 이벤트 유형입니다. 이벤트 유형에 대한 설명은 이 항목 뒷부분의 메시지 추적 로그의 이벤트 유형 섹션에 나와 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>현재 메시지를 처리 중인 Exchange 서버에서 할당한 메시지 식별자입니다.</p>
<p>특정 메시지의 <strong>internal-message-id</strong> 값은 해당 메시지의 전송과 관련된 모든 Exchange 서버의 메시지 추적 로그에서 서로 다릅니다. <code>73014444033</code>과 같은 값을 예로 들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>메시지 헤더의 <strong>Message-Id:</strong> 헤더 필드 값입니다. <strong>Message-Id:</strong> 헤더 필드가 없거나 비어 있으면 임의의 값이 할당됩니다. 이 값은 메시지 수명을 나타내는 상수입니다. Exchange에서 작성하는 메시지의 경우 값은 <code>&lt;GUID@ServerFQDN&gt;</code> 형식이며 꺾쇠 괄호(<code>&lt; &gt;</code>)를 포함합니다. 예를 들면 <code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>입니다. 다른 메시징 시스템에서는 다른 구문이나 값을 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>분기 또는 메일 그룹 확장으로 인해 작성될 수 있는 메시지 복사본 전체에서 유지되는 고유한 메시지 ID 값입니다. <code>1341ac7b13fb42ab4d4408cf7f55890f</code>와 같은 값을 예로 들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>메시지 받는 사람의 전자 메일 주소입니다. 전자 메일 주소가 여러 개인 경우 세미콜론(;)으로 구분합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>이 필드에는 세미콜론(;)으로 구분된 각 받는 사람의 받는 사람 상태가 포함됩니다. 상태 값은 <strong>recipient-address</strong> 필드의 값과 같은 순서로 받는 사람에 대해 표시됩니다. <code>250 2.1.5 Recipient OK</code>, <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code> 등의 상태 값을 예로 들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>첨부 파일이 포함된 메시지의 크기(바이트)입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>메시지를 받는 사람의 수입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>이 필드에 <strong>EXPAND</strong>, <strong>REDIRECT</strong> 및 <strong>RESOLVE</strong> 이벤트를 함께 사용하여 메시지와 관련된 다른 받는 사람의 전자 메일 주소를 표시합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>이 필드에는 특정 유형의 이벤트에 대한 추가 정보가 포함됩니다. 예를 들면 다음과 같습니다.</p>
<p><strong>DSN</strong>   보고서 링크를 포함합니다. 이 이벤트 이후에 DSN(배달 상태 알림)이 생성된 경우 관련 DSN의 <strong>Message-Id</strong> 값입니다. DSN 메시지인 경우에는 <strong>Reference</strong> 필드에 해당 DSN이 생성된 원본 메시지의 <strong>Message-Id</strong> 값이 포함됩니다.</p>
<p><strong>EXPAND</strong>   Reference 필드에는 관련 메시지의 <strong>related-recipient-address</strong> 값이 포함됩니다.</p>
<p><strong>RECEIVE</strong>   저널링 또는 받은 편지함 규칙과 같은 기타 프로세스에 의해 메시지가 생성된 경우 Reference 필드에 관련 메시지의 <strong>Message-Id</strong> 값이 포함될 수 있습니다.</p>
<p><strong>SEND</strong>   Reference 필드에는 모든 DSN 메시지의 <strong>Internal-Message-Id</strong> 값이 포함됩니다.</p>
<p><strong>THROTTLE</strong>   Reference 필드에는 메시지가 제한된 이유가 포함됩니다.</p>
<p><strong>TRANSFER</strong>   참조 필드에는 분기 중인 메시지의 Internal-Message-Id가 포함됩니다.</p>
<p>받은 편지함 규칙에 의해 생성된 메시지의 경우 <strong>Reference</strong> 필드에는 받은 편지함 규칙이 아웃바운드 메시지를 생성하도록 한 인바운드 메시지의 <strong>Internal-Message-Id</strong> 값이 포함됩니다.</p>
<p>기타 이벤트 유형의 경우에는 <strong>Reference</strong> 필드에 분기된 메시지의 <strong>Internal-Message-Id</strong> 값이 포함될 수 있습니다.</p>
<p>기타 이벤트 유형에서는 보통 <strong>Reference</strong> 필드가 비어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>메시지 제목은 <code>Subject:</code> 헤더 필드에 있습니다. 메시지 제목 추적은 <strong>Set-TransportService</strong> 또는 <strong>Set-MailboxServer</strong> cmdlet의 <em>MessageTrackingLogSubjectLoggingEnabled</em> 매개 변수에 의해 제어됩니다. 기본적으로 메시지 제목 추적은 사용하도록 설정되어 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p><code>Sender:</code> 헤더 필드에 지정된 전자 메일 주소이거나, <code>Sender:</code>가 없으면 <code>From:</code> 헤더 필드에 지정된 전자 메일 주소입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p><code>MAIL FROM:</code>에서 지정한 메시지 봉투의 반환 전자 메일 주소입니다. 이 필드는 비어 있지 않지만 <code>&lt;&gt;</code>로 표시되는 null 보낸 사람 주소 값을 가질 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>메시지에 대한 추가 정보입니다. 예를 들면 다음과 같습니다.</p>
<ul>
<li><p><strong>DELIVER</strong> 및 <strong>SEND</strong> 이벤트에 대한 메시지 발생 UTC 날짜/시간입니다. 발생 날짜/시간은 메시지가 Exchange 조직에 처음 들어간 시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, 여기서 위치 <em>yyyy</em> = 년, <em>mm</em> = 월, <em>dd</em> = 일, T는 시간 구성 요소의 시작을 나타내며 <em>hh</em> = 시간, <em>mm</em> = 분, <em>ss</em> = 초, <em>fff</em> = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.</p></li>
<li><p>인증 오류입니다. 예를 들어 <code>11a</code> 값과 인증 오류 발생 시 사용한 인증 유형이 표시될 수 있습니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>메시지의 방향입니다. 예를 들어 <code>Incoming</code>, <code>Undefined</code>, <code>Originating</code> 값이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>이 필드는 온-프레미스 Exchange 2013 조직에서는 사용되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>원래 클라이언트의 IPv4 또는 IPv6 주소입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>원래 서버의 IPv4 또는 IPv6 주소입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>이 필드에는 특정 이벤트 유형과 관련된 데이터가 포함됩니다. 예를 들어 전송 규칙 에이전트는 이 필드를 사용하여 메시지에 적용된 전송 규칙 또는 DLP 정책의 GUID를 기록합니다. 이러한 전송 규칙 에이전트 값에 대한 자세한 내용은 <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">DLP 정책 검색 보고서 보기</a> 항목의 &quot;데이터 기록&quot; 섹션을 참조하십시오.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메시지 추적 로그의 이벤트 유형

**event-id** 필드의 다양한 이벤트 유형을 사용하여 메시지 추적 로그의 메시지 이벤트를 분류합니다. 한 가지 유형의 메시지 추적 로그 파일에만 나타나는 메시지 이벤트도 있고, 모든 유형의 메시지 추적 로그 파일에 나타나는 메시지 이벤트도 있습니다. 각 메시지 이벤트를 분류하는 데 사용되는 이벤트 유형은 다음 표에 설명되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>이벤트 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>전송 에이전트가 사용자 지정 데이터를 기록하는 데 사용하는 이벤트입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>메시지가 배달하거나 반환할 수 없는 Pickup 디렉터리나 Replay 디렉터리에서 전송되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>메시지 배달이 지연되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>메시지가 로컬 사서함으로 배달되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>메시지가 배달 상태 알림(DSN, 바운스 메시지, 배달 못 함 보고서 또는 NDR이라고도 함) 없이 삭제되었습니다. 예를 들면 다음과 같습니다.</p>
<ul>
<li><p>중재 승인 요청 완료 메시지</p></li>
<li><p>NDR 없이 자동으로 삭제된 스팸 메시지</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>DSN(배달 상태 알림)이 생성되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>받는 사람에게 중복 메시지가 배달되었습니다. 받는 사람이 중첩된 여러 메일 그룹의 구성원이면 메시지가 중복될 수 있습니다. 정보 저장소에서 중복 메시지를 찾아 제거합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>메일 그룹 확장 중에 중복된 받는 사람이 검색되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>메시지의 다른 받는 사람이 이미 받는 사람입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>메일 그룹이 확장되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>메시지를 배달하지 못했습니다. 원본에는 <strong>SMTP</strong>, <strong>DNS</strong>, <strong>QUEUE</strong>, <strong>ROUTING</strong>이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>기본 복사본을 다음 홉으로 배달한 후 섀도 메시지가 삭제되었습니다. 자세한 내용은 <a href="shadow-redundancy-exchange-2013-help.md">섀도 중복성</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>로컬 DAG(데이터베이스 사용 가능 그룹) 또는 Active Directory 사이트의 서버가 섀도 메시지를 받았습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>섀도 메시지가 작성되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>섀도 메시지를 작성하지 못했습니다. 세부 정보는 <strong>source-context</strong> 필드에 저장됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>중재된 받는 사람에게 보낸 메시지가 승인을 위해 중재 사서함으로 전송되었습니다. 자세한 내용은 <a href="manage-message-approval-exchange-2013-help.md">메시지 승인 관리</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>부팅 시 메시지가 정상적으로 로드되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>중재된 받는 사람에 대한 중재자가 메시지를 승인하거나 거부하지 않아 메시지가 만료되었습니다. 중재된 받는 사람에 대한 자세한 내용은 <a href="manage-message-approval-exchange-2013-help.md">메시지 승인 관리</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>중재된 받는 사람에 대한 중재자가 메시지를 승인하여 메시지가 중재된 받는 사람에게 배달되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>중재된 받는 사람에 대한 중재자가 메시지를 거부하여 메시지가 중재된 받는 사람에게 배달되지 않았습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>중재된 받는 사람의 모든 중재자에게 보낸 모든 승인 요청을 배달할 수 없어 배달 못 함 보고서(NDR)가 생성되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>로컬 서버에 있는 사서함의 보낼 편지함에서 메시지가 검색되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>로컬 서버에 있는 사서함의 보낼 편지함에서 메시지가 검색되었으며 메시지의 섀도 복사본을 만들어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>메시지가 포이즌 메시지 큐에 추가되었거나 포이즌 메시지 큐에서 제거되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>메시지가 처리되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>모임 메시지가 사서함 전송 배달 서비스에 의해 처리되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>Pickup/Replay 디렉터리 또는 Transport Service의 SMTP 수신 구성 요소(원본: <code>SMTP</code>)가 메시지를 받았거나, 사서함에서 사서함 전송 제출 서비스로 메시지를 전송했습니다(원본: <code>STOREDRIVER</code>).</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>메시지가 Active Directory 조회 후에 다른 받는 사람에게 리디렉션되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>메시지 받는 사람을 Active Directory 조회 후에 다른 전자 메일 주소로 확인했습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>보안 네트워크에서 메시지가 자동으로 다시 전송되었습니다. 자세한 내용은 <a href="safety-net-exchange-2013-help.md">보안 네트워크</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>보안 네트워크에서 다시 전송된 메시지가 지연되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>보안 네트워크에서 다시 전송된 메시지에 오류가 발생했습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>메시지가 Transport Service 간에 SMTP를 통해 전송되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>사서함 전송 제출 서비스에서 메시지를 Transport Service로 전송했습니다. <strong>SUBMIT</strong> 이벤트의 경우 <strong>source-context</strong> 속성에는 다음 세부 정보가 포함됩니다.</p>
<ul>
<li><p><strong>MDB</strong>   사서함 데이터베이스 GUID입니다.</p></li>
<li><p><strong>Mailbox</strong>   사서함 GUID입니다.</p></li>
<li><p><strong>Event</strong>   이벤트 시퀀스 번호입니다.</p></li>
<li><p><strong>MessageClass</strong>   메시지의 유형입니다. 예: <code>IPM.Note</code>.</p></li>
<li><p><strong>CreationTime</strong>   메시지 전송 날짜/시간입니다.</p></li>
<li><p><strong>ClientType</strong>   <code>User</code>, <code>OWA</code> 또는 <code>ActiveSync</code> 등이 있습니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>사서함 전송 제출 서비스에서 Transport Service로의 메시지 전송이 지연되었습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>사서함 전송 제출 서비스에서 Transport Service로의 메시지 전송이 실패했습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>메시지가 전송되지 않았습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>메시지가 제한되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>콘텐츠 변환, 메시지 받는 사람 수 제한 또는 에이전트로 인해 받는 사람이 분기된 메시지로 이동되었습니다. 원본에는 <strong>ROUTING</strong> 또는 <strong>QUEUE</strong>가 포함됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메시지 추적 로그의 원본 값

메시지 추적 로그의 **source** 필드 값은 메시지 추적 이벤트를 담당하는 전송 구성 요소를 나타냅니다. 다음 표에서는 **source** 필드의 값에 대해 설명합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>원본 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>이벤트 원본이 수동 작업입니다. 예를 들어 관리자가 큐 뷰어를 사용하여 메시지를 삭제했거나 Replay 디렉터리를 사용하여 메시지 파일을 전송했습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>이벤트 원본이 전송 에이전트입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>이벤트 원본이 중재된 받는 사람에게 사용되는 승인 프레임워크입니다. 자세한 내용은 <a href="manage-message-approval-exchange-2013-help.md">메시지 승인 관리</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>이벤트 원본이 부팅 시에 서버에 존재하는 처리되지 않은 메시지입니다. <strong>LOAD</strong> 이벤트 유형과 관련이 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>이벤트 원본이 DNS입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>이벤트 원본이 DSN(배달 상태 알림)입니다. 배달 못 함 보고서(NDR) 등을 예로 들 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>이벤트 원본이 외부 커넥터입니다. 자세한 내용은 <a href="foreign-connectors-exchange-2013-help.md">외부 커넥터</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>이벤트 원본이 받은 편지함 규칙입니다. 자세한 내용은 <a href="https://go.microsoft.com/fwlink/?linkid=285479">받은 편지함 규칙</a>을 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>이벤트 원본이 모임 업데이트를 기준으로 일정을 업데이트하는 모임 메시지 프로세서입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>이벤트 원본이 ORAR(Originator Requested Alternate Recipient)입니다. <strong>New-ReceiveConnector</strong> 또는 <strong>Set-ReceiveConnector</strong> cmdlet에서 <em>OrarEnabled</em> 매개 변수를 사용하여 수신 커넥터에서 ORAR 지원을 사용하거나 사용하지 않도록 설정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>이벤트 원본이 Pickup 디렉터리입니다. 자세한 내용은 <a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Pickup 디렉터리 및 Replay 디렉터리</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>이벤트 원본이 포이즌 메시지 식별자입니다. 포이즌 메시지 및 포이즌 메시지 큐에 대한 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>이벤트 원본이 메일 사용 가능 공용 폴더입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>이벤트 원본이 큐입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>이벤트 원본이 섀도 중복성입니다. 자세한 내용은 <a href="shadow-redundancy-exchange-2013-help.md">섀도 중복성</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>이벤트 원본이 Transport Service에 있는 분류기의 라우팅 확인 구성 요소입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>이벤트 원본이 보안 네트워크입니다. 자세한 내용은 <a href="safety-net-exchange-2013-help.md">보안 네트워크</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>Transport Service의 SMTP 송신 또는 SMTP 수신 구성 요소가 메시지를 전송했습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>이벤트 원본이 로컬 서버에 있는 사서함의 MAPI 전송입니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메시지 추적 로그의 항목 예

두 사용자 간에 이벤트가 없는 메시지가 전송되어 메시지 추적 로그에 여러 항목이 생성됩니다. **Get-MessageTrackingLog** cmdlet을 사용하여 결과를 확인할 수 있습니다. 자세한 내용은 [메시지 추적 로그 검색](search-message-tracking-logs-exchange-2013-help.md)을 참조하십시오.

이 예는 chris@contoso.com 사용자가 michelle@contoso.com 사용자에게 테스트 메시지를 보내는 경우 생성되는 메시지 추적 로그 항목의 압축된 예입니다. 두 사용자의 사서함은 같은 서버에 있습니다.

    EventId    Source      Sender            Recipients             MessageSubject
    -------    ------      ------            ----------             --------------
    NOTIFYMAPI STOREDRIVER                   {}
    RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
    HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
    RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
    AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
    SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
    DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test

맨 위로 이동

## 메시지 추적 로그에 대한 보안 문제

메시지 내용은 메시지 추적 로그에 저장되지 않습니다. 기본적으로 전자 메일 메시지의 제목 줄은 메시지 추적 로그에 저장됩니다. 날로 증가하는 보안이나 프라이버시 요구 사항을 충족하기 위해 메시지 제목 로깅을 사용하지 않을 수 있습니다. 메시지 제목 로깅을 사용하거나 사용하지 않도록 설정하려면 먼저 제목 줄 정보의 공개에 대해 조직의 정책을 확인해야 합니다. 자세한 내용은 [메시지 추적 구성](configure-message-tracking-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

