---
title: 'UM IP 게이트웨이에 메시지 대기 표시기 (MWI)을 허용 합니다.: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이에 메시지 대기 표시기 (MWI)을 허용 합니다.
ms:assetid: 5667e37c-48c6-4659-9dc9-94b1dd8ba232
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd297995(v=EXCHG.150)
ms:contentKeyID: 50483143
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이에 메시지 대기 표시기 (MWI)을 허용 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-23_

UM(통합 메시징) IP 게이트웨이에서 수신한 통화에 대해 사용자에게 음성 메일 알림을 보내거나 보내지 않도록 지정할 수 있습니다. 이 설정을 사용하면 UM IP 게이트웨이가 사용자에 대해 SIP NOTIFY 메시지를 보내고 받을 수 있습니다. MWI(Message Waiting Indicator)는 기본적으로 사용되며 메시지 대기 알림이 사용자에게 전송되도록 하지만, 필요에 따라 이 기능을 사용하지 않을 수 있습니다.

MWI(Message Waiting Indicator)는 사용자에게 새로운 또는 듣지 않은 음성 메시지에 대해 알려줍니다. MWI는 Outlook 및 Outlook Web App과 같은 클라이언트의 받은 편지함에 표시됩니다. 등록된 휴대폰으로 문자(SMS) 메시지를 전송하거나, Exchange 서버에서 새 메시지를 재생하도록 구성된 번호로 전화를 걸거나, 사용자 탁상 전화에 램프가 켜지게 하는 방식일 수도 있습니다.


> [!TIP]
> 사용자 그룹의 UM 사서함 정책에서 MWI 알림을 설정 및 해제할 수도 있습니다.



UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 MWI(Message Waiting Indicator) 허용

1.  EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동하고, 변경할 UM IP 게이트웨이를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM IP 게이트웨이** 페이지에서 **MWI(Message Waiting Indicator) 허용** 옆의 확인란을 선택합니다.

3.  **저장**을 클릭합니다.

## 셸을 사용하여 MWI(Message Waiting Indicator) 허용

이 예에서는 IP 주소가 10.10.10.1인 `MyUMIPGateway`라는 UM IP 게이트웨이에 연결된 사용자에게 Message Waiting Indicator가 표시되도록 허용합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $true

