---
title: '메시지 제한: Exchange 2013 Help'
TOCTitle: 메시지 제한
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 50484580
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 제한

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

*메시지 제한* 메시지와 Microsoft Exchange Server 2013 컴퓨터에서 처리할 수 있는 연결 수에 설정 된 제한의 그룹을 참조 합니다. 이러한 제한에는 Exchange 서버의 시스템 리소스의 우연히 또는 고의적 소모 되지 않게 합니다.

**콘텐츠**

범위를 제한 하는 메시지

비용 메시지 및 메일 흐름 제한

서버에서 제한 되는 메시지

송신 커넥터에서 제한 되는 메시지

수신 커넥터에서 제한 되는 메시지

메시지 제한 정책

## 범위를 제한 하는 메시지

메시지 제한 하는 다양 한 비율, SMTP 연결 속도 및 SMTP 세션 제한 시간 값을 처리 하는 메시지에 대 한 제한 포함 됩니다. 이러한 제한 사항에 동의 하 고 메시지를 전달 하 여 너무 많을에서 Exchange 서버를 보호 하기 위해 함께 작동 합니다. 메시지와 연결 큰 백로그 처리 기다리고 있을 수 있습니다, 있지만 메시지 제한 제한 순차적인 방식으로 메시지 및 연결을 처리 하는 Exchange 서버를 활성화 합니다.

메시지 제한 외에도 메시지의 받는 사람, 메시지 헤더의 크기 또는 개별 첨부 파일의 크기 번호 등의 개별 구성 요소에 크기 제한의 넣을 수 있습니다. 메시지 크기 제한에 대 한 자세한 내용은 [메시지 크기 제한](message-size-limits-exchange-2013-help.md)을 참조 하십시오.

다른 Exchange 전송 서버의 시스템 리소스를 초과 방지할 수 있는 기능은 *역 압력*있습니다. 역 압력은 시스템 리소스 모니터링 하 고 Edge 전송 서버에서 사서함 서버의 전송 서비스의 기능입니다. 예: 하드 디스크 사용률 또는 메모리 사용률을 모니터링된 시스템 리소스를 지정된 된 임계값을 초과 하면 서버는 메시지를 하 고 새 연결을 허용 하 고 기존 메시지 배달에 중점을 두고 속도 줄입니다. 모니터링된 시스템 리소스의 사용률이 정상 수준을 반환 하는 경우 서버는 새 연결을 수락 하 고 다음 보통 수준을 설정 하는 속도 느리게 증가 합니다.

맨위로 돌아가기

## 비용 메시지 및 메일 흐름 제한

보다 일관성 있는 메시지 처리량 및 예측 가능한 메시지 배달 대기 시간을 제공 하려면 Exchange 2013 메시지는 누적된 비용을 설정 합니다. 이 품질 QoS (서비스) 기능을 Microsoft Exchange Server 2010 비용은 다음 기준에 따라 SP1This에에서 추가 되었습니다.

  - 메시지 크기

  - 받는 사람 수

  - 전송 빈도

Exchange 2013 전송 서버는 개별 사용자가 보낸 메시지의 평균 배달 비용을 추적 합니다. 메시지 비용을 사용 하 여 Exchange 2013 사용자 또는 연결은 Exchange 조직에 주는 영향을 제어할 수 있는 설정의 그룹을 제공 합니다. 이 그룹 설정에는 *제한 정책*이라고 합니다. 반복 해 서 사용자 예: 큰 첨부 파일이 있는 메시지 또는 Exchange 2013 여러 받는 사람에 게 보낸 메시지를 비용이 많이 드는 메시지를 보낼 때-기반된 전송 서버 제한 정책을 사용 하 여에서 메시지를 더 높은 비용을 더 낮은 우선순위를 할당 하는 순위가 가장 낮은 메시지 배달를 계속 수행 하는 동안 사용자입니다. "서비스 품질" 측면 Exchange 2013 의 기능을 제한 하는 메시지에 추가 하는이 새로운 동작입니다.


