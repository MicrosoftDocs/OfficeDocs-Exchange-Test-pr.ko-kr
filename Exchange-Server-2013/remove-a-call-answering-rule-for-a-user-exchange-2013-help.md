---
title: '사용자에 대 한 전화 응답 규칙을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 전화 응답 규칙을 제거 합니다.
ms:assetid: 1da3c5bc-7227-4b37-96f6-67ceefc084d5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ898497(v=EXCHG.150)
ms:contentKeyID: 51407674
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 전화 응답 규칙을 제거 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-04-08_

셸을 사용 하 여 하나 이상의 전화 사용자에 대 한 응답 규칙을 제거할 수 있습니다. 하나 이상의 전화 여러 사용자에 대 한 응답 규칙을 제거 하려면 Exchange 관리 셸 스크립트에서 **Remove-UMCallAnsweringRule** cmdlet를 사용할 수 있습니다.

전화 응답 규칙은 받은 편지함 규칙을 받는 전자 메일 메시지에 적용 되는 방식과 비슷합니다 수신 통화에 적용 됩니다. 사용자에 대 한 UM (통합 메시징)을 사용 하는 경우에 기본적으로 전화 응답 규칙의 없이 구성 됩니다. 그럼에도 수신 전화는 메일 시스템에 의해 응답이 제공 되 고 발신자는 음성 메시지를 남길 하 라는 메시지가 표시 됩니다.


> [!NOTE]
> UM 사용이 가능한 사용자 만들기, 관리 및 전화 응답 규칙을 제거 하도록 Outlook Web App에 로그인 할 수 있습니다.



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



## 셸을 사용 하 여 전화 응답 규칙을 제거 하려면

이 예제에서는 사용자의 사서함에서 전화 응답 규칙 `MyUMCallAnsweringRule` 를 제거 합니다. 사용자의 사서함이 cmdlet을 실행 하는 사용자의 사서함입니다.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule

이 예에서는 Tony Smith의 사서함에서 전화 응답 규칙 `MyUMCallAnsweringRule` 를 제거합니다.

    Remove-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

