---
title: '우선순위 큐: Exchange 2013 Help'
TOCTitle: 우선순위 큐
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51407704
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 우선순위 큐

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

*우선 순위 큐*는 사서함 서버의 Transport Service에 의한 메시지 처리에 영향을 주기 위해 보낸 사람이 정의한 메시지 우선 순위를 사용하는 Microsoft Exchange Server 2013의 기능입니다.

Microsoft Outlook에서 보낸 사람은 메시지를 만들어 보낼 때 메시지 우선 순위를 할당하며, 다음과 같은 메시지 우선 순위 값을 설정할 수 있습니다.

  - 중요도 낮음

  - 중요도 중간

  - 중요도 높음

Outlook 또는 Outlook Web App에서 만들어진 메시지에 대한 기본 우선 순위는 보통입니다. 메시지 우선 순위는 메시지 머리글의 `X-Priority` 머리글 필드에 저장됩니다.

Exchange 2013 조직에서 보내거나 받는 모든 메시지는 먼저 사서함 서버의 Transport Service에서 분류되어야만 라우팅 및 배달될 수 있습니다. 사서함 서버에서 Transport Service의 분류기는 전송 큐에서 한 번에 하나의 메시지를 선택하여 받는 사람 확인, 라우팅 확인 및 메시지의 내용 변환을 수행한 후에 배달 큐에 메시지를 저장합니다. 자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md)을 참조하십시오.

배달 큐는 메시지의 대상에 따라 동적으로 만들어집니다. 자세한 내용은 [큐](queues-exchange-2013-help.md)을 참조하십시오.

동일한 대상을 가진 모든 메시지는 동일한 배달 큐에 저장됩니다. 우선 순위 큐는 배달 큐에서 대상 메시징 서버로의 메시지 전송에 영향을 줍니다. 우선 순위 큐를 사용하도록 설정한 경우 높은 우선 순위 메시지는 보통 우선 순위 메시지 전에 전송되며 보통 우선 순위 메시지는 낮은 우선 순위 메시지 전에 전송됩니다. 메시지 우선 순위에 따라 우선 순위가 지정된 메시지 배달을 통해 메시지 배달 시간에 대한 특정 SLA(서비스 수준 계약) 요구 사항을 정의할 수 있습니다.

## 우선 순위 큐의 구성 옵션

