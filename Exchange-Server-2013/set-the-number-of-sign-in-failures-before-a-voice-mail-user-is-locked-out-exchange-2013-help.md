---
title: '음성 메일 사용자를 잠그기 전에 로그인 실패 횟수 설정: Exchange 2013 Help'
TOCTitle: 음성 메일 사용자를 잠그기 전에 로그인 실패 횟수 설정
ms:assetid: 855e1980-2868-4983-b097-0b5f63f202b8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123544(v=EXCHG.150)
ms:contentKeyID: 50556028
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일 사용자를 잠그기 전에 로그인 실패 횟수 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

Outlook Voice Access 사용자가 자신의 사서함에서 잠기기 전에 허용되는 로그인 실패 횟수를 구성할 수 있습니다. 음성 메일 사용자가 잠기기 전에 허용되는 로그인 실패 횟수는 UM(통합 메시징) 사서함 정책에서 구성되며 UM 사서함 정책과 연결된 모든 UM 사용 가능 사용자에게 적용됩니다. 기본 설정은 15입니다.

보안을 강화하려면 실패한 시도 최대 횟수를 줄입니다. 그러나 이 횟수를 기본값보다 낮게 줄이면 불필요하게 사서함이 잠길 수 있습니다. 통합 메시징은 UM 사용 가능 사용자에 대해 PIN 인증이 실패하거나 사용자가 시스템에 로그인하지 못한 경우 이벤트 뷰어를 사용하여 볼 수 있는 경고 이벤트를 생성합니다. 이 설정은 PIN이 다시 설정되기 전에 허용되는 로그인 실패 횟수에 대한 설정보다 커야 합니다.

Outlook Voice Access PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 음성 메일 사용자가 잠기기 전에 허용되는 로그인 실패 횟수 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 변경하려는 UM 사서함 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **PIN 정책**을 클릭하고 **잠금 이전 로그인 오류 발생 횟수** 옆에 1~999 범위의 값을 입력합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 음성 메일 사용자가 잠기기 전에 허용되는 로그인 실패 횟수 구성

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 연결된 UM 사용 가능 사용자에 대해 최대 로그인 시도 횟수를 10으로 설정합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -MaxLogonAttempts 10

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 연결된 UM 사용 가능 사용자에 대해 Outlook Voice Access 사용자의 PIN이 다시 설정되기 전에 허용되는 로그인 실패 횟수를 3으로, 최대 로그인 시도 횟수를 5로, 최소 PIN 길이를 9로 설정합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9

