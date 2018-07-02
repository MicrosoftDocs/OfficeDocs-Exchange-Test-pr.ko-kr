---
title: '조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글: Exchange 2013 Help'
TOCTitle: 조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61060539
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

위쪽 이나 조직을 받거나 하는 전자 메일 메시지의 아래쪽에는 전자 메일 고 지 사항, 법적 고 지 사항, 공개 문, 서명 또는 기타 정보를 추가할 수 있습니다. 이 필요할 수 법률, 비즈니스 또는 잠재적으로 안전 하지 않은 전자 메일 메시지를 식별 하 규정 요구 사항에 대 한 또는 다른 이유로 조직에 고유 합니다.

고 지 사항을를 설정 하려면, 예: 특정 텍스트 패턴 및 텍스트를 추가 하려면 메시지를 포함 하는 경우 또는 특정 그룹에 보낸 사람이 때 조건을 포함 하는 전송 규칙을 만들 수 있습니다. 여러 법적 고 지 사항 단일 전자 메일 메시지에 적용할 여러 전송 규칙을 사용 합니다.


> [!IMPORTANT]
> <UL>
> <LI>
> <P>보내는 메시지에만 추가할 정보를 원하는 경우에 조직 외부에 있는 받는 사람에 게 같은 조건을 추가 해야 합니다. 기본적으로 전송 규칙은 수신 및 발신 메시지에 적용 됩니다.</P></LI></UL>



**목차**

예제

하면 고 지 사항을 범위 지정

서식에 고 지 사항

고 지 사항을 추가할 수 없는 경우 대체 옵션

자세한 내용

