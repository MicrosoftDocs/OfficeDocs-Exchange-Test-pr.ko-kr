---
title: '메시지 다시 시도, 다시 전송, 및 만료 간격: Exchange 2013 Help'
TOCTitle: 메시지 다시 시도, 다시 전송, 및 만료 간격
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51407660
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 다시 시도, 다시 전송, 및 만료 간격

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013 에서 성공적으로 배달할 수 없는 메시지는 메시지의 원본 및 대상에 따라 다양 한 다시 시도, 다시 전송, 및 만료 기한을 적용 됩니다. 대상와 갱신된 연결 시도 하는 *다시 시도* 합니다. *다시 전송* 하는 것은에 메시지를 다시 전송 큐를 다시 처리할 분류기에 대 한 전송 하는 행위입니다. 메시지 *만료* 모든 배달 방법이 지정 된 기간 동안 실패 합니다. 메시지 만료 되 면 배달 오류는 보낸사람에 게 알립니다. 다음은 메시지 큐에서 삭제 됩니다.

다시 시도, 다시 전송 또는 만료, 이 세 가지의 경우 모두 메시지에 대해 자동으로 작업이 수행되기 전에 사용자가 수동으로 개입할 수 있습니다.

이러한 간격을 구성하는 방법에 대한 지침은 [메시지 다시 시도, 다시 전송, 및 만료 간격 구성](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)을 참조하십시오.

## 메시지 다시 시도에 대한 구성 옵션

전송 서버가 다음 홉에 연결할 수 없으면 큐가 다시 시도 상태가 됩니다. 큐가 만료되거나 연결될 때까지 연결이 계속 시도됩니다.

## 자동 메시지 다시 시도에 대한 구성 옵션

메시지 다시 시도 간격에 사용할 수 있는 구성 옵션은 다음 표에 설명되어 있습니다.

### 메시지 다시 시도 간격에 사용할 수 있는 구성 옵션

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수 또는 키 이름</th>
<th>기본값</th>
<th>구성할 위치</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>이 키는 전송 서버가 대상 서버와 연결할 때 문제가 발생하면 즉시 실행되는 연결 시도의 횟수를 지정합니다. 이러한 연결 문제는 대부분 일시적인 네트워크 중단으로 인해 발생합니다.</p>
<p>이 키에는 0에서 15까지의 정수를 입력할 수 있습니다.</p>
<p>네트워크가 안정적이고 연결이 자주 끊어지지 않는다면 일반적으로 이 키를 수정할 필요는 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> 또는 1분</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>이 키는 <em>QueueGlitchRetryCount</em> 키로 지정된 각 연결 시도 사이의 연결 간격을 제어합니다.</p>
<p>네트워크가 안정적이고 연결이 자주 끊어지지 않는다면 일반적으로 이 매개 변수를 수정할 필요는 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p><strong>Set-TransportService</strong> cmdlet 또는 서버 속성에서 관리 센터 EAC (Exchange)</p></td>
<td><p>이 매개 변수는 <em>QueueGlitchRetryCount</em> 및 <em>QueueGlitchRetryInterval</em> 키에서 제어하는 연결 시도가 실패한 후에 실행되는 연결 시도의 횟수를 지정합니다. <em>QueueGlitchRetryCount</em> 및 <em>QueueGlitchRetryInterval</em> 키를 사용하는 연결 문제는 서버 다시 시작 또는 캐시된 DNS 조회 실패로 인해 발생할 수 있습니다.</p>
<p>이 매개 변수에는 0에서 15까지의 정수를 입력할 수 있습니다. 이 매개 변수를 0으로 설정하면 다음 연결 시도는 <em>OutboundConnectionFailureRetryInterval</em> 매개 변수가 제어합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>사서함 서버의 전송 서비스: <code>00:05:00</code> 또는 5분</p></li>
<li><p>Edge 전송 서버: <code>00:01:00</code> 또는 10분</p></li>
</ul></td>
<td><p><strong>Set-TransportService</strong> cmdlet 또는 EAC의 서버 속성</p></td>
<td><p>이 매개 변수는 <em>TransientFailureRetryCount</em> 매개 변수로 지정된 각 연결 시도 사이의 연결 간격을 제어합니다.</p>
<p>값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>사서함 서버의 전송 서비스: <code>00:10:00</code> 또는 10분</p></li>
<li><p>Edge 전송 서버: <code>00:30:00</code> 또는 30분</p></li>
</ul></td>
<td><p><strong>Set-TransportService</strong> cmdlet 또는 EAC의 서버 속성</p></td>
<td><p>이 매개 변수는 이전에 실패한 아웃바운드 연결 시도에 대한 다시 시도 간격을 지정합니다. 이전에 실패한 연결 시도는 <em>TransientFailureRetryCount</em> 및 <em>TransientFailureRetryInterval</em> 매개 변수로 제어됩니다.</p>
<p>값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> or15 시간 (분)</p></td>
<td><p><strong>Set-TransportService</strong> cmdlet</p></td>
<td><p>이 매개 변수는 다시 시도 상태인 개별 메시지에 대한 다시 시도 간격을 지정합니다. Microsoft 고객 지원 서비스에서 권고하지 않는 한 기본값을 수정하지 않는 것이 좋습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> 또는 5분</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>이 키는 연결할 수 없는 대상 사서함 데이터베이스의 사서함 전송 배달 서비스에 큐가 연결을 시도하는 간격을 지정합니다.</p>
<p>값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.</p>
<p>이 키에는 00:00:01에서 1.00:00:00까지의 값을 입력할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 수동 메시지 다시 시도에 대한 구성 옵션

