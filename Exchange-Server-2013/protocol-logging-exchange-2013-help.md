---
title: '프로토콜 로깅: Exchange 2013 Help'
TOCTitle: 프로토콜 로깅
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 50482952
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 프로토콜 로깅

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

프로토콜 로깅은 메시지 배달의 일부로 메시징 서버 간에 발생하는 SMTP 대화를 기록합니다. 이러한 SMTP 대화는 클라이언트 액세스 서버의 프런트 엔드 전송 서비스 및 사서함 서버의 전송 서비스 그리고 사서함 서버의 사서함 전송 서비스에 있는 송신 커넥터와 수신 커넥터에서 발생합니다. 프로토콜 로깅을 사용하여 메일 흐름 문제를 진단할 수 있습니다.

기본적으로 프로토콜 로깅은 모든 송신 커넥터 및 수신 커넥터에서 비활성화되어 있습니다. 프로토콜 로깅은 커넥터에 따라 활성화 또는 비활성화됩니다. 다른 프로토콜 로깅 옵션은 서버의 각 개별 전송 서비스에 있는 모든 수신 커넥터 또는 모든 송신 커넥터에 대해 설정됩니다. 전송 서비스의 모든 수신 커넥터는 동일한 프로토콜 로그 파일과 프로토콜 로그 옵션을 공유합니다. 이러한 프로토콜 로그 파일 및 프로토콜 로그 옵션은 동일한 서버의 전송 서비스에 있는 송신 커넥터 프로토콜 로그 파일 및 프로토콜 로그 옵션과 구분됩니다.

Exchange 서버의 각 전송 서비스에 있는 모든 송신 커넥터나 모든 수신 커넥터의 프로토콜 로그에 대해 다음 옵션을 사용할 수 있습니다.

  - 송신 커넥터나 수신 커넥터 프로토콜 로그 파일의 위치를 지정합니다.

  - 송신 커넥터나 수신 커넥터 프로토콜 로그 파일의 최대 크기를 지정합니다. 기본 크기는 10MB입니다.

  - 송신 커넥터나 수신 커넥터 프로토콜 로그 파일이 포함된 디렉터리의 최대 크기를 지정합니다. 기본 크기는 250MB입니다.

  - 송신 커넥터나 수신 커넥터 프로토콜 로그 파일의 최대 보존 기간을 지정합니다. 기본 보존 기간은 30일입니다.

기본적으로 Exchange는 순환 로깅을 사용하여 파일 크기 및 파일 보존 기간을 기준으로 프로토콜 로그를 제한함으로써 로그 파일이 사용하는 하드 디스크 공간 제어에 도움을 줍니다.

조직 내 송신 커넥터라는 특수 송신 커넥터가 모든 사서함 서버의 전송 서비스와 모든 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 있습니다. 이 커넥터는 암시적으로 만들어지고 표시되지 않으며 관리할 필요가 없습니다. 조직 내 송신 커넥터는 다음 전송 서비스에서 사용됩니다.

  - **사서함 서버의 전송 서비스**
    
      - 조직의 다른 Exchange 2013 사서함 서버에 있는 전송 서비스와 사서함 전송 서비스로 메시지를 릴레이합니다.
    
      - 조직의 다른 Exchange 2007 또는 Exchange 2010 허브 전송 서버로 메시지를 릴레이합니다.
    
      - 경계 네트워크의 Edge 전송 서버로 메시지를 릴레이합니다.

  - **클라이언트 액세스 서버의 프런트 엔드 전송 서비스**   조직의 Exchange 2013 사서함 서버에 있는 전송 서비스로 메시지를 릴레이합니다.

사서함 배달 송신 커넥터라는 동등한 송신 커넥터가 모든 사서함 서버의 사서함 전송 서비스에 있습니다. 이 커넥터도 암시적으로 만들어져 보이지 않으므로 관리할 필요가 없습니다. 사서함 배달 송신 커넥터는 조직의 다른 사서함 서버에 있는 전송 서비스와 사서함 전송 서비스로 메시지를 릴레이하는 데 사용됩니다.

기본적으로 사서함 배달 송신 커넥터의 프로토콜 로깅도 사용하지 않도록 설정됩니다. **Set-MailboxTransportService** cmdlet에서 *MailboxDeliveryConnectorProtocolLoggingLevel* 매개 변수를 사용하여 사서함 배달 송신 커넥터의 프로토콜 로깅을 사용하거나 사용하지 않도록 설정할 수 있습니다. 사서함 배달 송신 커넥터의 프로토콜 로깅을 사용하도록 설정하면 사서함 서버의 사서함 전송 서비스에 대한 송신 커넥터 프로토콜 로그에 로깅이 발생합니다.

**목차**

Structure of the protocol log files

Information written to the protocol log

## 프로토콜 로그 파일의 구조

기본적으로 프로토콜 로그 파일은 다음 위치에 있습니다.

  - **사서함 서버의 전송 서비스에 대한 수신 커넥터 프로토콜 로그 파일**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **사서함 서버의 사서함 전송 서비스에 대한 수신 커넥터 프로토콜 로그 파일**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 대한 수신 커넥터 프로토콜 로그 파일**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **사서함 서버의 전송 서비스에 대한 송신 커넥터 프로토콜 로그 파일**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **사서함 서버의 사서함 전송 서비스에 대한 송신 커넥터 프로토콜 로그 파일**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 대한 송신 커넥터 프로토콜 로그 파일**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