> [!NOTE]
> 메시지 제한 사용자의 관점에서 볼 때 메시지 우선순위 영향을 미치지 않습니다. 메시지는 사용자가 설정 하는 원래 우선순위를 계속 유지 됩니다. 예, 메시지 중요 또는 긴급의 설정을 유지 하 고 등입니다.



이 기능을 지원 하려면 Exchange 2013 에서는 다음과 같은 메커니즘을 사용 합니다.

  - **내부 우선순위 에이전트**   이 에이전트 **OnResolvedMessage** 이벤트에서 트리거되는 및 높은 누적 비용 동일한 보낸에서 메시지에 더 낮은 우선순위를 할당 합니다. 이 비용 1 분의 일정 기간 동안 측정 및 500 명이 넘는 받는 사람에 게가 있는 또는 1 메가바이트 (MB)를 초과 하는 메시지에 영향을 줍니다.

  - **MapiDelivery 큐 형식에 대 한 큐 할당량 기반 우선순위**   이 메커니즘 하면 Exchange가 낮은 우선순위 큐의 메시지 보다 더 자주 보통 우선순위 큐에서 메시지를 배달 합니다. 기본적으로 20: 1은 보통-낮음 메시지 비율입니다. 그러나 낮은 우선순위 큐에서 새 메시지 더 높은 우선순위 큐에서 새 항목 보다 빨리 배달 되지 됩니다. 다음 시나리오를 가정해봅니다 예:
    
    1.  20 개 보통 우선순위 메시지가 배달 됩니다. 기본적으로 다음 전달 된 메시지는 더 낮은 우선순위 메시지가입니다.
    
    2.  전송 서버에 의해 두 새 메시지를 받을: 하 고 더 낮은 우선순위 큐에서 메시지를 하나 더 높은 우선순위 큐에서 메시지를 하나입니다.
    
    이 시나리오에서는 더 높은 우선순위 큐에서 메시지는 먼저 배달 됩니다. 그런 다음, 낮은 우선순위 큐에서 메시지 배달 됩니다.

  - **메시징 데이터베이스 상태에 따라 동시 연결 제한**   이 메커니즘 (MDB) 데이터베이스 상태를 메시징 Exchange의 상태를 모니터링 하 고 할당된 된 상태 측정 값에 따라 Exchange 전송 서버에 대 한 동시 연결 하면 제한 합니다. MDB은 사서함 서버의 전송 서비스에서 리소스 상태 모니터 API에 의해 모니터링 하 고-1에서 100 사이의 상태 값이 할당 됩니다. 이 값은 사서함 전송 서비스에서 Store.exe 프로세스에서 각 RPC 응답에 포함 된 RPC 성능 통계를 기반으로 합니다. 리소스 상태 프레임 워크를 사용 하 여 **초당 요청** 속도 성능 카운터와 **평균 RPC 대기 시간** 성능 카운터를 모두 데이터베이스에 대 한 상태 값을 계산 합니다. 일관성 있는 대화형 사용자 경험을 유지 하려면 Exchange 상태 값 감소도 동시 연결 수를 줄입니다. 다음 상태 값의 범위를 사용할 수 있습니다.
    
      - **-1**:이 값을 지정 MDB 상태 상태를 알 수 없습니다. 이 값은 데이터베이스를 시작할 때 할당 됩니다. 이 시나리오에서는 데이터베이스 정상 간주 됩니다.
    
      - **0:** 데이터베이스가 정상적인 상태가 하는 경우이 값이 할당 됩니다. 이 상태 데이터베이스를 연결할 수 있어야 합니다.
    
      - **1부터 99 까지의:** 이러한 값 공정 상태를 나타냅니다. 낮은 값 덜 정상 상태 데이터베이스를 나타냅니다.
    
      - **100**:이 값이 정상 데이터베이스를 나타냅니다.

Microsoft Exchange 제한 서비스 메일 흐름 제한에 대 한 프레임 워크를 제공 합니다. Microsoft Exchange 제한 서비스 제한 설정을 특정 사용자에 대 한 메일 흐름을 추적 하 고 메모리에 제한 정보를 캐시 합니다. 메일 흐름 제한 설정은도 알려져 *예산*입니다. Microsoft Exchange 제한 서비스를 다시 시작 예산이 제한 하는 메일 흐름으로 다시 설정 합니다.

