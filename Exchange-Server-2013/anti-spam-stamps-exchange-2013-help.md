---
title: '스팸 방지 스탬프: Exchange 2013 Help'
TOCTitle: 스팸 방지 스탬프
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 50482752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스팸 방지 스탬프

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

스팸 방지 스탬프를 사용하면 보낸 사람별 정보, 퍼즐 유효성 검사 결과 및 콘텐츠 필터링 결과와 같은 진단 메타데이터 또는 스탬프를 인터넷에서 인바운드 메시지를 필터링하는 스팸 방지 기능을 통과하는 메시지에 적용함으로써 스팸 관련 문제를 진단할 수 있습니다. 스팸 방지 스탬프에는 피싱 지수 스탬프, 스팸 지수 스탬프 및 보낸 사람 ID 스탬프의 세 가지가 있습니다.

스팸 방지 스탬프를 진단 도구로 사용하여 개인 사용자의 사서함으로 배달되는 오판정 및 의심스러운 스팸 메시지에 대해 취할 조치를 결정할 수 있습니다.

## 스팸 방지 스탬프 보기

스팸 방지 스탬프는 Microsoft Outlook을 사용하여 볼 수 있습니다. 자세한 내용은 [Outlook에서 스팸 방지 스탬프 보기](view-anti-spam-stamps-in-outlook-exchange-2013-help.md) 항목을 참조하십시오.

## 스팸 방지 보고서 이해

스팸 방지 보고서는 전자 메일 메시지에 적용된 스팸 방지 필터 결과가 요약되어 있는 보고서입니다. 콘텐츠 필터 에이전트는 이 스탬프를 다음과 같이 X-헤더 형식으로 메시지 봉투에 적용합니다.

```powershell
X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance
``` 

다음 표에서는 스팸 방지 보고서에 나타날 수 있는 필터 정보에 대해 설명합니다.


> [!NOTE]  
> 스팸 방지 보고서에는 특정 메시지에 적용된 필터에 대한 정보만 표시됩니다. 스팸 방지 보고서에 일반적으로 다음 표에 나열된 모든 정보가 포함되지는 않습니다. 예를 들어, 다음과 같은 스팸 방지 보고서를 받을 수 있습니다. <CODE>DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures</CODE>.



### 스팸 방지 보고서의 필터 정보

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>스탬프</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SID</p></td>
<td><p>SID(보낸 사람 ID) 스탬프는 전자 메일의 도메인 사용을 인증하는 SPF(보낸 사람 정책 프레임워크)를 기반으로 합니다. SPF는 메시지 봉투에 <code>Received-SPF</code>로 표시됩니다. 보낸 사람 ID 평가 프로세스에서 메시지의 보낸 사람 ID 상태가 생성됩니다. 이 상태는 다음 값 중 하나로 반환될 수 있습니다.</p>
<ul>
<li><p><strong>Pass</strong>   IP 주소 및 PRA(Purported Responsible Address)가 모두 보낸 사람 ID 유효성 검사를 통과했습니다.</p></li>
<li><p><strong>Neutral</strong>   게시된 보낸 사람 ID 데이터가 명시적으로 확실치 않습니다.</p></li>
<li><p><strong>Soft fail</strong>   PRA의 IP 주소가 허용되지 않은 집합에 포함될 수 있습니다.</p></li>
<li><p><strong>Fail</strong>   IP 주소가 허용되지 않거나, 수신 메일에서 PRA를 찾을 수 없거나, 보내는 도메인이 없습니다.</p></li>
<li><p><strong>None</strong>   보낸 사람의 DNS에 게시된 SPF 데이터가 없습니다.</p></li>
<li><p><strong>TempError</strong>   사용할 수 없는 DNS 서버와 같은 일시적인 DNS 오류가 발생했습니다.</p></li>
<li><p><strong>PermError</strong>   레코드 형식 오류와 같은 잘못된 DNS 레코드입니다.</p></li>
</ul>
<p>보낸 사람 ID 스탬프는 다음과 같이 메시지 봉투에 X-헤더로 표시됩니다.</p>

