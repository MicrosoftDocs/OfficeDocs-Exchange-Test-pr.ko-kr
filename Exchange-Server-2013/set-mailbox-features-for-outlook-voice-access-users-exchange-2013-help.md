---
title: 'Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50555941
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 사서함 기능을 설정 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

Outlook Voice Access에는 TUI(전화 사용자 인터페이스)와 VUI(음성 사용자 인터페이스)의 두 가지 인터페이스가 있습니다. 사용자가 Exchange 2013의 UM(통합 메시징) 시스템을 사용하여 사서함에 액세스할 때 UM 사용 가능 사용자의 TUI 설정을 구성할 수 있습니다. UM 사서함 정책에서 UM 사용이 가능한 사용자의 TUI 설정을 수정하면 변경 내용이 UM 사서함 정책에 연결된 모든 사용자에게 영향을 줍니다. UM 사서함 정책에서 다음 TUI 설정을 수정할 수 있습니다.

  - 음성 메일에 대한 PIN 없는 액세스

  - 다른 메시지에 대한 음성 응답

  - 일정에 대한 TUI 액세스

  - 디렉터리에 대한 TUI 액세스

  - 전자 메일에 대한 TUI 액세스

  - 개인 연락처에 대한 TUI 액세스


> [!NOTE]
> 셸에서만 UM 사용 가능 사용자의 Outlook Voice Access TUI 설정을 수정할 수 있습니다.



UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 UM 사서함 정책의 TUI 설정 수정

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책의 TUI 관련 설정을 지정합니다.

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

