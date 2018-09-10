---
title: '사용자에 대 한 음성 메일을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 음성 메일을 사용 하지 않도록 설정
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 50484184
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 음성 메일을 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-05_

UM 사용이 가능한 사용자에 대 한 UM (통합 메시징)을 사용 하지 않도록 설정할 수 있습니다. 이렇게 하면 통합 메시징에 음성 메일 기능 더이상 사용할 수 없습니다. 원하는 경우 사용자에 대 한 UM을 사용 하지 않도록 설정할 때, 사용자에 대 한 UM 설정을 유지할 수 있습니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 기존 사용자가 현재 통합 메시징에 사용하도록 설정되어 있는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자가 통합 메시징 및 음성 사서함을 사용하지 않도록 설정

1.  EAC에서 **받는 사람**을 클릭합니다.

2.  목록 보기에서 통합 메시징을 사용하지 않도록 설정할 사서함의 사용자를 선택합니다.

3.  세부 정보 창의 **전화 및 음성 기능** 아래에 있는 **통합 메시징**에서 **사용 안 함**을 클릭합니다.

4.  **경고** 대화 상자가 표시되면 **예**를 클릭하여 사용자가 통합 메시징을 사용하지 않도록 하는 설정을 수행합니다.

## 셸을 사용하여 사용자가 통합 메시징 및 음성 사서함을 사용하지 않도록 설정

이 예에서는 tonysmith@contoso.com 사용자가 통합 메시징 및 음성 사서함을 사용하지 않도록 설정하지만 UM 사서함 설정은 그대로 둡니다.

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