```powershell
X-MS-Exchange-Organization-SenderIdResult:<status>
```
<p>보낸 사람 ID에 대한 자세한 내용은 <a href="sender-id-exchange-2013-help.md">보낸사람 ID</a> 항목을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>DV</p></td>
<td><p>DV(DAT 버전) 스탬프는 메시지를 검색할 때 사용했던 스팸 정의 파일의 버전을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>SA</p></td>
<td><p>SA(서명 작업) 스탬프는 메시지에서 발견된 서명으로 인해 메시지가 복원 또는 삭제되었음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p>SV</p></td>
<td><p>SV(서명 DAT 버전) 스탬프는 메시지를 검색할 때 사용했던 서명 파일의 버전을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>PCL</p></td>
<td><p>PCL(피싱 지수) 스탬프는 콘텐츠를 기준으로 메시지의 등급을 표시하며 콘텐츠 필터 에이전트에서 메시지를 처리할 때 적용됩니다. 이 상태는 다음 값 중 하나로 반환될 수 있습니다.</p>
<ul>
<li><p><strong>Neutral   </strong>메시지 내용이 피싱이 아닙니다.</p></li>
<li><p><strong>Suspicious   </strong>메시지 내용이 피싱일 가능성이 있습니다.</p></li>
</ul>
<p>PCL 값은 1부터 8까지로 지정할 수 있습니다. PCL 등급이 1부터 3까지이면 <code>Neutral</code> 상태가 반환됩니다. 즉, 해당 메시지의 내용은 피싱일 가능성이 낮습니다. PCL 등급이 4부터 8까지이면 <code>Suspicious</code> 상태가 반환됩니다. 이러한 메시지의 경우에는 피싱 메시지일 가능성이 높습니다.</p>
<p>이 값은 Outlook이 메시지에 대해 수행하는 작업을 결정하는 데 사용됩니다. Outlook은 PCL 스탬프를 사용하여 의심스러운 메시지의 내용을 차단합니다.</p>
<p>PCL 스탬프는 다음과 같이 메시지 봉투에 X-헤더로 표시됩니다.</p>

```powershell
X-MS-Exchange-Organization-PCL:&lt;status&gt;
```
</td>
</tr>
<tr class="even">
<td><p>SCL</p></td>
<td><p>메시지의 SCL(스팸 지수) 스탬프에는 콘텐츠를 기반으로 한 메시지 등급이 표시됩니다. 콘텐츠 필터 에이전트는 메시지의 내용을 평가하고 SCL 등급을 각 메시지에 할당하기 위해 Microsoft SmartScreen 기술을 사용합니다. SCL 값은 0에서 9 사이이며 이 값이 낮을수록 스팸일 가능성이 낮고 높을수록 스팸일 가능성이 높은 것으로 간주됩니다. Exchange 및 Outlook에서 수행하는 작업은 SCL 임계값 설정에 따라 달라집니다.</p>
<p>SCL 스탬프는 다음과 같이 메시지 봉투에 X-헤더로 표시됩니다.</p>  

```powershell
X-MS-Exchange-Organization-SCL:&lt;status&gt;
```

