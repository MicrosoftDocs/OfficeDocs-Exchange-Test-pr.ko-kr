---
title: '음성 메일에 대 한 PIN 수명 설정: Exchange 2013 Help'
TOCTitle: 음성 메일에 대 한 PIN 수명 설정
ms:assetid: d17f0bf6-0ad6-40a4-bdd5-f7098f39250d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124712(v=EXCHG.150)
ms:contentKeyID: 50556093
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일에 대 한 PIN 수명 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

UM(통합 메시징)을 사용하도록 설정된 사용자에 대해 PIN 수명을 구성할 수 있습니다. PIN 수명은 Outlook Voice Access PIN이 UM 사용 가능 받는 사람에 대해 유효한 최대 시간입니다. PIN 수명 설정은 UM 사서함 정책에 구성되며 해당 UM 사서함 정책과 연결된 모든 UM 사용 가능 사용자에게 적용됩니다.

UM 사서함 정책에 대해 다양한 PIN 관련 설정을 구성할 수 있습니다. PIN 수명 설정은 Outlook Voice Access 사용자가 마지막으로 자신의 PIN을 변경한 날짜부터 PIN을 다시 변경해야 하는 날짜까지의 시간 간격(일)을 제어합니다. 범위는 0에서 999까지이며, 기본값은 60일입니다. 0을 입력하면 사용자 PIN이 만료되지 않습니다. 이 설정을 0으로 구성할 경우 네트워크의 보안이 매우 약화되므로 그러지 않는 것이 좋습니다.


> [!IMPORTANT]
> 통합 메시징에서는 PIN이 만료될 시기를 사용자에게 알리지 않습니다.



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

## EAC를 사용하여 PIN 수명 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 변경하려는 UM 사서함 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **PIN 정책**을 클릭하고 **PIN 수명(일) 적용** 옆에 0에서 999 사이의 값을 입력합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 PIN 수명 구성

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 연결된 Outlook Voice Access 사용자에 대해 PIN을 사용할 수 있는 날짜를 30일로 설정합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINLifetime 30

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책에 연결된 Outlook Voice Access 사용자에 대해 다음과 같은 PIN 관련 설정을 구성합니다.

  - 사용자의 PIN을 다시 설정하기 전까지 로그온 실패 횟수를 3으로 설정합니다.

  - 최대 로그온 시도 횟수를 5로 설정합니다.

  - 최소 PIN 길이를 9자리로 설정합니다.

  - PIN이 40일 후 만료되도록 설정합니다.

<!-- end list -->

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -LogonFailuresBeforePINReset 3
    -MaxLogonAttempts 5 -MinPINLength 9 -PINLifetime 40

