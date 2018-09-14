---
title: '메일 흐름 또는 전송 규칙: Exchange 2013 Help'
TOCTitle: 메일 흐름 규칙 (전송 규칙)
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 50484104
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 흐름 또는 전송 규칙

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-04-28_

메일 흐름 규칙 (전송 규칙이 라고도 함)를 사용 하 여 식별 하 고 메시지 Exchange 2013 조직을 통해 흐름에 대해 조치를 취할 수 있습니다. 메일 흐름 규칙 Outlook 및 Outlook Web App 에서 제공 되는 받은 편지함 규칙을 하는 것과 유사 합니다. 주요 차이점은 메일 흐름 규칙, 전송 중인 동안 및 메시지는 사서함에 배달 된 후에 하지 메시지에 조치를 취할입니다. 메일 흐름 규칙에 다양 한 종류의 메시징 정책 구현 하는 유연성을 제공 하는 조건, 예외 및 작업의 다양 한 집합을 포함 합니다.

이 문서에서는 메일 흐름 규칙의 구성 요소와 작동 방식을 설명합니다.

Exchange Online 에서 메일 흐름 규칙에 대 한 정보를 [Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\))을 참조 하십시오. Exchange Online Protection 에서 메일 흐름 규칙에 대 한 정보를 [Exchange Online Protection의 메일 흐름 규칙(전송 규칙)](https://technet.microsoft.com/ko-kr/library/dn271424\(v=exchg.150\)) 을 참조 하십시오.

메일 흐름 규칙을 관리 하 Exchange 관리 센터 (EAC) 또는 Exchange 관리 셸 를 사용할 수 있습니다. 전송 규칙을 관리 하는 방법에 대 한 자세한 내용은 [메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)를 참조 하십시오.

각 규칙에 대해 규칙을 적용하거나, 규칙을 테스트하거나, 규칙을 테스트하고 보낸 사람에게 알릴 수 있는 옵션이 제공됩니다. 테스트 옵션에 대한 자세한 내용은 [메일 흐름 규칙을 테스트 합니다.](test-a-mail-flow-rule-exchange-2013-help.md) 및 [정책 팁](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/policy-tips)을 참조하세요.

메일 흐름 규칙을 사용해서 특정 메시징 정책을 실행하려면 다음 항목을 참조하세요.

  - [전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [일반적인 첨부 파일 차단 시나리오](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [메시지 포함 되는 문서를 무시할 수 있도록 메일 흐름 규칙을 사용 하 여](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter)

  - [메일 흐름 규칙 단어, 구 또는 패턴의 목록을 기반으로 전자 메일 라우팅에 사용 하 여](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email)

  - [일반적인 메시지 승인 시나리오](common-message-approval-scenarios-exchange-2013-help.md)

## 메일 흐름 규칙 구성 요소

메일 흐름 규칙은 조건, 예외, 작업 및 속성의 이루어집니다.

  - **조건** 수행할 작업에 적용할 메시지를 식별합니다. 일부 조건은 받는 사람, 보낸 사람, 참조 필드 등의 메시지 헤더 필드를 검사하며 다른 조건은 메시지 제목, 본문, 첨부 파일, 메시지 크기, 메시지 분류 등의 메시지 속성을 검사합니다. 대부분의 조건에는 같음, 같지 않음 또는 포함 등의 비교 연산자 및 일치시킬 값을 지정해야 합니다. 조건이나 예외가 없는 경우 규칙이 모든 메시지에 적용됩니다.
    
    Exchange 2013 의 메일 흐름 규칙 조건에 대 한 자세한 내용은 [전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)를 참조 하십시오.

  - **예외** 선택적으로 해당 작업이 적용되면 안 되는 메시지를 식별합니다. 조건에서 사용할 수 있는 동일한 메시지 식별자를 예외에서도 사용할 수 있습니다. 예외는 조건을 재정의하며, 메시지가 구성된 모든 조건과 일치하더라도 규칙 작업이 메시지에 적용되지 않도록 합니다.

  - **작업** 규칙의 조건과 일치하고 예외와는 일치하지 않는 메시지에 수행할 작업을 지정합니다. 메시지를 거부, 삭제 또는 리디렉션하거나, 받는 사람을 추가하거나, 메시지 제목에 접두사를 추가하거나, 메시지 본문에 고지 사항을 삽입하는 등 다양한 작업을 수행할 수 있습니다.
    
    Exchange 2013 에서 메일 흐름 규칙 동작에 대 한 자세한 내용은 [전송 규칙 동작](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

  - **속성** 조건, 예외 또는 작업이 아닌 다른 규칙 설정을 지정합니다. 예를 들어, 규칙이 적용되는 시기, 규칙 적용 또는 테스트 여부, 규칙이 활성화되는 시기를 지정합니다.
    
    자세한 내용은이 항목의 메일 흐름 규칙 속성 섹션을 참조 하십시오.

## 여러 조건, 예외 및 작업

다음 표에는 규칙에서 여러 조건, 조건 값, 예외 및 작업이 처리되는 방식이 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>구성 요소</th>
<th>논리</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>여러 조건</p></td>
<td><p>AND</p></td>
<td><p>메시지는 규칙의 모든 조건과 일치해야 합니다. 하나의 조건 또는 다른 조건과 일치해야 하는 경우 각 조건에 대해 별도의 규칙을 사용합니다. 예를 들어 특정 텍스트를 포함하는 메시지 및 첨부 파일이 있는 메시지에 동일한 고지 사항을 추가하려면 각 조건에 대해 하나의 규칙을 만듭니다. EAC에서는 규칙을 쉽게 복사할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>값이 여러 개인 조건</p></td>
<td><p>OR</p></td>
<td><p>일부 조건에는 둘 이상의 값을 지정할 수 있습니다. 메시지는 지정된 값 중 하나에만(전체 아님) 일치하면 됩니다. 예를 들어 전자 메일 메시지의 제목이 <strong>주가 정보</strong>이고 <strong>제목에 다음 단어 포함</strong> 조건이 <strong>Contoso</strong> 또는 <strong>주가</strong>라는 단어와 일치하도록 구성된 경우 지정된 값 중 적어도 하나가 제목에 포함되어 있으므로 조건이 충족됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>여러 예외</p></td>
<td><p>OR</p></td>
<td><p>예외 중 하나라도 메시지와 일치하면 작업은 메시지에 적용되지 않습니다. 메시지가 모든 예외와 일치할 필요는 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>여러 작업</p></td>
<td><p>AND</p></td>
<td><p>규칙 조건에 일치하는 메시지에는 규칙에 지정된 모든 작업이 적용됩니다. 예를 들어, <strong>메시지 제목 앞에 다음 추가</strong> 및 <strong>숨은 참조란에 받는 사람 추가</strong> 작업을 선택하면 두 작업 모두 메시지에 적용됩니다.</p>
<p><strong>아무에게도 알리지 않고 메시지 삭제</strong> 등의 일부 작업을 적용할 경우 후속 규칙이 메시지에 적용되지 않습니다. <strong>메시지 전달</strong> 등의 다른 작업은 추가 작업을 허용하지 않습니다.</p>
<p>해당 규칙이 적용될 때 후속 규칙은 메시지에 적용되지 않도록 규칙에 대해 작업을 설정할 수도 있습니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 메일 흐름 규칙 속성

다음 표에서 메일 흐름 규칙에서 사용할 수 있는 규칙 속성을 설명합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC의 속성 이름</th>
<th>PowerShell의 매개 변수 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>우선 순위</strong></p></td>
<td><p><em>Priority</em></p></td>
<td><p>메시지에 규칙이 적용되는 순서를 나타냅니다. 기본 우선 순위는 규칙을 만들 때를 기준으로 합니다(이전 규칙은 새로운 규칙보다 우선 순위가 높고, 우선 순위가 높은 규칙은 우선 순위가 낮은 규칙보다 먼저 처리됨).</p>
<p>규칙을 규칙 목록에서 위 또는 아래로 이동하여 EAC에서 규칙 우선 순위를 변경합니다. PowerShell에서 우선 순위 번호를 설정합니다(0이 가장 높은 우선 순위임).</p>
<p>예를 들어 신용 카드 번호가 포함된 메시지는 거부하는 규칙과 승인을 요구하는 또 다른 규칙이 있을 때 거부 규칙이 먼저 적용되도록 한 다음 다른 규칙이 적용되지 않도록 할 수 있습니다.</p>
<p>자세한 내용은 <a href="manage-mail-flow-rules-exchange-2013-help.md">메일 흐름 규칙의 우선 순위 설정</a>을 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p><strong>모드</strong></p></td>
<td><p><em>Mode</em></p></td>
<td><p>규칙이 메시지 처리를 즉시 시작하도록 할지 여부 또는 메시지의 배달에 영향을 주지 않고 규칙을 테스트할지 여부를 지정할 수 있습니다(데이터 손실 방지 또는 DLP 정책 팁 사용 또는 사용 안 함).</p>
<p>정책 팁은 Outlook 또는 웹에서 Outlook에서 메시지를 작성하는 사람에게 가능한 정책 위반에 대한 정보를 제공하는 간단한 메모를 표시합니다. 자세한 내용은 <a href="https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/policy-tips">정책 팁</a>을 참조하세요.</p>
<p>모드에 대한 자세한 내용은 <a href="test-a-mail-flow-rule-exchange-2013-help.md">메일 흐름 규칙을 테스트 합니다.</a>를 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p><strong>다음 날짜에 이 규칙 활성화</strong></p>
<p><strong>다음 날짜에 이 규칙 비활성화</strong></p></td>
<td><p><em>ActivationDate</em></p>
<p><em>ExpiryDate</em></p></td>
<td><p>규칙이 활성화되는 날짜 범위를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>설정</strong> 확인란 선택 또는 선택 취소</p></td>
<td><p>새 규칙: <strong>New-TransportRule</strong> cmdlet의 <em>Enabled</em> 매개 변수</p>
<p>기존 규칙: <strong>Enable-TransportRule</strong> 또는 <strong>Disable-TransportRule</strong> cmdlet을 사용합니다.</p>
<p>해당 값은 규칙의 <strong>State</strong> 속성에 표시됩니다.</p></td>
<td><p>사용되지 않도록 설정된 규칙을 만들고 테스트할 준비가 되면 사용하도록 설정할 수 있습니다. 또는 규칙을 삭제하지 않고 사용하지 않도록 설정하여 설정을 유지할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>규칙 처리가 완료되지 않으면 메시지 연기</strong></p></td>
<td><p><em>RuleErrorAction</em></p></td>
<td><p>규칙 처리를 완료할 수 없는 경우 메시지를 처리할 방법을 지정할 수 있습니다. 기본적으로 규칙은 무시되지만 처리를 위해 메시지를 다시 전송하도록 선택할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지의 보낸 사람 주소 일치</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>규칙이 보낸 사람의 전자 메일 주소를 검사하는 조건 또는 예외를 사용하는 경우 메시지 머리글이나 메시지 봉투 또는 둘 다에 있는 값을 찾을 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>추가 규칙 처리 중지</strong></p></td>
<td><p><em>SenderAddressLocation</em></p></td>
<td><p>규칙에 대한 작업이지만 EAC의 속성과 같습니다. 규칙이 메시지를 처리하면 메시지에 추가 규칙을 적용하지 않도록 선택할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>설명</strong></p></td>
<td><p><em>Comments</em></p></td>
<td><p>규칙에 대한 설명을 입력할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 메일 흐름 규칙은 메시지에 적용 하는 방법

조직을 통해 이동되는 모든 메시지가 조직에 대해 사용하도록 설정된 메일 흐름 규칙을 기준으로 평가됩니다. 규칙은 EAC의 **메일 흐름** \> **규칙** 페이지에 표시된 순서로 처리되거나 PowerShell의 해당 *Priority* 매개 변수 값에 따라 처리됩니다.

또한 각 규칙은 일치할 경우 추가 규칙의 처리를 중지하는 옵션도 제공됩니다. 이 설정은 여러 메일 흐름 규칙의 조건과 일치하는 메시지에 중요합니다(메시지에 어떤 규칙을 적용할까요? 모두? 하나만?).

## 메시지 유형에 따른 처리 방식의 차이

조직을 통과하는 메시지 유형에는 몇 가지가 있습니다. 다음 표에는 메일 흐름 규칙으로 처리될 수 있는 메시지 유형이 나와 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메시지 유형</th>
<th>규칙을 적용할 수 있는지 여부</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>일반 메시지</strong>   단일 RTF(서식 있는 텍스트), HTML 또는 일반 텍스트 메시지 본문 또는 여러 부분으로 된 메시지 본문 집합이나 대체 메시지 본문 집합이 포함된 메시지입니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 메시지 암호화</strong>    Office 365에서 Office 365 메시지 암호화에 의해 암호화된 메시지입니다. 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=392525">Office 365 메시지 암호화</a>를 참조하세요.</p></td>
<td><p>규칙은 항상 봉투 헤더에 액세스하여 해당 헤더를 검사하는 조건을 바탕으로 메시지를 처리할 수 있습니다.</p>
<p>암호화된 메시지의 내용을 검사하거나 수정하는 규칙의 경우, 전송 암호 해독이 사용되도록 설정되어 있는지 확인해야 합니다(필수 또는 옵션. 기본값은 옵션임). 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">전송 암호 해독 사용 또는 사용 안 함</a>을 참조하세요.</p>
<p>암호화된 메시지의 암호를 자동으로 해독하는 규칙을 만들 수도 있습니다. 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=402846">전자 메일 메시지를 암호화하거나 암호를 해독하는 규칙 정의</a>를 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p><strong>S/MIME 암호화 메시지</strong></p></td>
<td><p>규칙은 봉투 헤더에 액세스하여 해당 헤더를 검사하는 조건을 바탕으로 메시지를 처리할 수만 있습니다.</p>
<p>메시지 내용을 검사해야 하는 조건이 포함된 규칙이나 메시지의 내용을 수정하는 작업은 처리할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>RMS 보호 메시지</strong>   Active Directory Rights Management Services(AD RMS) 또는 RMS(Azure 권한 관리) 정책이 적용된 메시지입니다.</p></td>
<td><p>규칙은 항상 봉투 헤더에 액세스하여 해당 헤더를 검사하는 조건을 바탕으로 메시지를 처리할 수 있습니다.</p>
<p>RMS 보호 메시지의 내용을 검사하거나 수정하는 규칙의 경우, 전송 암호 해독이 사용되도록 설정되어 있는지 확인해야 합니다(필수 또는 옵션. 기본값은 옵션임). 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=848060">전송 암호 해독 사용 또는 사용 안 함</a>을 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p><strong>일반 텍스트 서명된 메시지</strong>   서명되었지만 암호화되지는 않은 메시지입니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>UM 메시지</strong>   음성 사서함, 팩스, 부재 중 전화 알림, Microsoft Outlook Voice Access를 사용하여 만들었거나 전달된 메시지 등 통합 메시징 서비스에서 생성하거나 처리한 메시지입니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p><strong>익명 메시지</strong>   익명 보낸 사람이 보낸 메시지입니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p><strong>읽기 보고서</strong>   받는 사람이 읽기 확인을 요청한 경우에 생성되는 보고서입니다. 읽기 보고서에는 <code>IPM.Note*.MdnRead</code> 또는 <code>IPM.Note*.MdnNotRead</code>라는 메시지 클래스가 표시됩니다.</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


## 전송 규칙과 그룹 구성원

메일 그룹의 구성원 자격을 확장하는 조건을 사용하여 전송 규칙을 적용하면 그에 따른 받는 사람 목록이 규칙을 적용하는 사서함 서버의 전송 서비스에서 캐시됩니다. 이를 *확장 그룹 캐시*라고 하며 저널링 에이전트에서 저널 규칙 적용 시에 그룹 구성원 자격을 평가하는 데에도 사용됩니다. 기본적으로 확장 그룹 캐시의 그룹 구성원은 4시간 동안 저장됩니다. 동적 메일 그룹의 받는 사람 필터를 통해 반환된 받는 사람도 여기에 저장됩니다. 확장 그룹 캐시는 Active Directory를 반복적으로 읽고 쓸 필요가 없도록 하여 그룹 구성원 확인을 위한 네트워크 트래픽을 해소합니다.

Exchange 2013에서는 이러한 캐시 간격과 기타 확장 그룹 캐시 관련 매개 변수를 구성할 수 있습니다. 캐시 만료 간격을 낮추거나 캐싱 기능을 완전히 사용하지 않도록 설정하면 그룹 구성원을 더 자주 새로 고치게 됩니다. 단, 이 경우 Active Directory 도메인 컨트롤러에서 메일 그룹 확장 쿼리에 따른 로드가 증가하는 데 대해 대비해야 합니다. 또한 사서함 서버에서 Microsoft Exchange Transport Service를 다시 시작하여 캐시를 지울 수도 있습니다. 캐시는 각 사서함 서버에서 별도로 지워야 합니다. 메일 그룹 구성원을 기준으로 한 조건을 사용하는 전송 규칙을 만들고 테스트하고 관련 문제를 해결할 때에는 확장 그룹 캐시에 미치는 영향도 고려해야 합니다.

## 규칙 저장소 및 복제

메일 흐름 규칙 만들기 및 사서함 서버에서 구성 하는 Active Directory 저장 되 고 읽고 조직의 모든 사서함 서버의 전송 서비스에 의해 적용 합니다. 만들기, 수정 또는 메일 흐름 규칙을 제거 하는 경우 해당 변경 하면 조직에서 도메인 컨트롤러 간에 복제 됩니다. 이 집합을 제공 하는 일관성 있는 메일 흐름 규칙 조직 전체에 걸쳐 Exchange 수 있습니다.

**참고**:

  - 도메인 컨트롤러 간에 복제 Exchange (예: Active Directory 사이트 수) 및 네트워크 링크의 속도 의해 제어 되지 않은 요인에 따라 달라 집니다. 따라서 조직에서 메일 흐름 규칙을 구현 하는 경우 복제 지연을 고려해 야 합니다. Active Directory 복제 하는 방법에 대 한 자세한 내용은 [Active Directory 복제 및 토폴로지 관리를 사용 하 여 Windows PowerShell 소개](https://go.microsoft.com/fwlink/p/?linkid=274904)을 참조 하십시오.

  - 각 사서함 서버 반복 해 서 Active Directory 그룹의 구성원을 확인 하는 쿼리를 방지 하기 위해 확장 된 메일 그룹을 캐시 합니다. 기본적으로 확장 된 그룹 캐시의 항목에는 4 시간 마다 만료 됩니다. 따라서 그룹의 구성원 자격의 변경 확장 된 그룹 캐시 업데이트 될 때까지 메일 흐름 규칙에 의해 검색 되지 않습니다. 사서함 서버에서 캐시의 업데이트를 즉시 수행 하도록 Microsoft Exchange 전송 서비스 다시 시작 합니다. 캐시를 강제로 업데이트 하려는 각 사서함 서버에서 서비스를 다시 시작 해야 합니다.

메일 흐름 규칙 만들기 및 Edge 전송 서버에서 구성 하는 서버에서 로컬 인스턴스의 AD LDS에 저장 됩니다. 메일 흐름 규칙의 자동화 된 복제 없음 Edge 전송 서버에서 발생합니다. Edge 전송 서버에 대 한 규칙 로컬 서버를 통과 하는 메시지에만 적용 됩니다. 여러 Edge 전송 서버에서 메일 흐름 규칙의 동일한 집합을 적용 해야하는 경우 Edge 전송 서버 구성을 복제 수 또는 내보내기 및 메일 흐름 규칙을 가져옵니다. 자세한 내용은 [Edge 전송 서버 복제 된 구성](edge-transport-server-cloned-configuration-exchange-2013-help.md) 및 [가져오기 또는 내보내기 메일 흐름 규칙 컬렉션](manage-mail-flow-rules-exchange-2013-help.md)을 참조 하십시오.

사서함 서버 또는 Edge 전송 서버에서 전송 서비스에서 수정 된 메일 흐름 규칙을 발견 하면 때마다 이벤트 (이벤트 ID 4002 사서함 서버의 및 Edge 전송 서버에서 이벤트 ID 16028) 이벤트 뷰어에서 응용 프로그램 로그에 기록 됩니다.

## 혼합 환경에서 규칙 복제 및 저장

Exchange 2013 에 공통 되는 혼합된 환경 시나리오는

  - **조직 구성원이 UNRESOLVED\_TOKEN\_VAL(Office365) 에 상주 하는 하이브리드 배포**
    
    하이브리드 환경에서 온-프레미스 Exchange 조직 사이의 UNRESOLVED\_TOKEN\_VAL(Office365) 규칙의 복제가 있습니다. 따라서 Exchange 에서 규칙을 만들 때 UNRESOLVED\_TOKEN\_VAL(Office365) 에 일치 하는 규칙을 만들려면 해야 합니다. UNRESOLVED\_TOKEN\_VAL(Office365) 에서 작성 한 규칙 클라우드에 저장 된, 온-프레미스 조직에서 만드는 규칙 사용 하지만 Active Directory 에 로컬로 저장 됩니다. 하이브리드 환경에서 규칙을 관리 하는 경우 두 위치에서의 변경 사항을 또는 하나의 환경에서의 변경 작업 수행 하 고 다음 내보내기 (영문) 규칙 및 다른 환경에서 가져오기 동기화 되는 규칙의 두 집합을 유지 해야 합니다.
    

    > [!IMPORTANT]
    > 조건 및 UNRESOLVED_TOKEN_VAL(Office365) 및 Exchange Server 에서 사용할 수 있는 작업 간의 많이 중복 인 경우에 차이점이 있습니다. 두 위치에서 동일한 규칙을 만드는 방법에 대해 계획 하는 경우 모든 조건 및 동작을 사용 하려는 사용할 수 있는지 확인 합니다. 사용 가능한 조건 및 UNRESOLVED_TOKEN_VAL(Office365) 에서 사용할 수 있는 작업의 목록을 보려면 다음 항목을 참조 합니다.<BR><A href="https://technet.microsoft.com/ko-kr/library/jj919235(v=exchg.150)">Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)</A><BR><A href="https://technet.microsoft.com/ko-kr/library/jj919237(v=exchg.150)">Exchange Online 흐름 규칙 동작을 메일</A>



  - **Exchange 2010 또는 Exchange 2007 과 동시 사용**
    
    Exchange 2010 또는 Exchange 2007 와 함께 사용할 때 모든 메일 흐름 규칙 Active Directory 에 저장 되며 규칙을 만들 때 사용한 Exchange Server 버전에 관계 없이 조직 전체에서 복제 됩니다. 그러나 모든 메일 흐름 규칙은 Exchange Server 서버 버전을 만들고, 사용 되 고 Active Directory 의 버전별 컨테이너에 저장 된에 연관 됩니다. 조직에서 Exchange 2013 처음 배포할 때 기존의 모든 규칙 설치 프로세스의 일부로 Exchange 2013 가져옵니다. 그러나 변경 내용을 나중에 해야 두 버전 모두를 사용 하 여 수 있습니다. 예, Exchange 2013 (Exchange 관리 셸 또는 EAC)에서 기존 규칙을 변경 하는 경우 Exchange 2010 (Exchange 관리 셸 또는 UNRESOLVED\_TOKEN\_VAL(exEMC) )에서 동일한 변경 작업을 수행 해야 합니다. 또는 Exchange 2013 에서 규칙을 내보낼 Exchange 2010 로 가져올 수 있습니다.
    
    Exchange 2010 15 **버전** 또는 **RuleVersion** 값을 포함 하는 규칙을 처리할 수 없습니다. *n*. *n*. *n*. 하도록 하려면 모든 규칙 처리할 수만 14 값을 포함 하는 규칙을 사용 합니다. *n*. *n*. *n*.

## 자세한 내용

[메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)

[전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 동작](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[전송 에이전트](transport-agents-exchange-2013-help.md)