제한 정책에 대 한 개별 예산 설정을 구성 하려면 Exchange 2013 에서 제공 되는 제한 정책 cmdlet을 사용할 수 있습니다. 예산은 특정 설정에 대 한 사용자 또는 응용 프로그램이 포함 될 수 있는 액세스의 양입니다. 예산 한 사용자가 얼마나 많은 연결 또는 사용자 얼마나 많은 활동 각 1 분 기간에 대 한 권한이 부여 될 수를 나타냅니다. 예, 사용자 수 시간을 백분율로 나타내는 ActiveSync, Outlook Web App 또는 Exchange 웹 서비스와 같은 Exchange에서 특정 기능을 사용 하는 시간을 설정 하려면 예산을 구성할 수 있습니다. 이 임계값 제한 정책에 저장 되 고 예산 정의 합니다.

예산에 대 한 시간 설정은 1 분의 백분율로 설정 됩니다. 따라서 100%의 임계값 60 초를 나타냅니다. 예, 시간 하는 동안 사용자 클라이언트 액세스 서버에서 Outlook Web App 코드를 실행할 수 및 사용자를 600 클라이언트 액세스 서버와 통신할 수 시간 제한 하는 Outlook Web App 정책 설정을 지정 하려면 가정 1 분 일정 기간 동안 시간 (밀리초)입니다. 이를 위해 해야 1 %1 분 (600 밀리초)의 값을 설정 하려면 다음 매개 변수를 모두에 대 한.

  - **OWAPercentTimeInCAS:** 1

  - **OWAPercentTimeInMailboxRPC:** 1

이 정책을 적용을 가진 사용자에 게 예산이 OWAPercentTimeInCAS 600 시간 (밀리초) 및 OWAPercentageTimeInMailboxRPC 600 시간 (밀리초)입니다. 이 시나리오에서는 사용자가 Outlook Web App 로그인 한 경우 사용자 600 최대 시간 (밀리초)에 대 한 클라이언트 액세스 코드를 실행할 수 있습니다. 600 밀리초 기간 후 연결 예산을 것으로 간주 됩니다 및 Exchange server 예산 제한에 도달 하면 1 분까지 이후 Outlook Web App 작업을 허용 하지 않습니다. 1 분 기간이 지난 후 사용자는 다른 600 시간 (밀리초)에 대 한 Outlook Web App 클라이언트 액세스 코드를 실행할 수 있습니다.

맨위로 돌아가기

## 서버에서 제한 되는 메시지

다음 위치에서 옵션을 제한 하는 메시지를 설정할 수 있습니다.

  - 전송 서비스

  - 송신 커넥터에서

  - 수신 커넥터

Exchange 관리 셸을 사용 하 여 클라이언트 액세스 서버의 프런트엔드 전송 서비스 또는 사서함 서버의 사서함 전송 서비스에서 사서함 서버의 전송 서비스에서 사용할 수 있는 옵션을 제한 하는 모든 메시지를 설정할 수 있습니다. Exchange 관리 센터 (EAC)에서 전송 서버 속성을 구성 하 여 동일한 옵션 중 일부를 설정할 수도 있습니다.

다음 표에서 전송 서버에서 사용할 수 있는 옵션을 제한 하는 메시지를 보여줍니다.

