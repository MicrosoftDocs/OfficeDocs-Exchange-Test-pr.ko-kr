---
title: '원본 위치 eDiscovery에 대 한 메시지의 속성 및 검색 연산자: Exchange 2013 Help'
TOCTitle: 원본 위치 eDiscovery에 대 한 메시지의 속성 및 검색 연산자
ms:assetid: 402b74e4-8853-4c51-9737-1a9c19f8e3dd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn774955(v=EXCHG.150)
ms:contentKeyID: 62618512
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 eDiscovery에 대 한 메시지의 속성 및 검색 연산자

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

이 항목에서는 원본 위치 eDiscovery 및 유지를 사용 하 여 검색할 수 있는 Exchange 전자 메일 메시지의 속성을 설명 Exchange Server 2013 및 Exchange Online 합니다. 부울 검색 연산자 및 eDiscovery 검색 결과 구체화 하는데 사용할 수 있는 다른 검색 쿼리 기법에도 항목에 설명 합니다.

원본 위치 eDiscovery 키워드 쿼리 언어 (KQL)를 사용합니다. 자세한 내용은 [키워드 쿼리 언어 구문 참조 (영문)](https://go.microsoft.com/fwlink/?linkid=269603)을 참조 하십시오.

## Exchange에서 검색 가능한 속성

다음 표에 원본 위치 eDiscovery 검색을 사용 하 여 검색할 수 있는 전자 메일 메시지 속성 또는 **New-MailboxSearch** 또는 **Set-MailboxSearch** cmdlet을 사용 하 여 합니다. 테이블의 각 속성 및 예제에서 반환 된 검색 결과에 대 한 설명을 *property:value* 구문 예를 포함 합니다.


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
<th>속성 설명</th>
<th>예제</th>
<th>예제에서 반환된 검색 결과</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Attachment</p></td>
<td><p>전자 메일 메시지에 첨부되는 파일의 이름입니다.</p></td>
<td><p>attachment:annualreport.ppt</p>
<p>attachment:annual*</p></td>
<td><p>첨부 파일이 있는 메시지 라는 annualreport.ppt 합니다.</p>
<p>두번째 예제에서는 와일드 카드를 사용 하 여 메시지를 반환 라는 단어가 들어 있는 첨부 파일의 파일 이름에 &quot;연간&quot; 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Bcc</p></td>
<td><p>전자 메일 메시지의 숨은 참조 필드입니다.1</p></td>
<td><p>bcc:pilarp@contoso.com</p>
<p>bcc:pilarp</p>
<p>bcc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>모든 예제는 숨은 참조 필드에 Pilar Pinilla가 포함된 메시지를 반환합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Category</p></td>
<td><p>검색할 범주입니다. Outlook 또는 Outlook Web App을 사용하여 범주를 정의할 수 있습니다. 가능한 값은 다음과 같습니다.</p>
<ul>
<li><p>blue</p></li>
<li><p>green</p></li>
<li><p>orange</p></li>
<li><p>purple</p></li>
<li><p>red</p></li>
<li><p>yellow</p></li>
</ul></td>
<td><p>category:&quot;Red Category&quot;</p></td>
<td><p>원본 사서함에서 red 범주가 지정된 메시지입니다.</p></td>
</tr>
<tr class="even">
<td><p>Cc</p></td>
<td><p>전자 메일 메시지의 참조 필드입니다.1</p></td>
<td><p>cc:pilarp@contoso.com</p>
<p>cc:&quot;Pilar Pinilla&quot;</p></td>
<td><p>두 예제 모두에서 참조 필드에 Pilar Pinilla가 지정된 메시지입니다.</p></td>
</tr>
<tr class="odd">
<td><p>From</p></td>
<td><p>전자 메일 메시지의 보낸 사람입니다.1</p></td>
<td><p>from:pilarp@contoso.com</p>
<p>from:contoso.com</p></td>
<td><p>지정된 사용자가 보냈거나 지정된 도메인에서 보낸 메시지입니다.</p></td>
</tr>
<tr class="even">
<td><p>Importance</p></td>
<td><p>보낸 사람이 메시지를 보낼 때 지정할 수 있는 전자 메일 메시지의 중요도입니다. 기본적으로 보낸 사람이 중요도를 <strong>높음</strong> 또는 <strong>낮음</strong>으로 설정하지 않았다면 메시지는 보통 중요도로 전송됩니다.</p></td>
<td><p>importance:high</p>
<p>importance:medium</p>
<p>importance:low</p></td>
<td><p>높음 중요도, 보통 중요도 또는 낮은 중요도로 표시된 메시지입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Kind</p></td>
<td><p>검색할 메시지의 유형입니다. 사용 가능한 값:</p>
<ul>
<li><p>contacts</p></li>
<li><p>docs</p></li>
<li><p>email</p></li>
<li><p>faxes</p></li>
<li><p>im</p></li>
<li><p>journals</p></li>
<li><p>meetings</p></li>
<li><p>notes</p></li>
<li><p>posts</p></li>
<li><p>rssfeeds</p></li>
<li><p>작업</p></li>
<li><p>voicemail</p></li>
</ul></td>
<td><p>kind:email</p>
<p>kind:email OR kind:im OR kind:voicemail</p></td>
<td><p>검색 조건에 맞는 전자 메일 메시지입니다. 두 번째 예제에서는 검색 조건을 만족하는 전자 메일 메시지, 메신저 대화 및 음성 메시지를 반환합니다.</p></td>
</tr>
<tr class="even">
<td><p>Participants</p></td>
<td><p>전자 메일 메시지의 모든 사용자 필드로, 보낸 사람, 받는 사람, 참조 및 숨은 참조가 여기에 해당됩니다.1</p></td>
<td><p>participants:garthf@contoso.com</p>
<p>participants:contoso.com</p></td>
<td><p>하 여 메시지를 보내거나 garthf@contoso.com로 전송 합니다.</p>
<p>보낸 또는 contoso.com 도메인의 사용자에 게 보내는 모든 메시지를 반환 하는 두번째 예제입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Received</p></td>
<td><p>받는 사람이 전자 메일 메시지를 받은 날짜입니다.</p></td>
<td><p>received:04/15/2014</p>
<p>received&gt;=01/01/2014 AND received&lt;=03/31/2014</p></td>
<td><p>2014년 4월 15일에서 받은 메시지입니다. 두 번째 예제에서는 2014년 1월 1일과 2014년 3월 31일 사이에 수신된 모든 메시지를 반환합니다.</p></td>
</tr>
<tr class="even">
<td><p>Recipients</p></td>
<td><p>전자 메일 메시지의 모든 받는 사람 필드로, 받는 사람, 참조 및 숨은 참조가 여기에 해당됩니다.1</p></td>
<td><p>recipients:garthf@contoso.com</p>
<p>recipients:contoso.com</p></td>
<td><p>Garthf@contoso.com에 보낸 메시지입니다.</p>
<p>두번째 예제에서는 contoso.com 도메인의 모든 받는 사람에 게 보낸 메시지를 반환 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Sent</p></td>
<td><p>보낸 사람이 전자 메일 메시지를 보낸 날짜입니다.</p></td>
<td><p>sent:07/01/2014</p>
<p>sent&gt;=06/01/2014 AND sent&lt;=07/01/2014</p></td>
<td><p>지정된 날짜 또는 지정된 날짜 범위 내에서 전송된 메시지입니다.</p></td>
</tr>
<tr class="even">
<td><p>Size</p></td>
<td><p>항목의 크기(바이트)입니다.</p></td>
<td><p>size&gt;26214400</p>
<p>size:1..1048576</p></td>
<td><p>25MB 보다 큰 사용 되는 메시지입니다.</p>
<p>두번째 예제 1의 크기가 1048576 바이트 (1MB)를 통해 메시지를 반환합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Subject</p></td>
<td><p>전자 메일 메시지 제목 줄의 텍스트입니다.</p></td>
<td><p>subject:&quot;Quarterly Financials&quot;</p>
<p>subject:northwind</p></td>
<td><p>정확 하 게 포함 하는 메시지 제목 줄의 텍스트에 &quot;Quarterly Financials&quot; anywhere 구 합니다.</p>
<p>두번째 예제에서는 word northwind 제목줄에 포함 된 모든 메시지를 반환 합니다.</p></td>
</tr>
<tr class="even">
<td><p>To</p></td>
<td><p>전자 메일 메시지의 받는 사람 필드입니다.1</p></td>
<td><p>to:annb@contoso.com</p>
<p>to:annb</p>
<p>to:&quot;Ann Beebe&quot;</p></td>
<td><p>모든 예제에서 받는 사람: 줄에 Ann Beebe가 지정된 메시지를 반환합니다.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;recipient 속성의 값에 SMTP 주소, 표시 이름 또는 별칭을 사용하여 사용자를 지정할 수 있습니다. 예를 들어 annb@contoso.com, annb 또는 "Ann Beebe"를 사용하여 사용자 Ann Beebe를 지정할 수 있습니다.



## 지원 되는 검색 연산자

**AND**, **OR**, 예: 부울 검색 연산자를 포함 하거나 검색 쿼리에 특정 단어를 제외 하 여 더 정확한 사서함 검색을 정의 하는데 도움이 됩니다. 속성 연산자를 사용 하 여 등의 기타 기술을 (같은 \> = 또는..), 따옴표, 괄호 및 와일드 카드를 사용 하는 데 도움이 eDiscovery 검색 쿼리를 구체화 합니다. 다음 표에서 범위를 좁힐 또는 검색 결과 확장 하는데 사용할 수 있는 연산자를 보여줍니다.


> [!IMPORTANT]
> 검색 쿼리에서 대문자 부울 연산자를 사용 해야 합니다. 예, <STRONG>AND</STRONG>;를 사용 하 여 <STRONG>and</STRONG>를 사용 하지 마십시오. 검색 쿼리에서 소문자 연산자를 사용 하면 오류가 반환 됩니다.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>연산자</th>
<th>사용 현황</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AND</p></td>
<td><p>keyword1 AND keyword2</p></td>
<td><p>지정 된 키워드 또는 <code>property:value</code> 식의 모두 포함 하는 메시지를 반환 합니다.</p></td>
</tr>
<tr class="even">
<td><p>+</p></td>
<td><p>keyword1 + keyword2 + keyword3</p></td>
<td><p>또한 <code>keyword1</code>를 포함 하는 <em><code>keyword2 </code>또는 <code>keyword3</code><em>및</em></em>포함 된 항목을 반환 합니다. 따라서이 예제는 쿼리 <code>(keyword2 OR keyword3) AND keyword1</code>에 해당 합니다.</p>
<p>사항에 유의 쿼리 <code>keyword1 + keyword2</code> ( <strong>+</strong> 후 공백을 사용 하 여 기호) <strong>AND</strong> 연산자를 사용 하 여 동일 하지 않습니다. 이 쿼리 <code>&quot;keyword1 + keyword2&quot;</code> 에 해당 되 고 정확한 단계 <code>&quot;keyword1 + keyword2&quot;</code>사용 하는 항목을 반환 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>OR</p></td>
<td><p>keyword1 OR keyword2</p></td>
<td><p>지정 된 키워드 또는 <code>property:value</code> 식 중 하나 이상을 포함 하는 메시지를 반환 합니다.</p></td>
</tr>
<tr class="even">
<td><p>NOT</p></td>
<td><p>keyword1 NOT keyword2</p>
<p>NOT from:&quot;Ann Beebe&quot;</p></td>
<td><p>키워드 또는 <code>property:value</code> 식으로 지정 된 메시지를 제외 합니다. 예, <code>NOT from:&quot;Ann Beebe&quot;</code> Ann Beebe가 보낸 메시지를 제외 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>-</p></td>
<td><p>keyword1 -keyword2</p></td>
<td><p>동일 <strong>NOT</strong> 연산자입니다. 이 쿼리는 <code>keyword1</code> 를 포함 하는 항목을 반환 하 고 <code>keyword2</code>를 포함 하는 항목을 제외 합니다.</p></td>
</tr>
<tr class="even">
<td><p>NEAR</p></td>
<td><p>keyword1 NEAR(n) keyword2</p></td>
<td><p>여기서 n은 구분 단어의 개수를 서로 가까이 있는 단어와 메시지를 반환 합니다. 예, <code>best NEAR(5) worst</code> 는 다섯 개의 단어 &quot;최고&quot;의 내에 단어 &quot;최하위 값&quot;이 있는 메시지 반환 합니다. 없는 번호를 지정 하는 경우 기본 간격은 8 개의 단어입니다.</p></td>
</tr>
<tr class="odd">
<td><p>:</p></td>
<td><p>property:value</p></td>
<td><p><code>property:value</code> 구문에 콜론 (:)에 대 한 검색 되는 속성 값에 지정 된 값과 같으면 있는지를 지정 합니다. 예, <code>recipients:garthf@contoso.com</code> garthf@contoso.com가 보낸 모든 메시지를 반환 합니다.</p></td>
</tr>
<tr class="even">
<td><p>&lt;</p></td>
<td><p>property&lt;value</p></td>
<td><p>검색 중인 속성이 지정된 값보다 작음을 나타냅니다. 1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;</p></td>
<td><p>property&gt;value</p></td>
<td><p>검색 중인 속성이 지정된 값보다 큼을 나타냅니다.1</p></td>
</tr>
<tr class="even">
<td><p>&lt;=</p></td>
<td><p>property&lt;=value</p></td>
<td><p>검색 중인 속성이 특정 값보다 작거나 같음을 나타냅니다.1</p></td>
</tr>
<tr class="odd">
<td><p>&gt;=</p></td>
<td><p>property&gt;=value</p></td>
<td><p>검색 중인 속성을 특정 값보다 크거나 같음을 나타냅니다.1</p></td>
</tr>
<tr class="even">
<td><p>..</p></td>
<td><p>property:value1..value2</p></td>
<td><p>검색 중인 속성을 value1보다 크거나 같고 value2보다 작거나 같음을 나타냅니다.1</p></td>
</tr>
<tr class="odd">
<td><p>&quot; &quot;</p></td>
<td><p>&quot;fair value&quot;</p>
<p>subject:&quot;Quarterly Financials&quot;</p></td>
<td><p>큰따옴표(&quot; &quot;)를 사용하여 키워드 및 <code>property:value</code> 검색 쿼리에서 정확한 구나 용어를 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>*</p></td>
<td><p>cat*</p>
<p>subject:set*</p></td>
<td><p>키워드 또는 <code>property:value</code> 쿼리 0 개 이상의 문자에 대 한 접두사 와일드 카드 검색 (별표 배치 되는 위치는 단어의 끝에)과 일치 합니다. 예, <code>subject:set*</code> 제목줄에 word 집합, 설정 및 설정 (및 &quot;설정&quot;로 시작 하는 다른 단어)을 포함 하는 메시지를 반환 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>( )</p></td>
<td><p>(공정한 또는 있음) 및 from:contoso.com</p>
<p>(IPO OR initial) AND (stock OR shares)</p>
<p>(quarterly financials)</p></td>
<td><p>괄호를 사용하여 부울 구, <code>property:value</code> 항목 및 키워드를 그룹화합니다. 예를 들어 <code>(quarterly financials)</code>는 단어 quarterly 및 financials가 들어 있는 항목을 반환합니다.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1&nbsp;&nbsp;&nbsp;날짜 또는 숫자 값이 있는 속성에는 이 연산자를 사용합니다.



## 검색 쿼리에서 지원 되지않는 문자

검색 쿼리를 지원 하지 않는 문자는 일반적으로 검색 오류가 발생 하거나 원하지 않는 결과 반환 합니다. 문자는 종종 숨겨지고 다른 응용 프로그램 (예: Microsoft Word 또는 Microsoft Excel)에서 쿼리 또는 쿼리의 일부를 복사 하 고 원본 위치 eDiscovery 검색의 쿼리 페이지에 있는 키워드 상자에 복사 하는 경우 쿼리를 추가 일반적으로 지원 되지 않습니다.

원본 위치 eDiscovery 검색 쿼리에 대 한 지원 되지않는 문자 목록은 다음과 같습니다.

  - **스마트 인용 부호**   스마트 단일와 큰따옴표 ( *둥근 따옴표*라고도 함)이 지원 되지 않습니다. 검색 쿼리에서 곧은 따옴표를 사용할 수 있습니다.

  - **인쇄할 수 없는 및 제어 문자**   인쇄할 수 없는 및 제어 문자 영숫자 문자 등의 서 면된 기호를 표시 하지 않습니다. 인쇄할 수 없는의 예 및 제어 문자 텍스트 또는 여러 줄 텍스트의 서식을 지정 하는 문자를 포함 합니다.

  - **오른쪽으로 왼쪽 및 오른쪽에서 왼쪽으로 표시**   이것은 문자를 텍스트 방향을 왼쪽에서 오른쪽으로 쓰는 언어 (예: 영어와 스페인어) 및 오른쪽에서 왼쪽으로 쓰는 언어 (예: 아랍어 및 히브리어)를 나타내는 데 사용 되는 컨트롤입니다.

  - **소문자 부울 연산자**   같이 이전 설명, 대문자의 부울 연산자, **AND** 및 **또는**, 예: 검색 쿼리를 사용 해야 합니다. 메모를 나타내는 쿼리 구문 자주 소문자 연산자를 사용할 수 있는 경우에 부울 연산자가 사용 중인 예: `(WordA or WordB) and (WordC or WordD)`합니다.

**검색 쿼리를 지원 하지 않는 문자를 방지 하는 방법?** 지원 되지않는 문자를 방지 하기 위해 쿼리 키워드 상자에 입력 하는 가장 좋은 방법은 합니다. 또는 Word 또는 Excel에서 쿼리를 복사할 수 있으며 Microsoft 메모장 등의 일반 텍스트 편집기에서 파일에 붙여넣습니다. 그런 다음 텍스트 파일을 저장 하 고 **ANSI인코딩** 드롭다운 목록에서 선택 합니다. 모든 서식 및 지원 되지않는 문자를 사용 하 여 제거 됩니다. 다음 복사 하 고 키워드 쿼리 상자에 텍스트 파일에서 쿼리를 붙여넣을 수 있습니다.

## 검색 팁과 트릭

  - 키워드 검색은 대/소문자를 구분하지 않습니다. 예를 들어 **cat** 및 **CAT**은 같은 결과를 반환합니다.

  - 두 키워드 또는 두 `property:value` 식 사이 공백을 **AND**를 사용 하는 것 같습니다. 예, `from:"Sara Davis" subject:reorganization` word **재구성** 제목줄에 포함 된 Sara Davis 하 여 보낸 모든 메시지를 반환 합니다.

  - `property:value` 형식과 일치 하는 구문을 사용 합니다. 값은 대/소문자를 구분 하지 하 고 연산자 뒤 공간을 가질 수 없습니다. 공백이 있으면 사용자가 의도 한 값은 방금 전체 텍스트 검색 됩니다. 예 **를: pilarp** 키워드와 "pilarp"에 대 한 아니라 pilarp 전송 된 메시지를 검색 합니다.

  - 받는 사람 속성(예: To, From, Cc 또는 Recipients)을 검색하는 경우 SMTP 주소, 별칭 또는 표시 이름을 사용하여 받는 사람을 나타낼 수 있습니다. 예를 들어, pilarp@contoso.com, pilarp, 또는 "Pilar Pinilla"를 사용할 수 있습니다.

  - 만 접두사 와일드 카드 검색을 사용 하 여 수-예 **고양이 \*** 또는 **집합 \***. 와일드 카드 검색을 접미사 (\* 고양이) 와일드 카드 검색을 하위 문자열 또는 (\* 고양이 \*) 지원 되지 않습니다.

  - 속성을 검색할 때 사용 큰따옴표 ("") 여러 단어 검색 값으로 구성 된 경우. **제목: 예산 Q1예산** 에 포함 된 메시지를 반환 하는 예는 제목줄 하 고 있는 포함 **Q1** 외부 메시지에 또는 메시지 속성 중 하나에서 합니다. 사용 하 여 **제목: "Q1 예산"예산 Q1** 제목줄에 포함 된 모든 메시지를 반환 합니다.

