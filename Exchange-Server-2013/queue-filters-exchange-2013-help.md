---
title: '큐 필터입니다.: Exchange 2013 Help'
TOCTitle: 큐 필터입니다.
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 50484594
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 큐 필터입니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

필터링 큐의 다양 한 보기를 생성합니다. 큐 속성을 사용 하 여 필터 옵션으로 합니다. 필터 조건 지정을 하 여 큐를 찾아 하 고 조치를 취할 신속 하 게 있습니다. 다음 시나리오는 큐 메일 흐름을 관리 하기 위한 필터링을 사용 하는 방법을의 예:

  - 큐 길이 설정 된 임계값을 초과한 있는지 여부를 나타내는 Microsoft System Center Operations Manager에서 메시지를 수신 합니다. 서버 전체 메일 흐름 문제가 있는지 여부를 확인 하려고 합니다.
    
    일반적인 고려 무엇을 초과 하는 메시지 수 있는 모든 큐를 보려면 필터를 만들 수 있습니다. 메일 흐름 문제는 표시 되는 경우 필터 결과에 있는 모든 큐를 선택할 수 있으며 조사를 계속 하는 동안에 큐를 일시 중단 수 있습니다.

  - 메일 흐름 문제의 원인을 확인 하는 여러 큐를 일시 중단 합니다. 이 문제는 잘못 된 커넥터 구성에 의해 발생 한 및 고정 됩니다를 확인 합니다.
    
    일시 중지 됨, 상태가 하 고 다음 필터 결과의 모든 큐를 선택 하 고 큐를 다시 시작 하는 모든 큐를 보려면 필터를 만들 수 있습니다.

## 큐를 필터링 할 때 사용 하 여 큐 속성

큐 속성 필터를 만들고 지정 된 조건을 충족 하는 큐를 찾습니다를 사용할 수 있습니다. 큐 뷰어 또는 큐 관리 cmdlet에서 *Filter* 매개 변수를 사용 하 여 필터를 만들 수 있습니다. Note 큐 관리 cmdlet 큐 뷰어 것 보다 많은 필터링 할 수 있는 속성을 지원 합니다. 다음 표에 큐 속성으로 필터링 할 수 있는 하 고 해당 속성에 대 한 유효한 값입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>큐 뷰어에서 큐 속성</th>
<th>셸 큐 속성</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>이 속성은 받는 사람 확인 하는 동안 발생 한 일시적인 오류로 인해 전송 큐에 반환 된 메시지 수가 식별 합니다. 지연 된 메시지에 대 한 자세한 내용은 <a href="recipient-resolution-exchange-2013-help.md">받는 사람 확인</a>을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>배달 유형</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p><strong>DeliveryType</strong> 에 대 한 유효한 값은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션에서 설명 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>Identity</code></p></td>
<td><p>이 속성은 <em>&lt;Server&gt;\&lt;Queue&gt;</em>의 형태로 큐의 id입니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;큐 identity&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>이 속성은 메시지가 큐로 들어오는 속도 나타내는 계산 된 숫자입니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;IncomingRate, outgoingrate, Velocity&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>마지막 오류</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>이 속성은 큐에 대 한 기록 된 마지막 오류의 텍스트 문자열을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>마지막 시간을 다시 시도</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>이 속성은 날짜/시간 마지막 연결 시도의 <code>Retry</code>의 상태를 갖고 있는 큐에 대 한를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>이 속성은 Microsoft 내부에서 사용을 위해 예약 및 온-프레미스 Exchange 2013 조직에서 사용 되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지 수</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>이 속성은 큐의 메시지 수를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>이 속성은 <code>Internal</code> 또는 <code>External</code> 으로 큐의 다음 홉을 지정 하 고 큐의 <strong>DeliveryType</strong> 속성의 값을 기반 합니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>다음 홉의 GUID 이며 큐의 <strong>DeliveryType</strong> 속성의 값에 기반 합니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="odd">
<td><p><strong>다음 홉 도메인</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>이 속성은 다음 홉의 이름 및 큐의 <strong>DeliveryType</strong> 속성의 값에 기반 합니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;NextHopSolutionKey&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>다음 시간을 다시 시도</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>이 속성은 날짜/시간 다음 연결 시도의 <code>Retry</code>의 상태를 갖고 있는 큐에 대 한를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>이 속성은 메시지 큐에서 나가는 속도 나타내는 계산 된 숫자입니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;IncomingRate, outgoingrate, Velocity&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>이 속성은 Microsoft 내부에서 사용을 위해 예약 및 온-프레미스 Exchange 2013 조직에서 사용 되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>상태</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>이 속성의 현재 큐 상태를 나타냅니다. 큐는 다음 상태 값을 연결 하는 경우, 없음, 활성 중 하나를 가질 수 준비, 일시 중단 하거나 다시 시도 합니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;큐 상태&quot; 섹션을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>해당 없음</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>이 속성은 도메인 도메인 보안에 대해 구성 된 경우 대상 도메인의 FQDN을 포함 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>해당 없음</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>이 속성 큐 드레이닝는 얼마나 효율적으로 나타내는 계산 된 숫자를 포함 합니다. 자세한 내용은 <a href="queues-exchange-2013-help.md">큐</a> 항목의 &quot;IncomingRate, outgoingrate, Velocity&quot; 섹션을 참조 하십시오.</p></td>
</tr>
</tbody>
</table>