### 전송 서버에서이 옵션을 제한 하는 메시지

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>이 매개 변수는 배달 스레드 사서함에 메시지 배달에 동시에 전송 서비스 열려 있을 수 있는 최대 수를 지정 합니다. 이 매개 변수에 유효한 입력된 범위는 1에서 256 사이의 합니다. Microsoft 고객 서비스 및 지원 하도록 권장할 경우이 작업을 수행 하지 않으면 기본 값을 수정 하지 않는 것이 좋습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>이 매개 변수는 전송 스레드 사서함에서 메시지를 보내는 동시에 전송 서비스 열려 있을 수 최대 수를 지정 합니다. 이 매개 변수에 유효한 입력된 범위는 1에서 256 사이의 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>이 매개 변수는 연결 전송 서비스를 사용 하 여 연 수에 허용 되는 최대 속도 지정 합니다. 동시에 전송 서비스와 함께 포함할 연결을 하려고 하는 경우 <em>MaxConnectionRatePerMinute</em> 매개 변수는 속도 제한 하는 연결 열린 서버 리소스의 초과 되지 않도록 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> 또는</p>
<p>전송 서버 속성</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>이 매개 변수는 한번에 열 수 있는 아웃 바운드 연결의 최대 수를 지정 합니다. <code>unlimited</code>의 값을 입력할 경우 아웃 바운드 연결 수에 제한이 없습니다 적용 됩니다. 이 매개 변수 값은 <em>MaxPerDomainOutboundConnections</em> 매개 변수 값 보다 크거나 이어야 합니다.</p>
<p>EAC를 사용 하 여 <strong>서버</strong> 에서이 값 구성할 수도 있습니다 &gt; <strong>서버</strong> &gt; <strong>속성</strong> &gt; <strong>전송 제한</strong> &gt; <strong>아웃 바운드 연결 제한</strong> 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> 또는</p>
<p>전송 서버 속성</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>이 매개 변수는 모든 단일 도메인에 대 한 동시 연결의 최대 수를 지정 합니다. <code>unlimited</code>의 값을 입력 하면 제한 없음 도메인당 아웃 바운드 연결 수에 적용 됩니다. 이 매개 변수 값은 <em>MaxOutboundConnections</em> 매개 변수 값 보다 크거나 이어야 합니다.</p>
<p>EAC를 사용 하 여 <strong>서버</strong> 에서이 값 구성할 수도 있습니다 &gt; <strong>서버</strong> &gt; <strong>속성</strong> &gt; <strong>전송 제한</strong> &gt; <strong>아웃 바운드 연결 제한</strong> 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>이 매개 변수는 Pickup 디렉터리 및 Replay 디렉터리 분당 처리 되는 메시지의 최대 수를 지정 합니다. 각 디렉터리가 매개이 변수에 의해 지정 된 속도로 메시지 파일 독립적으로 처리할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 송신 커넥터에서 제한 되는 메시지

다음 표에서 송신 커넥터에서 사용할 수 있는 옵션을 제한 하는 메시지를 보여줍니다. 이 옵션을 구성 하려면 Exchange 관리 셸을 사용 하 여 해야 합니다.

### 송신 커넥터에 사용할 수 있는 옵션을 제한 하는 메시지

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10분</p></td>
<td><p>이 매개 변수는 대상 메시징 서버와의 열린 SMTP 연결이 닫히기 전에 유휴 상태를 유지할 수 있는 최대 시간을 지정합니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 수신 커넥터에서 제한 되는 메시지

다음 표에서 사서함 서버 또는 Edge 전송 서버에서 전송 서비스에서 구성 된 수신 커넥터에서 사용할 수 있는 옵션을 제한 하는 메시지를 보여줍니다. 이러한 옵션을 구성 하려면 Exchange 관리 셸을 사용 하 여 해야 합니다.

