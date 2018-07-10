---
title: 'UM IP 게이트웨이에서 거는 전화를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이에서 거는 전화를 사용 하도록 설정
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 50484091
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이에서 거는 전화를 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-13_

발신 전화가 허용되지 않은 경우 UM(통합 메시징) IP 게이트웨이에서 발신 전화를 허용하도록 설정할 수 있습니다. UM IP 게이트웨이에 대한 속성에서 **이 UM 게이트웨이를 통해 나가는 호출 허용** 옵션을 선택하면 VoIP(Voice over IP) 게이트웨이, SIP(Session Initiation Protocol)에 사용할 수 있는 PBX(Private Branch eXchange), IP PBX 또는 SBC(Session Border Controller)에 대한 발신 전화를 허용하고 보내도록 UM IP 게이트웨이를 구성할 수 있습니다. **이 UM IP 게이트웨이를 통해 나가는 호출 허용** 설정에 따라 VoIP 게이트웨이, SIP에 사용할 수 있는 PBX, IP PBX 또는 SBC가 사용자에 대한 발신 전화를 시작할 수 있는지 여부가 제어되지만 UM IP 게이트웨이의 호출 전송 또는 수신 전화에는 영향을 주지 않습니다.

*외부로 전화 걸기*는 UM 다이얼 플랜의 사용자가 다른 다이얼 플랜의 UM 사용이 가능한 사용자 또는 외부 전화 번호로 전화를 거는 경우를 설명하는 데 사용되는 용어입니다.

UM 사용 가능 사용자에 대해 외부 전화 걸기를 허용하려면 다음을 수행해야 합니다.

  - UM IP 게이트웨이에서 보내는 호출을 허용하는지 확인합니다.

  - UM IP 게이트웨이와 연결된 UM 다이얼 플랜에서 전화 걸기 규칙 항목을 만들어 전화 걸기 규칙 그룹을 만듭니다.

  - UM 다이얼 플랜, 자동 전화 교환 또는 UM 사서함 정책의 **전화 걸기 권환 부여**에 있는 전화 걸기 제한 목록에 올바른 전화 걸기 규칙 그룹을 추가합니다.

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

## EAC를 사용하여 UM IP 게이트웨이에서 발신 전화를 허용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동하고, 변경할 UM IP 게이트웨이를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM IP 게이트웨이** 페이지에서 **이 UM IP 게이트웨이를 통해 나가는 호출 허용** 옆의 확인란을 선택합니다.

3.  **저장**을 클릭합니다.

## 셸을 사용하여 UM IP 게이트웨이에서 발신 전화를 허용하도록 설정

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이에서 발신 전화를 허용하도록 설정합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true

