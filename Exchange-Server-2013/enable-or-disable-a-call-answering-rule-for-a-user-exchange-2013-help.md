---
title: '사용 하도록 설정 하거나 사용자에 대 한 전화 응답 규칙을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용 하도록 설정 하거나 사용자에 대 한 전화 응답 규칙을 사용 하지 않도록 설정
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54651805
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하도록 설정 하거나 사용자에 대 한 전화 응답 규칙을 사용 하지 않도록 설정

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-04-08_

셸을 사용 하 여 하나를 사용 하지 않도록 설정 하거나 사용 또는 사용자에 대 한 자세한 전화 응답 규칙. 여러 사용자에 대 한 자세한 전화 응답 규칙 또는 하나를 사용 하지 않도록 설정 하거나 사용 Exchange 관리 셸 스크립트에서 **Enable-UMCallAnsweringRule** 또는 **Disable-UMCallAnsweringRule** cmdlet을 사용할 수도 있습니다.

전화 응답 규칙은 받은 편지함 규칙을 받는 전자 메일 메시지에 적용 되는 방식과 비슷합니다 수신 통화에 적용 됩니다. 사용자에 대 한 UM (통합 메시징)을 사용 하는 경우에 기본적으로 전화 응답 규칙의 없이 구성 됩니다. 그럼에도 수신 전화는 메일 시스템에 의해 응답이 제공 되 고 발신자는 음성 메시지를 남길 하 라는 메시지가 표시 됩니다.

전화 응답 규칙에 관련 된 추가 관리 작업을 [프로시저를 호출 하는 착신 전환](forwarding-calls-procedures-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "UM 전화 응답 규칙" 항목.

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요. Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용 하 여 전화 응답 규칙을 사용 하도록 설정 하려면

통화 응답 규칙을 만들 때 활성화 됩니다. 셸을 사용 하 여 이전에 비활성화 된 전화 응답 규칙을 사용 하도록 설정 수 있습니다. 전화 응답 규칙을 조건 및 지정 된 전화 응답 규칙에 대 한 작업을 포함 하 여 통화를 재개 하려면 **Enable-UMCallAnsweringRule** cmdlet를 사용 하면 응답 규칙을 사용 하도록 설정 합니다.

이 예에서는 Tony Smith에 대 한는 전화 응답 규칙 `MyUMCallAnsweringRule` 의 사서함에서 수 있습니다.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

*WhatIf* 스위치를 사용 하 여 전화의 사서함에서 규칙 `MyUMCallAnsweringRule` Tony Smith에 대 한 응답은 사용할 준비가 여부와 명령 내에서 오류가 있는지를 테스트 하는 예제입니다.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

이 예에서는 전화의 사서함에서 규칙 `MyUMCallAnsweringRule` Tony Smith에 대 한 응답을 사용 하도록 설정 하 고 묻는 메시지에 서명에 전화 응답 규칙을 사용할 수 있는지 확인 합니다.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## 셸을 사용 하 여 전화 응답 규칙을 사용 하지 않도록 설정 하려면

전화 응답 규칙 없으므로 못 검색 하 고 수신 전화를 받을 때 처리를 사용 하지 않도록 설정 합니다. 전화 응답 규칙을 만들 때 조건 및 동작을 설정 하는 동안 해제 해야 합니다. 이렇게 하면 전화 응답 규칙을에서 전화 응답 규칙을 올바르게 구성 했는지 전에 수신 전화를 받을 때 처리 되지 않습니다.

이 예에서는 Tony Smith에 대 한는 전화 응답 규칙 `MyUMCallAnsweringRule` 의 사서함에서를 비활성화합니다.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

이 예제에서는 *WhatIf* 스위치를 사용 하 여 전화의 사서함에서 규칙 `MyUMCallAnsweringRule` Tony Smith에 대 한 응답은 사용 하지 않도록 설정할 준비가 여부 및 명령 내에서 오류가 있는지를 테스트 합니다.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

이 예에서는 전화의 사서함에서 규칙 `MyUMCallAnsweringRule` Tony Smith에 대 한 응답을 사용 하지 않도록 설정 하 고 로그인 하 라는 전화 응답 규칙을 확인 합니다.

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

