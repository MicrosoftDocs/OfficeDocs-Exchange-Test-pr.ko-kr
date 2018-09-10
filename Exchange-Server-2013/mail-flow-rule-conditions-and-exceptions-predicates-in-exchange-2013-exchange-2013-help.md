---
title: '전송 규칙 조건 (조건자): Exchange 2013 Help'
TOCTitle: 메일 흐름 규칙 조건 및 예외 (조건자)
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 50484139
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 규칙 조건 (조건자)

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-12-20_

조건 및 예외 메일 흐름 규칙 (전송 규칙이 라고도 함)에 규칙이 적용 되거나에 적용 되지 메시지를 식별 합니다. 예는 고 지 사항을 메시지에 추가 하는 규칙을 하는 경우 특정 단어, 특정 사용자가 보낸 메시지를 포함 하는 메시지 또는 특정 그룹의 구성원으로 보낸 항목을 제외한 모든 메시지에만 적용 하는 규칙을 구성할 수 있습니다. 전체적으로, 조건 및 메일 흐름 규칙에서 예외는로 알려져 *조건자*없으므로 모든 조건에 대 한 정확한 동일한 설정 및 구문을 사용 하는 경우 해당 예외입니다. 유일한 차이점은 조건 예외를 제외 하는 메시지를 지정 하는 동안 포함할 메시지를 지정 합니다.

대부분의 조건 및 예외는 하나 이상의 값을 필요로 하는 하나의 속성이 있습니다. 예, **보낸 사람이 다음과 같음** 조건에 메시지를 보낸 사람이 필요 합니다. 일부 조건은 두 속성이 있습니다. 예 **A 메시지 헤더 단어가 포함 된 다음이 단어의** 조건에 메시지 헤더 필드를 지정 하는 하나의 속성 및 헤더 필드에서 찾을 텍스트를 지정 하는 두번째 속성이 필요 합니다. 일부 조건 또는 예외 항목에는 모든 속성이 없습니다. 예, **첨부 파일에 실행 가능한 콘텐츠가 있음** 조건은 단순히 실행 가능한 콘텐츠가 포함 된 메시지의 첨부 파일에 대 한 찾습니다.

Exchange Server 2013 에서 메일 흐름 규칙에 대 한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

