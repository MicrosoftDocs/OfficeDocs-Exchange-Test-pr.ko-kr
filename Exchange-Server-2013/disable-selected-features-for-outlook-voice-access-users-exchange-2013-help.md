---
title: 'Outlook Voice Access 사용자에 대 한 일부 기능을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 일부 기능을 사용 하지 않도록 설정
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50555967
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 일부 기능을 사용 하지 않도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

Outlook Voice Access에는 TUI(전화 사용자 인터페이스)와 VUI(음성 사용자 인터페이스)의 두 가지 인터페이스가 있습니다. 기본적으로 사용자는 Outlook Voice Access로 전화를 걸 때 일정, 전자 메일 및 개인 연락처에 액세스하고 디렉터리를 검색할 수 있습니다. 관리자는 사용자가 Outlook Voice Access를 통해 자신의 사서함에 액세스할 때 이러한 기능 중 일부에 액세스하지 못하도록 셸을 사용하여 설정할 수 있습니다. UM(통합 메시징) 사서함 정책에서 Outlook Voice Access 기능을 수정하면 변경 내용이 UM 사서함 정책에 연결된 모든 사용자에게 영향을 줍니다.

UM 사서함 정책의 다음 Outlook Voice Access 기능에 사용자가 액세스하지 못하게 할 수 있습니다.

  - 일정

  - 디렉터리

  - Email

  - 개인 연락처

UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

또한 셸을 사용하여 UM 사용이 가능한 단일 사용자의 사서함에서 Outlook Voice Access 기능을 사용하지 않도록 설정할 수 있습니다. 이렇게 하면 해당 사용자만 기능을 사용할 수 없습니다. 단일 사용자의 UM 사서함 정책에 있는 모든 Outlook Voice Access 기능을 사용하지 않도록 설정할 수는 없지만, 일정 및 전자 메일에 액세스하지 못하도록 설정할 수는 있습니다.

UM 사서함과 관련된 추가 관리 작업에 대한 자세한 내용은 [사용자에 대 한 음성 메일](voice-mail-for-users-exchange-2013-help.md)을 참조하십시오.


> [!NOTE]
> UM 사서함 정책 또는 UM 사용 가능 단일 사용자의 사서함에서 UM 사용 가능 사용자의 Outlook Voice Access 기능을 수정하려면 셸을 사용해야만 합니다.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 사용자가 UM을 사용할 수 있도록 설정되었는지 확인하십시오. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 UM 사서함 정책에서 UM 사용이 가능한 사용자에 대해 선택된 Outlook Voice Access 기능을 사용하지 않도록 설정

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자가 Outlook Voice Access로 전화를 걸 때 일정에 액세스할 수 없도록 합니다.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자가 Outlook Voice Access로 전화를 걸 때 디렉터리에 액세스할 수 없도록 합니다.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자가 Outlook Voice Access로 전화를 걸 때 자신의 전자 메일에 액세스할 수 없도록 합니다.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자가 Outlook Voice Access로 전화를 걸 때 개인 연락처에 액세스할 수 없도록 합니다.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## 셸을 사용하여 UM 사용이 가능한 단일 사용자의 사서함에서 선택된 Outlook Voice Access 기능을 사용하지 않도록 설정

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

이 예에서는 사용자가 Outlook Voice Access로 전화를 걸 때 tony@contoso.com이라는 UM 사서함의 일정에 액세스하지 못하게 합니다.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

이 예에서는 사용자가 Outlook Voice Access로 전화를 걸 때 tony@contoso.com이라는 UM 사서함의 전자 메일에 액세스할 수 없도록 합니다.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