절차 필요 하신가요? [조직 전체의 메시지 법적 고 지 사항, 서명, 바닥글 또는 Office 365에서 머리글](https://technet.microsoft.com/ko-kr/library/dn600323\(v=exchg.150\))를 참조 하십시오.

## 예제

고 지 사항을 사용 하는 방법에 대 한 몇가지 아이디어는 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>종류</th>
<th>추가 예제 텍스트</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>법적-보내는 메시지</p></td>
<td><p>이 전자 메일와 함께 전송 되는 모든 파일은 기밀 및 개인 또는 해결 누구에 게 엔터티를 사용 하는 용도로 의도 한입니다. 오류로 인해이 전자 메일을 받은 경우에 시스템 관리자에 게 알릴 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>법률 – 받는 메시지</p></td>
<td><p>직원은 하지 비방 명령문을 확인 하 고 하지을 침해 또는 모든 침해의 저작권 또는 기타 법적 권리 전자 메일 통신 하 여 대 한 권한 부여 명시적으로 필요 합니다. 이러한 전자 메일을 수신 하는 직원에 알려야가 supervisor 즉시 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>별칭에 해당 메시지를 보낸 것을 알합니다</p></td>
<td><p>이 메시지는 Sales 토론 그룹에 전송 되었습니다.</p></td>
</tr>
<tr class="even">
<td><p>서명-각 직원에 대 한 데이터를 가져와서</p></td>
<td><p>Kathleen Mayer<br />
영업부<br />
Contoso<br />
www.contoso.com<br />
kathleen@contoso.com<br />
셀: 111-222-1234</p></td>
</tr>
<tr class="odd">
<td><p>광고</p></td>
<td><p>3 월 특별 행사에 대 한 여기를 클릭 하십시오.</p></td>
</tr>
</tbody>
</table>


이 문서의 예제로 사용 하기 위해이 아닙니다-됩니다. 필요에 맞게 수정 합니다.

## 하면 고 지 사항을 범위 지정

대화 법적 고 지 사항에서 작동 되는 메시지에 적용 되는 해야 고려해 야 합니다. 등 특정 부서에서 사용자가 보낸 메시지 또는 내부 및 외부 메시지에 대 한 서로 다른 법적 고 지 사항을 사용할 수 있습니다. 대화의 첫번째 메시지만는 고 지 사항을 가져옵니다 있는지 확인 하십시오에 고 지 사항에 고유한 텍스트를 찾고 있는 예외를 발생을 추가 합니다.

다음은 몇가지 예의 조건 및 예외를 사용할 수 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>설명</th>
<th>조건 및 예외 EAC에서</th>
<th>조건 및 예외 셸에서</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>원본 메시지에 고 지 사항, &quot;CONTOSO 법적 고 지 사항&quot; 등의 텍스트를 포함 되지 않은 경우 조직 외부</p></td>
<td><p>조건: <strong>에서 받는 사람이 있는</strong> &gt; <strong>조직 외부의</strong></p>
<p>예외: <strong>제목이 나 본문</strong> &gt; <strong>다음 텍스트 패턴과 일치 하는 제목이 나 본문</strong> &gt; <strong>CONTOSO 법적 고 지 사항</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches &quot;CONTOSO LEGAL NOTICE&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>실행 파일 첨부 파일이 받는 메시지</p></td>
<td><p>조건 1: <strong>보낸 사람이 위치</strong> &gt; <strong>조직 외부의</strong></p>
<p>조건 2: <strong>첨부 파일</strong> &gt; <strong>에 실행 가능한 콘텐츠가 있음</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -AttachmentHasExecutableContent</code></pre></td>
</tr>
<tr class="odd">
<td><p>보낸 사람이 마케팅 부서에</p></td>
<td><p>조건: <strong>보낸 사람이</strong> &gt; <strong>이 그룹의 구성원은</strong> &gt; <strong>그룹 이름</strong></p></td>
<td><pre><code>-FromMemberOf &quot;Marketing Team&quot;</code></pre></td>
</tr>
<tr class="even">
<td><p>판매 토론 그룹에 외부에서 제공 되는 모든 메시지</p></td>
<td><p>조건 1: <strong>보낸 사람이 위치</strong> &gt; <strong>조직 외부의</strong></p>
<p>조건 2: <strong>메시지</strong> &gt; <strong>에이 사용자를 포함 하는 참조 상자 또는</strong> &gt; <strong>그룹 이름</strong></p></td>
<td><pre><code>-FromScope NotInOrganization -SentTo &quot;Sales Discussion Group&quot; -PrependSubject &quot;Sent to Sales Discussion Group: &quot;</code></pre></td>
</tr>
<tr class="odd">
<td><p>한 달에 대 한 보내는 메시지에 대 한 보급 앞에 추가</p></td>
<td><p>조건 1: <strong>에서 받는 사람이 있는</strong> &gt; <strong>조직 외부의</strong></p>
<p><strong>새 규칙</strong> 대화 상자 맨 아래에 날짜를 지정 합니다.</p></td>
<td><p>-ApplyHtmlDisclaimerLocation '를 추가 해서는'-SentToScope 'NotInOrganization'-ActivationDate ' 03/1/2014 년-ExpiryDate ' 03/31/2014 '</p></td>
</tr>
</tbody>
</table>


전체 목록은 전송 규칙 조건에 대 한 대상으로 고 지 사항, 다음 중 하나를 참조를 사용할 수 있습니다.

  - [Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)](https://technet.microsoft.com/ko-kr/library/jj919235\(v=exchg.150\)) (Exchange Online)

  - [전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) (Exchange 2013)

  - [Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)](https://technet.microsoft.com/ko-kr/library/jj919235\(v=exchg.150\)) (Exchange Online Protection)

## 서식에 고 지 사항

필요에 따라 하면 고 지 사항을 서식을 지정할 수 있습니다. 고 지 사항 텍스트에 포함 될 수 있는 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>이러한 유형의 정보</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>텍스트</p></td>
<td><p>최대 길이 모든 HTML 태그와 인라인 계단식 스타일 시트 (CSS)을 포함 하는 최대 5, 000 자입니다.</p></td>
</tr>
<tr class="even">
<td><p>HTML 및 CSS 인라인</p></td>
<td><p>다음은 텍스트의 서식을 지정 하려면 HTML 및 인라인 CSS 스타일을 사용할 수 있습니다. 예, <code>&lt;HR&gt;</code> 태그를 사용 하 여 고 지 사항 앞에 있는 줄을 추가 합니다.</p>
<p>일반 텍스트 메시지에 고 지 사항 추가 되는 고 지 사항에는 HTML은 무시 됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>이미지를 추가 합니다.</p></td>
<td><p><code>&lt;IMG&gt;</code> 태그를 사용 하 여 인터넷에서 사용할 수 있는 이미지를 가리키도록 합니다. 예: <code>&lt;IMG src=&quot;http://contoso.com/images/companylogo.gif&quot; alt=&quot;Contoso logo&quot;&gt;</code></p>
<p>염두에 Outlook Web App 및 Outlook 블록 외부 웹 콘텐츠를 기본적으로 이미지를 포함 합니다. 사용자가 차단 된 외부 콘텐츠 보기를 원하는 경우 특정 작업을 수행 해야 합니다. 즉, 않을 <code>IMG</code> 태그를 사용 하 여 추가 된 이미지를 기본적으로 표시 하지 수 있습니다. 받는 사람에 게는 제대로 표시 되는지 확인 하는를 사용 하 여 경우가 전자 메일 클라이언트에는 고 지 사항을 <code>IMG</code> 태그를 테스트 하는 것이 좋습니다.</p></td>
</tr>
<tr class="even">
<td><p>개인 설정 된 서명에 대 한 정보를 추가 합니다.</p></td>
<td><p>모든 사람에 게 하려는 경우 서명 동일한 정보와 동일한 방식으로 서식이 지정 된, <code>DisplayName</code>, <code>FirstName</code>, <code>LastName</code>, <code>PhoneNumber</code>, <code>Email</code>, <code>FaxNumber</code>및 <code>Department</code>와 같은 각 직원에 대 한 고유한 정보를 추가할 수 있습니다. 이 정보 정보의 양쪽에 2% 기호 (%)로 묶어야 합니다. 예, <code>DisplayName</code>를 사용 하 여 사용 해야 <strong>%%DisplayName % %</strong> 에 고 지 사항에 있습니다.</p>
<p>고 지 사항 규칙이 트리거되는 경우 해당 사용자에 대 한 해당 값이 삽입 됩니다. 보낸 사람의 Active Directory 사용자 계정 (온-프레미스 Exchange 서버)에서 또는 Exchange Online 에 대 한 보낸 사람의 Office 365 계정에서 데이터를 가져옵니다.</p>
<p>법적 고 지 사항 및 개인 설정 된 서명에서 사용할 수 있는 특성을 전체 목록은 <a href="mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md">전송 규칙 조건 (조건자)</a> (Exchange Server), <a href="https://technet.microsoft.com/ko-kr/library/jj919235(v=exchg.150)">Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)</a> (Exchange Online ) 또는 <a href="https://technet.microsoft.com/ko-kr/library/jj919234(v=exchg.150)">메일 흐름 규칙 조건 및 예외 (조건자) Exchange 온라인 보호</a> (Exchange Online Protection)의 <code>ADAttribute</code> 속성에 대 한 설명을 참조 하십시오.</p></td>
</tr>
</tbody>
</table>


