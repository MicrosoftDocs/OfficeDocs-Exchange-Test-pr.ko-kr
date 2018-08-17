---
title: '-ContentFilter 매개 변수에 대 한 필터링 할 수 있는 속성: Exchange 2013 Help'
TOCTitle: -ContentFilter 매개 변수에 대 한 필터링 할 수 있는 속성
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 50556086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# \-ContentFilter 매개 변수에 대 한 필터링 할 수 있는 속성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-09-10_

이 항목에서는 *ContentFilter* 매개 변수의 필터링할 수 있는 속성에 대해 설명합니다. *ContentFilter* 매개 변수를 사용하여 메시지를 필터가 일치하는 .pst 파일로 내보낼 수 있습니다. *ContentFilter* 매개 변수는 [New-MailboxExportRequest](https://technet.microsoft.com/ko-kr/library/ff607299\(v=exchg.150\)) cmdlet에서 사용됩니다.

## 필터링할 수 있는 속성

*ContentFilter* 매개 변수의 여러 속성에는 와일드카드 문자를 사용할 수 있습니다. 와일드카드 문자를 사용하는 경우 **-eq** 연산자 대신 **-like** 연산자를 사용합니다. **-like** 연산자는 문자열 등 다양한 형식으로 패턴 일치를 찾는 데 사용되는 반면 **-eq** 연산자는 정확한 일치를 찾는 데 사용됩니다.

다음 표에는 *ContentFilter* 매개 변수의 필터링할 수 있는 속성 목록이 포함되어 있습니다. 이 표는 속성의 이름, 설명, 사용 가능한 값 및 구문 예를 보여줍니다. OPATH 필터에 대한 자세한 내용은 [받는 사람 셸 명령에 대 한 필터](https://technet.microsoft.com/ko-kr/library/bb124268\(v=exchg.150\))를 참조하십시오.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>속성</th>
<th>설명</th>
<th>값</th>
<th>구문 예</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>All</p></td>
<td><p>이 속성은 인덱스 속성에 특정 문자열이 있는 모든 메시지를 반환합니다. 예를 들어 받는 사람, 보낸 사람으로 &quot;Ayla&quot;가 있거나 메시지 본문에 언급된 이름이 있는 모든 메시지를 내보내려는 경우 이 속성을 사용합니다.</p></td>
<td><p>문자열</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {All -like &#39;*Ayla*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Attachment</p></td>
<td><p>이 속성은 첨부 파일의 콘텐츠나 첨부 파일 이름에 지정된 문자열이 있는 메시지를 반환합니다.</p></td>
<td><p>문자열</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {Attachment -like &#39;*.jpg&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>BCC</p></td>
<td><p>이 속성은 숨은 참조 필드에 지정된 받는 사람이 있는 보낸 메시지를 반환합니다.</p></td>
<td><p>표시 이름</p>
<p>별칭</p>
<p>SMTP 주소</p>
<p>LegacyDN</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {(BCC -eq &#39;ayla@contoso.com&#39;) -or (BCC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="even">
<td><p>Body</p></td>
<td><p>이 속성은 메시지 본문 내에 지정된 문자열이 있는 메시지를 반환합니다.</p></td>
<td><p>문자열</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {Body -like &#39;*prospectus*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>이 속성은 일치하는 범주가 있는 메시지를 반환합니다. 범주는 사용자 또는 받은 편지함 규칙에 따라 설정됩니다.</p></td>
<td><p>문자열</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {Category -like &#39;*Blue*&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>CC</p></td>
<td><p>이 속성은 참조 필드에 지정된 받는 사람이 있는 보낸 메시지를 반환합니다.</p></td>
<td><p>표시 이름</p>
<p>별칭</p>
<p>SMTP 주소</p>
<p>LegacyDN</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {(CC -eq &#39;ayla@contoso.com&#39;) -or (CC -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Expires</p></td>
<td><p>이 속성은 지정한 만료 시간 스탬프가 있는 메시지를 반환합니다.</p></td>
<td><p>날짜-시간 스탬프</p></td>
<td><pre><code>-ContentFilter {Expires -lt &#39;01/01/2013&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>HasAttachment</p></td>
<td><p>이 속성은 첨부 파일이 있는 메시지 또는 첨부 파일이 없는 메시지를 반환합니다.</p></td>
<td><p>부울</p>
<p><code>$true</code> 또는 <code>$false</code></p></td>
<td><pre><code>-ContentFilter {HasAttachment -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Importance</p></td>
<td><p>이 속성은 지정된 중요도가 있는 메시지를 반환합니다.</p></td>
<td><p>0 또는 &quot;낮음&quot;</p>
<p>1 또는 &quot;표준&quot;</p>
<p>2 또는 &quot;높음&quot;</p></td>
<td><pre><code>-ContentFilter {Importance -eq &#39;high&#39;}</code></pre>
<pre><code>-ContentFilter {Importance -eq 2}</code></pre></td>
</tr>
<tr class="even">
<td><p>IsFlagged</p></td>
<td><p>이 속성은 사용자 또는 받은 편지함 규칙에 의해 플래그가 지정된 메시지를 반환합니다.</p></td>
<td><p>부울</p>
<p><code>$true</code> 또는 <code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsFlagged -eq $true}</code></pre></td>
</tr>
<tr class="odd">
<td><p>IsRead</p></td>
<td><p>이 속성은 사용자가 읽은 메시지 또는 읽지 않은 메시지를 반환합니다.</p></td>
<td><p>부울</p>
<p><code>$true</code> 또는 <code>$false</code></p></td>
<td><pre><code>-ContentFilter {IsRead -eq $true}</code></pre></td>
</tr>
<tr class="even">
<td><p>MessageKind</p></td>
<td><p>이 속성은 지정된 형식의 메시지를 반환합니다.</p></td>
<td><p>일정</p>
<p>연락처</p>
<p>문서</p>
<p>전자 메일</p>
<p>팩스</p>
<p>InstantMessage</p>
<p>저널</p>
<p>메모</p>
<p>게시물</p>
<p>RSSFeed</p>
<p>작업</p>
<p>음성 사서함</p></td>
<td><pre><code>-ContentFilter {MessageKind -eq &#39;Calendar&#39;}</code></pre>
<pre><code>-ContentFilter {MessageKind -ne &#39;Email&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>MessageLocalee</p></td>
<td><p>이 속성은 지정된 로캘의 메시지를 반환합니다.</p></td>
<td><p>CultureInfo</p></td>
<td><pre><code>-ContentFilter {MessageLocale -ne &#39;en-US&#39;}</code></pre>
<pre><code>-ContentFilter {MessageLocale -eq &#39;tr-TR&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>이 속성은 받는 사람, 숨은 참조 또는 참조 필드에 지정된 받는 사람이 있는 메시지를 반환합니다.</p></td>
<td><p>표시 이름</p>
<p>별칭</p>
<p>SMTP 주소</p>
<p>LegacyDN</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {(Participants -eq &#39;ayla@contoso.com&#39;) -or (Participants -eq &#39;tony@contoso.com&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>PolicyTag</p></td>
<td><p>이 속성은 정책 태그가 있는 메시지를 반환합니다. Exchange 저장소는 정책 태그를 GUID로 유지합니다. 그러므로 문자열은 PR_POLICY_TAG로 검색되는 명시적인 GUID 값 또는 와일드카드 문자열을 포함할 수 있습니다.</p>
<p>지원되는 값이 GUID가 아닌 경우 명령은 Active Directory 정보를 사용하여 GUID에 대한 이름을 확인합니다.</p></td>
<td><p>문자열</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {PolicyTag -ne &#39;00000000-0000-0000-0000-000000000000&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Received</p></td>
<td><p>이 속성은 지정된 Received 타임스탬프가 있는 메시지를 반환합니다.</p></td>
<td><p>날짜-시간 스탬프</p></td>
<td><pre><code>-ContentFilter {Received -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Received -lt &#39;01/01/2013&#39;) -and (Received -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Sender</p></td>
<td><p>이 속성은 지정한 보낸 사람으로부터 받은 메시지를 반환합니다.</p></td>
<td><p>표시 이름</p>
<p>별칭</p>
<p>SMTP 주소</p>
<p>LegacyDN</p>
<p>와일드카드</p></td>
<td><pre><code>ContentFilter {Sender -eq &#39;tony&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Sent</p></td>
<td><p>이 속성은 지정된 Sent 타임스탬프가 있는 메시지를 반환합니다.</p></td>
<td><p>날짜-시간 스탬프</p></td>
<td><pre><code>-ContentFilter {Sent -lt &#39;01/01/2013 9:00&#39;}</code></pre>
<pre><code>-ContentFilter {(Sent -lt &#39;01/01/2013&#39;) -and (Sent -gt &#39;01/01/2012&#39;)}</code></pre></td>
</tr>
<tr class="odd">
<td><p>Size</p></td>
<td><p>이 속성은 특정 크기의 메시지를 반환합니다.</p></td>
<td><p>B(바이트)</p>
<p>KB(킬로바이트)</p>
<p>MB(메가바이트)</p></td>
<td><pre><code>-ContentFilter {Size -gt &#39;10KB&#39;}</code></pre></td>
</tr>
<tr class="even">
<td><p>Subject</p></td>
<td><p>이 속성은 메시지 제목 내에 지정된 문자열이 있는 메시지를 반환합니다.</p></td>
<td><p>문자열</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {Subject -like &#39;*meeting*&#39;}</code></pre></td>
</tr>
<tr class="odd">
<td><p>To</p></td>
<td><p>이 속성은 받는 사람 필드에 지정된 받는 사람이 있는 보낸 메시지를 반환합니다.</p></td>
<td><p>표시 이름</p>
<p>별칭</p>
<p>SMTP 주소</p>
<p>LegacyDN</p>
<p>와일드카드</p></td>
<td><pre><code>-ContentFilter {To -eq &#39;aylakol&#39;}</code></pre></td>
</tr>
</tbody>
</table>

