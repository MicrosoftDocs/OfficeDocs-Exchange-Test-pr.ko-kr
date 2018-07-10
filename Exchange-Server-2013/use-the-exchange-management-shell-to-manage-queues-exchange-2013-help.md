---
title: 'Exchange 관리 셸을 사용 하 여 큐를 관리: Exchange 2013 Help'
TOCTitle: Exchange 관리 셸을 사용 하 여 큐를 관리
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51407699
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 관리 셸을 사용 하 여 큐를 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

이전 버전의 Exchange에서와 마찬가지로 Microsoft Exchange Server 2013의 Exchange 관리 셸을 사용하여 큐 및 해당 큐의 메시지에 대한 정보를 보고 큐 및 메시지에 대해 관리 작업을 수행할 수 있습니다. Exchange 2013에서 큐는 사서함 서버 및 Edge 전송 서버에 있습니다. 이 항목에서는 이러한 서버를 *전송 서버*라고 합니다.

셸을 사용하여 전송 서버에서 큐 및 큐의 메시지를 보고 관리할 경우 관리할 큐나 메시지를 식별하는 방법을 이해하는 것이 중요합니다. 일반적으로 전송 서버에는 배달할 여러 큐 및 메시지가 포함되어 있습니다. 큐 및 메시지 관리 cmdlet에 제공되는 필터링 매개 변수를 사용하여 보거나 관리할 큐나 메시지를 식별할 수 있습니다.

Exchange 도구 상자의 큐 뷰어를 사용하여 큐 및 큐의 메시지를 관리할 수도 있습니다. 단, 큐 뷰어에 비해 큐 및 메시지 보기 cmdlet이 보다 다양한, 필터링 가능한 속성 및 필터 옵션을 지원합니다. 큐 뷰어를 사용하는 방법에 대한 자세한 내용은 [큐 뷰어](queue-viewer-exchange-2013-help.md)를 참조하십시오.

**목차**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## 큐 필터링 매개 변수

다음 표에는 큐 관리 cmdlet에서 사용할 수 있는 필터링 매개 변수가 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>필터링 매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p><em>Identity</em> 매개 변수는 <em>Filter</em> 매개 변수와 동일한 명령에 사용할 수 없습니다. <em>Include</em> 및 <em>Exclude</em> 매개 변수는 동일한 명령에서 <em>Filter</em> 매개 변수와 함께 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p><em>Identity</em> 매개 변수나 <em>Filter</em> 매개 변수를 사용해야 하며, 동일한 명령에 이 두 매개 변수를 모두 사용할 수는 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p><em>Server</em>, <em>Dag</em>, <em>Site</em> 또는 <em>Forest</em> 매개 변수를 사용해야 하며, 동일한 명령에 이러한 매개 변수를 같이 사용할 수는 없습니다. <em>Filter</em> 매개 변수는 다른 필터링 매개 변수와 함께 사용할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


*Server* 매개 변수는 모든 큐 관리 cmdlet에서 사용할 수 있습니다. **Get-QueueDigest** cmdlet에서 *Server* 매개 변수는 큐에 대한 요약 정보를 보려는 서버를 지정하는 범위 매개 변수입니다. 그 이외의 모든 큐 관리 cmdlet에서는 *Server* 매개 변수를 사용하여 특정 서버에 연결하고 해당 서버에서 큐 관리 명령을 실행할 수 있습니다. *Server* 매개 변수를 *Filter* 매개 변수와 함께 또는 이 매개 변수 없이 사용할 수 있지만 *Server* 매개 변수를 *Identity* 매개 변수와 함께 사용할 수는 없습니다. *Server* 매개 변수에서는 전송 서버의 호스트 이름이나 FQDN을 사용합니다.

맨 위로 이동

## 큐 ID

큐 관리 cmdlet의 *Identity* 매개 변수는 특정 큐를 식별합니다. *Identity* 매개 변수를 사용할 경우 다른 큐 필터링 매개 변수는 지정할 수 없습니다. 이미 큐가 고유하게 식별되었기 때문입니다. *Identity* 매개 변수에서는 기본 구문 *\<Server\>*\\*\<Queue\>*가 사용됩니다.

