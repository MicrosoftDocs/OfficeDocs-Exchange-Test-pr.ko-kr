---
title: '메일 흐름 규칙을 구성 하기 위한 모범 사례: Exchange Online Protection Help'
TOCTitle: 메일 흐름 규칙을 구성 하기 위한 모범 사례
ms:assetid: abd863c3-c0ce-42f3-9470-a573adc3cbba
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn960147(v=EXCHG.150)
ms:contentKeyID: 65211631
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 흐름 규칙을 구성 하기 위한 모범 사례

 

_**적용 대상:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

일반적인 구성 오류를 방지 하기 위해 이러한 Exchange 전송 규칙에 대 한 모범 사례 권장 사항을 따릅니다. 각 것이 좋습니다 예 및 단계별 지침과 함께 항목에 연결 합니다.

## 규칙 테스트

사용자의 전자 메일에 예기치 않은 작업을 수행할 수 없습니다 하 고 있는지 확인 하 고 있는 실제로 있는지 확인 하려면 비즈니스, 법률 또는 규정 준수 의도 규칙의 모임 사용할 철저 하 게 테스트 해야 합니다. 다양 한 옵션 및 수 있으므로 규칙과 일치 하는 사용자와 실수로 너무 일반 규칙을 수행한 경우에 규칙 일치 하지 않게 것으로 예상 하는 테스트 메시지에 중요 규칙 서로 상호작용할 수 있습니다. 규칙을 테스트 하는 것에 대 한 모든 옵션 [메일 흐름 규칙을 테스트 합니다.](test-a-mail-flow-rule-exchange-2013-help.md)를 참조 하십시오.

## 규칙의 범위

하도록 하려는 메시지에만 적용 하는 규칙 있는지 확인 하십시오. 예를 들어:

  - **으로 들어오는 또는 조직 외부로 이동 하는 메시지에 규칙을 제한 합니다.**
    
    기본적으로 새 규칙 중 하나 또는 받는 조직에서 사용자가 받은 메시지에 적용 됩니다. 따라서 하나만 방식으로 적용 하려면 규칙을 사용 하도록 하려는 경우 해야 하는 규칙에 대 한 조건에 지정 합니다. 예, [일반적인 첨부 파일 차단 시나리오](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)을 참조 하십시오.

  - **보낸 사람의 또는 수신자의 도메인에 따라 규칙 제한**
    
    기본적으로 새 규칙에서 보내거나 받은 모든 도메인에서 메시지에 적용 됩니다. 규칙을 하나의 도메인 또는 하나를 제외한 다른 모든 도메인에 적용 하는 경우가 있습니다. 예제를 보려면 [Office 365에서 조직 수준의 수신 허용-보낸사람 또는 수신된 거부 목록 만들기](https://technet.microsoft.com/ko-kr/library/dn198251\(v=exchg.150\))를 참조 하십시오.

모든 조건 및 전송 규칙에 사용할 수 있는 예외의 전체 목록은, 다음을 참조 합니다.

  - [Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)](https://technet.microsoft.com/ko-kr/library/jj919235\(v=exchg.150\))

  - [전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

  - [메일 흐름 규칙 조건 및 예외 (조건자) Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj919234\(v=exchg.150\))

## 두 규칙이 필요한 경우 파악

원하는 작업을 수행 하는 두 규칙 걸리는 경우가 종종 있습니다. 전송 규칙은 여러 규칙 같은 메시지에 적용할 수 있도록 순서로 처리 됩니다. 예, 작업 중 하나는 메시지를 차단 하는 것 권한도 예: 보낸 사람의 관리자에 게 메시지를 복사 또는 알림 메시지의 제목을 변경 적용 하려는 다른 작업 하는 경우 두 규칙이 해야 합니다. 첫번째 규칙이 수 보낸 사람의 관리자에 게 메시지를 복사 하 고 제목, 변경 하 고 두번째 규칙 메시지를 차단할 수 있습니다.

다음과 같은 두 규칙을 사용 하는 경우 조건은 동일 해야 합니다. 예제를 보려면 3 [일반적인 메시지 승인 시나리오](common-message-approval-scenarios-exchange-2013-help.md), [일반적인 첨부 파일 차단 시나리오](common-attachment-blocking-scenarios-for-mail-flow-rules-exchange-2013-help.md)및 [조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)예제 3의에서 예제를 살펴봅니다.

## 대화의 모든 전자 메일에 대 한 작업을 반복 안함

대화의 전자 메일의 체인 많은 개별 메시지를 포함할 수 하 고 스레드에 있는 각 메시지에 대 한 작업을 반복 성가신 얻을 수 있습니다. 예는 고 지 사항을 추가 하는 것과 같은 작업을 설치한 경우 수 원하는 스레드의 첫번째 메시지에만 적용 합니다. 그렇다면 이미 고 지 사항 텍스트를 포함 하는 메시지에 대 한 예외를 추가 합니다. 예, [조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)을 참조 하십시오.

## 규칙 처리를 중지 하는 시기를 알고 있습니다

때때로 규칙 일치 하는 규칙 처리를 중지 하도록 것이 좋습니다. 예, 첨부 파일이 있는 메시지를 차단 하려면 규칙을 하나 및 패턴을 일치 하는 메시지에는 고 지 사항을 삽입 하려면 1을 설치한 경우 잠재적인 중지 해야 메시지가 차단 되 면 규칙 처리 합니다. 추가 작업을 위해 않아도가 됩니다.

규칙의 규칙에는 규칙이 트리거되는 후 처리를 중지 하려면 **추가 규칙 처리 중지** 확인란을 선택 합니다.

## 키워드 또는 일치 시킬 패턴을 많을 경우 해당 파일에서 로드

예 허용 되지않는 또는 잘못 된 단어의 목록을 포함 하는 경우 전송 되지 않도록 전자 메일을 방지 하기 위해 사용할 수 있습니다. 이러한 단어와 구를, 포함 된 텍스트 파일을 만들고 Windows PowerShell 를 사용 하 여이 사용 하는 메시지를 차단 하는 전송 규칙을 설정할 수 있습니다.

텍스트 파일은 패턴에 대한 정규식을 포함할 수 있습니다. 이러한 식은 대/소문자를 구분하지 않습니다. 일반적인 정규식은 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>식</strong></p></td>
<td><p><strong>일치 항목</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>.</strong></p></td>
<td><p>임의의 단일 문자</p></td>
</tr>
<tr class="odd">
<td><p><strong>*</strong></p></td>
<td><p>임의의 추가 문자</p></td>
</tr>
<tr class="even">
<td><p><strong>\d</strong></p></td>
<td><p>임의의 10진수</p></td>
</tr>
<tr class="odd">
<td><p>[<em>character_group</em>]</p></td>
<td><p><em>character_group</em>에 포함된 임의의 단일 문자</p></td>
</tr>
</tbody>
</table>


정규식 및 사용을 참조 하십시오 [메일 흐름 규칙 단어, 구 또는 패턴의 목록을 기반으로 전자 메일 라우팅에 사용 하 여](use-mail-flow-rules-to-route-email-based-on-a-list-of-words-phrases-or-patterns-exchange-2013-help.md)Exchange 모듈 Windows PowerShell 명령을 사용 하 여 텍스트 파일을 표시 하는 예제입니다.

정규식을 사용 하 여 패턴을 지정 하는 방법을 알아보려면 [일반 식을 참조 (영문)](https://go.microsoft.com/fwlink/p/?linkid=532394)을 참조 하십시오.