각 프로토콜 로그 디렉터리에서 로그 파일에 대한 명명 규칙은 *prefixyyyymmdd-nnnn*.log입니다. 자리 표시자는 다음 정보를 표시합니다.

  - 자리 표시자 *prefix*는 송신 커넥터의 경우는 SEND 또는 수신 커넥터의 경우는 RECV입니다.

  - 자리 표시자 *yyyymmdd*는 로그 파일이 만들어진 UTC(Coordinated Universal Time) 날짜입니다. 자리 표시자 *yyyy*는 년, *mm*은 월 그리고 *dd*는 일입니다.

  - 자리 표시자 *nnnn*은 각 날짜에 대해 값 1에서 시작하는 인스턴스 번호입니다.

파일 크기가 지정된 최대 값에 도달할 때까지 로그 파일에 정보가 기록되며, 증가된 인스턴스 번호를 지닌 새 로그 파일이 열립니다. 이 프로세스는 하루 종일 반복됩니다. 프로토콜 로그 디렉터리가 지정된 최대 크기에 도달하거나 로그 파일이 지정된 최대 보존 기간에 도달하면 순환 로깅은 가장 오래된 로그 파일을 삭제합니다.

프로토콜 로그 파일은 쉼표로 분리된 값 파일(CSV) 형식의 데이터가 포함된 텍스트 파일입니다. 각 프로토콜 로그 파일에는 다음과 같은 정보가 들어있는 헤더가 있습니다.

  - **\#Software:**   프로토콜 로그 파일을 만든 소프트웨어의 이름입니다. 일반적으로 이 값은 Microsoft Exchange Server입니다.

  - **\#Version:**   프로토콜 로그 파일을 만든 소프트웨어의 버전 번호입니다. 현재 이 값은 15.0.0.0입니다.

  - **\#Log-Type:**   이 필드의 로그 유형 값은 SMTP 수신 프로토콜 로그나 SMTP 송신 프로토콜 로그입니다.

  - **\#Date:**   로그 파일이 만들어진 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. *yyyy-mm-dd*T*hh:mm:ss.fff*Z, 여기서 위치 *yyyy* = 년, *mm* = 월, *dd* = 일, T는 시간 구성 요소의 시작을 나타내며 *hh* = 시간, *mm* = 분, *ss* = 초, *fff* = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.

  - **\#Fields:**   프로토콜 로그 파일에서 사용되는 쉼표로 분리된 필드 이름입니다.

맨 위로 이동

## 프로토콜 로그에 기록되는 정보

프로토콜 로그는 프로토콜 로그의 한 줄에 각 SMTP 프로토콜 이벤트를 저장합니다. 각 줄에 저장된 정보는 필드로 구성되고 이러한 필드는 쉼표로 분리됩니다. 다음 표에서는 각 프로토콜을 분류하는 데 사용되는 필드에 대해 설명합니다.

### 각 프로토콜 이벤트를 분류하는 데 사용되는 필드

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
<td><p>프로토콜 이벤트의 UTC 날짜-시간입니다. UTC 날짜-시간은 다음과 같은 ISO 8601 날짜-시간 형식으로 표시됩니다. <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, 여기서 위치 <em>yyyy</em> = 년, <em>mm</em> = 월, <em>dd</em> = 일, T는 시간 구성 요소의 시작을 나타내며 <em>hh</em> = 시간, <em>mm</em> = 분, <em>ss</em> = 초, <em>fff</em> = 초의 소수 단위, Z = Zulu(UTC를 표시하는 다른 방식)를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>SMTP 이벤트와 연결된 커넥터의 DN(고유 이름)입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>각 SMTP 세션에 대해서는 고유하지만 해당 SMTP 세션과 연결된 각 이벤트에 대해서는 동일한 GUID입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>같은 SMTP 세션 내에서 각 이벤트에 대해 0에서 시작하여 증가되는 카운터입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>SMTP 세션의 로컬 끝점입니다. IP 주소와 TCP 포트 번호로 구성되며 형식은 <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>SMTP 세션의 원격 끝점입니다. IP 주소와 TCP 포트 번호로 구성되며 형식은 <em>&lt;IP address&gt;</em>:<em>&lt;port&gt;</em>입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>프로토콜 이벤트를 표시하는 단일 문자입니다. 이벤트에 대해 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p><strong>+</strong>   Connect</p></li>
<li><p><strong>-</strong>   Disconnect</p></li>
<li><p><strong>&gt;</strong>   Send</p></li>
<li><p><strong>&lt;</strong>   Receive</p></li>
<li><p><strong>*</strong>   정보</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>SMTP 이벤트와 연결된 텍스트 정보입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>SMTP 이벤트와 연결될 수 있는 추가적인 문맥 정보입니다.</p></td>
</tr>
</tbody>
</table>


단일 전자 메일 메시지의 송수신을 나타내는 단일 SMTP 대화는 여러 SMTP 이벤트를 생성합니다. 이러한 SMTP 이벤트에 따라 여러 줄이 프로토콜 로그에 기록됩니다. 복수 전자 메일 메시지의 송수신을 나타내는 복수 SMTP 대화는 동시에 발생할 수 있습니다. 이에 따라 떨어져 있는 서로 다른 SMTP 대화에서 프로토콜 로그 항목이 만들어집니다. 그러나 session-id 및 sequence-number 필드를 사용하여 SMTP 대화별로 프로토콜 로그 항목을 정렬할 수 있습니다.

맨 위로 이동

