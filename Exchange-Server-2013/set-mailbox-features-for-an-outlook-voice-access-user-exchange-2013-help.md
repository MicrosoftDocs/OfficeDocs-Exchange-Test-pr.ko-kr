---
title: 'Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.
ms:assetid: a56bfd75-7bc5-49b9-b098-06855a720dcd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124030(v=EXCHG.150)
ms:contentKeyID: 50556048
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

TUI(전화 사용자 인터페이스) 설정은 사용자가 Outlook Voice Access를 사용하여 UM(통합 메시징) 시스템에 액세스할 때 사용됩니다. UM 사용 가능 사용자의 TUI 구성 설정을 수정할 때는 UM 사용 가능 사용자의 사서함에 대한 속성과 해당 값을 수정해야 합니다.

UM 사용 가능 사용자에 대해 다음 TUI 설정을 변경할 수 있습니다.

  - 구독자 액세스 허용

  - 일정에 대한 TUI 액세스 허용

  - 전자 메일에 대한 TUI 액세스 허용

  - 자동 음성 인식 허용

UM 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.](set-mailbox-features-for-an-outlook-voice-access-user-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행하기 전에 기존의 Exchange 받는 사람이 통합 메시징과 음성 메일을 사용할 수 있는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 단일 UM 사용 가능 사용자의 TUI 설정 수정

이 예에서는 Tony Smith라는 UM 사용 가능 사용자의 TUI를 사용하여 일정 및 전자 메일 액세스를 사용하도록 설정합니다.

    Set-UMMailbox -Identity tony@contoso.com TUIAccessToCal True -TUIAccessToEmail True -OperatorNumber 111111 -DisableMissedCallNotification False -AnonCallBlock True


> [!NOTE]
> 사용자에 대한 TUI 설정은 UM 사서함 정책에서도 제공됩니다. UM 사서함 정책에서 TUI 설정을 수정하면 해당 UM 사서함 정책과 연결된 모든 사용자가 영향을 받습니다. UM 사서함 정책에서 TUI 설정을 수정하는 방법에 대한 자세한 내용은 <A href="set-mailbox-features-for-outlook-voice-access-users-exchange-2013-help.md">Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.</A>을 참조하십시오.