우선 순위 큐 지원은 `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML 응용 프로그램 구성 파일의 키로 제어됩니다. 우선 순위 큐를 구성하는 방법에 대한 자세한 내용은 [사용 하도록 설정 하 고 우선순위 큐 구성](enable-and-configure-priority-queuing-exchange-2013-help.md)을 참조하십시오.

다음 표에서는 각 키에 대해 더 자세히 설명합니다.

### EdgeTransport.exe.config 파일의 우선 순위 큐 키

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>키</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>이 키는 사서함 서버의 Transport Service에서 우선 순위 큐를 사용하거나 사용하지 않도록 설정합니다. 이 키의 올바른 입력은 <code>true</code> 또는 <code>false</code>입니다.</p>
<p>이 키가 <code>false</code>일 경우 우선 순위 큐가 사용하지 않도록 설정되며, EdgeTransport.exe.config 파일에 있는 모든 우선 순위 큐 메시지 제한은 무시됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>이 키는 우선 순위가 높음인 메시지의 최대 허용 크기를 지정합니다. 우선 순위가 높음인 메시지가 이 키에 의해 지정된 값보다 크면 자동으로 메시지의 우선 순위가 높음에서 보통으로 내려갑니다.</p>
<p>이 키의 값은 <strong>Set-TransportConfig</strong> cmdlet의 <em>MaxSendMessageSize</em> 매개 변수 값보다 현저히 낮아야 합니다. 이 매개 변수의 기본값은 <code>10 MB</code>입니다. 이 두 값의 차이를 통해 우선 순위가 높음인 메시지에 대한 일관되고 예측 가능한 배달 시간이 보장됩니다.</p>
<p>값을 입력할 때 다음 단위 중 하나로 된 값을 사용합니다.</p>
<ul>
<li><p>KB(킬로바이트)</p></li>
<li><p>MB(메가바이트)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>낮음</strong>   <code>8:00:00</code>(8시간)</p>
<p><strong>보통</strong>   <code>4:00:00</code>(4시간)</p>
<p><strong>높음</strong>   <code>00:30:00</code>(30분)</p></td>
<td><p>이 키는 메시지 우선 순위를 바탕으로 지연 DSN(배달 상태 알림) 메시지의 시간 제한 간격을 지정합니다.</p>
<p>각각의 메시지 배달에 실패하면 Transport Service는 지연 DSN(배달 상태 알림) 메시지를 생성하고 배달할 수 없는 메시지를 보낸 사람에게 배달하기 위해 큐에 대기시킵니다. 지정된 지연 알림 시간 제한 간격이 지나고 실패한 메시지가 이 시간 중에 배달되지 못한 경우에만 이 지연 DSN 메시지를 보냅니다. 이러한 지연을 통해 일시적인 메시지 전송 실패로 인해 필요 없는 지연 DSN 메시지를 보내는 것을 방지할 수 있습니다.</p>
<p>값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>낮음</strong>   <code>2.00:00:00</code>(2일)</p>
<p><strong>보통</strong>   <code>2.00:00:00</code>(2일)</p>
<p><strong>높음</strong>   <code>8:00:00</code>(8시간)</p></td>
<td><p>이 키는 Transport Service가 실패한 메시지의 배달을 시도하는 최대 시간을 지정합니다. 만료 시간 제한 간격이 지나기 전에 메시지를 배달할 수 없으면 원본 메시지 또는 메시지 머리글이 포함된 NDR(배달 못 함 보고서)이 보낸 사람에게 배달됩니다.</p>
<p>값을 지정하려면 dd.hh:mm:ss 형식으로 기간을 입력합니다. 여기서 d는 일, h는 시간, m은 분, s는 초를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>낮음</strong>   2</p>
<p><strong>보통</strong>   15</p>
<p><strong>높음</strong>   3</p></td>
<td><p>이 키는 Transport Service에서 단일 원격 도메인에 대해 열 수 있는 최대 연결 수를 지정합니다. 사서함 서버에 있는 배달 큐 및 송신 커넥터를 사용하여 원격 도메인으로 나가는 연결이 발생합니다.</p>
<p>이 세 키의 합계는 <strong>Set-TransportService</strong> cmdlet의 <em>MaxPerDomainOutboundConnections</em> 매개 변수 값보다 작거나 같아야 합니다. 이 매개 변수의 기본값은 <code>20</code>입니다.</p></td>
</tr>
</tbody>
</table>


## 우선 순위 큐가 사서함 서버의 기타 메시지 제한에 영향을 주는 방법

Transport Service를 통과하는 모든 메시지에 다양한 메시지 다시 시도, 다시 전송 및 만료 제한이 적용됩니다. 자세한 내용은 [메시지 크기 제한](message-size-limits-exchange-2013-help.md)을 참조하십시오.

**Set-TransportService** cmdlet에서 사용할 수 있는 일부 메시지 제한에는 EdgeTransport.exe.config 응용 프로그램 구성 파일에서 사용할 수 있는 상응하는 우선 순위 큐 메시지 제한이 있습니다. 다음 표에서는 이러한 해당 메시지 제한을 보여줍니다.

### EdgeTransport.exe.config 파일의 우선 순위 큐 메시지 제한에 해당하는 Set-TransportService cmdlet의 메시지 제한

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수 또는 키</th>
<th>기본값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>(4시간)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code>(4시간)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code>(2일)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code>(2일)</p></td>
</tr>
</tbody>
</table>


우선 순위 큐를 사용하지 않도록 설정한 경우 EdgeTransport.exe.config 구성 파일에 있는 모든 우선 순위 큐 메시지 제한은 무시됩니다. **Set-TransportService** cmdlet의 모든 메시지 제한은 사서함 서버의 Transport Service를 통과하는 모든 메시지에 적용됩니다.

우선 순위 큐를 사용하도록 설정한 경우 EdgeTransport.exe.config 구성 파일의 우선 순위 큐 메시지 제한은 **Set-TransportService** cmdlet의 해당 메시지 제한보다 우선합니다. **Set-TransportService** cmdlet의 다른 모든 메시지 제한은 사서함 서버의 Transport Service를 통과하는 낮은 우선 순위, 보통 우선 순위, 높은 우선 순위 메시지에 계속 적용됩니다.

## 우선 순위 큐의 사용자 설정

**Set-Mailbox** cmdlet에는 *DowngradeHighPriorityMessagesEnabled* 매개 변수가 포함됩니다. 기본값은 `$false`입니다. 이 매개 변수를 `$true`로 설정하면 사서함에서 보내진 모든 높음 우선 순위 메시지는 자동으로 보통 우선 순위로 내려갑니다.

