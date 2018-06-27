---
title: '전송 규칙 동작: Exchange 2013 Help'
TOCTitle: 메일 흐름 규칙 동작
ms:assetid: 5d11a955-b1cc-4150-a0b9-a8cc48ba9bde
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998315(v=EXCHG.150)
ms:contentKeyID: 50483219
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 규칙 동작

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-05-03_

메일 흐름 규칙 (전송 규칙이 라고도 함)의 작업을 규칙의 조건과 일치 하는 메시지를 수행 하기 위해 원하는 항목을 지정 합니다. 예를 중재자에 게 특정 사람이 보낸에서 메시지를 전달 하거나 모든 아웃 바운드 메시지에 고 지 사항 또는 개인 설정 된 서명을 추가 하는 규칙을 만들 수 있습니다.

작업에는 일반적으로 추가 속성이 필요합니다. 예, 규칙에서 메시지를 메시지 리디렉션을 위치를 지정 해야 합니다. 일부 작업은 여러 속성을 사용할 수 있거나 필요 합니다. 예, 메시지 헤더에 헤더 필드를 추가 하는 규칙을 하는 경우 이름과 헤더의 값을 지정 해야 합니다. 메시지에는 고 지 사항을 추가 하는 규칙을 고 지 사항 텍스트를 지정할 필요가 없지만 텍스트를 삽입할 위치 또는 고 지 사항이 메시지에 추가할 수 없는 경우 수행할 작업을 지정할 수도 있습니다. 일반적으로 규칙에서 여러 작업을 구성할 수 있습니다 하지만 일부 작업은 없습니다. 예 규칙을 하나 거부 하 고 같은 오류 메시지가 리디렉션할 수 없습니다.

Exchange Server 2013 에서 메일 흐름 규칙에 대 한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)을 참조 하십시오.

조건 및 메일 흐름 규칙에서 예외에 대 한 자세한 내용은 [전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)를 참조 하십시오.

