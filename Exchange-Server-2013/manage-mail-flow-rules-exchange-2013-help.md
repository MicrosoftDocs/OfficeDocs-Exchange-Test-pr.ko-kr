---
title: '메일 흐름 규칙 관리: Exchange Online Protection Help'
TOCTitle: 메일 흐름 규칙 관리
ms:assetid: e7a81372-b6d7-4d1f-bc9e-a845a7facac2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657505(v=EXCHG.150)
ms:contentKeyID: 50484415
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 흐름 규칙 관리

 

_**적용 대상:** Exchange Online, Exchange Online Protection, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

조직을 통해 전달 하 고에서 해당 작업을 수행 하는 메시지에 대 한 특정 조건에 대 한 확인 메일 흐름 규칙로 알려져 전송 규칙을 사용할 수 있습니다. 이 항목에서는 만들기, 복사, 순서를 조정, 사용 또는 사용 안함, 삭제또는 가져오기 또는 내보내기 규칙 하는 방법 및 규칙 사용 모니터링하는 방법입니다.


> [!TIP]
> 규칙에서 예상 되는 방식으로 작동 하려면 각 규칙 및 규칙 간의 상호작용을 완벽 하 게 테스트 해야 합니다.



이 절차가 사용되는 시나리오를 확인하려면 다음 항목을 참조하세요.

  - [조직 전체의 법적 고 지 사항, 서명, 바닥글 또는 머리글](organization-wide-disclaimers-signatures-footers-or-headers-exchange-online-help.md)

  - [전송 규칙을 사용 하 여 메시지 첨부 파일을 검사 하려면](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

  - [일반적인 첨부 파일 차단 시나리오](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios)

  - [메일 흐름 규칙 단어, 구 또는 패턴의 목록을 기반으로 전자 메일 라우팅에 사용 하 여](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/use-rules-to-route-email)

  - [일반적인 메시지 승인 시나리오](common-message-approval-scenarios-exchange-2013-help.md)

  - [메시지 포함 되는 문서를 무시할 수 있도록 메일 흐름 규칙을 사용 하 여](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter)

  - [메일 흐름 규칙을 구성 하기 위한 모범 사례](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/mail-flow-rules/configuration-best-practices)

  - [메일 흐름 규칙을 사용 하 여 Office 365의 메시지 첨부 파일을 검사 하려면](https://technet.microsoft.com/ko-kr/library/jj919236\(v=exchg.150\))

  - [전송 규칙을 사용 하 여 대량 전자 메일 필터링을 구성 하려면](https://technet.microsoft.com/ko-kr/library/dn720438\(v=exchg.150\))

  - [전자 메일 메시지를 암호화하거나 암호를 해독하는 규칙 정의](https://go.microsoft.com/fwlink/p/?linkid=402846)

  - [Office 365에서 조직 수준의 수신 허용-보낸사람 또는 수신된 거부 목록 만들기](https://technet.microsoft.com/ko-kr/library/dn198251\(v=exchg.150\))

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)(Exchange Server) 또는 [Exchange Online의 기능 사용 권한](https://technet.microsoft.com/ko-kr/library/jj200673\(v=exchg.150\))의 "규칙 전송" 항목

  - 규칙을 **14 버전** 으로 표시 되 면 규칙은 기반 하는 Exchange Server 2010 메일 흐름 규칙 형식으로는 것을 의미 합니다. 모든 옵션은 이러한 규칙에 사용할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 메일 흐름 규칙 만들기

새 규칙을 만들 데이터 손실 방지 (DLP) 정책을 설정 하 여 또는 규칙을 복사 하 여 메일 흐름 규칙을 만들 수 있습니다. Exchange 관리 센터 (EAC) 또는 Exchange 관리 셸 를 사용할 수 있습니다.


> [!NOTE]
> 만들거나 메일 흐름 규칙을 수정 후 전자 메일에 적용할 신규 또는 업데이트 된 규칙에 대 한 최대 30 분까지 걸릴 수 있습니다.



## DLP 정책을 사용 하 여 메일 흐름 규칙을 만들 수

각 DLP 정책은 메일 흐름 규칙의 컬렉션입니다. DLP 정책을 만든 후에 아래 절차를 사용 하 여 규칙을 미세 조정할 수 있습니다.

1.  DLP 정책을 만듭니다. 해당 지침은 다음 항목을 참조하세요.
    
      - [Exchange Server 2013 DLP 절차](dlp-procedures-exchange-2013-help.md)
    
      - [Exchange Online DLP 절차](dlp-procedures-exchange-2013-help.md)

2.  DLP 정책에 의해 만들어진 메일 흐름 규칙을 수정 합니다. 참조 보기 또는 전송 규칙을 수정합니다.

## EAC를 사용 하 여 메일 흐름 규칙을 만들려면

EAC를 사용 하면 처음부터 또는 서식 파일을 복사 하는 기존 규칙을 사용 하 여 메일 흐름 규칙을 만들 수 있습니다.

1.  **메일 흐름** \> **규칙**으로 이동합니다.

2.  다음 옵션 중 하나를 사용하여 규칙을 만듭니다.
    
      - 템플릿에서 규칙을 만들려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 템플릿을 선택합니다.
    
      - 규칙을 복사하려면 규칙을 선택하고 **복사**![복사 아이콘](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "복사 아이콘")를 선택합니다.
    
      - 처음부터 완전히 새로 규칙을 만들려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭한 다음 **새 규칙 만들기**를 선택합니다.

3.  **새 규칙** 대화 상자에서 규칙 이름을 지정한 다음 이 규칙의 조건과 동작을 선택합니다.
    
    1.  **다음의 경우 이 규칙 적용...** 에서 사용 가능한 조건 목록에서 원하는 조건을 선택합니다.
        
          - 일부 조건 값을 지정 해야 합니다. 예, **보낸사람 제도..** 조건을 선택 하면 보낸사람 주소를 지정 해야 합니다. 단어 또는 구를 추가 하는 경우 note 후행 공백이 허용 되지 않습니다.
        
          - 원하는 조건이 목록에 없거나 예외를 추가해야 하는 경우 **기타 옵션**을 선택합니다. 추가 조건 및 예외가 나열됩니다.
        
          - 조건을 지정하지 않고 조직의 모든 메시지에 이 규칙을 적용하려면 **\[모든 메시지에 적용\]** 조건을 선택합니다.
    
    2.  **다음 작업 실행...** 에서 사용 가능한 동작 목록 중 규칙에서 해당 조건과 일치하는 메시지에 적용할 동작을 선택합니다.
        
          - 일부 동작은 값을 지정해야 합니다. 예를 들어 **승인을 위해 다음에 메시지 전달…** 조건을 선택한 경우 조직에서 받는 사람을 선택해야 합니다.
        
          - 원하는 조건이 목록에 없으면 **기타 옵션**을 선택합니다. 추가 조건이 나열됩니다.
    
    3.  [데이터 손실 방지 (DLP) 보고서](https://go.microsoft.com/fwlink/p/?linkid=402768) 및 [전송 규칙 보고서](https://go.microsoft.com/fwlink/p/?linkid=402769)에이 규칙에 대 한 규칙 일치 하는 데이터 표시 방법을 지정 합니다.
        
          - **심각도 수준으로이 규칙 감사** 아래에서이 규칙에 대 한 심각도 수준을 지정 하려면 수준을 선택 합니다. Office 365 활동 심각도 수준에 따라 그룹 규칙과 일치 하는 메일 흐름 규칙에 대 한 보고 합니다. 심각도 수준은 보고서를 보다 쉽게 사용 하 여 필터 뿐입니다. 심각도 수준에 규칙 처리 되는 우선순위를 영향을 주지 않습니다.
            

            > [!NOTE]
            > <STRONG>심각도 수준으로이 규칙 감사</STRONG> 확인란의 선택을 취소 하면 규칙 일치 하는 결과에 나타나지 않습니다 규칙 보고서 합니다.

    
    4.  규칙에 대 한 모드를 설정 합니다. 메일 흐름에 영향을 주지 않고도 규칙을 테스트 하는 두 테스트 모드 중 하나를 사용할 수 있습니다. 두 테스트 모드에서 조건에 해당 하는 경우 메시지 추적에 항목이 추가 됩니다.
        
          - **적용**   규칙이 켜지고 메시지 처리가 즉시 시작됩니다. 규칙에 대한 모든 동작이 수행됩니다.
        
          - **정책 설명을 포함하여 테스트**   이 옵션을 선택하면 규칙이 설정되고 모든 정책 설명 동작(**정책 설명과 함께 보낸 사람에게 알림**)이 전송되지만 메시지 배달과 관련된 동작은 수행되지 않습니다. 이 모드를 사용하려면 DLP(데이터 손실 방지)가 필요합니다. 자세한 내용은 [정책 팁](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/data-loss-prevention/policy-tips)을 참조하세요.
        
          - **정책 설명 없이 테스트**   문제 보고서 생성 동작만 적용되며 메시지 배달과 관련된 동작은 수행되지 않습니다.

4.  규칙이 만족스러운 경우 5단계로 이동하고, 다른 조건이나 동작을 추가하거나 예외를 지정하거나 추가 속성을 설정하려는 경우 **기타 옵션**을 클릭합니다. **기타 옵션**을 클릭한 후에 다음 필드를 완성하여 규칙을 만듭니다.
    
    1.  조건을 더 추가하려면 **조건 추가**를 클릭합니다. 둘 이상의 조건이 있는 경우 조건 옆에 있는 **제거 X**를 클릭하여 제거할 수 있습니다. **기타 옵션**을 클릭하면 훨씬 더 다양한 조건을 사용할 수 있습니다.
    
    2.  작업을 더 추가하려면 **작업 추가**를 클릭합니다. 둘 이상의 동작이 있는 경우 동작 옆에 있는 **제거 X**를 클릭하여 제거할 수 있습니다. **기타 옵션**을 클릭하면 훨씬 더 다양한 동작을 사용할 수 있습니다.
    
    3.  예외를 지정하려면 **예외 추가**를 클릭하고 **다음의 경우 제외...** 드롭다운을 사용하여 예외를 선택합니다. 예외 옆에 있는 **제거 X**를 클릭하여 규칙에서 예외를 제거할 수 있습니다.
    
    4.  특정 날짜 이후에 이 규칙이 적용되게 하려면 **다음 날짜에 이 규칙 활성화:** 를 클릭하고 날짜를 지정합니다. 해당 날짜 이전에는 규칙이 사용 가능하게 설정되어 있지만 처리되지는 않습니다.
        
        마찬가지로 특정 날짜에 규칙 처리가 중지되도록 할 수 있습니다. 이렇게 하려면 **다음 날짜에 이 규칙 비활성화:** 를 클릭하고 날짜를 지정합니다. 규칙이 사용 가능하게 설정되어 있지만 처리되지 않습니다.
    
    5.  이 규칙이 메시지를 처리하면 추가 규칙을 적용하지 않도록 선택할 수 있습니다. 이렇게 하려면 **더 이상 규칙 수행 중지**를 클릭합니다. 이 옵션을 선택한 다음 이 규칙에 따라 메시지가 처리되면 해당 메시지에 대해 어떠한 후속 규칙도 처리되지 않습니다.
    
    6.  규칙 처리를 완료할 수 없는 경우 메시지를 처리할 방법을 지정할 수 있습니다. 기본적으로는 규칙이 무시되고 메시지가 정상적으로 처리되지만, 처리를 위해 메시지를 다시 전송할 수도 있습니다. 이렇게 하려면 **규칙 처리가 완료되지 않으면 메시지 연기** 확인란을 선택합니다.
    
    7.  규칙은 보낸 사람 주소를 분석할 때 기본적으로 메시지 헤더만 검사합니다. 그러나 SMTP 메시지 봉투도 검사하도록 규칙을 구성할 수 있습니다. 검사 내용을 지정하려면 **메시지에서 보낸 사람 주소 일치**에 대해 다음 값 중 하나를 클릭합니다.
        
          - **헤더**   메시지 헤더만 검사합니다.
        
          - **봉투**   SMTP 메시지 봉투만 검사합니다.
        
          - **헤더 또는 봉투**   메시지 헤더와 SMTP 메시지 봉투를 모두 검사합니다.
    
    8.  **설명** 상자에 이 규칙에 대한 설명을 추가할 수 있습니다.

5.  **저장**을 클릭하여 규칙 만들기를 완료합니다.

## Exchange 관리 셸 를 사용 하 여 메일 흐름 규칙을 만들려면

이 예제에서는 [New-TransportRule](https://technet.microsoft.com/ko-kr/library/bb125138\(v=exchg.150\)) cmdlet를 사용 하 여 Sales Department 메일 그룹에는 조직 외부에서 보낸 메시지를 앞에 "`External message to Sales DG:`"를 추가 하는 새 메일 흐름 규칙을 만듭니다.

    New-TransportRule -Name "Mark messages from the Internet to Sales DG" -FromScope NotInOrganization -SentTo "Sales Department" -PrependSubject "External message to Sales DG:"

규칙 매개 변수 및 함수는 위의 절차에서 사용 되는 예제입니다. 모든 사용 가능한 메일 흐름 규칙 조건 및 동작을 선택할 요구 사항에 맞는 결정을 검토 합니다.

## 작동 여부는 어떻게 확인합니까?

새 메일 흐름 규칙을 성공적으로 만들었습니다을 확인 하려면 다음을 수행 합니다.

  - EAC에서 만든 새 메일 흐름 규칙의 **규칙** 목록에 나타나는지 확인 합니다.

  - Exchange 관리 셸 에서 만들어졌는지 확인 새 메일 흐름 규칙 성공적으로 (아래 예제에서는 위의 Exchange 관리 셸 예제에서 만든 규칙을 확인 함)에 다음 명령을 실행 하 여:
    
        Get-TransportRule "Mark messages from the Internet to Sales DG"

## 메일 흐름 규칙 보기 또는 수정


> [!NOTE]
> 만들거나 메일 흐름 규칙을 수정 후 전자 메일에 적용할 신규 또는 업데이트 된 규칙에 대 한 최대 30 분까지 걸릴 수 있습니다.



## EAC를 사용 하 여 메일 흐름 규칙 보기 또는 수정 하려면

1.  EAC에서 **메일 흐름** \> **규칙**으로 이동합니다.

2.  목록에서 규칙을 선택하면 해당 규칙의 조건, 동작, 예외 및 선택 속성이 세부 정보 창에 표시됩니다. 특정 규칙의 모든 속성을 보려면 해당 규칙을 두 번 클릭합니다. 이렇게 하면 규칙 편집기 창이 열리고 규칙을 변경할 수 있게 됩니다. 규칙 속성에 대한 자세한 내용은 이 항목 앞부분에 나오는 Use the EAC to create a new Transport rule 섹션을 참조하세요.

## Exchange 관리 셸 를 사용 하 여 메일 흐름 규칙 보기 또는 수정

다음 예제에서는 조직에 구성된 모든 규칙 목록을 표시합니다.

    Get-TransportRule

특정 메일 흐름 규칙의 속성을 보려면 해당 규칙 또는 해당 GUID의 이름을 제공할 수 있습니다. 일반적으로 출력 속성의 서식을 지정 하려면 **Format-List** cmdlet을 전송 하는 것이 좋습니다. 다음 예제에서는 **보낸 사람이 마케팅의 구성원**이라는 메일 흐름 규칙의 모든 속성을 반환 합니다.

    Get-TransportRule "Sender is a member of marketing" | Format-List

기존 규칙의 속성을 수정하려면 [Set-TransportRule](https://technet.microsoft.com/ko-kr/library/bb123534\(v=exchg.150\)) cmdlet을 사용합니다. 이 cmdlet을 사용하면 규칙과 연결된 모든 속성, 조건, 동작 또는 예외를 변경할 수 있습니다. 다음 예에서는 "Sender is a member of marketing" 규칙에 예외를 추가하여 사용자 Kelly Rollin이 보낸 메시지에 해당 규칙이 적용되지 않도록 합니다.

    Set-TransportRule "Sender is a member of marketing" -ExceptIfFrom "Kelly Rollin"

## 작동 여부는 어떻게 확인합니까?

메일 흐름 규칙을 수정 되었는지 확인 하려면 다음을 수행 합니다.

  - EAC의 규칙 목록에서 수정한 규칙을 **규칙** 목록에서 클릭하면 세부 정보 창이 표시됩니다.

  - Exchange 관리 셸 에서 수정 확인 메일 흐름 규칙 성공적으로 (아래 예제에서는 위의 Exchange 관리 셸 예제에서 수정한 규칙을 확인 함) 규칙의 이름이 수정 되는 속성을 나열 하려면 다음 명령을 실행 하 여:
    
        Get-TransportRule "Sender is a member of marketing" | Format-List Name,ExceptIfFrom

## 메일 흐름 규칙 속성

또한 조직에서 기존 전송 규칙을 수정 하려면 Set-transportrule cmdlet을 사용할 수 있습니다. 다음은 목록 속성을 변경할 수 있는 EAC에서 사용할 수 없습니다. 에 대 한 자세한 내용은 Set-transportrule cmdlet를 사용 하 여 이러한 변경 [Set-TransportRule](https://technet.microsoft.com/ko-kr/library/bb123534\(v=exchg.150\)) 을 참조 하려면


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>EAC의 조건 이름</th>
<th>Exchange 관리 셸 의 조건 이름</th>
<th>속성</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>규칙 처리 중지</strong></p></td>
<td><p><code>StopRuleProcessing </code></p></td>
<td><p><code> Not applicable</code></p></td>
<td><p>추가 규칙 처리를 중지할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>머리글/봉투 일치</strong></p></td>
<td><p><code>SenderAddressLocation </code></p></td>
<td><p>해당 없음</p></td>
<td><p>머리글을 확인 하 고 일치 하는 명의 포함 하는 SMTP 메시지 봉투를 검사할 수 있습니다.</p>
<p></p></td>
</tr>
<tr class="odd">
<td><p><strong>감사 심각도</strong></p></td>
<td><p><code>SetAuditSeverity </code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>감사에 대 한 심각도 선택할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>규칙 모드</strong></p></td>
<td><p><code>Mode</code></p></td>
<td><p><code>Not applicable</code></p></td>
<td><p>규칙에 대 한 모드를 설정할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 메일 흐름 규칙의 우선순위 설정

목록 맨 위에 나오는 규칙이 맨 먼저 처리됩니다. 이 규칙의 **우선 순위**는 0입니다.

## EAC를 사용하여 규칙의 우선 순위 설정

1.  EAC에서 **메일 흐름** \> **규칙**으로 이동합니다. 이렇게 하면 규칙이 처리되는 순서대로 표시됩니다.

2.  규칙을 선택하고 화살표를 사용하여 규칙을 목록 위 또는 아래로 이동합니다.

## Exchange 관리 셸 를 사용 하 여 규칙의 우선순위를 설정 하려면

다음 예제에서는 "Sender is a member of marketing"의 우선 순위를 2로 설정합니다.

    Set-TransportRule "Sender is a member of marketing" priority "2"

## 작동 여부는 어떻게 확인합니까?

메일 흐름 규칙을 수정 되었는지 확인 하려면 다음을 수행 합니다.

  - EAC의 규칙 목록에서 규칙의 순서를 확인합니다.

  - Exchange 관리 셸 에서 (아래 예제에서는 위의 Exchange 관리 셸 예제에서 수정한 규칙을 확인 함) 규칙의 우선순위를 확인 합니다.
    
        Get-TransportRule * | Format-List Name,Priority

## 메일 흐름 규칙을 사용 하지 않도록 설정 하거나 사용

규칙을 만들 때 사용할 수 있습니다. 메일 흐름 규칙을 사용 하지 않도록 설정할 수 있습니다.

## EAC를 사용 하 여 사용 하도록 설정 하거나 메일 흐름 규칙을 사용 하지 않도록 설정

1.  EAC에서 **메일 흐름** \> **규칙**으로 이동합니다.

2.  규칙을 사용하지 않도록 설정하려면 규칙 이름 옆의 확인란을 선택 취소합니다.

3.  사용되지 않도록 설정한 규칙을 사용하도록 설정하려면 규칙 이름 옆의 확인란을 선택합니다.

## Exchange 관리 셸 를 사용 하 여 메일 흐름 규칙을 사용할지 여부를

다음 예제에서는 "보낸 사람이 다음과 같음 a member of marketing" 메일 흐름 규칙을 비활성화 합니다.

    Disable-TransportRule "Sender is a member of marketing"

다음 예제에서는 "보낸 사람이 다음과 같음 a member of marketing" 메일 흐름 규칙을 수 있습니다.

    Enable-TransportRule "Sender is a member of marketing"

## 작동 여부는 어떻게 확인합니까?

성공적으로 사용 하도록 설정 하거나 했는지 메일 흐름 규칙을 사용 하지 않도록 설정을 확인 하려면 다음을 수행 합니다.

  - EAC의 **규칙** 목록에서 규칙 목록을 확인하고 **설정** 열에서 확인란의 상태를 확인합니다.

  - Exchange 관리 셸 에서 해당 상태 조직에서 모든 규칙 목록을 반환 하는 다음 명령을 실행 합니다.
    
        Get-TransportRule | Format-Table Name,State

## 메일 흐름 규칙을 제거 합니다.

## EAC를 사용 하 여 메일 흐름 규칙을 제거 하려면

1.  EAC에서 **메일 흐름** \> **규칙**으로 이동합니다.

2.  제거할 규칙을 선택한 다음 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

## Exchange 관리 셸 를 사용 하 여 메일 흐름 규칙을 제거 하려면

다음 예제에서는 "보낸 사람이 다음과 같음 a member of marketing" 메일 흐름 규칙을 제거 합니다.

    Remove-TransportRule "Sender is a member of marketing"

## 작동 여부는 어떻게 확인합니까?

메일 흐름 규칙 성공적으로 제거 되는지 확인 하려면 다음을 수행 합니다.

  - EAC의 **규칙** 목록에서 규칙을 확인한 후, 제거한 규칙이 더 이상 표시되지 않는지 확인합니다.

  - Exchange 관리 셸 에서 다음 명령을 실행 하 고 제거한 규칙이 더이상 나열 되는지 확인 합니다.
    
        Get-TransportRule

## 규칙 사용 모니터링

Exchange Online 또는 Exchange Online Protection을 사용하는 경우 규칙 보고서를 사용하여 각 규칙에서 일치 조건을 확인한 횟수를 확인할 수 있습니다. 규칙을 보고서에 포함하려면 규칙의 **심각도 수준으로 이 규칙 감사** 확인란을 선택해야 합니다. 보고서를 온라인으로 보거나 모든 메일 보호 보고서의 Excel 버전을 다운로드할 수도 있습니다.


> [!NOTE]
> 대부분의 데이터가 24시간 내에 보고서에 추가되지만 일부 데이터는 5일까지 소요될 수 있습니다.



## Office 365 관리 센터를 사용하여 규칙 보고서 생성

1.  Office 365 관리 센터에서 **보고서**를 선택합니다.

2.  **규칙** 섹션에서 **메일에 대한 상위 규칙 일치** 또는 **메일에 대한 규칙 일치**를 선택합니다.

자세한 내용은 [메일 보호 보고서 보기](https://go.microsoft.com/fwlink/p/?linkid=402958)를 참조 합니다.

## Excel 버전의 보고서 다운로드

1.  Office 365 관리 센터의 보고서 페이지에서 **메일 보호 보고서(Excel)** 를 선택합니다.

2.  Excel 메일 보호 보고서를 처음 사용하는 경우 다운로드 페이지에 대한 탭이 열립니다.
    
    1.  **다운로드**를 선택하여 Exchange Online 보고용 Microsoft Office 365 Excel 플러그 인을 다운로드합니다.
    
    2.  다운로드를 엽니다.
    
    3.  **Office 365 설치에 대한 메일 보호 보고서** 대화 상자에서 **다음**을 선택하고 사용권 계약에 동의한 후 **다음**을 선택합니다.
    
    4.  사용 중인 서비스를 선택하고 **다음**을 선택합니다.
    
    5.  필수 구성 요소를 확인하고 **다음**을 선택합니다.
    
    6.  **설치**를 선택합니다. 바탕 화면에 보고서 바로 가기가 표시됩니다.

3.  바탕 화면에서 **Office 365 메일 보호 보고서**를 선택합니다.

4.  보고서에서 **규칙** 탭을 선택합니다.

## 메일 흐름 규칙 컬렉션 내보내기 또는 가져오기

메일 흐름 규칙 컬렉션 내보내기 또는 가져오기를 Exchange 관리 셸 를 사용 해야 합니다. XML 파일에서 메일 흐름 규칙 컬렉션을 가져오는 방법에 대 한 정보를 [Import-TransportRuleCollection](https://technet.microsoft.com/ko-kr/library/bb123582\(v=exchg.150\))을 참조 하십시오. 메일 흐름 규칙 컬렉션을 XML 파일로 내보내는 방법에 대 한 자세한 내용은 [Export-TransportRuleCollection](https://technet.microsoft.com/ko-kr/library/bb124410\(v=exchg.150\))을 참조 하십시오.

## 도움이 더 필요하십니까?

Exchange Online 에 대 한 리소스:

[Exchange Online에서 흐름 규칙 (전송 규칙) 메일](https://technet.microsoft.com/ko-kr/library/jj919238\(v=exchg.150\))

[Exchange Online의 메일 흐름 규칙 조건 및 예외 (조건자)](https://technet.microsoft.com/ko-kr/library/jj919235\(v=exchg.150\))

[Exchange Online 흐름 규칙 동작을 메일](https://technet.microsoft.com/ko-kr/library/jj919237\(v=exchg.150\))

[전송 및 받은 편지함 규칙 제한](https://go.microsoft.com/fwlink/p/?linkid=324584)

Exchange Online Protection 에 대 한 리소스:

[Mail flow rules (transport rules) in Exchange Online Protection](https://technet.microsoft.com/ko-kr/library/dn271424\(v=exchg.150\))

[메일 흐름 규칙 조건 및 예외 (조건자) Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj919234\(v=exchg.150\))

[메일 흐름 규칙 동작 Exchange 온라인 보호](https://technet.microsoft.com/ko-kr/library/jj920117\(v=exchg.150\))

[전송 및 받은 편지함 규칙 제한](https://go.microsoft.com/fwlink/p/?linkid=324584)

Exchange Server 2013용 리소스:

[메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[전송 규칙 동작](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

