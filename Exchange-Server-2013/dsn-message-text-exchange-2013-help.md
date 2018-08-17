---
title: 'DSN 메시지 텍스트: Exchange 2013 Help'
TOCTitle: DSN 메시지 텍스트
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 50484468
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN 메시지 텍스트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013 에서 사용자 지정 된 배달 상태 알림 (DSN) 메시지에 텍스트를 포함할 수 하 고 해당 텍스트를 HTML 서식을 지정할 수 있습니다.

DSN 메시지의 받는 사람에 게 표시 하려는 모든 정보를 포함할 수 있습니다. 예, 지원 센터에 및 지원 부서의 웹사이트에 대 한 링크에 대 한 연락처 정보는 DSN에 대 한 자세한 설명을 포함할 수 있습니다. 각 DSN 메시지에는 최대 512 자까지 포함 될 수 있습니다.

HTML의 DSN 메시지를 표시할 수 있으므로 DSN 텍스트의 HTML 서식 태그를 포함할 수 있습니다. 예, DSN 메시지 일부 텍스트를 굵게 하려는 경우 \< B \>에서 텍스트 및 \</B \> HTML 태그를 묶습니다. 다음 표에서 DSN 메시지 텍스트에 사용할 수 있는 유효한 HTML 태그에 대 한 예가 제공 됩니다.

### DSN 메시지에 사용 하기 위해 유효한 HTML 태그

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>HTML 태그</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt; B &gt;</p></td>
<td><p>굵게 시작</p></td>
</tr>
<tr class="even">
<td><p>&lt;/B &gt;</p></td>
<td><p>굵게 끝</p></td>
</tr>
<tr class="odd">
<td><p>&lt; A HREF = &quot;url&quot; &gt;</p></td>
<td><p>하이퍼링크 시작</p></td>
</tr>
<tr class="even">
<td><p>&lt;/A &gt;</p></td>
<td><p>하이퍼링크 끝</p></td>
</tr>
<tr class="odd">
<td><p>&lt; b R &gt;</p></td>
<td><p>링크 나누기</p></td>
</tr>
<tr class="even">
<td><p>&lt; EM &gt;</p></td>
<td><p>기울임꼴 시작</p></td>
</tr>
<tr class="odd">
<td><p>&lt; /EM &gt;</p></td>
<td><p>기울임꼴 끝</p></td>
</tr>
<tr class="even">
<td><p>&lt; P &gt;</p></td>
<td><p>단락 시작</p></td>
</tr>
<tr class="odd">
<td><p>&lt; /P &gt;</p></td>
<td><p>단락 끝</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 기본적으로 Exchange HTML DSN 메시지를 보내고 있지만 Exchange HTML DSN 메시지를 보냅니다 내부 보낸사람, 외부 보낸사람 또는 둘 모두 있는지 여부를 구성할 수 있습니다. 이 동작을 구성 하려면 <EM>InternalDsnSendHtml</EM> 매개 변수 및 <STRONG>Set-TransportService</STRONG> 명령 사용 하 여 <EM>ExternalDsnSendHtml</EM> 매개 변수를 수정 합니다.<BR><EM>InternalDsnSendHtml</EM> 매개 변수는 <CODE>$false</CODE>로설정하면 Exchange 내부 보낸사람에 게 DSN 메시지에 HTML 태그를 생략 합니다. <EM>ExternalDsnSendHtml</EM> 매개 변수는 <CODE>$false</CODE>로설정하면 Exchange 외부 보낸사람에 게 DSN 메시지에 HTML 태그를 생략 합니다.



DSN 메시지 텍스트의 Exchange를 사용 하는 다음 문자는 특별 한 의미를 갖습니다.

  - 보다 큼 (\>) 기호

  - 보다 작음 기호 (\<)

  - 앰퍼샌드 (&)

  - 큰따옴표 (")

이러한 문자는 HTML 태그 시작 하 고 하순, 위치 및 보낸 사람에 게 표시할 텍스트 시작 하 고 중지 하는 위치를 결정 하는데 사용 됩니다. DSN 메시지에 이러한 문자를 표시 하려는 경우에 다음 표에 있는 이스케이프 코드를 사용 해야 합니다.

예, `"Please contact the Help Desk at <1234>."`메시지 표시 하려는 경우 `"Please contact the Help Desk at &lt;1234&gt;." `DSN 메시지 텍스트에 추가 해야 합니다.

### DSN 메시지 문자 이스케이프 코드

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>이스케이프 코드</th>
<th>문자</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&amp; l t;</p></td>
<td><p>&lt;</p></td>
</tr>
<tr class="even">
<td><p>&amp; g t;</p></td>
<td><p>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>&amp; q u o t;</p></td>
<td><p>&quot;</p></td>
</tr>
<tr class="even">
<td><p>&amp; 재료 데이터베이스</p></td>
<td><p>&amp;</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> 큰따옴표 ("), <CODE>&lt;A HREF="url"&gt;</CODE>등을 포함 하는 DSN 메시지 텍스트에 HTML 태그를 포함 하는 경우에 전체 DSN 메시지 텍스트 주위 작은따옴표 (')를 사용 해야 합니다. 큰따옴표 중심으로 전체 DSN 메시지 텍스트 및 HTML 태그를 사용 하는 경우 오류 메시지를 받습니다.


