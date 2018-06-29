---
title: 'Outlook Voice Access PIN 정책 설정: Exchange 2013 Help'
TOCTitle: Outlook Voice Access PIN 정책 설정
ms:assetid: 5b2800b7-bfa6-4282-975c-0706ae25ad64
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998285(v=EXCHG.150)
ms:contentKeyID: 50555993
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access PIN 정책 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

UM(통합 메시징) 사서함 정책에 대해 PIN 정책을 설정할 수 있습니다. 사용자에게 조직에 미리 정의된 PIN 정책을 따르도록 요청하여 Outlook Voice Access를 사용하는 UM 사용 가능한 사용자에 대한 보안 수준이 향상되도록 UM 사서함 정책을 구성할 수 있습니다.

Outlook Voice Access 사용자에 대한 PIN 정책을 설정하려면 새 UM 사서함 정책을 만들거나 기존 UM 사서함 정책을 수정할 수 있습니다. 새 UM 사서함 정책을 만든 후에는 다음 PIN 설정을 구성하여 UM 사서함 정책을 구성할 수 있습니다.

  - `MinPasswordLength`

  - `PINLifetime`

  - `LogonFailuresBeforePINReset`

  - `MaxLogonAttempts`

  - `AllowCommonPatterns`

  - `PINHistoryCount`

UM 사용자에 대해 강력한 PIN 요구 사항을 구현하는 것이 가장 좋은 보안 방법입니다. 이러한 방법은 PIN에 6자리 이상의 숫자를 지정하도록 하는 UM PIN 정책을 작성하여 시행할 수 있으며, 이를 통해 네트워크의 보안 수준을 향상시킬 수 있습니다.

PIN 정책을 변경하면 새 PIN 설정이 현재 UM 사서함 정책과 연결된 사용자에게 적용됩니다. 예를 들어, UM 사서함 정책을 수정하고 최소 PIN 길이를 7자리에서 10자리로 변경하면 사용자는 다음에 로그온할 때 변경된 PIN 요구 사항을 따르기 위해 PIN을 변경해야 합니다.

Outlook Voice Access PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Voice Access 사용자에 대한 PIN 정책 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 편집하려는 UM 다이얼 플랜을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 편집할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **속성**을 클릭합니다.

4.  **UM 사서함 정책** 페이지에서 **PIN 정책**을 클릭합니다.

5.  **PIN 정책** 페이지에서 이 UM 사서함 정책과 연결된 Outlook Voice Access 사용자에 대한 PIN 설정을 구성한 다음 **저장**을 클릭합니다.

## 셸을 사용하여 Outlook Voice Access 사용자에 대한 PIN 정책 설정

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy`와 관련된 사용자에 대해 PIN 설정을 지정합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 8 -MaxLogonAttempts 12 -MinPINLength 8 -PINHistoryCount 10 -PINLifetime 60 -ResetPINText "The PIN used to allow you access to your mailbox using Outlook Voice Access has been reset."