### 수신 커넥터에서 사용할 수 있는 옵션을 제한 하는 메시지

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>사서함 서버의 전송 서비스에서 5분</p>
<p>클라이언트 액세스 서버의 프런트 엔드 전송 서비스에서 5분</p>
<p>Edge 전송 서버에서 1분</p></td>
<td><p>이 매개 변수는 원본 메시징 서버와의 열린 SMTP 연결이 닫히기 전에 유휴 상태를 유지할 수 있는 최대 시간을 지정합니다. 이 매개 변수의 값은 <em>ConnectionTimeout</em> 매개 변수로 지정된 값보다 작아야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>사서함 서버의 전송 서비스에서 10분</p>
<p>클라이언트 액세스 서버의 프런트 엔드 전송 서비스에서 10분</p>
<p>Edge 전송 서버에서 5분</p></td>
<td><p>이 매개 변수는 원본 메시징 서버가 데이터를 전송 중인 경우에도 원본 메시징 서버와의 SMTP 연결이 열린 상태로 유지될 수 있는 최대 시간을 지정합니다. 이 매개 변수의 값은 <em>ConnectionInactivityTimeout</em> 매개 변수로 지정된 값보다 커야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>이 매개 변수는이 수신 커넥터가 동시에 수 있게 하는 인바운드 SMTP 연결의 최대 수를 지정 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>사서함 서버의 전송 서비스의 기본 수신 커넥터에 100%</p>
<p>사서함 서버의 전송 서비스 및 클라이언트 액세스 서버의 프런트엔드 전송 서비스에서 다른 수신 커넥터에서 %2입니다.</p></td>
<td><p>이 매개 변수는 메시징 서버는 단일 소스에서 동시에 수신 커넥터를 허용 하는 SMTP 연결의 최대 수를 지정 합니다. 값은 수신 커넥터에서 사용 가능한 나머지 연결의 백분율로 표시 됩니다. 수신 커넥터에서 허용 되는 연결의 최대 수는 <em>MaxInboundConnection</em> 매개 변수에 의해 정의 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>사서함 서버의 전송 서비스의 기본 수신 커넥터에 unlimited</p>
<p>사서함 서버의 전송 서비스 및 클라이언트 액세스 서버의 프런트엔드 전송 서비스에서 다른 수신 커넥터에서 20입니다.</p></td>
<td><p>이 매개 변수는 메시징 서버는 단일 소스에서 동시에 수신 커넥터를 허용 하는 SMTP 연결의 최대 수를 지정 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>이 매개 변수는 수신 커넥터 허용 원본 메시징 서버와의 연결에 수신 커넥터 닫히고 하기 전에 SMTP 프로토콜 오류의 최대 수를 지정 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 초</p></td>
<td><p>이 매개 변수는 <em>타피팅</em>에 사용 되는 지연 시간을 지정 합니다. 타피팅은 인해 디렉터리 수집 공격 또는 기타 원치 않는 메시지를 표시 하는 특정 SMTP 통신 패턴에 대 한 SMTP 응답을 연기 하는 방식입니다. <em>디렉터리 수집 공격</em> 은 원치 않는 상업성 전자 메일에 대 한 대상으로 사용 하 여 특정 조직에서 유효한 전자 메일 주소를 수집 하려고 합니다.</p>
<p><em>TarpitInterval</em> 매개 변수에 의해 지정 된 지연 익명 연결에만 적용 됩니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 메시지 제한 정책

Exchange 2013 각 사서함에 있는 *ThrottlingPolicy* 설정 되어있습니다. 이 설정에 대 한 기본값은 빈 (`$null`). 사서함에 대 한 제한 정책을 구성 하려면 **Set-Mailbox** cmdlet에서 *ThrottlingPolicy* 매개 변수를 사용할 수 있습니다.

기본 Exchange에 연결 하는 사용자에 대 한 예산 구성 집합을 제공 하는 기본 제한 정책 존재 합니다. 하나 이상의 사용자에 대 한 사용자 지정 된 예산 설정을 변경 하려면 새 제한 정책을 만듭니다. 해당 하는 사용자 또는 그룹에 정책을 적용 한 다음, 합니다.


> [!IMPORTANT]
> 기본 제한 정책 수정 하지 하는 것이 좋습니다.



Exchange 관리 셸에서 사서함 서버에서 사용할 수 있는 옵션을 제한 하는 모든 메시지를 설정할 수 있습니다. 다음 cmdlet 제한 정책 관리를 사용할 수 있습니다.

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

사용자가 특정 연결 또는 기간을 통해 Exchange에 대해 수행할 수 얼마나 많은 활동을 구성 하는 **New-ThrottlingPolicy** 및 **Set-ThrottlingPolicy** cmdlet을 사용할 수 있습니다. 이러한 설정은 사용자의 예산이 구성 합니다. 다음 Exchange 기능에 대 한 액세스를 제어 하는 제한 정책을 설정할 수 있습니다.

  - Exchange ActiveSync

  - Exchange Web Services

  - Outlook Web App

  - 통합 메시징

  - IMAP4

  - POP3

  - Outlook 클라이언트 연결 (MAPI 또는 RPC 연결)

  - 메일 흐름 설정

  - PowerShell 명령

  - CPU 사용

맨위로 돌아가기

