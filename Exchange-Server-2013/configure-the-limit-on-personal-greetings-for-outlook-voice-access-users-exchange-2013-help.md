---
title: 'Outlook Voice Access 사용자에 대 한 개인 인사말에서 제한을 구성합니다: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 개인 인사말에서 제한을 구성합니다
ms:assetid: d400f250-0f55-45f5-9918-5f1d7819fbdf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201731(v=EXCHG.150)
ms:contentKeyID: 50556089
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 개인 인사말에서 제한을 구성합니다

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-05_

**개인 인사말 제한(분)** 설정을 사용하면 UM(통합 메시징) 사서함 정책과 연결된 사용자가 음성 사서함 인사말을 녹음할 수 있는 최대 시간(분)을 입력할 수 있습니다. 이 설정은 해당 사용자의 표준 음성 사서함과 부재 중 음성 사서함 인사말에 모두 적용됩니다. 최대 인사말 시간은 기본적으로 5분으로 설정됩니다. 그러나 1분에서 10분 사이의 원하는 값으로 최대 인사말 시간을 구성할 수 있습니다.

UM 사서함 정책에 관련된 추가 관리 작업은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 최대 인사말 시간 변경

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리하려는 UM 사서함 정책을 선택한 다음 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지 \> **일반**의 **개인 인사말 제한(분)** 아래에서 음성 사서함 사용자의 개인 인사말에 허용되는 최대 시간(분)을 입력합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 최대 인사말 시간 변경

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy`의 최대 인사말 시간을 3분으로 구성합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy MaxGreetingDuration 3