조건 및 Exchange Online Protection 또는 Exchange Online 의 메일 흐름 규칙에서 예외에 대 한 자세한 내용은 [Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)](https://technet.microsoft.com/ko-kr/library/jj919235\(v=exchg.150\)) 또는 [메일 흐름 규칙 조건 및 예외 (조건자) Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj919234\(v=exchg.150\))를 참조 하십시오.

## 조건 및 사서함 서버에서 메일 흐름 규칙에 대 한 예외

다음 섹션에 있는 표에서 조건 및 사서함 서버에서 메일 흐름 규칙에서 사용할 수 있는 예외에 설명 합니다. 속성 형식 속성 유형 섹션에 설명 되어있습니다.

보낸사람

받는 사람

메시지 제목이 나 본문

첨부 파일

모든 받는 사람

에 중요 한 정보 유형, 메시지 받는 사람과 참조 값, 크기 및 문자 집합

보낸사람 및 받는 사람

메시지 속성

메시지 헤더

**참고**:

  - 궁극적으로 **하는 경우이 규칙을 적용** 하거나 **하는 경우를 제외 하 고** 필드에 표시 되는 값은 서로 다른 자주 Exchange 관리 센터 (EAC) 조건 또는 예외를 선택한 후 선택한 클릭 경로 값 보다 (짧은). 또한 서식 파일 (시나리오의 필터링 된 목록)을 기반으로 새 규칙을 만들 때에 종종 전체 클릭 경로 수행 하는 대신 짧은 조건 이름을 선택할 수 있습니다. 짧은 이름 및 전체 값은 테이블에서 EAC 열에 표시 되는 경로 클릭 합니다.

  - EAC에서 **\[모든 메시지에 적용\]을** 선택 하는 경우에 다른 조건을 지정할 수 없습니다. Exchange 관리 셸 에 해당 하는 조건 매개 변수를 지정 하지 않고 규칙을 만드는 것입니다.

  - 설정 및 속성 않으므로 조건 및 예외에 동일 **Get-TransportRulePredicate** cmdlet의 출력을 예외를 개별적으로 나열 되지 않습니다. 또한이 cmdlet에 의해 반환 되는 조건자 중 일부의 이름을 해당 하는 매개 변수 이름이 보다 다른 되며 조건자 여러 매개 변수 해야할 수 있습니다.

## 보낸사람

조건 및 보낸 사람의 주소를 검사 하는 예외에 대 한 규칙은 보낸 사람의 주소를 찾는 위치를 지정할 수 있습니다.

**이 규칙의 속성** 섹션에서 EAC에서 **메시지에서 일치 하는 보낸사람 주소** 를 클릭 합니다. Note이 설정을 확인 하려면 **기타 옵션** 클릭 해야할 수 있습니다. Exchange 관리 셸, 매개 변수는 *SenderAddressLocation*됩니다. 사용 가능한 값입니다.

  - **머리글**    메시지 헤더 (예: **From**, **Sender**또는 **Reply-To** 필드)의 보낸 사람이만 검사 합니다. 이 값은 기본값 및 누적 업데이트 1 (CU1) Exchange 2013 하기 전에 메일 흐름 규칙 작동 하는 방법입니다.

  - **봉투**    메시지 봉투 (일반적으로 **Return-Path** 필드에 저장 되는 SMTP 전송에 사용 되는 **MAIL FROM** 값)에서 보낸사람을만 검사 합니다. 메시지 봉투 검색 다음과 같은 조건 (및 해당 예외)에 대해 사용할 수 있는 인지 note:
    
      - **보낸 사람이 다음과 같음** (*From*)
    
      - **보낸 사람이의 구성원** (*FromMemberOf*)
    
      - **보낸사람 주소에 다음 포함** (*FromAddressContainsWords*)
    
      - **보낸사람 주소가 다음과 일치** (*FromAddressMatchesPatterns*)
    
      - **보낸 사람의 도메인은** (*SenderDomainIs*)

  - **헤더 또는 봉투** (`HeaderOrEnvelope`)   메시지 헤더와 메시지 봉투의 보낸 사람이 검사 합니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>보낸 사람이 다음과 같음</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>이 사용자는</strong></p></td>
<td><p><em>From</em></p>
<p><em>ExceptIfFrom</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정 된 사서함, 메일 사용자 또는 Exchange 조직에서 메일 연락처를 통해 전송 되는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람 위치</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>외부/내부 인</strong></p></td>
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>내부 보낸사람 또는 외부 보낸 사람이 보낸 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>보낸 사람이 다음의 구성원임</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>이 그룹의 구성원</strong></p></td>
<td><p><em>FromMemberOf</em></p>
<p><em>ExceptIfFromMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정된 된 그룹의 구성원에 의해 전송 되는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람 주소에 다음 포함</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>주소에 다음 단어이 포함</strong></p></td>
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>보낸 사람의 전자 메일 주소에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>보낸 사람 주소가 다음과 일치</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>이러한 텍스트 패턴을 일치 하는 주소</strong></p></td>
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지를 보낸 사람의 전자 메일 주소 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람의 지정된 속성에 다음 단어 포함</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>에 다음 단어를 포함 하 여 특정 속성이</strong></p></td>
<td><p><em>SenderADAttributeContainsWords</em></p>
<p><em>ExceptIfSenderADAttributeContainsWords</em></p></td>
<td><p>첫번째 속성: <code>ADAttribute</code></p>
<p>두번째 속성: <code>Words</code></p></td>
<td><p>보낸 사람의 지정 된 Active Directory 특성 포함 된 메시지에 지정 된 단어 중 하나입니다.</p>
<p><strong>Country</strong> 특성 (예: 독일 DE)의 두 문자로 된 국가 코드 값 필요 하다는 메모 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>보낸 사람의 지정된 속성이 다음 텍스트 패턴과 일치</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>에 다음 텍스트 패턴과 일치 하는 특정 속성이</strong></p></td>
<td><p><em>SenderADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfSenderADAttributeMatchesPatterns</em></p></td>
<td><p>첫번째 속성: <code>ADAttribute</code></p>
<p>두번째 속성: <code>Patterns</code></p></td>
<td><p>메시지를 보낸 사람의 지정 된 Active Directory 특성 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람이 정책 팁을 재정의함</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>사람이 정책 팁을 재정의</strong></p></td>
<td><p><em>HasSenderOverride</em></p>
<p><em>ExceptIfHasSenderOverride</em></p></td>
<td><p>해당 없음</p></td>
<td><p>보낸 사람이 데이터 손실 방지 (DLP) 정책 무시 하도록 선택한 메시지입니다. DLP 정책에 대 한 자세한 내용은 <a href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention">데이터 손실 방지</a>을 참조 하십시오.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>보낸 사람 IP 주소가 범위에 있음</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>IP 주소에 이러한 범위 중 하나 또는 정확 하 게 일치</strong></p></td>
<td><p><em>SenderIPRanges</em></p>
<p><em>ExceptIfSenderIPRanges</em></p></td>
<td><p><code>IPAddressRanges</code></p></td>
<td><p>보낸 사람의 IP 주소가 지정 된 IP 주소와 일치 하거나 지정한 IP 주소 범위에 들어가는 메시지입니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람의 도메인이 다음과 같음</strong></p>
<p><strong>보낸 사람이</strong> &gt; <strong>도메인은</strong></p></td>
<td><p><em>SenderDomainIs</em></p>
<p><em>ExceptIfSenderDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>보낸 사람의 전자 메일 주소의 도메인 지정된 된 값을 일치 하는 메시지입니다.</p>
<p>보낸 사람이 도메인 해당 <em>포함</em> 지정 된 도메인 (예는 도메인의 모든 하위), (<em>FromAddressMatchesPatterns</em>) <strong>보낸사람 주소가 다음과 일치</strong> 조건을 사용 하 여 찾아 구문을 사용 하 여 도메인을 지정 해야 하는 경우: <code>'@domain\.com$'</code>합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 받는 사람


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>받는 사람이 다음과 같음</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>이 사용자는</strong></p></td>
<td><p><em>SentTo</em></p>
<p><em>ExceptIfSentTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정 된 사서함, 메일 사용자 또는 메일은 받는 사람 중 한 메시지 Exchange 조직에 문의 합니다. 메시지의 <strong>To</strong>, <strong>Cc</strong>또는 <strong>Bcc</strong> 필드에는 받는 사람에 게 될 수 있습니다.</p>
<p><strong>참고:</strong> 메일 그룹 또는 메일 사용이 가능한 보안 그룹을 지정할 수 없습니다. 그룹에 보낸 메시지에 작업을 수행 해야 하는 경우 (<em>AnyOfToHeader</em>) <strong>상자에 포함</strong> 조건을 대신 사용 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람 위치</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>외부/외부</strong></p></td>
<td><p><em>SentToScope</em></p>
<p><em>ExceptIfSentToScope</em></p></td>
<td><p><code>UserScopeTo</code></p></td>
<td><p>내부 받는 사람, 외부 받는 사람, 파트너 조직에서 외부 받는 사람 또는 비 파트너 조직에서 외부 받는 사람에 게 전송 되는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>받는 사람이 다음의 구성원임</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>이 그룹의 구성원</strong></p></td>
<td><p><em>SentToMemberOf</em></p>
<p><em>ExceptIfSentToMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정된 된 그룹의 구성원 인 받는 사람을 포함 하는 메시지입니다. 메시지의 <strong>To</strong>, <strong>Cc</strong>또는 <strong>Bcc</strong> 필드에는 그룹 될 수 있습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람 주소에 다음 포함</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>주소에 다음 단어이 포함</strong></p></td>
<td><p><em>RecipientAddressContainsWords</em></p>
<p><em>ExceptIfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>받는 사람의 전자 메일 주소에 지정 된 단어가 있는 메시지입니다.</p>
<p><strong>참고:</strong> 이 조건은 받는 사람 프록시 주소로 보낸 메시지는 고려하지 않습니다. 받는 사람의 기본 전자 메일 주소로 보낸 메시지만 일치시킵니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>받는 사람 주소가 다음과 일치</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>이러한 텍스트 패턴을 일치 하는 주소</strong></p></td>
<td><p><em>RecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지를 받는 사람의 전자 메일 주소 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p>
<p><strong>참고:</strong> 이 조건은 받는 사람 프록시 주소로 보낸 메시지는 고려하지 않습니다. 받는 사람의 기본 전자 메일 주소로 보낸 메시지만 일치시킵니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람의 지정된 속성에 다음 단어 포함</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>에 다음 단어를 포함 하 여 특정 속성이</strong></p></td>
<td><p><em>RecipientADAttributeContainsWords</em></p>
<p><em>ExceptIfRecipientADAttributeContainsWords</em></p></td>
<td><p>첫번째 속성: <code>ADAttribute</code></p>
<p>두번째 속성: <code>Words</code></p></td>
<td><p>받는 사람의 지정 된 Active Directory 특성이 포함 된 메시지에 지정 된 단어 중 하나입니다.</p>
<p><strong>Country</strong> 특성 (예: 독일 DE)의 두 문자로 된 국가 코드 값 필요 하다는 메모 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>받는 사람의 지정된 속성이 다음 텍스트 패턴과 일치</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>에 다음 텍스트 패턴과 일치 하는 특정 속성이</strong></p></td>
<td><p><em>RecipientADAttributeMatchesPatterns</em></p>
<p><em>ExceptIfRecipientADAttributeMatchesPatterns</em></p></td>
<td><p>첫번째 속성: <code>ADAttribute</code></p>
<p>두번째 속성: <code>Patterns</code></p></td>
<td><p>메시지를 받는 사람의 지정 된 Active Directory 특성이 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람의 도메인이 다음과 같음</strong></p>
<p><strong>받는 사람</strong> &gt; <strong>도메인은</strong></p></td>
<td><p><em>RecipientDomainIs</em></p>
<p><em>ExceptIfRecipientDomainIs</em></p></td>
<td><p><code>DomainName</code></p></td>
<td><p>받는 사람의 전자 메일 주소의 도메인 지정된 된 값을 일치 하는 메시지입니다.</p>
<p>해당 <em>포함</em> 지정 된 도메인 (예는 도메인의 모든 하위) 도메인을 받는 사람을 찾으려면 해야하는 경우 (<em>RecipientAddressMatchesPatterns</em>) <strong>받는 사람 주소가 다음과 일치</strong> 조건을 사용 하 고 <code>'@domain\.com$'</code>구문을 사용 하 여 도메인을 지정 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 메시지 제목이 나 본문


> [!NOTE]
> ASCII 텍스트의 SMTP 서버 간에 바이너리 메시지를 전송하는 데 사용되는 MIME 콘텐츠 전송 인코딩 메서드에서 메시지가 디코딩된 <EM>후</EM> 메시지의 제목이나 다른 머리글 필드에 있는 단어 또는 텍스트 패턴이 검색됩니다. 조건이나 예외를 사용하여 메시지의 제목이나 다른 머리글 필드에 있는 원시(일반적으로, Base64) 인코딩된 값을 검색할 수 없습니다.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>제목 또는 본문에 다음 포함</strong></p>
<p><strong>제목이 나 본문</strong> &gt; <strong>제목이 나 본문에 다음 단어 포함</strong></p></td>
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> 필드 또는 메시지 본문에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>제목 또는 본문이 다음과 일치</strong></p>
<p><strong>제목이 나 본문</strong> &gt; <strong>제목이 나 본문에 다음 텍스트 패턴과 일치</strong></p></td>
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>여기서 <strong>Subject</strong> 필드 또는 메시지 본문 포함 텍스트 패턴을 하는 메시지에 지정된 된 정규식과 일치 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>제목에 다음 포함</strong></p>
<p><strong>제목이 나 본문</strong> &gt; <strong>제목 다음 단어를 포함 합니다.</strong></p></td>
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> 필드에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>제목이 다음과 일치</strong></p>
<p><strong>제목이 나 본문</strong> &gt; <strong>다음 텍스트 패턴과 일치 하는 주체</strong></p></td>
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지 <strong>Subject</strong> 필드는 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 첨부 파일

메일 흐름 규칙 메시지 첨부 파일을 검사 하는 방법에 대 한 자세한 내용은 [전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)을 참조 하십시오.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>첨부 파일 내용에 다음 포함</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>콘텐츠 다음 단어를 포함 합니다.</strong></p></td>
<td><p><em>AttachmentContainsWords</em></p>
<p><em>ExceptIfAttachmentContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>메시지 첨부 파일에 지정 된 단어를 포함 하는 위치입니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>모든 첨부 파일 내용이 다음과 일치 함</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>다음 텍스트 패턴과 일치 하는 콘텐츠</strong></p></td>
<td><p><em>AttachmentMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지 첨부 파일이 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p>
<p><strong>참고</strong>:만 첫번째 150 (kb)의 첨부 파일을 검색 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>모든 첨부 파일의 내용을 검사할 수 없습니다.</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>콘텐츠는 검사할 수 없습니다.</strong></p></td>
<td><p><em>AttachmentIsUnsupported</em></p>
<p><em>ExceptIfAttachmentIsUnsupported</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지 첨부 파일 Exchange 하 여 기본적으로 인식 되지 않으면 장소와 필요한 IFilter는 사서함 서버에 설치 되지 않습니다. 자세한 내용은 <a href="register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md">Exchange 2013으로 Filter Pack IFilter 등록</a>을 참조 하십시오.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>첨부 파일의 파일 이름이 다음과 일치함</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>다음 텍스트 패턴과 일치 하는 파일 이름</strong></p></td>
<td><p><em>AttachmentNameMatchesPatterns</em></p>
<p><em>ExceptIfAttachmentNameMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지 첨부 파일의 파일 이름 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>첨부 파일의 파일 확장명이 다음과 일치함</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>다음이 단어를 포함 하는 파일 확장명</strong></p></td>
<td><p><em>AttachmentExtensionMatchesWords</em></p>
<p><em>ExceptIfAttachmentExtensionMatchesWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>지정 된 단어 중 하나라도 첨부 파일의 파일 확장명 일치 하는 메시지입니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>첨부 파일이 보다 크거나 같음</strong></p>
<p><strong>첨부 파일 &gt; 크기는 보다 크거나 같음</strong></p></td>
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>메시지 첨부 파일에 지정 된 값 보다 크거나입니다.</p>
<p>EAC에서 크기 (kb)만 지정할 수 있습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지가 검사를 완료하지 않음</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>검사를 완료 하지</strong></p></td>
<td><p><em>AttachmentProcessingLimitExceeded</em></p>
<p><em>ExceptIfAttachmentProcessingLimitExceeded</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지를 첨부 파일의 검사 규칙 엔진을 완료 하지 못했습니다. 이 조건은 협력을 식별 하 고 콘텐츠 수 없으며 완벽 하 게 검색 한 메시지를 처리 하는 규칙을 만들 사용할 수 있습니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>첨부 파일에 실행 가능한 콘텐츠가 있음</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>에 실행 가능한 콘텐츠가 있음</strong></p></td>
<td><p><em>AttachmentHasExecutableContent</em></p>
<p><em>ExceptIfAttachmentHasExecutableContent</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지 첨부 파일은 실행 파일입니다. 파일의 속성을 검사 하는 시스템 파일의 확장명에 의존 하는 대신 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>첨부 파일이 암호로 보호됨</strong></p>
<p><strong>첨부 파일</strong> &gt; <strong>파일이 암호로 보호 되어</strong></p></td>
<td><p><em>AttachmentIsPasswordProtected</em></p>
<p><em>ExceptIfAttachmentIsPasswordProtected</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지 위치는 첨부 파일이 암호로 보호 된 (하 고 검사할 수 없는). Office 문서 및.zip 파일에 대 한 암호 검색 에서만 작동합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 모든 받는 사람

조건 및 예외가이 섹션의 메시지에 지정 된 받는 사람 중 하나 이상이 포함 하는 경우 *모든* 받는 사람에 게 영향을 주는 고유한 기능을 제공 합니다. 예, 메시지를 거부 하는 규칙이 있는 가정해 보겠습니다. 받는 사람에 게 섹션에서 받는 사람 조건을 사용 하는 경우 지정된 된 받는 사람에 대 한 메시지 거부만 됩니다. 예, 규칙 메시지를 하지만 메시지에 지정 된 받는 사람을 찾아 5 명의 다른 받는 사람에 게를 들어 있습니다. 메시지는 한 명의 받는 사람에 대 한 거부 되 고 5 명의 다른 받는 사람에 게 배달 됩니다.

이 섹션에서 받는 사람 조건을 추가 하는 경우 검색 된 받는 사람 및 5 명의 다른 받는 사람에 대 한 해당 동일한 메시지가 거부 됩니다.

반면, 받는 사람 예외를이 섹션 *수 없도록* 감지 된 받는 사람에 게 아니라는 메시지의 받는 사람 *모두* 에 적용 되지 않도록 규칙 동작에서 합니다.

**참고:**  이 조건은 받는 사람 프록시 주소로 보낸 메시지는 고려하지 않습니다. 받는 사람의 기본 전자 메일 주소로 보낸 메시지만 일치시킵니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>모든 받는 사람 주소에 다음 포함</strong></p>
<p><strong>모든 받는 사람</strong> &gt; <strong>주소에 다음 단어이 포함</strong></p></td>
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>메시지의 <strong>To</strong>, <strong>Cc</strong>또는 <strong>Bcc</strong> 필드에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>모든 받는 사람 주소가 다음과 일치</strong></p>
<p><strong>모든 받는 사람</strong> &gt; <strong>이러한 텍스트 패턴을 일치 하는 주소</strong></p></td>
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지 <strong>To</strong>, <strong>Cc</strong>또는 <strong>Bcc</strong> 필드는 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 에 중요 한 정보 유형, 메시지 받는 사람과 참조 값, 크기 및 문자 집합

이 조건 섹션에서 모든 받는 사람에 게 섹션에 있는 조건에 다음과 같이 작동 하는 **To** 및 **Cc** 필드의 값에 대 한 해당 모양 (메시지의 받는 사람*모두* 에 미치는 영향 뿐아니라 검색 된 규칙 받는 사람)입니다.

**참고:**  이 조건은 받는 사람 프록시 주소로 보낸 메시지는 고려하지 않습니다. 받는 사람의 기본 전자 메일 주소로 보낸 메시지만 일치시킵니다.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>메시지에 중요한 정보가 포함됨</strong></p>
<p><strong>메시지</strong> &gt; <strong>이러한 유형의 중요 한 정보를 포함 합니다.</strong></p></td>
<td><p><em>MessageContainsDataClassifications</em></p>
<p><em>ExceptIfMessageContainsDataClassifications</em></p></td>
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>데이터 손실 방지 (DLP) 정책에 의해 정의 된 중요 한 정보를 포함 하는 메시지입니다.</p>
<p>이 조건은 <strong>정책 설명과 함께 보낸사람에 게 알림</strong> (<em>NotifySender</em>) 매크로 함수를 사용 하는 규칙에 대 한 필수입니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람란에 다음 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>상자에이 사용자를 포함 합니다.</strong></p></td>
<td><p><em>AnyOfToHeader</em></p>
<p><em>ExceptIfAnyOfToHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지를 지정한 받는 사람 중 <strong>To</strong> 필드 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>받는 사람란에 다음의 구성원 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>상자에이 그룹의 구성원 포함</strong></p></td>
<td><p><em>AnyOfToHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정된 된 그룹의 구성원 인 받는 사람이 포함 된 <strong>To</strong> 필드는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>참조란에 다음 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>참조란이이 사용자를 포함 합니다.</strong></p></td>
<td><p><em>AnyOfCcHeader</em></p>
<p><em>ExceptIfAnyOfCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지를 지정한 받는 사람 중 <strong>Cc</strong> 필드 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>참조란에 다음의 구성원 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>이 그룹의 구성원 포함</strong></p></td>
<td><p><em>AnyOfCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정된 된 그룹의 구성원 인 받는 사람이 포함 된 <strong>Cc</strong> 필드는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람란 또는 참조란에 다음 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>에이 사용자를 포함 하는 참조 상자 또는</strong></p></td>
<td><p><em>AnyOfToCcHeader</em></p>
<p><em>ExceptIfAnyOfToCcHeader</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지를 지정한 받는 사람 중 하나는 <strong>To</strong> 또는 <strong>Cc</strong> 필드 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>받는 사람란 또는 참조란에 다음의 구성원 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>를이 그룹의 구성원을 포함 하는 참조 상자 또는</strong></p></td>
<td><p><em>AnyOfToCcHeaderMemberOf</em></p>
<p><em>ExceptIfAnyOfToCcHeaderMemberOf</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지 <strong>To</strong> 또는 <strong>Cc</strong> 필드에서 지정된 된 그룹의 구성원 인 받는 사람을 포함 하는 위치입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지 크기가 다음 크기보다 크거나 같음</strong></p>
<p><strong>메시지</strong> &gt; <strong>크기는 보다 크거나 같음</strong></p></td>
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>메시지를 지정된 된 값 보다 크거나 (메시지 및 첨부 파일)의 총 크기입니다.</p>
<p>EAC에서 크기 (kb)만 지정할 수 있습니다.</p>
<p><strong>참고:</strong> 메시지 크기 제한이 사서함에서 메일 흐름 규칙 보다 먼저 평가 됩니다. 이러한 조건 가진 규칙은 메시지에 영향을 줄 수 전에 너무 큰 사서함에 대 한 메시지를 거부 됩니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지 문자 집합 이름에 다음 단어 포함</strong></p>
<p><strong>메시지</strong> &gt; <strong>문자 집합 이름에 다음 단어이 포함</strong></p></td>
<td><p><em>ContentCharacterSetContainsWords</em></p>
<p><em>ExceptIfContentCharacterSetContainsWords</em></p></td>
<td><p><code>CharacterSets</code></p></td>
<td><p>지정된 된 문자 중 하나를 포함 하는 메시지 이름을 설정 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 보낸사람 및 받는 사람


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>보낸 사람이 받는 사람의 중 하나</strong></p>
<p><strong>보낸사람 및 받는 사람</strong> &gt; <strong>받는 사람에 게 보낸 사람의 관계는</strong></p></td>
<td><p><em>SenderManagementRelationship</em></p>
<p><em>ExceptIfSenderManagementRelationship</em></p></td>
<td><p><code>ManagementRelationship</code></p></td>
<td><p>두 보낸 사람이 받는 사람의 관리자 하거나 보낸 사람이 받는 사람으로 관리 되는 메시지입니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지가 다음 그룹의 구성원 사이에 있음</strong></p>
<p><strong>보낸사람 및 받는 사람</strong> &gt; <strong>메시지는 이러한 그룹의 구성원 사이</strong></p></td>
<td><p><em>BetweenMemberOf1</em> 및 <em>BetweenMemberOf2</em></p>
<p><em>ExceptIfBetweenMemberOf1</em> 및 <em>ExceptIfBetweenMemberOf2</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정 된 그룹의 구성원 간에 전송 되는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>보낸 사람 또는 받는 사람의 관리자</strong></p>
<p><strong>보낸사람 및 받는 사람</strong> &gt; <strong>보낸사람 또는 받는 사람의 관리자는이 사람</strong></p></td>
<td><p><em>ManagerForEvaluatedUser</em> 및 <em>ManagerAddress</em></p>
<p><em>ExceptIfManagerForEvaluatedUser</em> 및 <em>ExceptIfManagerAddress</em></p></td>
<td><p>첫번째 속성: <code>EvaluatedUser</code></p>
<p>두번째 속성: <code>Addresses</code></p></td>
<td><p>여기서 지정 된 사용자는는 보낸 사람의 관리자 또는 지정 된 사용자는 받는 사람의 관리자 메시지입니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>다음과 비교되는 보낸 사람 및 받는 사람 속성</strong></p>
<p><strong>보낸사람 및 받는 사람</strong> &gt; <strong>으로 비교 하는 보낸사람 및 받는 사람 속성</strong></p></td>
<td><p><em>ADAttributeComparisonAttribute</em> 및 <em>ADComparisonOperator</em></p>
<p><em>ExceptIfADAttributeComparisonAttribute</em> 및 <em>ExceptIfADComparisonOperator</em></p></td>
<td><p>첫번째 속성: <code>ADAttribute</code></p>
<p>두번째 속성: <code>Evaluation</code></p></td>
<td><p>여기서 보낸사람 및 받는 사람에 대 한 지정한 Active Directory 특성 일치 하거나 일치 하지 않는 메시지입니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 메시지 속성


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>메시지 유형</strong></p>
<p><strong>메시지 속성</strong> &gt; <strong>메시지 유형이 포함</strong></p></td>
<td><p><em>MessageTypeMatches</em></p>
<p><em>ExceptIfMessageTypeMatches</em></p></td>
<td><p><code>MessageType</code></p></td>
<td><p>지정 된 형식의 메시지입니다.</p>

> [!NOTE]
> Outlook 또는 Outlook Web App 메시지를 전달 하도록 구성 되 면 <STRONG>ForwardingSmtpAddress</STRONG> 속성은 메시지에 추가 됩니다. 메시지 유형 <CODE>AutoForward</CODE>로 변경 되지 않습니다.


</td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지가 다음으로 분류됨</strong></p>
<p><strong>메시지 속성</strong> &gt; <strong>이 분류를 포함 합니다.</strong></p></td>
<td><p><em>HasClassification</em></p>
<p><em>ExceptIfHasClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>지정 된 메시지 분류가 있는 메시지입니다. <strong>New-MessageClassification</strong> cmdlet을 사용 하 여 조직에서 만들 수 있는 사용자 지정 메시지 분류입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지가 분류로 표시되지 않음</strong></p>
<p><strong>메시지 속성</strong> &gt; <strong>모든 분류를 포함 하지 않음</strong></p></td>
<td><p><em>HasNoClassification</em></p>
<p><em>ExceptIfHasNoClassification</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지 분류가 없는 메시지입니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지에 다음보다 크거나 같은 SCL이 포함되어 있음</strong></p>
<p><strong>메시지 속성</strong> &gt; <strong>보다 크거나 같은 SCL 포함</strong></p></td>
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>신뢰도 scl (스팸)를 지정된 된 값 보다 크거나 할당 되는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지 중요도가 다음으로 표시되어 있음</strong></p>
<p><strong>메시지 속성</strong> &gt; <strong>중요도 포함 합니다.</strong></p></td>
<td><p><em>WithImportance</em></p>
<p><em>ExceptIfWithImportance</em></p></td>
<td><p><code>Importance</code></p></td>
<td><p>지정된 된 중요도 수준으로 표시 되도록 하는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 메시지 헤더


> [!NOTE]
> ASCII 텍스트의 SMTP 서버 간에 바이너리 메시지를 전송하는 데 사용되는 MIME 콘텐츠 전송 인코딩 메서드에서 메시지가 디코딩된 <EM>후</EM> 메시지의 제목이나 다른 머리글 필드에 있는 단어 또는 텍스트 패턴이 검색됩니다. 조건이나 예외를 사용하여 메시지의 제목이나 다른 머리글 필드에 있는 원시(일반적으로, Base64) 인코딩된 값을 검색할 수 없습니다.




<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 또는 예외 EAC에서</th>
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>메시지 헤더에 다음 포함</strong></p>
<p><strong>메시지 헤더</strong> &gt; <strong>다음 단어 포함</strong></p></td>
<td><p><em>HeaderContainsMessageHeader</em> 및 <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> 및 <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>첫번째 속성: <code>MessageHeaderField</code></p>
<p>두번째 속성: <code>Words</code></p></td>
<td><p>지정 된 헤더 필드 및 해당 헤더 필드의 값을 포함 하는 메시지에 지정 된 단어를 포함 합니다.</p>
<p>헤더 필드의 이름 및 헤더 필드의 값은 항상 함께 사용 됩니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지 헤더가 다음과 일치</strong></p>
<p><strong>메시지 헤더</strong> &gt; <strong>다음 텍스트 패턴과 일치</strong></p></td>
<td><p><em>HeaderMatchesMessageHeader</em> 및 <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> 및 <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>첫번째 속성: <code>MessageHeaderField</code></p>
<p>두번째 속성: <code>Patterns</code></p></td>
<td><p>지정 된 헤더 필드 및 해당 헤더 필드의 값을 포함 하는 메시지는 지정 된 정규식을 포함 합니다.</p>
<p>헤더 필드의 이름 및 헤더 필드의 값은 항상 함께 사용 됩니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 조건 및 Edge 전송 서버에서 메일 흐름 규칙에 대 한 예외

조건 및 예외 Edge 전송 서버에서 메일 흐름 규칙에서 제공 되는 사서함 서버에서 제공 되는 항목의 작은 하위 집합입니다. 방법이 없는 EAC Edge 전송 서버에서 로컬 Edge 전송 서버에서 Exchange 관리 셸 의 메일 흐름 규칙만 관리할 수 있도록 합니다. 조건 및 예외는 다음 표에 설명 되어있습니다. 속성 형식 속성 유형 섹션에 설명 되어있습니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>조건 및 예외 Exchange 관리 셸 매개 변수</th>
<th>속성 형식</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AnyOfRecipientAddressContainsWords</em></p>
<p><em>ExceptIfAnyOfRecipientAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>To</strong>, <strong>Cc</strong>또는 <strong>Bcc</strong> 필드에 지정 된 단어가 있는 메시지입니다.</p>
<p>메시지가 지정 된 받는 사람을 포함 하는 경우 규칙 동작이 됩니다 (되거나 전혀 적용 되지) 메시지의 <em>모든</em> 받는 사람에 게 합니다. 등 뿐아니라 지정 된 받는 사람에 게는 메시지의 모든 받는 사람에 게는 메시지가 거부 됩니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><em>AnyOfRecipientAddressMatchesPatterns</em></p>
<p><em>ExceptIfAnyOfRecipientAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지 <strong>To</strong>, <strong>Cc</strong>또는 <strong>Bcc</strong> 필드는 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p>
<p>메시지가 지정 된 받는 사람을 포함 하는 경우 규칙 동작이 됩니다 (되거나 전혀 적용 되지) 메시지의 <em>모든</em> 받는 사람에 게 합니다. 등 뿐아니라 지정 된 받는 사람에 게는 메시지의 모든 받는 사람에 게는 메시지가 거부 됩니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>AttachmentSizeOver</em></p>
<p><em>ExceptIfAttachmentSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>첨부 파일이 있는 메시지 첨부 파일에 지정 된 값 보다 크거나입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>FromAddressContainsWords</em></p>
<p><em>ExceptIfFromAddressContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p>보낸 사람의 전자 메일 주소에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>FromAddressMatchesPatterns</em></p>
<p><em>ExceptIfFromAddressMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지를 보낸 사람의 전자 메일 주소 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>FromScope</em></p>
<p><em>ExceptIfFromScope</em></p></td>
<td><p><code>UserScopeFrom</code></p></td>
<td><p>내부 보낸사람 또는 외부 보낸 사람이 보낸 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>HeaderContainsMessageHeader</em> 및 <em>HeaderContainsWords</em></p>
<p><em>ExceptIfHeaderContainsMessageHeader</em> 및 <em>ExceptIfHeaderContainsWords</em></p></td>
<td><p>첫번째 속성: <code>MessageHeaderField</code></p>
<p>두번째 속성: <code>Words</code></p></td>
<td><p>지정 된 헤더 필드 및 해당 헤더 필드의 값을 포함 하는 메시지에 지정 된 단어를 포함 합니다.</p>
<p>헤더 필드의 이름 및 헤더 필드의 값은 항상 함께 사용 됩니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>HeaderMatchesMessageHeader</em> 및 <em>HeaderMatchesPatterns</em></p>
<p><em>ExceptIfHeaderMatchesMessageHeader</em> 및 <em>ExceptIfHeaderMatchesPatterns</em></p></td>
<td><p>첫번째 속성: <code>MessageHeaderField</code></p>
<p>두번째 속성: <code>Patterns</code></p></td>
<td><p>지정 된 헤더 필드 및 해당 헤더 필드의 값을 포함 하는 메시지는 지정 된 정규식을 포함 합니다.</p>
<p>헤더 필드의 이름 및 헤더 필드의 값은 항상 함께 사용 됩니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>MessageSizeOver</em></p>
<p><em>ExceptIfMessageSizeOver</em></p></td>
<td><p><code>Size</code></p></td>
<td><p>메시지를 지정된 된 값 보다 크거나 (메시지 및 첨부 파일)의 총 크기입니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><em>SCLOver</em></p>
<p><em>ExceptIfSCLOver</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>있는 지정된 된 값 보다 크거나 같은 SCL을 지정 된 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectContainsWords</em></p>
<p><em>ExceptIfSubjectContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> 필드에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectMatchesPatterns</em></p>
<p><em>ExceptIfSubjectMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>메시지 <strong>Subject</strong> 필드는 지정 된 정규식과 일치 하는 텍스트 패턴을 포함 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>SubjectOrBodyContainsWords</em></p>
<p><em>ExceptIfSubjectOrBodyContainsWords</em></p></td>
<td><p><code>Words</code></p></td>
<td><p><strong>Subject</strong> 필드 또는 메시지 본문에 지정 된 단어가 있는 메시지입니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>SubjectOrBodyMatchesPatterns</em></p>
<p><em>ExceptIfSubjectOrBodyMatchesPatterns</em></p></td>
<td><p><code>Patterns</code></p></td>
<td><p>여기서 <strong>Subject</strong> 필드 또는 메시지 본문 포함 텍스트 패턴을 하는 메시지에 지정된 된 정규식과 일치 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 속성 형식

조건 및 예외에 사용 되는 속성 유형에 다음 표에 설명 되어있습니다.


> [!NOTE]
> 속성이 문자열인 경우 후행 공백을 사용할 수 없습니다.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>속성 형식</th>
<th>유효한 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ADAttribute</code></p></td>
<td><p>Active Directory 특성의 미리 정의 된 목록에서 선택</p></td>
<td><p>UNRESOLVED_TOKENBLOCK_VAL(PD_Transport_Rules_ADAttributes_Snippet)</p>
<p>EAC를 여러 단어 또는 동일한 특성에 대 한 텍스트 패턴을 지정 하려면 값은 쉼표로 구분 합니다. 예 &quot;City equals 샌프란시스코&quot;에 대 한 조회 <strong>샌프란시스코, 팔로 알토도시</strong> 특성에 대 한 값 또는 도시 equals 팔로 알토 &quot;합니다.</p>
<p>Exchange 관리 셸 에서 여기서 <code>Value</code> 는 단어 또는 텍스트 패턴을 일치 시킬 구문을 <code>&quot;AttributeName1:Value1,Value 2 with spaces,Value3...&quot;,&quot;AttributeName2:Word4,Value 5 with spaces,Value6...&quot;</code>를 사용 합니다.</p>
<p>예: <code>&quot;City:San Francisco,Palo Alto&quot;</code> 또는 <code>&quot;City:San Francisco,Palo Alto&quot;</code>,<code>&quot;Department:Sales,Finance&quot;</code>합니다.</p>
<p>여러 특성 또는 동일한 특성에 대 한 여러 값을 지정 하면 <strong>or</strong> 연산자가 사용 됩니다. 선행 또는 후행 공백 값을 사용 하지 마십시오.</p>
<p><strong>Country</strong> 특성에는 두 문자로 ISO 3166-1 국가 코드 값 (예: 독일 DE) 필요를 메모 합니다. 값을 검색 하려면 <a href="https://go.microsoft.com/fwlink/p/?linkid=331680">https://go.microsoft.com/fwlink/p/?LinkId=331680</a>을 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 받는 사람</p></td>
<td><p>조건 또는 예외 특성에 따라 (등 받는 사람 관련 조건), 조직에서 모든 메일 사용이 가능한 개체를 지정할 수 또는 있습니다. (예: 그룹 그룹 구성원에 대 한 특정 개체 형식에 제한 될 수 있습니다. 조건)입니다. 및 수 하나의 값이 필요 조건 또는 예외 또는 여러 값을 허용 합니다.</p>
<p>Exchange 관리 셸 에서 여러 값을 쉼표로 구분 합니다.</p>
<p><strong>참고:</strong> 이 조건은 받는 사람 프록시 주소로 보낸 메시지는 고려하지 않습니다. 받는 사람의 기본 전자 메일 주소로 보낸 메시지만 일치시킵니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>CharacterSets</code></p></td>
<td><p>문자 집합 이름 배열</p></td>
<td><p>메시지에 존재 하는 하나 이상의 콘텐츠 문자 집합입니다. 예를 들어:</p>
<ul>
<li><p><code>Arabic/iso-8859-6</code></p></li>
<li><p><code>Chinese/big5</code></p></li>
<li><p><code>Chinese/euc-cn</code></p></li>
<li><p><code>Chinese/euc-tw</code></p></li>
<li><p><code>Chinese/gb2312</code></p></li>
<li><p><code>Chinese/iso-2022-cn</code></p></li>
<li><p><code>Cyrillic/iso-8859-5</code></p></li>
<li><p><code>Cyrillic/koi8-r</code></p></li>
<li><p><code>Cyrillic/windows-1251</code></p></li>
<li><p><code>Greek/iso-8859-7</code></p></li>
<li><p><code>Hebrew/iso-8859-8</code></p></li>
<li><p><code>Japanese/euc-jp</code></p></li>
<li><p><code>Japanese/iso-022-jp</code></p></li>
<li><p><code>Japanese/shift-jis</code></p></li>
<li><p><code>Korean/euc-kr</code></p></li>
<li><p><code>Korean/johab</code></p></li>
<li><p><code>Korean/ks_c_5601-1987</code></p></li>
<li><p><code>Turkish/windows-1254</code></p></li>
<li><p><code>Turkish/iso-8859-9</code></p></li>
<li><p><code>Vietnamese/tcvn</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>DomainName</code></p></td>
<td><p>SMTP 도메인의 배열</p></td>
<td><p>예: <code>contoso.com</code> 또는 <code>eu.contoso.com</code>합니다.</p>
<p>Exchange 관리 셸 에서 쉼표로 구분 하 여 여러 도메인을 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>EvaluatedUser</code></p></td>
<td><p><strong>보낸사람</strong> 또는 <strong>받는 사람</strong> 의 단일 값</p></td>
<td><p>규칙은 보낸 사람의 관리자 또는 받는 사람의 관리자에 대 한 자세한 내용은 여부를 지정 합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Evaluation</code></p></td>
<td><p><strong>같음</strong> 또는 <strong>같지 않음</strong> (<code>NotEqual</code>)의 단일 값</p></td>
<td><p>보낸사람 및 받는 사람에 게 Active Directory 특성을 비교할 때 값이 일치 해야 하거나 일치 하지 여부를 지정 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Importance</code></p></td>
<td><p><strong>낮음</strong>, <strong>보통</strong> 또는 <strong>높음</strong> 의 단일 값</p></td>
<td><p>Outlook 또는 Outlook Web App 에서 보낸 사람이 메시지에 할당 된 중요도 수준입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>IPAddressRanges</code></p></td>
<td><p>IP 주소 또는 주소 범위 배열</p></td>
<td><p>다음 구문을 사용 하 여 IPv4 주소를 입력 합니다.</p>
<ul>
<li><p><strong>단일 IP 주소</strong>   예: <code>192.168.1.1</code>합니다.</p></li>
<li><p><strong>IP 주소 범위</strong>   예: <code>192.168.0.1-192.168.0.254</code>합니다.</p></li>
<li><p><strong>라우팅 CIDR (classless InterDomain) IP 주소 범위</strong>   예: <code>192.168.0.1/25</code>합니다.</p></li>
</ul>
<p>Exchange 관리 셸, 여러 IP 주소 또는 쉼표로 구분 하 여 범위를 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ManagementRelationship</code></p></td>
<td><p><strong>관리자</strong> 또는 <strong>직접 보고서</strong> (<code>DirectReport</code>)의 단일 값</p></td>
<td><p>보낸사람 및 받는 사람 중 하나라도 간의 관계를 지정합니다. 보낸 사람이 받는 사람의 관리자 또는 보낸 사람이 받는 사람으로 관리 되는 경우를 확인 Active Directory<strong>Manager</strong> 특성을 확인 하는 규칙입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageClassification</code></p></td>
<td><p>단일 메시지 분류</p></td>
<td><p>EAC에서 사용자가 만든 메시지 분류의 목록에서 선택 합니다.</p>
<p>Exchange 관리 셸, <strong>Get-MessageClassification</strong> cmdlet를 사용 하 여 메시지 분류를 식별 합니다. <code>Company Internal</code> 분류가 있는 메시지를 검색 하 고 메시지 제목 앞에 <code>CompanyInternal</code>값 다음 명령을 사용 예입니다.</p>
<p><code>New-TransportRule &quot;Rule Name&quot; -HasClassification @(Get-MessageClassification &quot;Company Internal&quot;).Identity -PrependSubject &quot;CompanyInternal&quot;</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>단일 문자열</p></td>
<td><p>헤더 필드의 이름을 지정합니다. 헤더 필드의 이름 (word 또는 텍스트 패턴 일치) 헤더 필드에 값을 항상 이룹니다.</p>
<p><em>메시지 헤더</em> 는 메시지에 대 한 필수 및 선택적 헤더 필드의 컬렉션입니다. 헤더 필드의 예는 <strong>To</strong>, <strong>From</strong>, <strong>Received</strong>및 <strong>Content-Type</strong>합니다. 공식 헤더 필드는 RFC 5322에 정의 됩니다. 비공식 헤더 필드 <strong>X-</strong> 로 시작 하 고 <em>X-헤더</em>로 알려져 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageType</code></p></td>
<td><p>단일 메시지 유형 값은</p></td>
<td><p>다음 메시지 유형 중 하나를 지정합니다.</p>
<ul>
<li><p><strong>자동 회신</strong> (<code>OOF</code>)</p></li>
<li><p><strong>자동 전달</strong> (<code>AutoForward</code>)</p></li>
<li><p><strong>암호화</strong></p></li>
<li><p><strong>일정 관리</strong></p></li>
<li><p><strong>사용 권한 제어</strong> (<code>PermissionControlled</code>)</p></li>
<li><p><strong>음성 메일</strong></p></li>
<li><p><strong>서명</strong></p></li>
<li><p><strong>승인 요청</strong> (<code>ApprovalRequest</code>)</p></li>
<li><p><strong>읽음 확인</strong> (<code>ReadReceipt</code>)</p></li>
</ul>

> [!NOTE]
> Outlook 또는 Outlook Web App 메시지를 전달 하도록 구성 되 면 <STRONG>ForwardingSmtpAddress</STRONG> 속성은 메시지에 추가 됩니다. 메시지 유형 <CODE>AutoForward</CODE>로 변경 되지 않습니다.


</td>
</tr>
<tr class="odd">
<td><p><code>Patterns</code></p></td>
<td><p>정규식의 배열</p></td>
<td><p>값의 텍스트 패턴을 식별 하는데 사용 되는 정규식 하나 이상 지정 합니다. 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=180327">일반 식 구문</a>을 참조 하십시오.</p>
<p>Exchange 관리 셸, 쉼표로 구분 하 여 여러 정규식을 지정 하 고 각 정규식 큰따옴표 (&quot;)로 묶을 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>SCLValue</code></p></td>
<td><p>다음 값 중 하나입니다.</p>
<ul>
<li><p><strong>바이패스 스팸 필터링</strong> (<code>-1</code>)</p></li>
<li><p>0에서 9 사이의 정수</p></li>
</ul></td>
<td><p>신뢰도 scl (스팸) 메시지에 할당 된를 지정 합니다. 더 높은 SCL 값을 메시지 스팸일 가능성이 임을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>SensitiveInformationTypes</code></p></td>
<td><p>중요 한 정보 유형 배열</p></td>
<td><p>조직에 정의 된 하나 이상의 중요 한 정보 형식을 지정 합니다. 기본 제공 중요 한 정보 유형 목록이 <a href="what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md">Exchange의 중요 한 정보 유형 찾아보십시오</a>을 참조 하십시오.</p>
<p>Exchange 관리 셸, <code>@{&lt;SensitiveInformationType1&gt;},@{&lt;SensitiveInformationType2&gt;},...</code>구문을 사용 합니다. 예를 적어도 두 신용 카드 번호와 하나 이상의 ABA 라우팅 번호를 포함 하는 콘텐츠를 찾도록 값 <code>@{Name=&quot;Credit Card Number&quot;; minCount=&quot;2&quot;},@{Name=&quot;ABA Routing Number&quot;; minCount=&quot;1&quot;}</code>를 사용 합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Size</code></p></td>
<td><p>단일 크기 값</p></td>
<td><p>첨부 파일 또는 전체 메시지의 크기를 지정합니다.</p>
<p>EAC에서 크기 (kb)만 지정할 수 있습니다.</p>
<p>Exchange 관리 셸 에서 값을 입력할 때 다음 단위 중 하나로 값을 사용 합니다.</p>
<ul>
<li><p><code>B</code>(바이트)</p></li>
<li><p><code>KB</code>(킬로바이트)</p></li>
<li><p><code>MB</code>(메가바이트)</p></li>
<li><p><code>GB</code>(기가바이트)</p></li>
</ul>
<p>예: <code>20MB</code></p>
<p>정규화되지 않은 값은 대개 바이트로 처리되지만 작은 값은 가장 가까운 킬로바이트로 반올림될 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>UserScopeFrom</code></p></td>
<td><p><strong>조직 내부</strong> (<code>InOrganization</code>) 또는 <strong>조직 외부의</strong> (<code>NotInOrganization</code>)의 단일 값</p></td>
<td><p>보낸 사람이 다음 조건 중 하나에 해당 하는 경우 조직 내부 것으로 간주 됩니다.</p>
<ul>
<li><p>보낸 사람이 사서함, 메일 사용자, 그룹 또는 조직의 Active Directory 에 있는 메일 사용이 가능한 공용 폴더는 합니다.</p></li>
<li><p>신뢰할 수 있는 도메인 또는 <strong>하 고</strong> 메시지를 보내거나 인증 된 연결을 통해 받은 내부 릴레이 도메인으로 구성 된 허용된 도메인에서 보낸 사람의 전자 메일 주소는 합니다. 허용된 도메인에 대 한 자세한 내용은 <a href="accepted-domains-exchange-2013-help.md">허용 도메인</a>을 참조 하십시오.</p></li>
</ul>
<p>보낸 사람이 다음 조건 중 하나에 해당 하는 경우 조직 외부의 것으로 간주 됩니다.</p>
<ul>
<li><p>허용된 도메인에서 보낸 사람의 전자 메일 주소 되지 않습니다.</p></li>
<li><p>외부 릴레이 도메인으로 구성 된 허용된 도메인에서 보낸 사람의 전자 메일 주소는 합니다.</p></li>
</ul>

> [!NOTE]
> 메일 연락처는 조직의 내부 또는 외부으로 간주 되는지 여부를 확인 하려면 보낸 사람의 주소는 조직의 허용된 도메인으로 구성 된과 비교 됩니다.


</td>
</tr>
<tr class="even">
<td><p><code>UserScopeTo</code></p></td>
<td><p>다음 값 중 하나입니다.</p>
<ul>
<li><p><strong>조직 내부</strong> (<code>InOrganization</code>)</p></li>
<li><p><strong>조직 외부의</strong> (<code>NotInOrganization</code>)</p></li>
<li><p><strong>외부 파트너 조직에서</strong> (<code>ExternalPartner</code>)</p></li>
<li><p><strong>외부 파트너 아닌 조직에서</strong> (<code>ExternalNonPartner</code>)</p></li>
</ul></td>
<td><p>받는 사람이 다음 조건 중 하나에 해당 하는 경우 조직 내부 것으로 간주 됩니다.</p>
<ul>
<li><p>받는 사람 사서함, 메일 사용자, 그룹 또는 조직의 Active Directory 에 있는 메일 사용이 가능한 공용 폴더는 합니다.</p></li>
<li><p>신뢰할 수 있는 도메인 또는 <strong>하 고</strong> 메시지를 보내거나 인증 된 연결을 통해 받은 내부 릴레이 도메인으로 구성 된 허용된 도메인에서 받는 사람의 전자 메일 주소는 합니다.</p></li>
</ul>
<p>받는 사람이 다음 조건 중 하나에 해당 하는 경우 조직 외부의 것으로 간주 됩니다.</p>
<ul>
<li><p>허용된 도메인에서 받는 사람의 전자 메일 주소 되지 않습니다.</p></li>
<li><p>외부 릴레이 도메인으로 구성 된 허용된 도메인에서 받는 사람의 전자 메일 주소는 합니다.</p></li>
</ul>
<p>외부 파트너 조직 외부 도메인은 메일을 보낼 수 있는 도메인 보안 (mutual TLS 인증)을 구성한 경우</p>
<p>파트너 도메인으로 간주 하는 다른 모든 외부 도메인 업무는 외부 파트너가 아닌 조직의 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Words</code></p></td>
<td><p>문자열 배열</p></td>
<td><p>찾을 단어를 하나 이상 지정 합니다. 단어 대/소문자를 구분 하지 및 공백이 나 문장 부호 둘러싸인 될 수 있습니다. 와일드 카드와 부분적으로 일치 지원 되지 않습니다.</p>
<p>예, &quot;contoso&quot;는 &quot;Contoso.&quot;를 찾습니다. 그러나 다른 문자로 된 텍스트에 대 한 주위를 일치 하는 간주 되지 않습니다. 예, &quot;contoso&quot;는 다음 값 일치 하지 않습니다.</p>
<ul>
<li><p>Acontoso</p></li>
<li><p>Contosoa</p></li>
<li><p>Acontosob</p></li>
</ul>
<p>별표 (*)는 리터럴 문자로 취급 되므로 및 와일드 카드 문자 사용 되지 않습니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 자세한 내용

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 동작](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[메일 흐름 또는 전송 규칙 절차](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

Exchange Online 에 대 한 [Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)](https://technet.microsoft.com/ko-kr/library/jj919235\(v=exchg.150\))

Exchange Online Protection 에 대 한 [메일 흐름 규칙 조건 및 예외 (조건자) Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj919234\(v=exchg.150\))