배달 큐가 다시 시도 상태이면 Exchange 도구 상자의 큐 뷰어 또는 셸의 **Retry-Queue** cmdlet을 사용하여 즉시 연결 시도를 수동으로 강제 실행할 수 있습니다. 수동 다시 시도 실행은 예약된 다음 다시 시도 시간보다 우선합니다. 연결이 실패하면 다시 시도 간격 타이머가 재설정됩니다. 이 기능을 사용하려면 배달 큐가 다시 시도 상태여야 합니다.

자세한 내용은 [큐 관리](manage-queues-exchange-2013-help.md)의 "큐 다시 시도" 섹션을 참조하십시오.

맨 위로 이동

## 지연 DSN 메시지에 대한 구성 옵션

각 메시지 배달이 실패하게 되면, Edge 전송 서버나 사서함 서버의 전송 서비스는 지연 DSN(배달 상태 알림) 메시지를 생성하고 배달할 수 없는 메시지를 보낸 사람에게 배달하기 위해 큐에 대기시킵니다. 지정된 지연 알림 시간 제한 간격이 지나고 실패한 메시지가 이 시간 중에 배달되지 못한 경우에만 이 지연 DSN 메시지를 보냅니다. 기본적으로 지연 알림 시간 제한 간격은 4시간입니다. 이러한 지연을 통해 일시적인 메시지 전송 실패로 인해 필요 없는 지연 DSN 메시지를 보내는 것을 방지할 수 있습니다. Exchange 조직의 내부나 외부에서 보낸 메시지에 대해 선별적으로 지연 DSN 알림 메시지 보내기를 사용하거나 사용하지 않을 수 있습니다.

지연 DSN 알림 메시지에 사용할 수 있는 구성 옵션은 다음 표에 설명되어 있습니다.

### 지연 DSN 알림 메시지에 사용할 수 있는 구성 옵션

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수 이름</th>
<th>기본값</th>
<th>위치</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4시간</p></td>
<td><p><strong>Set-TransportService</strong> 또는 EAC의 서버 속성</p></td>
<td><p>이 매개 변수는 보낸 사람에게 지연 DSN 메시지를 보내기 전에 서버가 대기하는 시간을 지정합니다. 이 매개 변수 값은 항상 <em>TransientFailureRetryCount</em> 매개 변수 값에 <em>TransientFailureRetryInterval</em> 매개 변수 값을 곱한 값보다 커야 합니다.</p>
<p>값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>이 매개 변수는 Exchange 조직의 외부에 있는 메시지를 보낸 사람에게 지연 DSN 메시지를 보낼 수 있는지 여부를 지정합니다.</p>
<p>이 매개 변수의 올바른 입력은 <code>$true</code> 또는 <code>$false</code>입니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>이 매개 변수는 Exchange 조직의 내부에 있는 메시지를 보낸 사람에게 지연 DSN 메시지를 보낼 수 있는지 여부를 지정합니다.</p>
<p>이 매개 변수의 올바른 입력은 <code>$true</code> 또는 <code>$false</code>입니다.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Exchange 2007 허브 전송 서버에서 모든 <EM>ExternalDSN*</EM> 및 <EM>InternalDSN*</EM> 매개 변수는 <STRONG>Set-TransportServer</STRONG> cmdlet에서 사용할 수 있습니다(<STRONG>Set-TransportConfig</STRONG> cmdlet에서는 사용할 수 없음). 조직에 Exchange 2007 허브 전송 서버가 있는 경우 각 Exchange 2007 허브 전송 서버에서 <STRONG>Set-TransportServer</STRONG> cmdlet을 사용하여 이 값을 변경해야 합니다.



맨 위로 이동

