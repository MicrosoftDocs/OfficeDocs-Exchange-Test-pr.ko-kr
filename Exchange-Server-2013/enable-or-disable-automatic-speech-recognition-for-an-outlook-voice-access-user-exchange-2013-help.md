---
title: 'Outlook Voice Access 사용자에 대 한 자동 음성 인식 기능을 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 자동 음성 인식 기능을 사용 하지 않도록 설정 하거나 사용
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50556001
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 자동 음성 인식 기능을 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

UM(통합 메시징) 및 음성 사서함 사용이 가능한 사용자에 대해 ASR(자동 음성 인식)을 구성할 수 있습니다. 사서함에서 ASR을 사용하도록 설정된 Outlook Voice Access 사용자는 음성 명령을 사용하여 사서함 메뉴에서 이동할 수 있습니다. ASR은 기본적으로 사용됩니다. ASR을 사용하도록 설정되지 않은 사용자는 터치톤이라고도 하는 DTMF(복합 주파수 부호) 입력을 사용하여 메뉴에서 이동해야 합니다.


> [!NOTE]
> 이 기능을 구성하는 데 EAC를 사용할 수 없습니다. 음성 사서함 사용자에 대해 ASR을 사용하거나 사용하지 않도록 설정하려면 셸을 사용해야 합니다.



UM 또는 음성 메일 사용자에 게 관련 된 추가 관리 작업을 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)을 참조 하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 UM 사용이 가능한 사용자에 대해 ASR을 사용하거나 사용하지 않도록 구성

이 예에서는 `tonysmith`라는 UM 사용이 가능한 사용자에 대해 ASR을 사용하도록 설정합니다.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

이 예에서는 `tonysmith`라는 UM 사용이 가능한 사용자에 대해 ASR을 사용하지 않도록 설정합니다.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