<p>SCL 임계값 및 작업에 대한 자세한 내용은 <a href="spam-confidence-level-threshold-exchange-2013-help.md">스팸 지수 임계값</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>CW</p></td>
<td><p>메시지의 CW(사용자 지정 가중치) 스탬프는 해당 메시지에 승인되지 않는 단어나 구가 포함되어 있으며 해당 단어나 구의 SCL 값(가중치)이 최종 SCL 점수에 적용되었음을 나타냅니다.</p>
<ul>
<li><p>승인되지 않은 구 또는 차단 구의 가중치는 최대로 지정되며 SCL 점수는 9로 변경됩니다.</p></li>
<li><p>승인된 단어나 구 또는 허용 구의 가중치는 최저로 지정되며 SCL 점수는 0으로 변경됩니다.</p></li>
</ul>
<p>승인된 단어/구와 승인되지 않은 단어/구를 콘텐츠 필터링 에이전트에 추가하는 방법에 대한 자세한 내용은 <a href="manage-content-filtering-exchange-2013-help.md">콘텐츠 필터링 관리</a> 항목을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>PP</p></td>
<td><p>PP(사전 해결된 퍼즐) 스탬프는 보낸 사람의 메시지에 Outlook 전자 메일 소인 유효성 검사 기능을 기준으로 유효하며 해결된 계산 소인이 있는 경우 해당 보낸 사람은 악의적일 가능성이 없음을 나타냅니다. 이런 경우 콘텐츠 필터 에이전트가 SCL 등급을 낮출 것입니다.</p>
<p>콘텐츠 필터 에이전트는 전자 메일 소인 유효성 검사를 사용하며 다음 조건 중 하나가 충족되는 경우에는 SCL 등급을 변경하지 않습니다.</p>
<ul>
<li><p>인바운드 메시지에 계산 소인 헤더가 없는 경우</p></li>
<li><p>계산 소인 헤더가 유효하지 않은 경우</p></li>
</ul>
<p>소인 유효성 검사 기능에 대한 자세한 내용은 <a href="content-filtering-exchange-2013-help.md">콘텐츠 필터링</a> 항목을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>TIME:TimeBasedFeatures</p></td>
<td><p>TIME 스탬프는 메시지를 보낸 시간과 메시지를 받은 시간 사이에 오랜 시간 지연이 있었음을 나타냅니다. TIME 스탬프는 메시지의 최종 SCL 등급을 결정하는 데 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p>MIME:MIMECompliance</p></td>
<td><p>MIME 스탬프는 전자 메일 메시지가 MIME 호환 메시지가 아님을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>P100:PhishingBlock</p></td>
<td><p>P100 스탬프는 피싱 정의 파일에 있는 URL이 메시지에 들어 있음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p>IPOnAllowList</p></td>
<td><p>IPOnAllowList 스탬프는 보낸 사람의 IP 주소가 IP 허용 목록에 있음을 나타냅니다. IP 허용 목록에 대한 자세한 내용은 <a href="http://go.microsoft.com/fwlink/?linkid=268732">연결 필터링 이해</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>MessageSecurityAntispamBypass</p></td>
<td><p>MessageSecurityAntispamBypass 스탬프는 메시지의 콘텐츠를 필터링하지 않았으며 보낸 사람이 스팸 방지 필터를 무시하도록 허용되었음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p>SenderBypassed</p></td>
<td><p>SenderBypassed 스탬프는 콘텐츠 필터 에이전트에서 해당 보낸 사람으로부터 받은 메시지에 대해서는 콘텐츠 필터링을 처리하지 않음을 나타냅니다. 자세한 내용은 <a href="manage-content-filtering-exchange-2013-help.md">콘텐츠 필터링 관리</a> 항목을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>AllRecipientsBypassed</p></td>
<td><p>AllRecipientsBypassed 스탬프는 메시지의 모든 받는 사람에 대해 다음 조건 중 하나가 충족됨을 나타냅니다.</p>
<ul>
<li><p>받는 사람 사서함의 <em>AntispamBypassedEnabled</em> 매개 변수가 <code>$true</code>로 설정되어 있습니다. 이는 <strong>Set-Mailbox</strong> cmdlet을 사용하여 관리자만 설정할 수 있는 받는 사람별 설정입니다.</p></li>
<li><p>메시지 보낸 사람이 받는 사람의 Outlook 수신 허용 - 보낸 사람 목록에 있습니다. 수신 허용 - 보낸 사람 목록에 대한 자세한 내용은 <a href="manage-safelist-aggregation-exchange-2013-help.md">수신 허용 목록 집계 관리</a> 항목을 참조하십시오.</p></li>
<li><p>콘텐츠 필터 에이전트가 해당 받는 사람에게 전송된 메시지에 대해서는 콘텐츠 필터링을 처리하지 않습니다. 받는 사람 예외에 대한 자세한 내용은 <a href="manage-content-filtering-exchange-2013-help.md">콘텐츠 필터링 관리</a> 항목을 참조하십시오.</p></li>
</ul></td>
</tr>
</tbody>
</table>