## 메시지 다시 전송에 대한 구성 옵션

메시지를 다시 전송하면 배달되지 않은 메시지가 분류기에서 다시 처리되도록 전송 큐로 다시 보내집니다.

## 자동 메시지 다시 전송

배달 큐가 다시 시도 상태이며 지정된 기간 동안 메시지를 배달할 수 없으면, 배달되지 않은 메시지가 자동으로 다시 전송됩니다. 이 기간은 EdgeTransport.exe.config 응용 프로그램 구성 파일의 *MaxIdleTimeBeforeResubmit* 키에 의해 제어됩니다. 배달 큐에 있는 메시지만 자동 다시 전송의 후보입니다.

값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.

기본값은 `12:00:00` 또는 12시간입니다.

## 수동 메시지 다시 전송

수동으로 메시지 전송 서비스에서 사서함 서버 또는 Edge 전송 서버에서 다음 상태를 제출할 수 있습니다.

  - 다시 시도 상태의 배달 큐. 큐의 메시지는 일시 중단 상태가 아니어야 합니다.

  - 연결할 수 없는 큐에 있으며 일시 중단 상태가 아닌 메시지.

  - 포이즌 메시지 큐에 있는 메시지.

포이즌 메시지 큐 및 연결할 수 없는 큐에 대한 자세한 내용은 [큐](queues-exchange-2013-help.md) 항목의 "포이즌 메시지 큐 및 연결할 수 없는 큐 정보"를 참조하십시오.

*MaxIdleTimeBeforeResubmit* 매개 변수에서 지정한 시간이 지날 때까지 기다리지 않고 배달 큐 또는 연결할 수 없는 큐에 있는 메시지를 수동으로 다시 전송하려면 **Retry-Queue** cmdlet을 *Resubmit* 매개 변수와 함께 사용해야 합니다. 포이즌 메시지 큐에 있는 메시지를 수동으로 다시 전송하려면 큐 뷰어 또는 **Resume-Message** cmdlet을 사용하여 메시지를 다시 시작할 수 있습니다. 자세한 내용은 [큐 관리](manage-queues-exchange-2013-help.md)의 "큐에 있는 메시지 다시 전송" 섹션을 참조하십시오.

메시지를 수동으로 다시 전송할 수 있는 다른 방법은 메시지를 일시 중단하고 .eml 파일 이름 확장명이 있는 텍스트 파일로 메시지를 내보낸 후에 사서함 서버 또는 Edge 전송 서버의 Replay 디렉터리로 .eml 파일을 복사하는 것입니다. 이 다시 전송 방법을 배달 큐 또는 연결할 수 없는 큐에 있는 메시지에 사용할 수 있습니다. 포이즌 메시지 큐에 있는 메시지는 이미 일시 중단 상태입니다. 전송 큐에 있는 메시지를 일시 중단하거나 내보낼 수 없습니다.


> [!NOTE]
> 메시지를 큐에서 내보내도 큐에서 해당 메시지가 제거되지는 않습니다. 메시지를 내보낸 다음 Replay 디렉터리를 사용하여 이 메시지를 다시 전송한 후에는 중복 메시지 배달이 발생하지 않도록 일시 중단된 메시지를 제거해야 합니다.



자세한 내용은 [큐에서 메시지 내보내기](export-messages-from-queues-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 메시지 만료에 대한 구성 옵션

Edge 전송 서버 또는 사서함 서버의 전송 서비스에서 실패 한 메시지를 제공 하려고 하는 시간의 최대 길이 지정 하는 *메시지 만료 시간 제한 간격* 입니다. 메시지의 만료 시간 제한 간격 통과 하기 전에 성공적으로 배달할 수 없는, 하는 경우 원본 메시지 또는 메시지 헤더를 포함 하는 NDR 보낸사람에 게 배달 됩니다.

## 자동 메시지 만료

메시지 만료 시간 제한 간격은 **Set-TransportService** cmdlet의 *MessageExpirationTimeOut* 매개 변수에서 또는 EAC의 서버 속성에서 제어합니다.

값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.

기본값은 `2.00:00:00` 또는 2일입니다. 이 매개 변수에는 `00:00:05`에서 `90.00:00:00`까지의 값을 입력할 수 있습니다.

## 수동 메시지 만료

수동으로 메시지가 만료되도록 할 수는 없지만, NDR을 사용하거나 사용하지 않고 전송 큐를 제외한 모든 큐에서 메시지를 수동으로 제거할 수 있습니다.

자세한 내용은 [큐에서 메시지 관리](manage-messages-in-queues-exchange-2013-help.md)의 "큐에서 메시지 제거" 섹션을 참조하십시오.

맨 위로 이동