예 서명을, `IMG` 태그 및 포함 된 CSS를 포함 하는 HTML 고 지 사항의 한 예를 살펴보겠습니다.

    <div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
    %%displayname%%</br>
    %%title%%</br>
    %%company%%</br>
    %%street%%</br>
    %%city%%, %%state%% %%zipcode%%</div>
    &nbsp;</br>
    <div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
    <div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
    <span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span></br>
    <p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.  </p>
    <span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc. </a></span></br></br>
    </div>

## 고 지 사항을 추가할 수 없는 경우 대체 옵션

암호화 된 메시지와 같은 일부 메시지 원본 메시지의 내용을 수정에서 Exchange를 방지 합니다. 조직에서 이러한 메시지를 처리 하는 방법을 제어할 수 있습니다. 메시지 봉투에서 수정할 수 없는 메시지를 배치 하 고 지 사항이 포함 된, 여부는 고 지 사항을 추가할 수 없는 또는 고 지 사항 동작을 무시 및는 고 지 사항 없이 메시지를 배달 하는 경우 메시지를 거부를 지정 합니다.

다음 목록에서는 각 대체 작업에 대해 설명합니다.

  - **줄바꿈**    고 지 사항을 원본 메시지에 삽입할 수 없을 경우에 Exchange 둘러싸는, 또는 "줄바꿈," 새 메시지 봉투의 원본 메시지입니다. 그런 다음 고 지 사항이 새 메시지에 삽입 됩니다. 새 메시지 봉투의 원본 메시지에 배치할 수 없습니다, 원본 메시지 배달 되지 않습니다. 메시지를 보낸 사람이 메시지가 배달 되지 이유를 설명 하는 배달 못함 보고서 (NDR)를 받습니다.
    

    > [!IMPORTANT]
    > 원본 메시지가 새 메시지 봉투에서 줄 바꿈되면 원본 메시지가 아닌 새 메시지 봉투에 후속 전송 규칙이 적용됩니다. 따라서 다른 전송 규칙을 구성한 후 새 메시지 본문에서 원본 메시지를 줄 바꿈하는 고지 사항 동작으로 전송 규칙을 구성해야 합니다.



  - **거부 합니다.**    고 지 사항을 원본 메시지에 삽입할 수 없을 경우 Exchange 메시지를 배달 하지 않습니다. 메시지를 보낸 사람이 메시지 배달 되지 않은 이유를 설명 하는 NDR을 받습니다.

  - **무시**    고 지 사항을 원본 메시지에 삽입할 수 없을 경우 Exchange는 수정 하지 않고 원래 메시지를 배달 합니다. 없음 고 지 사항 추가 됩니다.

## 자세한 내용

[조직 전체의 메시지 법적 고 지 사항, 서명, 바닥글 또는 Office 365에서 머리글](https://technet.microsoft.com/ko-kr/library/dn600323\(v=exchg.150\))

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) (Exchange Server 2013)

[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\)) (Exchange Online)

[Exchange Online Protection의 메일 흐름 규칙(전송 규칙)](https://technet.microsoft.com/ko-kr/library/dn271424\(v=exchg.150\)) (Exchange Online Protection)

