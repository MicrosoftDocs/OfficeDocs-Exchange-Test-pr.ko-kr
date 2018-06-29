---
title: 'UM IP 게이트웨이 삭제 합니다.: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이 삭제 합니다.
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 50483146
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이 삭제 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-21_

UM(통합 메시징) IP 게이트웨이를 삭제하면 Exchange 서버는 해당 UM IP 게이트웨이와 연결된 VoIP(Voice over IP) 게이트웨이, SIP(Session Initiation Protocol) 사용 가능 PBX(Private Branch eXchange), IP PBX 또는 SBC(Session Border Controller)에서 들어오는 수신 전화를 더 이상 수락할 수 없게 됩니다.


> [!IMPORTANT]
> VoIP 게이트웨이, IP PBX 또는 SBC와의 통신을 해제할 경우 받게 될 영향을 완전히 이해한 후 UM IP 게이트웨이를 삭제하는 것이 좋습니다.



UM IP 게이트웨이와 관련된 추가 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM IP 게이트웨이 삭제

1.  EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동하고, 삭제할 UM IP 게이트웨이를 선택한 다음 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

2.  **경고** 페이지에서 **예**를 클릭합니다.

## 셸을 사용하여 UM IP 게이트웨이 삭제

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이를 삭제합니다.

    Remove-UMIPGateway -Identity MyUMIPGateway