Exchange Online 또는 Exchange Online Protection 의 메일 흐름 규칙의 작업에 대 한 자세한 내용은 [Exchange Online 흐름 규칙 동작을 메일](https://technet.microsoft.com/ko-kr/library/jj919237\(v=exchg.150\)) 또는 [메일 흐름 규칙 동작 Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj920117\(v=exchg.150\))을 참조 하십시오.

## 사서함 서버에서 메일 흐름 규칙에 대 한 작업

사서함 서버에서 메일 흐름 규칙에서 사용할 수 있는 작업은 다음 표에 설명 되어있습니다. 각 속성에 대 한 유효한 값은 속성 값 섹션에 설명 되어있습니다.

**참고**:

  - Exchange 관리 센터 (EAC) 동작을 선택한 후 표시 되는 궁극적으로 **다음을 수행** 하는 필드 값이 선택한 클릭 경로에서 서로 다른 경우가 많습니다. 또한 새 규칙을 만들 때 수행할 수 있습니다 때때로 (에 따라 선택한) 완료를 클릭 한 경로 수행 하는 대신 서식 파일 (그런 다음 필터링 된 작업 목록)에서 짧은 작업 이름을 선택 합니다. 짧은 이름 및 전체 값 표에 EAC 열에 표시 되는 경로 클릭 합니다.

  - 일부 **Get-TransportRuleAction** cmdlet에 의해 반환 되는 작업의 이름을 해당 하는 매개 변수 이름이 보다 다른 되며 여러 매개 변수는 작업에 대 한 필요할수도 있습니다.


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
<th>EAC에서 함수</th>
<th>Exchange 관리 셸 에서 action 매개 변수</th>
<th>속성</th>
<th>설명</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>이러한 사람에 게 승인을 위해 메시지를 전달 합니다.</strong></p>
<p><strong>승인을 위해 메시지 음성 메일로 착신 전환</strong> &gt; <strong>이러한 사람에 게</strong></p></td>
<td><p><em>ModerateMessageByUser</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>승인 요청에서 래핑된 첨부 파일로 지정 된 중재자에 게 메시지를 전달 합니다. 자세한 내용은 <a href="common-message-approval-scenarios-exchange-2013-help.md">일반적인 메시지 승인 시나리오</a>을 참조 하십시오. 메일 그룹을 사용 하 여 중재자 수는 없습니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>보낸 사람의 관리자에 게 승인을 위해 메시지 전달</strong></p>
<p><strong>승인을 위해 메시지 음성 메일로 착신 전환</strong> &gt; <strong>보낸 사람의 관리자에 게</strong></p></td>
<td><p><em>ModerateMessageByManager</em></p></td>
<td><p>해당 없음</p></td>
<td><p>승인을 위해 보낸 사람의 관리자에 게 메시지를 전달 합니다.</p>
<p>이 매크로 함수는 보낸 사람의 <strong>Manager</strong> 특성이 Active Directory 에 정의 된 경우에 작동 합니다. 그렇지 않은 경우 메시지는 중재 없이 받는 사람에 게 배달 됩니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>이러한 받는 사람에 게 메시지를 리디렉션</strong></p>
<p><strong>메시지를 리디렉션</strong> &gt; <strong>이러한 받는 사람</strong></p></td>
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정 된 받는 사람에 게 메시지를 리디렉션합니다. 원래 받는 사람에 게 메시지가 배달 되지 하 고 보낸 사람이 나 원래 받는 사람에 알림이 전송 됩니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지를 거부하고 설명 포함</strong></p>
<p><strong>메시지 차단</strong> &gt; <strong>메시지를 거부 하 고 설명 포함</strong></p></td>
<td><p><em>RejectMessageReasonText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>거부 이유도 지정 된 텍스트가 있는 배달 못함 보고서 (라고도 하는 NDR 또는 튀어오르 메시지로)에서 보낸사람에 게 메시지를 반환합니다. 받는 사람을 원본 메시지 또는 알림을 수신 하지 못합니다.</p>
<p>사용 되는 기본 확장 상태 코드는 <code>5.7.1</code>.</p>
<p>만들거나 Exchange 관리 셸 에서 규칙을 수정 하는 경우에 <em>RejectMessageEnhancedStatusCode</em> 매개 변수를 사용 하 여 DSN 코드를 지정할 수 있습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지를 거부하고 확장 상태 코드 포함</strong></p>
<p><strong>메시지 차단</strong> &gt; <strong>의 확장된 상태 코드를 통해 메시지를 거부 합니다.</strong></p></td>
<td><p><em>RejectMessageEnhancedStatusCode</em></p></td>
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>지정 된 향상 된 배달 상태 알림 (DSN) 코드가 포함 된 NDR에 보낸 사람에 게 메시지를 반환합니다. 받는 사람을 원본 메시지 또는 알림을 수신 하지 못합니다.</p>
<p>유효한 DSN 코드는 <code>5.7.1</code> 또는 <code>5.7.999</code>를 통해 <code>5.7.900</code> 입니다.</p>
<p>사용 되는 기본 이유 텍스트는 <code>Delivery not authorized, message refused</code>합니다.</p>
<p>만들거나 Exchange 관리 셸 에서 규칙을 수정 하는 경우에 <em>RejectMessageReasonText</em> 매개 변수를 사용 하 여 거부 이유 텍스트를 지정할 수 있습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>아무에게도 알리지 않고 메시지 삭제</strong></p>
<p><strong>메시지 차단</strong> &gt; <strong>아무 에게도 알리지 않고 메시지 삭제</strong></p></td>
<td><p><em>DeleteMessage</em></p></td>
<td><p>해당 없음</p></td>
<td><p>받는 사람이 나 보낸사람에 게 알림을 보내지 않고 해당 메시지를 자동으로 삭제 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>숨은 참조 상자에 받는 사람 추가</strong></p>
<p><strong>받는 사람 추가</strong> &gt; <strong>숨은 참조 상자에</strong></p></td>
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지의 <strong>Bcc</strong> 필드에 하나 이상의 받는 사람을 추가합니다. 원래 받는 사람에 게 통보 되지 하 고 추가 주소 볼 수는 없습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람 상자에 받는 사람 추가</strong></p>
<p><strong>추가 받는 사람</strong> &gt; <strong>받는 사람 상자에</strong></p></td>
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지의 <strong>To</strong> 필드에 하나 이상의 받는 사람을 추가합니다. 원래 받는 사람 추가 주소를 볼 수 있습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>참조란에 받는 사람 추가</strong></p>
<p><strong>추가 받는 사람</strong> &gt; <strong>참조 상자에</strong></p></td>
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지의 <strong>Cc</strong> 필드에 하나 이상의 받는 사람을 추가합니다. 원래 받는 사람 추가 주소를 볼 수 있습니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람으로 보낸 사람의 관리자를 추가 합니다.</strong></p>
<p><strong>추가 받는 사람</strong> &gt; <strong>받는 사람으로 보낸 사람의 관리자를 추가 합니다.</strong></p></td>
<td><p><em>AddManagerAsRecipientType</em></p></td>
<td><p><code>AddedManagerAction</code></p></td>
<td><p>지정 된 받는 사람 유형 (<strong>To</strong>, <strong>Cc</strong>, <strong>Bcc</strong>)으로 메시지를 보낸 사람의 관리자를 추가 하거나 보낸 사람의 관리자에 게 보낸 사람이 나 받는 사람에 게 알리지 않고 메시지를 리디렉션합니다.</p>
<p>이 매크로 함수는 보낸 사람의 <strong>Manager</strong> 특성이 Active Directory 에 정의 된 경우에 작동 합니다.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>고지 사항 추가</strong></p>
<p><strong>적용 되는 메시지에는 고 지 사항</strong> &gt; <strong>는 고 지 사항 추가</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>첫 번째 속성: <code>DisclaimerText</code></p>
<p>두번째 속성: <code>DisclaimerFallbackAction</code></p>
<p>세번째 속성 (Exchange 관리 셸 에 해당): <code>DisclaimerTextLocation</code></p></td>
<td><p>메시지의 끝에 지정 된 HTML 고 지 사항을 적용합니다.</p>
<p>만들거나 Exchange 관리 셸 에서 규칙을 수정 하는 경우 값 <code>Append</code>함께 <em>ApplyHtmlDisclaimerTextLocation</em> 매개 변수를 사용 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>고지 사항 앞에 추가</strong></p>
<p><strong>적용 되는 메시지에는 고 지 사항</strong> &gt; <strong>는 고 지 사항 앞에 추가</strong></p></td>
<td><p><em>ApplyHtmlDisclaimerText</em></p>
<p><em>ApplyHtmlDisclaimerFallbackAction</em></p>
<p><em>ApplyHtmlDisclaimerTextLocation</em></p></td>
<td><p>첫 번째 속성: <code>DisclaimerText</code></p>
<p>두번째 속성: <code>DisclaimerFallbackAction</code></p>
<p>세번째 속성 (Exchange 관리 셸 에 해당): <code>DisclaimerTextLocation</code></p></td>
<td><p>메시지의 시작 부분에 지정 된 HTML 고 지 사항을 적용합니다.</p>
<p>만들거나 Exchange 관리 셸 에서 규칙을 수정 하는 경우 값 <code>Prepend</code>함께 <em>ApplyHtmlDisclaimerTextLocation</em> 매개 변수를 사용 합니다.</p>
<p></p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>다음 헤더 제거</strong></p>
<p><strong>메시지 속성 수정</strong> &gt; <strong>메시지 헤더를 제거 합니다.</strong></p></td>
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>메시지 헤더에서 지정 된 헤더 필드를 제거합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>메시지 헤더를 이 값으로 설정</strong></p>
<p><strong>메시지 속성 수정</strong> &gt; <strong>메시지 헤더를 설정 합니다.</strong></p></td>
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>첫번째 속성: <code>MessageHeaderField</code></p>
<p>두번째 속성: <code>String</code></p></td>
<td><p>추가 또는 메시지 헤더에 지정 된 헤더 필드를 수정 하 고 헤더 필드에 지정 된 값을 설정 하는.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지 분류 적용</strong></p>
<p><strong>메시지 속성 수정</strong> &gt; <strong>메시지 분류 적용</strong></p></td>
<td><p><em>ApplyClassification</em></p></td>
<td><p><code>MessageClassification</code></p></td>
<td><p>메시지에 지정 된 메시지 분류를 적용합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>신뢰도 scl (스팸)로 설정</strong></p>
<p><strong>메시지 속성 수정</strong> &gt; <strong>는 신뢰도 scl (스팸)를 설정 합니다.</strong></p></td>
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>신뢰도 scl (스팸) 메시지의 지정 된 값으로 설정합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>다음을 포함하는 메시지에 권한 보호 적용</strong></p>
<p><strong>메시지 보안 수정</strong> &gt; <strong>권한 보호 적용</strong></p></td>
<td><p><em>ApplyRightsProtectionTemplate</em></p></td>
<td><p><code>RMSTemplate</code></p></td>
<td><p>지정된 RMS(Rights Management Services) 템플릿을 메시지에 적용합니다.</p>
<p>RMS 각 사서함에 대 한 Exchange 엔터프라이즈 클라이언트 액세스 라이선스 (Cal) 필요합니다. Cal에 대 한 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 라이선스</a>를 참조 하십시오.</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>TLS 암호화 필요</strong></p>
<p><strong>메시지 보안 수정</strong> &gt; <strong>TLS 암호화 필요</strong></p></td>
<td><p><em>RouteMessageOutboundRequireTls</em></p></td>
<td><p><code>n/a</code></p></td>
<td><p>아웃 바운드 메시지는 TLS를 통해 라우팅할 수를 적용 하는 연결을 암호화 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>메시지 제목 앞에 다음 추가</strong></p></td>
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>메시지의 <strong>Subject</strong> 필드의 시작 부분에 지정된 된 텍스트를 추가합니다. 원래 제목 텍스트를 구별 하기 위해 지정된 된 텍스트의 마지막 문자로 공백이 나 콜론 (:)를 사용 하 여 하는 것이 좋습니다.</p>
<p>를 방지 하기 위해 동일한 문자열에서 이미 제목 (예: 회신)에서 텍스트를 포함 하는 메시지에 추가 되는 규칙에 (<em>ExceptIfSubjectContainsWords</em>) <strong>제목에 다음 포함</strong> 예외를 추가 합니다.</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>정책 팁과 함께 보낸 사람에게 알림</strong></p></td>
<td><p><em>NotifySender</em></p>
<p><em>RejectMessageReasonText</em></p>
<p><em>RejectMessageEnhancedStatusCode</em> (Exchange 관리 셸 에 해당)</p></td>
<td><p>첫번째 속성: <code>NotifySenderType</code></p>
<p>두번째 속성: <code>String</code></p>
<p>세번째 속성 (Exchange 관리 셸 에 해당): <code>DSNEnhancedStatusCode</code></p></td>
<td><p>보낸사람에 게 알리는 또는 DLP 정책 일치 하는 경우 메시지를 차단 합니다.</p>
<p><strong>메시지에 중요 한 정보 포함</strong> (<em>MessageContainsDataClassification</em> 조건을 사용 하 여 해야이 함수를 사용 하는 경우</p>
<p>만들거나 Exchange 관리 셸 에서 규칙을 수정 하는 경우 <em>RejectMessageReasonText</em> 매개 변수는 선택 사항입니다. 이 매개 변수를 사용 하지 않으면 기본 텍스트 <code>Delivery not authorized, message refused</code> 사용 됩니다.</p>
<p>또한 Exchange 관리 셸, 확장된 상태 코드를 지정 하려면 <em>RejectMessageEnhancedStatusCode</em> 매개 변수는을 사용할 수 있습니다. 이 매개 변수를 사용 하지 않으면 기본 확장 상태 코드 <code>5.7.1</code> 사용 됩니다.</p>
<p>이 매크로 함수는 다른 조건, 예외 및 규칙에 구성할 수 있는 작업을 제한 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>문제 보고서를 생성하여 보낼 사람</strong></p></td>
<td><p><em>GenerateIncidentReport</em></p>
<p><em>IncidentReportContent</em></p></td>
<td><p>첫 번째 속성: <code>Addresses</code></p>
<p>두 번째 속성: <code>IncidentReportContent</code></p></td>
<td><p>지정 된 받는 사람에 게 지정된 된 콘텐츠를 포함 하는 문제 보고서를 보냅니다.</p>
<p>조직에서 데이터 손실 방지 (DLP) 정책에 맞는 메시지에 대 한 문제 보고서 생성 됩니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>받는 사람에게 메시지로 알림</strong></p></td>
<td><p><em>GenerateNotification</em></p></td>
<td><p><code>NotificationMessageText</code></p></td>
<td><p>텍스트, HTML 태그 및 해당 메시지의 받는 사람에 게 전송 된 알림 메시지에 포함할 메시지 키워드를 지정 합니다. 예, 메시지 된 규칙에 의해 거부 또는 스팸으로 표시 및 자신의 정크 메일 폴더에 전달 되는 받는 사람에 게 알릴 수 있습니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="odd">
<td><p><strong>이 규칙의 속성</strong> 섹션 &gt; <strong>심각도 수준으로이 규칙 감사</strong></p></td>
<td><p><em>SetAuditSeverity</em></p></td>
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>지정 여부:</p>
<ul>
<li><p>문제 보고서 및 메시지 추적 로그에에서 항목을 해당 항목의 생성을 하지 못했습니다.</p></li>
<li><p>지정한 심각도 수준 (낮음, 보통, 또는 높음) 사용 하 여 메시지 추적 로그에서 문제 보고서와 해당 항목을 생성 합니다.</p></li>
</ul></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
<tr class="even">
<td><p><strong>이 규칙의 속성</strong> 섹션 &gt; <strong>추가 규칙 처리 중지</strong></p>
<p><strong>기타 옵션</strong> &gt; <strong>이 규칙의 속성</strong> 섹션 &gt; <strong>추가 규칙 처리 중지</strong></p></td>
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지 규칙에 의해 영향을 받는 후 메시지는 다른 규칙에 의해 처리에서 제외 됨을 지정 합니다.</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## Edge 전송 서버에서 메일 흐름 규칙에 대 한 작업

사서함 서버에서 사용할 수 있는 작업의 작은 하위도 Edge 전송 서버에서 사용할 수 있지만 에서만 Edge 전송 서버에서 사용할 수 있는 일부 작업도 있습니다. 방법이 없는 EAC Edge 전송 서버에서 로컬 Edge 전송 서버에서 Exchange 관리 셸 의 메일 흐름 규칙만 관리할 수 있도록 합니다. 작업은 다음 표에 설명 되어있습니다. 속성 형식 속성 값 섹션에 설명 되어있습니다.


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
<th>Exchange 관리 셸 에서 action 매개 변수</th>
<th>속성</th>
<th>설명</th>
<th>사용 가능한 버전</th>
<th>사용 가능한 위치</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>AddToRecipients</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지의 <strong>To</strong> 필드에 하나 이상의 받는 사람을 추가합니다. 원래 받는 사람 추가 주소를 볼 수 있습니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>BlindCopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지의 <strong>Bcc</strong> 필드에 하나 이상의 받는 사람을 추가합니다. 원래 받는 사람에 게 통보 되지 하 고 추가 주소 볼 수는 없습니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>CopyTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>메시지의 <strong>Cc</strong> 필드에 하나 이상의 받는 사람을 추가합니다. 원래 받는 사람 추가 주소를 볼 수 있습니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>DeleteMessage</em></p></td>
<td><p>해당 없음</p></td>
<td><p>받는 사람이 나 보낸사람에 게 알림을 보내지 않고 해당 메시지를 자동으로 삭제 합니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>Disconnect</em></p></td>
<td><p>해당 없음</p></td>
<td><p>NDR을 생성 하지 않고 보내는 서버와 Edge 전송 서버 간의 SMTP 연결을 종료 합니다.</p></td>
<td><p>Edge 전송 서버에만</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>LogEventText</em></p></td>
<td><p><code>String</code></p></td>
<td><p>로컬 Edge 전송 서버에 대 한 응용 프로그램 로그에 지정된 된 텍스트를 사용 하 여 이벤트를 생성합니다. 항목은 다음과 같은 정보가 표시 됩니다.</p>
<ul>
<li><p><strong>수준</strong> <code>Information</code>   </p></li>
<li><p><strong>원본</strong> <code>MSExchange Messaging Policies</code>   </p></li>
<li><p><strong>이벤트 ID</strong> <code>4000</code>   </p></li>
<li><p><strong>작업 범주</strong> <code>Rules</code>   </p></li>
<li><p><strong>EventData</strong>   <code>The following message is logged by an action in the rules: &lt;text you specify&gt;.</code></p></li>
</ul></td>
<td><p>Edge 전송 서버에만</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>PrependSubject</em></p></td>
<td><p><code>String</code></p></td>
<td><p>메시지의 <strong>Subject</strong> 필드의 시작 부분에 지정된 된 텍스트를 추가합니다. 원래 주제를 구별 하기 위해 지정된 된 텍스트의 마지막 문자로 공백이 나 콜론 (:)를 사용 하 여 하는 것이 좋습니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>Quarantine</em></p></td>
<td><p>해당 없음</p></td>
<td><p>콘텐츠 필터링에서 Edge 전송 서버 구성에에서 정의 된 격리 사서함에 메시지를 배달 합니다. 자세한 내용은 <a href="configure-a-spam-quarantine-mailbox-exchange-2013-help.md">스팸 격리 사서함 구성</a>을 참조 하십시오.</p>
<p>격리 사서함이 구성 되지 않은 경우 메시지가 NDR에 보낸 사람에 게 반환 됩니다.</p></td>
<td><p>Edge 전송 서버에만</p></td>
<td><p>Exchange 2010 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>RedirectMessageTo</em></p></td>
<td><p><code>Addresses</code></p></td>
<td><p>지정 된 받는 사람에 게 메시지를 리디렉션합니다. 원래 받는 사람에 게 메시지가 배달 되지 하 고 보낸 사람이 나 원래 받는 사람에 알림이 전송 됩니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>RemoveHeader</em></p></td>
<td><p><code>MessageHeaderField</code></p></td>
<td><p>메시지 헤더에서 지정 된 헤더 필드를 제거합니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>SetHeaderName</em></p>
<p><em>SetHeaderValue</em></p></td>
<td><p>첫번째 속성: <code>MessageHeaderField</code></p>
<p>두번째 속성: <code>String</code></p></td>
<td><p>추가 또는 메시지 헤더에 지정 된 헤더 필드를 수정 하 고 헤더 필드에 지정 된 값을 설정 하는.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>SetSCL</em></p></td>
<td><p><code>SCLValue</code></p></td>
<td><p>지정 된 값으로 메시지의 SCL을 설정합니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="odd">
<td><p><em>SmtpRejectMessageRejectText</em></p>
<p><em>SmtpRejectMessageRejectStatusCode</em></p></td>
<td><p>첫번째 속성: <code>String</code></p>
<p>두번째 속성: <code>SMTPStatusCode</code></p></td>
<td><p>보내는 서버와 지정된 된 SMTP 상태 코드 및 지정 된 거부 텍스트와 Edge 전송 서버 간의 SMTP 연결을 종료합니다. 받는 사람을 원본 메시지 또는 알림을 수신 하지 못합니다.</p>
<p>SMTP 상태 코드에 대 한 유효한 값은 <code>500</code> RFC 3463에 정의 된를 통해 <code>400</code> 정수입니다.</p>
<p>SMTP 상태 코드를 지정 하지 않고 거부 텍스트를 지정 하는 경우에 기본 코드 <code>550</code> 사용 됩니다.</p>
<p>거부 텍스트를 지정 하지 않고 SMTP 상태 코드를 지정 하는 경우 사용 되는 텍스트 <code>Delivery not authorized, message refused</code>됩니다.</p></td>
<td><p>Edge 전송 서버에만</p></td>
<td><p>Exchange 2007 이상</p></td>
</tr>
<tr class="even">
<td><p><em>StopRuleProcessing</em></p></td>
<td><p>해당 없음</p></td>
<td><p>메시지 규칙에 의해 영향을 받는 후 메시지는 다른 규칙에 의해 처리에서 제외 됨을 지정 합니다.</p></td>
<td><p>사서함 서버 및 Edge 전송 서버</p></td>
<td><p>Exchange 2013 이상</p></td>
</tr>
</tbody>
</table>


## 속성 값

메일 흐름 규칙의 작업에 사용 되는 속성 값은 다음 표에 설명 되어있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>속성</th>
<th>유효한 값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>AddedManagerAction</code></p></td>
<td><p>다음 값 중 하나입니다.</p>
<ul>
<li><p><strong>종료</strong></p></li>
<li><p><strong>참조</strong></p></li>
<li><p><strong>숨은 참조</strong></p></li>
<li><p><strong>리디렉션</strong></p></li>
</ul></td>
<td><p>메시지에 보낸 사람의 관리자를 포함 하는 방법을 지정 합니다.</p>
<ul>
<li><p><strong>받는</strong> 사람, <strong>참조</strong> 또는 <strong>숨은 참조</strong> 를 선택 하는 경우 보낸 사람의 관리자는 지정된 된 필드에 대 한 받는 사람으로 추가 됩니다.</p></li>
<li><p><strong>리디렉션</strong> 을 선택 하는 경우 메시지는만 배달 보낸 사람의 관리자에 게 보낸 사람이 나 받는 사람에 게 알리지 않고.</p></li>
</ul>
<p>이 매크로 함수는 보낸 사람의 <strong>Manager</strong> 특성이 Active Directory 에 정의 된 경우에 작동 합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Addresses</code></p></td>
<td><p>Exchange 받는 사람</p></td>
<td><p>작업에 따라를 조직의 모든 메일 사용이 가능한 개체를 지정할 수 또는 특정 개체 형식에 제한 될 수 있습니다. 일반적으로 여러 받는 사람을 선택할 수 있지만 한 명의 받는 사람을만 문제 보고서를 보낼 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditSeverityLevel</code></p></td>
<td><p>다음 값 중 하나입니다.</p>
<ul>
<li><p><strong>감사 심각도 수준으로이 규칙</strong> 선택을 취소 하거나 <strong>지정 되지 않은</strong> (<code>DoNotAudit</code>) 값을 가진 <strong>감사 심각도 수준으로이 규칙을</strong> 선택 합니다.</p></li>
<li><p><strong>낮음</strong></p></li>
<li><p><strong>중간 규모</strong></p></li>
<li><p><strong>높음</strong></p></li>
</ul></td>
<td><p><strong>낮음</strong>, <strong>보통</strong> 또는 <strong>높은</strong> 값에는 문제 보고서에 및 메시지 추적 로그에에서 항목을 해당 항목에 할당 된 심각도 수준을 지정 합니다.</p>
<p>문제 보고서 생성 되 고 하는 것을 금지 하 고 해당 항목의 메시지 추적 로그에 기록 되 고 하지 않도록 설정 하는 다른 값 합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerFallbackAction</code></p></td>
<td><p>다음 값 중 하나입니다.</p>
<ul>
<li><p><strong>텍스트 배치</strong></p></li>
<li><p><strong>무시</strong></p></li>
<li><p><strong>거부 합니다.</strong></p></li>
</ul></td>
<td><p>고 지 사항이 메시지에 적용할 수 없습니다 하는 경우 수행할 작업을 지정 합니다. 메시지의 내용을 변경할 수 없게 하는 경우가 있습니다 (메시지 암호화 등). 사용 가능한 대체 동작은 다음과 같습니다.</p>
<ul>
<li><p><strong>줄바꿈</strong>    원래 메시지가 새 메시지 봉투를에서 포장 되 고 새 메시지에 고 지 사항 텍스트 삽입 됩니다. 값은 기본값입니다.</p>
<p><strong>참고</strong>:</p>
<ul>
<li><p>후속 메일 흐름 규칙은 새 메시지 봉투 원본 메시지는 적용 되지 않음에 적용 됩니다. 따라서 다른 규칙 보다 낮은 우선순위 이러한 규칙을 구성 합니다.</p></li>
<li><p>새 메시지 봉투의 원본 메시지에 배치할 수 없습니다, 원본 메시지 배달 되지 않습니다. NDR에 보낸 사람에 게 메시지가 반환 됩니다.</p></li>
</ul></li>
<li><p><strong>무시</strong>    규칙이 무시 되 고 메시지가 고 지 사항 없이 배달 됩니다.</p></li>
<li><p><strong>거부 합니다.</strong>    NDR에 보낸 사람에 게 메시지가 반환 됩니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DisclaimerText</code></p></td>
<td><p>HTML 문자열</p></td>
<td><p>IMG 태그를 사용 하 여 HTML 태그, 인라인 계단식 스타일 시트 (CSS) 태그 및 이미지를 포함할 수 있는 고 지 사항 텍스트를 지정 합니다. 최대 길이 5000 문자, 태그를 포함 합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>DisclaimerTextLocation</code></p></td>
<td><p>단일 값: <code>Append</code> 또는 <code>Prepend</code></p></td>
<td><p>Exchange 관리 셸, <em>ApplyHtmlDisclaimerTextLocation</em> 를 사용 하 여 메시지에 고 지 사항 텍스트의 위치를 지정 합니다.</p>
<ul>
<li><p><code>Append</code>   고 지 사항이 메시지 본문의 끝에 추가 합니다. 값은 기본값입니다.</p></li>
<li><p><code>Prepend</code>   고 지 사항이 메시지 본문의 시작 부분에 추가 합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>DSNEnhancedStatusCode</code></p></td>
<td><p>단일 DSN 코드 값:</p>
<ul>
<li><p><code>5.7.1</code></p></li>
<li><p><code>5.7.999</code> 를 통해 <code>5.7.900</code></p></li>
</ul></td>
<td><p>사용 되는 DSN 코드를 지정 합니다. <strong>New-SystemMessage</strong> cmdlet을 사용 하 여 사용자 지정 Dsn을 만들 수 있습니다.</p>
<p>DSN 코드와 함께 거부 이유 텍스트를 지정 하지 않으면 하는 경우 사용 되는 기본 이유 텍스트 <code>Delivery not authorized, message refused</code>됩니다.</p>
<p>만들거나 Exchange 관리 셸 에서 규칙을 수정 하는 경우에 <em>RejectMessageReasonText</em> 매개 변수를 사용 하 여 거부 이유 텍스트를 지정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>IncidentReportContent</code></p></td>
<td><p>다음 값 중 하나 이상</p>
<ul>
<li><p><strong>보낸사람</strong></p></li>
<li><p><strong>받는 사람</strong></p></li>
<li><p><strong>제목</strong></p></li>
<li><p><strong>참조 된 받는 사람</strong> (<code>Cc</code>)</p></li>
<li><p><strong>숨은 참조로 받는 사람에 게 지정 된</strong> (<code>Bcc</code>)</p></li>
<li><p><strong>심각도</strong></p></li>
<li><p><strong>보낸 사람이 재정의 정보</strong> (<code>Override</code>)</p></li>
<li><p><strong>일치 규칙</strong> (<code>RuleDetections</code>)</p></li>
<li><p><strong>잘못 된 보고서</strong> (<code>FalsePositive</code>)</p></li>
<li><p><strong>감지 데이터 분류</strong> (<code>DataClassifications</code>)</p></li>
<li><p><strong>콘텐츠와 일치 하는</strong> (<code>IdMatch</code>)</p></li>
<li><p><strong>원래 메일</strong> (<code>AttachOriginalMail</code>)</p></li>
</ul></td>
<td><p>문제 보고서에 포함할 원래 메시지 속성을 지정 합니다. 이러한 속성의 조합이 포함 하도록 선택할 수 있습니다. 지정 하는 속성, 외에도 메시지 ID는 항상 포함 됩니다. 사용할 수 있는 속성은입니다.</p>
<ul>
<li><p><strong>보낸사람</strong>   원본 메시지의 보낸사람입니다.</p></li>
<li><p><strong>받는 사람</strong>, <strong>참조 된 받는 사람</strong>, 및 <strong>숨은 참조로 받는 사람에 게 지정 된</strong> 메시지의 모든 받는 사람 또는 <strong>Cc</strong> 또는 <strong>Bcc</strong> 필드에 있는 받는 사람만 합니다. 각 속성에 대 한 처음 10 명의 받는 사람 문제 보고서에 포함 됩니다.</p></li>
<li><p><strong>제목</strong>    원본 메시지의 <strong>Subject</strong> 필드입니다.</p></li>
<li><p><strong>심각도</strong>    트리거된 규칙의 감사 심각도입니다. 메시지 추적 로그 감사 심각도 수준을 모두 포함 하 고 감사 심각도 의해 필터링 될 수 있습니다. EAC에서의 Exchange 관리 셸, <em>SetAuditSeverity</em> 매개 변수 값 <code>DoNotAudit</code>), (에서 <strong>심각도 수준으로이 규칙 감사</strong> 확인란의 선택을 취소 하면 규칙 보고서에 규칙과 일치 나타나지 않습니다. 둘 이상의 규칙에 의해 메시지를 처리 하는 경우 가장 높은 심각도 모든 문제 보고서에 포함 됩니다.</p></li>
<li><p><strong>보낸 사람이 재정의 정보</strong>    보낸 사람이 정책 팁을 무시 하도록 선택한 경우 재정의 합니다. 보낸 사람이 한 근거를 제공 하는 경우 양쪽 맞춤의 처음 100 자도 포함 됩니다.</p></li>
<li><p><strong>일치 규칙</strong>    메시지가 트리거된 규칙의 목록입니다.</p></li>
<li><p><strong>잘못 된 보고서</strong>    가양성 보낸 사람이 정책 팁에 대 한 메시지를 가양성으로 표시 하는 경우.</p></li>
<li><p><strong>감지 데이터 분류</strong>    메시지에서 검색 된 중요 한 정보 유형 목록입니다.</p></li>
<li><p><strong>콘텐츠와 일치 하는</strong>    중요 한 정보 검색 되는 유형, 메시지를 150 자를의 일치 하는 콘텐츠를 정확 하 게 일치 된 중요 정보 전후 합니다.</p></li>
<li><p><strong>원래 메일</strong>   규칙이 트리거되는 전체 메시지 문제 보고서에 연결 됩니다.</p></li>
</ul>
<p>Exchange 관리 셸 쉼표로 구분 하 여 여러 값을 지정 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MessageClassification</code></p></td>
<td><p>단일 메시지 분류 개체</p></td>
<td><p>EAC를 사용할 수 있는 메시지 분류의 목록에서 선택합니다.</p>
<p>Exchange 관리 셸 에서 사용할 수 있는 메시지 분류 개체를 볼 수 <strong>Get-MessageClassification</strong> cmdlet을 사용 합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MessageHeaderField</code></p></td>
<td><p>단일 문자열</p></td>
<td><p>추가, 제거 또는 수정 하려면 SMTP 메시지 헤더 필드를 지정 합니다.</p>
<p><em>메시지 헤더</em> 는 메시지에 대 한 필수 및 선택적 헤더 필드의 컬렉션입니다. 헤더 필드의 예는 <strong>To</strong>, <strong>From</strong>, <strong>Received</strong>및 <strong>Content-Type</strong>합니다. 공식 헤더 필드는 RFC 5322에 정의 됩니다. 비공식 헤더 필드 <strong>X-</strong> 로 시작 하 고 <em>X-헤더</em>로 알려져 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>NotificationMessageText</code></p></td>
<td><p>일반 텍스트, HTML 태그 및 키워드 조합</p></td>
<td><p>받는 사람 알림 메시지에서 사용 하 여 텍스트를 지정 합니다.</p>
<p>일반 텍스트 및 HTML 태그 외에도 원본 메시지의 값을 사용 하는 다음과 같은 키워드를 지정할 수 있습니다.</p>
<ul>
<li><p><code>%%From%%</code></p></li>
<li><p><code>%%To%%</code></p></li>
<li><p><code>%%Cc%%</code></p></li>
<li><p><code>%%Subject%%</code></p></li>
<li><p><code>%%Headers%%</code></p></li>
<li><p><code>%%MessageDate%%</code></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>NotifySenderType</code></p></td>
<td><p>다음 값 중 하나입니다.</p>
<ul>
<li><p><strong>보낸사람에 게 알림 하지만 보낼 수 있도록 허용</strong> (<code>NotifyOnly</code>)</p></li>
<li><p><strong>메시지 차단</strong> (<code>RejectMessage</code>)</p></li>
<li><p><strong>가양성 하지 않은 메시지를 차단 합니다.</strong> (<code>RejectUnlessFalsePositiveOverride</code>)</p></li>
<li><p><strong>메시지를 차단 하지만 보낸 사람이 재정의 하 고 보내도록 허용</strong> (<code>RejectUnlessSilentOverride</code>)</p></li>
<li><p><strong>메시지를 차단 하지만 보낸 사람이 업무상의 이유에와 재정의 하 고 보내도록 허용</strong> (<code>RejectUnlessExplicitOverride</code>)</p></li>
</ul></td>
<td><p>보낸 사람이 메시지를 DLP 정책 위반 하는 경우 수신 하는 정책 팁의 유형을 지정 합니다. 다음 목록에는 설정은 설명 합니다.</p>
<ul>
<li><p><strong>보낸사람에 게 알림 하지만 보낼 수 있도록 허용</strong> 보낸사람에 게 알리지만 메시지는 정상적으로 배달 됩니다.</p></li>
<li><p><strong>메시지 차단</strong> 메시지는 거부 하 고 보낸 사람에 게 알립니다.</p></li>
<li><p><strong>가양성 하지 않은 메시지를 차단 합니다.</strong> 보낸 사람이 가양성으로 표시 한 경우에 메시지가 거부 됩니다.</p></li>
<li><p><strong>메시지를 차단 하지만 보낸 사람이 재정의 하 고 보내도록 허용</strong> 보낸 사람이 정책 제한을 무시 하도록 선택한 경우에 메시지가 거부 됩니다.</p></li>
<li><p><strong>메시지를 차단 하지만 보낸 사람이 업무상의 이유에와 재정의 하 고 보내도록 허용</strong> 이것은 <strong>메시지를 차단 하지만 보낸 사람이 재정의 하 고 보내도록 허용</strong> 형식 비슷합니다 하지만 보낸 사람이 정책 제한을 무시 한 근거를 제공 합니다.</p></li>
</ul>
<p>이 매크로 함수를 사용 하면 (<em>MessageContainsDataClassification</em>) <strong>메시지에 중요 한 정보가 포함</strong> 조건을 사용 해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>RMSTemplate</code></p></td>
<td><p>단일 RMS template 개체</p></td>
<td><p>메시지에 적용 되는 서비스 RMS (권한 관리) 서식 파일을 지정 합니다.</p>
<p>EAC에서 목록에서 RMS 템플릿을 선택 합니다.</p>
<p>Exchange 관리 셸 에서 사용할 수 있는 RMS 서식 파일을 볼 수 <strong>Get-RMSTemplate</strong> cmdlet을 사용 합니다.</p>
<p>RMS 각 사서함에 대 한 Exchange 엔터프라이즈 클라이언트 액세스 라이선스 (Cal) 필요합니다. Cal에 대 한 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=237292">Exchange Server 라이선스</a>를 참조 하십시오.</p></td>
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
<td><p><code>String</code></p></td>
<td><p>단일 문자열</p></td>
<td><p>지정 된 메시지 헤더 필드, NDR, 또는 이벤트 로그 항목에 적용 되는 텍스트를 지정 합니다.</p>
<p>Exchange 관리 셸, 값에 공백이 포함 하는 경우 큰따옴표 (&quot;) 값을 묶습니다.</p></td>
</tr>
</tbody>
</table>


맨위로 돌아가기

## 자세한 내용

[메일 흐름 규칙 관리](manage-mail-flow-rules-exchange-2013-help.md)

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Exchange Online 흐름 규칙 동작을 메일](https://technet.microsoft.com/ko-kr/library/jj919237\(v=exchg.150\)) - Exchange Online

Exchange Online Protection의 [메일 흐름 규칙 동작 Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj920117\(v=exchg.150\))

[조직 전체의 메시지 법적 고 지 사항, 서명, 바닥글 또는 Office 365에서 머리글](https://technet.microsoft.com/ko-kr/library/dn600323\(v=exchg.150\))