*\<Server\>* 자리 표시자는 Exchange 서버의 FQDN 또는 호스트 이름입니다(예: `mailbox01` 또는 `mailbox01.contoso.com`). *\<Server\>* 한정자를 생략할 경우 로컬 서버가 묵시적으로 사용됩니다.

\<*Queue*\> 자리 표시자에는 다음 값 중 하나를 사용할 수 있습니다.

  - **영구 큐 이름**   영구 큐는 모든 사서함 서버나 Edge 전송 서버에서 고유하고 일관된 이름을 가집니다. 영구 큐 이름은 다음 중 하나가 될 수 있습니다.
    
      - **전송**   이 큐에는 분류기에서 처리되기를 대기하고 있는 메시지가 포함됩니다.
    
      - **연결할 수 없음**   이 큐에는 라우팅할 수 없는 메시지가 포함됩니다. 메시지가 큐에 배치되어야 이 큐가 표시됩니다.
    
      - **포이즌**   이 큐에는 Exchange 서버에 해로운 것으로 확인된 메시지가 포함됩니다. 메시지가 큐에 배치되어야 이 큐가 표시됩니다.

  - **배달 큐 이름**   배달 큐 이름은 큐의 **NextHopDomain** 속성의 값입니다. 예를 들어 큐 이름은 송신 커넥터의 주소 공간, Active Directory 사이트의 이름 또는 DAG의 이름이 될 수 있습니다. 자세한 내용은 [큐](queues-exchange-2013-help.md) 항목의 "NextHopSolutionKey" 섹션을 참조하십시오.

  - **큐 정수**   큐 데이터베이스에서 배달 큐 및 섀도 큐에 고유한 정수 값이 할당됩니다. 단, **Identity** 또는 **QueueIdentity** 속성의 큐에 대한 정수 값을 찾으려면 **Get-Queue** cmdlet을 실행해야 합니다.

  - **섀도 큐 이름**   섀도 큐에서는 구문 `Shadow\`*\<QueueInteger\>*가 사용됩니다.

다음 표에는 큐 관리 cmdlet에서 *Identity* 매개 변수와 함께 사용할 수 있는 구문이 요약되어 있습니다. 모든 값에서 *\<Server\>*는 서버의 FQDN 또는 호스트 이름입니다.

### 큐 ID 형식

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ID 매개 변수 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> 또는 <code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>지정된 서버나 로컬 서버의 영구 큐입니다.</p>
<p><em>&lt;PersistentQueueName&gt;</em>은 <code>Submission</code>, <code>Unreachable</code> 또는 <code>Poison</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> 또는 <code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>지정된 서버나 로컬 서버의 배달 큐입니다.</p>
<p><em>&lt;NextHopDomain&gt;</em>은 큐의 메시지에 대한 라우팅 대상 또는 배달 그룹입니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> 또는 <code>&lt;QueueInteger&gt;</code></p></td>
<td><p>지정된 서버나 로컬 서버의 배달 큐입니다.</p>
<p><em>&lt;QueueInteger&gt;</em>는 <strong>Get-Queue</strong> cmdlet의 <strong>Identity</strong> 속성에 표시되는, 큐의 고유한 정수 값입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> 또는 <code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>지정된 서버나 로컬 서버의 섀도 큐입니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> 또는 <code>*</code></p></td>
<td><p>지정된 서버나 로컬 서버의 모든 큐입니다. 이 값은 <strong>Get-Queue</strong> cmdlet과 함께 사용하는 경우에만 사용할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 큐 필터링 매개 변수

모든 큐 관리 cmdlet에서 *Filter* 매개 변수를 사용하여 큐 속성을 바탕으로 보거나 관리할 큐를 지정할 수 있습니다. *Filter* 매개 변수는 필터 조건을 충족하는 큐로 큐 작업을 제한하는 비교 연산자가 포함된 식을 만듭니다. `-and` 논리 연산자를 사용하여 결과와 일치하는 여러 조건을 지정할 수 있습니다.

*Filter* 매개 변수와 함께 사용할 수 있는 큐 속성에 대한 전체 목록은 [큐](queues-exchange-2013-help.md)를 참조하십시오.

*Filter* 매개 변수와 함께 사용할 수 있는 비교 연산자 목록은 이 항목의 Comparison operators to use when filtering queues or messages 섹션을 참조하십시오.

큐를 보고 관리하기 위해 *Filter* 매개 변수를 사용하는 절차와 관련된 예를 보려면 [큐 관리](manage-queues-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## Include 및 Exclude 매개 변수

Exchange 2013에는 `Get-Queue` cmdlet에서 사용할 수 있는 *Include* 및 *Exclude* 매개 변수가 있습니다. 이러한 매개 변수를 개별적으로 또는 함께 사용하거나 *Filter* 매개 변수와 함께 사용하여 로컬 전송 서버나 지정된 전송 서버에서 큐 결과를 세부적으로 조정할 수 있습니다. 예를 들어 다음을 수행할 수 있습니다.

  - 결과에서 빈 큐 제외

  - 결과에서 외부 대상에 대한 큐 제외

  - **DeliveryType**에 대해 특정 값을 가진 큐를 결과에 포함

*Include* 및 *Exclude* 매개 변수는 다음과 같은 큐 속성을 사용하여 큐를 필터링합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>값</th>
<th>설명</th>
<th>셸 코드 예제</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>이 값은 <strong>DeliveryType</strong> 속성을 바탕으로 큐를 포함하거나 제외하며, 쉼표로 구분하여 여러 값을 지정할 수 있습니다. <strong>DeliveryType</strong>의 올바른 값에 대한 설명은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션에 나와 있습니다.</p></td>
<td><p>이 예에서는 다음 홉이 스마트 호스트 라우팅에 대해 구성된 로컬 서버의 송신 커넥터인 로컬 서버의 모든 배달 큐를 반환합니다.</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>이 값은 빈 큐를 포함하거나 제외합니다. 빈 큐의 경우 <strong>MessageCount</strong> 속성 값이 <code>0</code>입니다.</p></td>
<td><p>이 예에서는 메시지가 포함된, 로컬 서버의 모든 큐를 반환합니다.</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>이 값은 <strong>NextHopCategory</strong> 속성에 값 <code>External</code>을 포함한 큐를 포함하거나 제외합니다.</p>
<p>외부 큐 값은 항상 <strong>DeliveryType</strong>에 대해 다음 값 중 하나로 지정됩니다.</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조하십시오.</p></td>
<td><p>이 예에서는 로컬 서버의 모든 내부 큐를 반환합니다.</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>이 값은 <strong>NextHopCategory</strong> 속성에 값 <code>Internal</code>을 포함한 큐를 포함하거나 제외합니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조하십시오.</p></td>
<td><p>이 예에서는 로컬 서버의 모든 내부 큐를 반환합니다.</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


*Filter* 매개 변수를 사용하여 *Include* 및 *Exclude* 매개 변수의 기능을 복제할 수 있습니다. 예를 들어 `Get-Queue -Exclude Empty` 명령은 `Get-Queue -Filter {MessageCount -gt 0}`와 같은 결과를 생성합니다. 단, 기억하는 데 있어 *Include* 및 *Exclude* 매개 변수 구문이 보다 간단하고 쉽습니다.

맨 위로 이동

## Get-QueueDigest

Exchange 2013에서는 **Get-QueueDigest**라는 새 큐 cmdlet이 추가됩니다. 이 cmdlet을 통해 단일 명령을 사용하여 Exchange 조직의 모든 큐나 일부 큐에 대한 정보를 볼 수 있습니다. 특히 **Get-QueueDigest** cmdlet을 통해 DAG, Active Directory 사이트 또는 전체 Active Directory 포리스트 등 서버의 위치를 바탕으로 큐에 대한 정보를 볼 수 있습니다. 경계 네트워크에서 구독된 Edge 전송 서버의 큐는 결과에 포함되지 않습니다. 또한 **Get-QueueDigest**는 Edge 전송 서버에서 제공되기는 하지만 결과는 Edge 전송 서버의 큐로 제한됩니다.


> [!NOTE]
> 기본적으로 <STRONG>Get-QueueDigest</STRONG> cmdlet은 메시지가 10개 이상 포함된 배달 큐를 표시하고 1~2분 후에 결과를 반환합니다. 이러한 기본값을 변경하는 방법에 대한 지침은 <A href="configure-get-queuedigest-exchange-2013-help.md">Get-QueueDigest 구성</A>을 참조하세요.



**Get-QueueDigest** cmdlet에서 사용할 수 있는 필터링 및 정렬 매개 변수가 다음 표에 설명되어 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Dag</em>, <em>Server</em> 또는 <em>Site</em></p></td>
<td><p>이 매개 변수는 함께 사용할 수 없으며, cmdlet의 범위를 설정합니다. 이 매개 변수 중 하나나 <em>Forest</em> 스위치를 지정해야 합니다. 일반적으로 서버, DAG 또는 Active Directory 사이트의 이름을 사용하지만 서버, DAG 또는 사이트를 고유하게 식별하는 모든 값을 사용할 수 있습니다. 여러 개의 서버, DAG 또는 사이트를 쉼표로 구분하여 지정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>이 스위치는 <em>Dag</em>, <em>Server</em> 또는 <em>Site</em> 매개 변수를 사용하지 않을 경우 필요합니다. 이 스위치에는 값을 지정하지 않습니다. 이 스위치를 사용하면 Active Directory 포리스트의 모든 Exchange 2013 사서함 서버에서 큐를 가져옵니다. <em>Forest</em> 스위치를 사용하여 원격 Active Directory 포리스트의 큐를 볼 수는 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>이 매개 변수에는 <code>None</code>, <code>Normal</code> 및 <code>Verbose</code> 값을 사용할 수 있으며, 기본값은 <code>Normal</code>입니다. <code>None</code> 값을 사용할 경우에는 큐 이름이 결과의 <strong>세부 정보</strong> 열에서 생략됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>이 매개 변수를 통해 큐 속성을 바탕으로 큐를 필터링할 수 있습니다. <a href="queue-filters-exchange-2013-help.md">큐 필터입니다.</a> 항목에 설명된 대로 필터링 가능한 모든 큐 속성을 사용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>이 매개 변수는 큐 결과를 그룹화합니다. 다음 속성 중 하나를 사용하여 결과를 그룹화할 수 있습니다.</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Status</p></li>
<li><p>ServerName</p></li>
</ul>
<p>기본적으로 결과는 <code>NextHopDomain</code>별로 그룹화됩니다. 이러한 큐 속성에 대한 자세한 내용은 <a href="queue-filters-exchange-2013-help.md">큐 필터입니다.</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>이 매개 변수는 큐 결과를 지정한 값으로 제한합니다. 큐는 큐의 메시지 수를 바탕으로 내림차순으로 정렬되며 <em>GroupBy</em> 매개 변수에서 지정한 값별로 그룹화됩니다. 기본값은 1000입니다. 즉 기본적으로 명령에는 <strong>NextHopDomain</strong>별로 그룹화된 최상위 1,000개의 큐가 표시되며, 가장 많은 메시지를 포함하는 큐부터 가장 적은 메시지를 포함하는 큐 순서로 정렬됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>이 매개 변수는 작업 시간이 초과하기 전의 시간(초)을 지정합니다. 기본값은 <code>00:00:10</code> 또는 10초입니다.</p></td>
</tr>
</tbody>
</table>


이 예에서는 Mailbox01,Mailbox02 및 Mailbox03이라는 Exchange 2013 사서함 서버의 비어 있지 않은 모든 외부 큐를 반환합니다.

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

맨 위로 이동

## 메시지 필터링 매개 변수

다음 표에는 메시지 관리 cmdlet에서 사용할 수 있는 필터링 매개 변수가 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>필터링 매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>모든 필터링 매개 변수는 함께 사용할 수 없으며, 동일한 명령에 함께 사용할 수는 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p><em>Identity</em> 매개 변수나 <em>Filter</em> 매개 변수를 사용해야 하며, 동일한 명령에 이 두 매개 변수를 모두 사용할 수는 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p><em>Identity</em> 매개 변수는 필수 사항입니다.</p></td>
</tr>
</tbody>
</table>


*Server* 매개 변수는 **Export-Message** cmdlet을 제외한 모든 메시지 관리 cmdlet에서 사용할 수 있습니다. *Server* 매개 변수를 사용하여 특정 서버에 연결하고 해당 서버에서 메시지 관리 명령을 실행할 수 있습니다. *Server* 매개 변수를 *Filter* 매개 변수와 함께 또는 이 매개 변수 없이 사용할 수 있지만 *Server* 매개 변수를 *Identity* 매개 변수와 함께 사용할 수는 없습니다. *Server* 매개 변수에서는 전송 서버의 호스트 이름이나 FQDN을 사용합니다.

맨 위로 이동

## 메시지 ID

메시지 관리 cmdlet의 *Identity* 매개 변수는 하나 이상의 큐에서 특정 메시지를 식별합니다. *Identity* 매개 변수를 사용할 경우 다른 메시지 필터링 매개 변수는 지정할 수 없습니다. 이미 메시지가 고유하게 식별되었기 때문입니다. *Identity* 매개 변수에서는 기본 구문 *\<Server\>*\\*\<Queue\>*\\*\<MessageInteger\>*가 사용됩니다.

*\<Server\>* 자리 표시자는 Exchange 서버의 FQDN 또는 호스트 이름입니다(예: `mailbox01` 또는 `mailbox01.contoso.com`). *\<Server\>* 한정자를 생략할 경우 로컬 서버가 묵시적으로 사용됩니다.

\<*Queue*\> 자리 표시자에는 이 항목의 "큐 ID" 섹션에 설명된 대로 큐의 ID가 사용됩니다. 예를 들어 영구 큐 이름, **NextHopDomain** 값 또는 큐 데이터베이스의 큐에 대한 고유한 정수 값을 사용할 수 있습니다.

*\<MessageInteger\>* 자리 표시자는 서버의 큐 데이터베이스에 처음 포함될 때 메시지에 할당된 고유 정수 값을 나타냅니다. 이 메시지가 여러 큐를 필요로 하는, 여러 받는 사람에게 전송되는 경우 큐 데이터베이스의 모든 큐의 모든 메시지 복사본에는 같은 정수 값이 포함됩니다. 단, **Get-Message** cmdlet을 실행하여 **Identity** 또는 **MessageIdentity** 속성의 메시지에 대한 정수 값을 찾아야 합니다.

다음 표에는 메시지 관리 cmdlet의 *Identity* 매개 변수에서 사용할 수 있는 구문이 요약되어 있습니다. 모든 값에서 *\<Server\>*는 서버의 FQDN 또는 호스트 이름입니다.

### 메시지 ID 형식

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>ID 매개 변수 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> 또는 <code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>지정된 서버나 로컬 서버의 특정 큐에 있는 메시지입니다.</p>
<p><em>&lt;MessageInteger&gt;</em>는 <strong>Get-Message</strong> cmdlet의 <strong>Identity</strong> 속성에 표시되는, 메시지의 고유한 정수 값입니다.</p>
<p><em>&lt;Queue&gt;</em>는 다음 값 중 하나를 나타냅니다.</p>
<ul>
<li><p><strong>영구 큐 이름</strong>   <code>Submission</code>, <code>Unreachable</code> 또는 <code>Poison</code> 값이 될 수 있습니다.</p></li>
<li><p><strong>배달 큐 이름</strong>   큐의 <strong>NextHopDomain</strong> 속성의 값으로, 실제로 큐의 이름입니다. 이 값은 라우팅 대상이나 배달 그룹이 될 수 있습니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조하십시오.</p></li>
<li><p><strong>큐 정수</strong>   <strong>Get-Message</strong> 또는 <strong>Get-Queue</strong> cmdlet의 <strong>Identity</strong> 속성에 표시되는 배달 큐 또는 섀도 큐의 고유한 정수 값입니다.</p></li>
<li><p><strong>섀도 큐 ID</strong>   섀도 큐 ID에서는 <code>Shadow\&lt;QueueInteger&gt;</code> 구문이 사용됩니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code>, <code>*\&lt;MessageInteger&gt;</code> 또는 <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>지정된 서버나 로컬 서버의 큐 데이터베이스에 있는 모든 큐의 메시지에 대한 모든 복사본입니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메시지 필터링 매개 변수

**Get-Message**, **Remove-Message**, **Resume-Message** 및 **Suspend-Message** cmdlet에서 *Filter* 매개 변수를 사용하여 메시지 속성을 바탕으로 보거나 관리할 메시지를 지정할 수 있습니다. *Filter* 매개 변수는 필터 조건을 충족하는 메시지로 메시지 작업을 제한하는 비교 연산자가 포함된 식을 만듭니다. `-and` 논리 연산자를 사용하여 결과와 일치하는 여러 조건을 지정할 수 있습니다.

*Filter* 매개 변수와 함께 사용할 수 있는 메시지 속성에 대한 전체 목록은 [큐](queues-exchange-2013-help.md)를 참조하십시오.

*Filter* 매개 변수와 함께 사용할 수 있는 비교 연산자 목록은 이 항목의 Comparison operators to use when filtering queues or messages 섹션을 참조하십시오.

메시지를 보고 관리하기 위해 *Filter* 매개 변수를 사용하는 절차와 관련된 예를 보려면 [큐 관리](manage-queues-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 큐 매개 변수

*Queue* 매개 변수는 **Get-Message** cmdlet과 함께 사용하는 경우에만 사용할 수 있습니다. 이 매개 변수를 통해 와일드카드 문자(\*)를 사용하여 여러 큐에서 모든 메시지를 가져오거나 특정 큐의 모든 메시지를 가져올 수 있습니다. *Queue* 매개 변수를 사용할 경우 이 항목의 "큐 ID" 섹션에 설명된 대로 큐 ID 형식 *\<Server\>*\\*\<Queue\>*를 사용합니다.

맨 위로 이동

## 큐나 메시지 필터링 시 사용할 비교 연산자

*Filter* 매개 변수를 사용하여 큐나 메시지 필터 식을 만들 경우 속성 값을 일치시키려면 비교 연산자를 포함해야 합니다. 다음 표에서는 필터 식에서 사용할 수 있는 비교 연산자와 각 연산자의 기능을 보여줍니다. 모든 연산자의 경우 비교되는 값은 대소문자를 구분하지 않습니다.

### 비교 연산자

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>연산자</th>
<th>기능</th>
<th>셸 코드 예제</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>이 연산자는 결과가 식에서 제공된 속성 값과 일치해야 함을 나타냅니다.</p></td>
<td><p>다시 시도 상태인 모든 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>다시 시도 상태인 모든 메시지의 목록 표시:</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>이 연산자는 결과가 식에서 제공된 속성 값과 일치하지 않아야 함을 나타냅니다.</p></td>
<td><p>활성 상태가 아닌 모든 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>활성 상태가 아닌 모든 메시지 목록 표시:</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>이 연산자는 값을 정수 또는 날짜/시간으로 나타내는 속성에 사용됩니다. 필터 결과에는 지정한 속성의 값이 식에서 제공된 값보다 큰 메시지나 큐만 포함됩니다.</p></td>
<td><p>현재 1,000개가 넘는 메시지가 있는 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>현재 다시 시도 횟수가 4회 이상인 메시지의 목록 표시:</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>이 연산자는 값을 정수 또는 날짜/시간으로 나타내는 속성에 사용됩니다. 필터 결과에는 지정한 속성의 값이 식에서 제공된 값보다 크거나 같은 메시지나 큐만 포함됩니다.</p></td>
<td><p>현재 1,000개 이상의 메시지가 있는 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>현재 다시 시도 횟수가 3회 이상인 메시지의 목록 표시:</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>이 연산자는 값을 정수 또는 날짜/시간으로 나타내는 속성에 사용됩니다. 필터 결과에는 지정한 속성의 값이 식에서 제공된 값보다 작은 메시지나 큐만 포함됩니다.</p></td>
<td><p>현재 1,000개 미만의 메시지가 있는 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>다음은 SCL이 6보다 작은 메시지의 목록 표시:</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>이 연산자는 값을 정수 또는 날짜/시간으로 나타내는 속성에 사용됩니다. 필터 결과에는 지정한 속성의 값이 식에서 제공된 값보다 작거나 같은 큐나 메시지만 포함됩니다.</p></td>
<td><p>현재 1,000개 이하의 메시지가 있는 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>다음은 SCL이 6 이하인 메시지의 목록 표시:</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>이 연산자는 값을 텍스트 문자열로 나타내는 속성에 사용됩니다. 필터 결과에는 지정한 속성의 값에 식에서 제공된 텍스트 문자열이 있는 메시지나 큐만 포함됩니다. 텍스트 문자열 필드에 적용되는 <strong>-like</strong> 식에는 * 와일드카드 문자를 사용할 수 있지만 열거 유형의 필드에는 사용할 수 없습니다.</p></td>
<td><p>Contoso.com으로 끝나는 임의의 SMTP 도메인에 대한 대상이 있는 배달 큐 목록 표시:</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>제목에 &quot;payday loan&quot;이라는 텍스트가 있는 메시지의 목록 표시:</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


**-and** 비교 연산자를 사용하여 여러 식을 평가하는 필터를 지정할 수 있습니다. 큐나 메시지는 결과에 포함할 필터의 모든 조건을 충족해야 합니다.

이 예에는 Contoso.com으로 끝나는 임의의 SMTP 도메인 이름에 대한 대상이 있고 현재 500개가 넘는 메시지가 포함된 큐 목록이 표시됩니다.

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

이 예에는 SCL이 5보다 큰, contoso.com 도메인의 모든 전자 메일 주소에서 보내는 메시지 목록이 표시됩니다.

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

맨 위로 이동

## 고급 페이징 매개 변수

현재 메일 흐름에 따라 큐 및 메시지에 대한 쿼리는 큰 개체 집합을 반환할 수 있습니다. 고급 페이징 매개 변수를 사용하여 쿼리 결과를 검색하고 표시하는 방법을 제어할 수 있습니다.

셸을 사용하여 큐 및 큐에 있는 메시지를 보는 경우 쿼리는 한 번에 한 페이지의 정보만 검색합니다. 고급 페이징 매개 변수는 결과 집합의 크기를 제어하고 결과를 정렬하는 데도 사용할 수 있습니다. 모든 고급 페이징 매개 변수는 옵션이며, **Get-Queue** 및 **Get-Message** cmdlet에서 사용할 수 있는 모든 매개 변수 집합 중 하나와 조합하여 사용할 수 있습니다. 고급 페이징 매개 변수를 지정하지 않으면 쿼리는 ID 오름차순으로 결과를 반환합니다.

정렬 순서가 지정되면 메시지 ID 속성은 기본적으로 항상 포함되며 오름차순으로 정렬됩니다. 이는 기본 순서 지정 관계입니다. 정렬 순서에 포함시킬 수 있는 다른 속성은 고유하지 않기 때문에 메시지 ID 속성이 포함됩니다. 메시지 ID 속성을 정렬 순서에 명시적으로 포함시켜면 결과에서 내림차순으로 정렬된 메시지 ID를 표시하도록 지정할 수 있습니다.

*BookmarkIndex* 및 *BookmarkObject* 매개 변수를 사용하여 정렬된 결과 집합에서의 위치를 표시할 수 있습니다. 다음 결과 페이지 검색에서 책갈피 개체가 더 이상 존재하지 않으면 기본 순서 지정 관계가 책갈피에 가장 가까운 개체로 결과 집합이 시작되도록 합니다. 가장 가까운 개체는 지정된 정렬 순서에 따라 달라집니다.

다음 표에서는 고급 페이징 매개 변수에 대해 설명합니다.

### 고급 페이징 매개 변수

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BookmarkIndex</em></p></td>
<td><p>이 매개 변수는 결과 집합에서 표시되는 결과가 시작되는 위치를 지정합니다. 이 매개 변수의 값은 전체 결과 집합에서 1부터 시작하는 인덱스입니다. 값이 0보다 작거나 같은 경우 첫 번째 완전한 결과 페이지가 반환됩니다. 값이 <code>Int.MaxValue</code>로 설정된 경우 마지막 완전한 결과 페이지가 반환됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>이 매개 변수는 결과 집합에서 표시되는 결과가 시작되는 개체를 지정합니다. 책갈피 개체를 지정하면 해당 개체는 검색을 시작하는 지점으로 사용됩니다. <em>SearchForward</em> 매개 변수의 값에 따라 해당 개체의 앞이나 뒤에 나오는 행이 검색됩니다. <em>BookmarkObject</em> 매개 변수 및 <em>BookmarkIndex</em> 매개 변수를 단일 쿼리에서 결합할 수 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>이 매개 변수는 결과 집합에 책갈피 개체를 포함시킬지 여부를 지정합니다. 기본적으로 이 값은 <code>$true</code>로 설정되어 책갈피 개체가 결과 집합에 포함됩니다. 제한된 결과 크기로 쿼리를 실행한 다음, 해당 결과 집합에 있는 마지막 항목을 다음 쿼리에 대한 책갈피로 지정하는 경우가 있습니다. 이 경우 개체가 두 개의 결과 집합 모두에 포함되지 않도록 <em>IncludeBookmark</em>를 <code>$false</code>로 설정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>이 매개 변수는 페이지당 표시할 결과의 수를 지정합니다. 값을 지정하지 않으면 기본 결과 크기인 1,000개의 개체가 사용됩니다. Exchange에서는 결과 집합을 250,000개로 제한합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>이 매개 변수는 숨겨진 매개 변수입니다. 이 매개 변수는 총 결과 수에 대한 정보와 현재 페이지의 첫 번째 개체의 인덱스를 반환합니다. 기본값은 <code>$false</code>입니다.</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>이 매개 변수는 결과 집합에서 앞으로 검색할지 또는 뒤로 검색할지 여부를 지정합니다. 이 매개 변수는 결과 집합이 반환되는 순서에 영향을 미치지 않습니다. 책갈피 인덱스 또는 개체를 기준으로 검색 방향을 결정합니다. 책갈피 인덱스 또는 개체가 지정되지 않으면 <em>SearchForward</em> 매개 변수에 따라 결과 집합의 첫 번째 개체부터 검색할지 마지막 개체부터 검색할지 여부가 결정됩니다.</p>
<p>이 매개 변수에 대한 기본값은 <code>$true</code>입니다. 이 매개 변수가 <code>$true</code>로 설정되고 책갈피가 지정되면 쿼리는 해당 책갈피부터 앞으로 검색합니다. 이 구성을 사용하는 경우 책갈피 이후 검색 결과가 없으면 쿼리는 결과의 마지막 전체 페이지를 반환합니다.</p>
<p><em>SearchForward</em> 매개 변수가 <code>$false</code>로 설정되고 책갈피가 지정되면 쿼리는 해당 책갈피부터 뒤로 검색합니다. 이 구성을 사용하는 경우 책갈피 이후 반환되는 검색 결과가 전체 페이지 분량이 되지 않으면 쿼리는 결과의 첫 번째 전체 페이지를 반환합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>이 매개 변수는 결과 집합의 정렬 순서를 제어하는 데 사용되는 메시지 속성의 배열을 지정합니다. 정렬 순서 속성은 우선 순위의 내림차순으로 지정됩니다. 각 속성은 쉼표로 구분하며, 오름차순으로 정렬하려면 + 기호를 추가하고 내림차순으로 정렬하려면 - 기호를 추가합니다.</p>
<p>이 매개 변수를 사용하여 정렬 순서를 명시적으로 지정하지 않으면 쿼리와 일치하는 레코드가 표시되며 레코드는 각 개체 유형에 대한 ID 필드에 따라 정렬됩니다. 정렬 순서가 명시적으로 지정되지 않으면 결과는 항상 ID의 오름차순으로 정렬됩니다.</p></td>
</tr>
</tbody>
</table>


다음 코드 예에서는 쿼리에서 고급 페이징 매개 변수를 사용하는 방법을 보여 줍니다. 이 예에서 명령은 지정된 서버에 연결하여 500개의 개체를 포함하는 결과 집합을 검색합니다. 결과는 정렬된 순서로 표시되는 데, 먼저 보낸 사람 주소의 오름차순으로 정렬된 다음 메시지 크기의 내림차순으로 정렬됩니다.

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

이어지는 페이지를 보려면 결과 집합에서 검색되는 마지막 개체에 대한 책갈피를 설정하고 추가 쿼리를 실행할 수 있습니다. 이 절차는 셸의 스크립팅 기능을 사용하여 수행해야 합니다.

다음 예에서는 스크립팅을 사용하여 결과의 첫 번째 페이지를 검색하고 책갈피 개체를 설정하고 결과 집합에서 책갈피 개체를 제외한 다음 지정된 서버에서 다음 500개 개체를 검색합니다.

1.  셸을 열고 다음 명령을 입력하여 결과의 첫 번째 페이지를 검색합니다.
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  책갈피 개체를 설정하려면 다음 명령을 입력하여 첫 번째 페이지의 마지막 요소를 변수에 저장합니다.
    
        $temp=$results[$results.length-1]

3.  지정된 서버에서 다음 500개의 개체를 검색하고 책갈피 개체를 제외하려면 다음 명령을 입력합니다.
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

맨 위로 이동

