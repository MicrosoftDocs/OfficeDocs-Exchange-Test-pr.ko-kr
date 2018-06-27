---
title: '메시지 필터: Exchange 2013 Help'
TOCTitle: 메시지 필터
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 50483652
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 필터

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

필터링을 통해 큐의 메시지를 다른 방식으로 볼 수 있습니다. 필터 조건을 지정하면 메시지를 빨리 찾아 조치를 취할 수 있습니다. 전자 메일 메시지의 받는 사람이 여러 명이면 메시지가 여러 큐에 있을 수 있습니다. 이 경우 메시지 속성으로 필터링하면 모든 큐에서 해당 메시지를 찾을 수 있습니다. 다음은 메시지 필터링을 사용하여 메일 흐름을 관리하는 방법을 보여주는 시나리오입니다.

  - 인터넷으로부터 전자 메일을 수신하는 사서함 서버나 Edge 전송 서버의 전송 큐에 배달을 위해 대기 중인 대량의 메시지가 있습니다. 이러한 메시지 중에는 제목이 같은 메시지가 많습니다. 정황으로 보아 조직에 스팸이 전송된 것 같습니다. 이 경우 필터를 만들어 제목 조건에 맞는 메시지를 모두 표시할 수 있습니다. 메시지가 스팸으로 확인되면 검색된 메시지를 모두 선택하여 NDR을 보내지 않고 배달 큐에서 삭제할 수 있습니다.

  - 한 사용자가 메일 흐름이 느리다고 보고했습니다. 큐를 검사해 보니 제목이 서로 다른 여러 메시지가 단일 도메인으로부터 전송된 것으로 확인되었습니다. 이 경우 대기 중인 메시지 중 해당 도메인에서 전송된 메시지를 모두 표시하는 필터를 만들 수 있습니다. 메시지가 스팸으로 확인되면 검색된 메시지를 모두 선택하여 NDR을 보내지 않고 큐에서 삭제할 수 있습니다.

## 필터로 사용되는 메시지 속성

메시지 속성을 사용하여 필터를 만들고 지정한 조건에 맞는 메시지를 찾을 수 있습니다. 메시지 관리 cmdlet에 대해 *Filter* 매개 변수를 사용하거나 큐 뷰어에서 필터를 만들 수 있습니다. 메시지 관리 cmdlet은 큐 뷰어보다 다양한, 필터링 가능한 속성을 지원합니다. 다음 표에는 필터링 기준으로 사용할 수 있는 메시지 속성 및 해당 속성과 관련된 값이 나와 있습니다.

### 메시지 필터링에 사용되는 메시지 속성

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>큐 뷰어 메시지 속성</th>
<th>셸 메시지 속성</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>받은 날짜</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>메시지가 큐로 보내진 날짜/시간입니다.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>이 속성은 메시지가 지연된 이유를 식별합니다. 메시지가 지연되지 않은 경우 이 속성 값은 <code>None</code>입니다. 받는 사람을 확인하는 동안 발생한 일시적인 오류로 인해 지연된 메시지는 전송 큐로 반환됩니다. 지연된 메시지에 대한 자세한 내용은 <a href="recipient-resolution-exchange-2013-help.md">받는 사람 확인</a>를 참조하십시오. 가능한 값은 다음과 같습니다.</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>만료 시간</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>이 속성에는 메시지를 배달할 수 없는 경우 메시지가 만료되어 큐에서 삭제되는 시간을 나타내는 날짜/시간이 포함됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람 주소</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>이 속성에는 보낸 사람의 SMTP 주소가 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>Identity</code></p></td>
<td><p>이 속성은 <em>&lt;서버&gt;\&lt;큐&gt;\&lt;MessageInteger&gt;</em> 형식의 메시지 ID입니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a>의 &quot;메시지 ID&quot; 섹션을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>인터넷 메시지 ID</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>이 속성에는 메시지 헤더에 있는 <code>Message-ID:</code> 헤더 필드의 값이 포함됩니다. 이 값은 GUID, FQDN, 보내는 SMTP 서버를 포함하는 전자 메일 주소로 표시됩니다. 예를 들면 다음과 같습니다.</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>마지막 오류</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>이 속성에는 메시지에 대 한 기록 된 마지막 오류 텍스트가 표시 됩니다. 예: <code>A matching connector cannot be found to route the external recipient</code>합니다.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>이 속성에는 메시지가 서버의 전송 큐에 처음 들어온 시간 및 메시지가 큐에 배치된 시간 간의 경과된 시간이 포함됩니다. 이 값에서는 <em>hh:mm:ss.ff</em> 구문이 사용됩니다. 여기서 <em>hh</em>는 시간, <em>mm</em>은 분, <em>ss</em>는 초 그리고 <em>ff</em>는 초의 소수 단위입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지 원본 이름</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>이 속성에는 메시지를 큐로 전송한 전송 구성 요소의 이름을 나타내는 텍스트 문자열이 포함됩니다. 예를 들어 메시지가 수신 커넥터를 통해 들어온 경우 이 값은 <code>SMTP:</code><em>&lt;ConnectorName&gt;</em>입니다. 메시지가 DSN(배달 상태 알림)인 경우 이 값은 <code>DSN</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>Priority</code></p></td>
<td><p>이 속성에는 Outlook이나 Outlook Web App의 사용자에 의해 할당된 메시지의 우선 순위가 포함됩니다. <code>Low</code>, <code>Normal</code> 및 <code>High</code> 값을 사용할 수 있습니다. 자세한 내용은 <a href="priority-queuing-exchange-2013-help.md">우선순위 큐</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>큐 ID</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>이 속성은 메시지가 포함된 큐의 ID입니다. 큐 ID에서는 <em>&lt;서버&gt;\&lt;큐&gt;</em> 구문이 사용됩니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a>의 &quot;큐 ID&quot; 섹션을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>이 속성은 자동 또는 수동으로 대상에 메시지 배달을 시도한 횟수를 식별합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>SCL(스팸 지수) 속성의 값은 메시지의 SCL을 나타냅니다. 유효한 SCL 항목은 0~9 사이의 정수입니다. SCL 속성 값이 비어 있으면 메시지가 콘텐츠 필터 에이전트에서 처리되지 않은 것입니다.</p>
<p>이 속성에는 메시지의 SCL(스팸 지수) 값이 포함됩니다. 유효한 SCL 항목은 0~9 사이의 정수 및 -1입니다. 자세한 내용은 <a href="spam-confidence-level-threshold-exchange-2013-help.md">스팸 지수 임계값</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>크기(KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>이 속성은 메시지의 크기를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>원본 IP</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>이 속성에는 큐에 메시지를 포함하는 Exchange 서버로 메시지를 전송한 서버의 IP 주소가 포함됩니다. 이 주소는 로컬 Exchange 서버의 IP 주소나 원격 SMTP 서버의 IP 주소가 될 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>상태</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>이 속성은 현재 메시지 상태를 나타냅니다. 메시지의 상태 값은 다음 중 하나입니다.</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a>의 &quot;메시지 속성&quot; 섹션을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>제목</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>이 속성은 메시지 헤더의 <code>Subject:</code> 헤더 필드에 있는 메시지 제목을 나타냅니다.</p></td>
</tr>
</tbody>
</table>

