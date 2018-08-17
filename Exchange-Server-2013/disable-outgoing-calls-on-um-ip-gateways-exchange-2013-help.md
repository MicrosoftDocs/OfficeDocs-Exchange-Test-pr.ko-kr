---
title: 'UM IP 게이트웨이에서 거는 전화를 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이에서 거는 전화를 사용 하지 않도록 설정
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 50483789
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이에서 거는 전화를 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-13_

UM(통합 메시징) IP 게이트웨이의 보내는 호출을 사용하거나 사용하지 않도록 설정할 수 있습니다. UM IP 게이트웨이의 속성에서 **이 UM IP 게이트웨이를 통한 발신 전화 허용** 옵션을 선택 취소하면 VoIP(Voice over IP) 게이트웨이, IP PBX 또는 SBC(Session Border Controller)에 대한 발신 전화를 수락하지 않고 보내지 않도록 UM IP 게이트웨이가 구성됩니다. **이 UM IP 게이트웨이를 통해 보내는 호출 허용** 설정에 따라 UM IP 게이트웨이가 사용자의 보내는 호출을 시작할 수 있는지 여부가 제어되지만 VoIP 게이트웨이, IP PBX 또는 SBC의 호출 전송 또는 들어오는 호출에는 영향을 주지 않습니다.

UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM IP 게이트웨이의 보내는 호출을 사용하지 않도록 설정

1.  EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동하고, 변경할 UM IP 게이트웨이를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM IP 게이트웨이** 페이지에서 **이 UM IP 게이트웨이를 통한 발신 전화 허용** 옆에 있는 확인란의 선택을 취소합니다.

3.  **저장**을 클릭합니다.

## 셸을 사용하여 UM IP 게이트웨이의 보내는 호출을 사용하지 않도록 설정

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이의 보내는 호출을 사용하지 않도록 설정합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false

