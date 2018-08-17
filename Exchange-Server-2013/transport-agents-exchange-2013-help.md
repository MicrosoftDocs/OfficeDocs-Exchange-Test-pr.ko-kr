---
title: '전송 에이전트: Exchange 2013 Help'
TOCTitle: 전송 에이전트
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 50484396
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 에이전트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

전송 에이전트를 사용 하면 Microsoft, 타사 공급 업체 또는 Exchange 서버에서 조직에서 만든 사용자 지정 소프트웨어를 설치할 수 있습니다. 이 소프트웨어는 전송 파이프라인을 통해 전달 되는 전자 메일 메시지를 처리할 수 있습니다. Microsoft Exchange Server 2013 에서 전송 파이프라인은 다음 프로세스 이루어집니다.

  - 클라이언트 액세스 서버의 프런트엔드 전송 서비스

  - 사서함 서버의 전송 서비스

  - 사서함 서버의 사서함 전송 서비스

  - Edge 전송 서버의 전송 서비스

전송 파이프라인에 대 한 자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md) 을 참조 하십시오.

이전 버전의 Exchange와 마찬가지로 Exchange 2013 전송 Microsoft Exchange Server 2013 전송 에이전트 SDK를 통해 확장성을 제공합니다. SDK의 Exchange 2013 버전은 Microsoft.NET Framework 버전 4.0에 기반 하 고 다음과 같은 미리 정의 된 클래스를 구현 하는 타사 수 있습니다:

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

SDK의 라이브러리에 대해 컴파일 때 Exchange 2013, 에이전트를 로드 하 고 특정 단계 SMTP 세션 또는 메시지를 처리 하는 동안 해당 이벤트 처리기를 호출 하는 결과 어셈블리 등록 됩니다. 이러한 단계를 또는 이벤트에는 에이전트 정의에 포함 됩니다. 에이전트 등록 정보는 XML 구성 파일에 저장 됩니다.

다음 목록에서는 Exchange 2013 에서 전송 에이전트를 사용 하기 위한 요구 사항에 설명 합니다.

  - 사서함 서버 및 Edge 전송 서버에서 전송 서비스는 완벽 하 게 SDK, 및 Microsoft Exchange Server 2010 에서 역할을 세워야 Exchange 2013 에서 전송 서비스에서 허브 전송 또는 Edge 전송 서버 용으로 작성 된 모든 제 3 자 전송 에이전트 따라서의 미리 정의 된 모든 클래스를 지원 합니다.

  - 프런트엔드 전송 서비스의 sdk에서만 **SmtpReceiveAgent** 클래스를 지원할 뿐 이며 제 3 자 에이전트 **OnEndOfData** SMTP 이벤트에서 작동할 수 없습니다.

  - 사서함 전송 서비스에서 모든 제 3 자 에이전트를 사용할 수 없습니다 사서함 전송 서비스 SDK를 전혀 지원 하지 않습니다.

버전 4.0 하기 전에 .NET Framework 의 버전에 따라 레거시 전송 에이전트에 대 한 지원 되지 않습니다 기본적으로 사용할 수 있지만 설정할 수 있습니다. 자세한 내용은 [레거시 전송 에이전트에 대 한 지원을 사용 하도록 설정](enable-support-for-legacy-transport-agents-exchange-2013-help.md)를 참조 하십시오.

**목차**

전송 에이전트 관리에 대 한 업데이트

전송 에이전트 및 SMTP 이벤트

전송 에이전트의 우선순위

기본 제공 전송 에이전트

전송 에이전트를 해결 합니다.

## 전송 에이전트 관리에 대 한 업데이트

Exchange 2013 전송 파이프라인에 업데이트를으로 인해 전송 에이전트 cmdlet는 클라이언트 액세스 서버와 사서함 서버는 동일한 컴퓨터에 설치 된 경우에 특히 전송 서비스 및 프런트엔드 전송 서비스를 구분 해야 합니다. 자세한 내용은 [전송 에이전트를 관리 합니다.](manage-transport-agents-exchange-2013-help.md)을 참조 하십시오.

전송 에이전트 관리 cmdlet `%ExchangeInstallPath%TransportRoles\Shared`에 있는 구성 파일을 조작 합니다. 사서함 서버 및 Edge 전송 서버에서 전송 서비스에 대 한 파일은 `agents.config`. 클라이언트 액세스 서버의 프런트엔드 전송 서비스에 대 한 파일은 `fetagents.config`. 두 파일 모두 Exchange 2010 와 같은 서식을 사용합니다. 전송 에이전트를 관리 하는 방법에 대 한 자세한 내용은 [전송 에이전트를 관리 합니다.](manage-transport-agents-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

## 전송 에이전트 및 SMTP 이벤트

전송 에이전트 SMTP 이벤트를 사용 합니다. 이러한 이벤트는 전송 파이프라인을 통해 이동 하는 메시지에 따라 트리거됩니다. SMTP 이벤트 귀하에 게 전송 에이전트 액세스 특정 시점 메시지 조직을 통해 메시지의 라우팅 및 SMTP 대화 중입니다.

Exchange 2013 에서 새 SMTP 수신 이벤트는 메모 합니다. 클라이언트 액세스 서버, 사서함 서버 및 Edge 전송 서버에서 전송 서비스 및 사서함 서버에 있는 사서함 전송 배달 서비스에 있는 프런트엔드 전송 서비스에 있는 SMTP 수신 합니다. 분류기는 Edge 전송 서버 및 사서함 서버에서 전송 서비스에만 존재 합니다. 전송 서비스 및 분류기 하는 방법에 대 한 자세한 내용은 [메일 라우팅](mail-routing-exchange-2013-help.md)을 참조 하십시오.

다음 표에서 전송 파이프라인에 있는 메시지에 대 한 액세스를 제공 하는 SMTP 이벤트를 나열 합니다.

### SMTP 수신 이벤트

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>시퀀스</th>
<th>SMTP 이벤트</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에서 초기 연결에 의해 트리거됩니다.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>HELO</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>EHLO</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>STARTTLS</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>AUTH</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트를 사용 하 여 인증을 처리 하는 중 때 트리거됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에서 인증을 완료 하는 경우 발생 합니다.</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>XSESSIONPARAMS</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>MAIL FROM</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>RCPT TO</code> 명령이 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>이 이벤트는 <code>DATA</code> (텍스트) 또는 <code>BDAT</code> (이진 데이터) 명령을 원격 SMTP 호스트에 의해 실행 될 때 트리거됩니다.</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트 전자 메일 메시지 헤더를 전송 완료 되 면 트리거됩니다. 이 경우 메시지 머리글 및 메시지 본문을 구분 하는 빈 줄 (<code>&lt;CRLF&gt;</code>)으로 표시 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>이 이벤트는 인바운드 SMTP 세션은 릴레이 때 트리거되는 <em>프록시</em> 사서함 서버의 전송 서비스에 대 한 클라이언트 액세스 서버의 프런트엔드 전송 서비스에 의해 또는 합니다.</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트 문제는 최종 데이터 명령의 때 트리거됩니다. <code>DATA</code> 명령에 의해 시작 텍스트 세션에 대 한 데이터 표시기의 끝 <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>됩니다. <code>BDAT</code> 명령에 의해 시작 이진 세션에 대 한 데이터 표시기의 끝 <code>BDAT LAST</code>됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>HELP</code> 명령을 실행 하는 경우 발생 합니다.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>이 이벤트는 원격 SMTP 호스트에 의해 <code>NOOP</code> 명령을 실행 하는 경우 발생 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>이 이벤트는 받는 SMTP 호스트에서 보내는 SMTP 호스트에 일시적 또는 영구적 배달 상태 알림 (DSN) 코드를 발급 하는 경우에 발생 합니다.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>이 이벤트는 보내는 SMTP 호스트에 의해 <code>RSET</code> 명령을 실행 하는 경우에 발생 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>이 이벤트는 수신 또는 SMTP 호스트를 보내는 SMTP 대화의 연결을 끊는에 의해 트리거됩니다. 일반적으로 이러한 <code>QUIT</code> 명령을 원격 SMTP 호스트에 의해 실행 될 때 발생 합니다.</p></td>
</tr>
</tbody>
</table>


\* \* 이러한 이벤트는 **OnDisconnectEvent**하기 전에 **OnConnectEvent** 후 언제 든 지 발생할 수 있습니다.

### 분류기 이벤트

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>시퀀스</th>
<th>분류기 이벤트</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>이 이벤트는 수신 사서함 서버 또는 Edge 전송 서버에서 전송 서비스에서 전송 큐에서 메시지가 도착할 때 트리거됩니다.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>이 이벤트는 모든 받는 사람에 게가 해결 되었지만 전에 다음 홉 각 받는 사람에 대해 결정 한 후에 발생 합니다. <strong>OnResolvedMessage</strong> 라우팅 이벤트를는 받는 사람별 <strong>SetRoutingOverride</strong> 메서드를 사용 하 여 기본 라우팅 동작을 재정의 하려면 후속 이벤트 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>이 이벤트는 메시지 분류 된 메일 그룹 확장 되었습니다, 하 고 받는 사람에 게 확인 된 후 발생 합니다.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>이 이벤트는 분류기 메시지 처리를 완료 될 때 트리거됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 전송 에이전트의 우선순위

전송 에이전트 전송 파이프라인에 있는 메시지에 작용 하는 순서를 결정 하는 두 요인 가지가 있습니다.

1.  여기서 전송 에이전트가 등록 되어 있고, SMTP 이벤트는 SMTP 이벤트 메시지를 발견 하는 경우 한 합니다.

2.  여러 에이전트가 있는 경우 전송 에이전트에 게 할당 된 우선순위 값 동일한 SMTP 이벤트에 등록 합니다. 가장 높은 우선순위는 1입니다. 높은 값을 더 낮은 에이전트 우선순위를 나타냅니다.

예 다음 전송 에이전트를 구성한 경우를 가정해 보겠습니다.

  - 전송 에이전트 A 1의 우선순위로 전송 에이전트 C 2의 우선순위로 **OnEndOfHeaders** SMTP 이벤트에 등록 됩니다.

  - 전송 에이전트 B 4의 우선순위로 **OnMailCommand** SMTP 이벤트에 등록 됩니다.

전송 에이전트 B 메시지에 먼저 적용 된 **OnMailCommand** 이벤트에서 **OnEndOfHeaders** 이벤트가 발생 하기 전에 메시지를 발생 하기 때문에 있습니다. 전송 에이전트 C 하기 전에 전송 에이전트 A 적용 메시지에 도달 하면 **OnEndOfHeaders** 이벤트, 전송 에이전트 A 전송 에이전트 C. 보다 더 높은 우선순위 (낮은 integer 값)에 있기 때문에

## 기본 제공 전송 에이전트

Exchange 2013 스팸 방지, 전송 규칙 및 저널링 등의 기능을 제공 하는 여러 기본 제공 전송 에이전트를 포함 합니다. Exchange 2013 사서함 서버 및 클라이언트 액세스 서버에서 기본 제공 전송 에이전트 대부분이 보이지 않게 하 고 전송 에이전트 관리 cmdlet에서 관리 불가능 합니다. 거의 모든는 보고 관리할 수 있는 기본 제공 전송 에이전트 모두에 Edge 전송 서버에서 사서함 서버의 전송 서비스에서.

사서함 서버에 더 흥미로운 기본 제공 전송 에이전트는 다음 표에 설명 되어있습니다. 참고가이 표에 다양 한 보이지 못하며 전송 에이전트를 포함 되지 않습니다.

### 사서함 서버에 관심 있는 기본 제공 전송 에이전트

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>에이전트 이름</th>
<th>관리할 수 있습니까?</th>
<th>우선 순위</th>
<th>SMTP 또는 분류기 이벤트</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전송 규칙 에이전트</p></td>
<td><p>예</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>맬웨어 에이전트</p></td>
<td><p>예</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>텍스트 메시징 라우팅 에이전트</p></td>
<td><p>예</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>텍스트 메시징 배달 에이전트</p></td>
<td><p>예</p></td>
<td><p>4</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>저널 에이전트</p></td>
<td><p>아니요</p></td>
<td><p>구성 가능</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>저널 보고서 암호 해독 에이전트</p></td>
<td><p>아니요</p></td>
<td><p>구성 가능</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 암호 해독 에이전트</p></td>
<td><p>아니요</p></td>
<td><p>구성 가능</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>RMS 암호화 에이전트</p></td>
<td><p>아니요</p></td>
<td><p>구성 가능</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>RMS 프로토콜 암호 해독 에이전트</p></td>
<td><p>아니요</p></td>
<td><p>구성 가능</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


Edge 전송 서버에서 대부분의 기본 제공 전송 에이전트는 보고 전송 에이전트 관리 cmdlet에서 또는 다른 기능별 cmdlet으로 관리할 수 있습니다.

Edge 전송 서버에서 더 흥미로운 기본 제공 전송 에이전트는 다음 표에 설명 되어있습니다. 참고가이 표가 표시 되지 않도록 하거나 관리할 수 없는 전송 에이전트를 포함 되지 않습니다.

### Edge 전송 서버에서 관심 있는 기본 제공 전송 에이전트

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>에이전트 이름</th>
<th>관리할 수 있습니까?</th>
<th>우선 순위</th>
<th>SMTP 또는 분류기 이벤트</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>연결 필터링 에이전트</p></td>
<td><p>예</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnMailCommand</strong>, <strong>OnRcptComand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>주소 다시 쓰기 인바운드 에이전트</p></td>
<td><p>예</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>에 지 규칙 에이전트</p></td>
<td><p>예</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>콘텐츠 필터 에이전트 *</p></td>
<td><p>예</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>보낸사람 ID 에이전트 *</p></td>
<td><p>예</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>보낸사람 필터 에이전트 *</p></td>
<td><p>예</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>받는 사람 필터 에이전트</p></td>
<td><p>예</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>프로토콜 분석 에이전트 *</p></td>
<td><p>예</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnEndOfHeaders</strong>, <strong>OnEndOfData</strong>, <strong>OnReject</strong>, <strong>OnRsetCommand</strong>, <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>첨부 파일 필터링 에이전트</p></td>
<td><p>예</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>주소 다시 쓰기 아웃 바운드 에이전트</p></td>
<td><p>예</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* 설치 및 사서함 서버에서 이러한 스팸 방지 에이전트를 구성할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

## 전송 에이전트를 해결 합니다.

전송 에이전트와 함께 문제를 해결 하는데 도움이 되, 다음과 같은 기능을 사용할 수 있습니다.

  - **Get-transportpipeline**   이 cmdlet는 SMTP 이벤트와 Exchange 서버에서 메시지에 발생 하는 해당 전송 에이전트를 보여줍니다. 자세한 내용은 [전송 파이프라인에 보기 전송 에이전트](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md)을 참조 하십시오.

  - **파이프라인 추적**   파이프라인 추적 하기 전에 메시지의 하 고 각 전송 에이전트를 발견 한 이후에 정확한 스냅숏을 만듭니다. 이 옵션을 사용 하면 예기치 않은 결과가 일으키는 전송 에이전트를 찾을 수 있습니다. 자세한 내용은 [파이프라인 추적](pipeline-tracing-exchange-2013-help.md)을 참조 하십시오.

맨 위로 이동

