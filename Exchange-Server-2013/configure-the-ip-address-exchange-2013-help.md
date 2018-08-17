---
title: 'IP 주소를 구성 합니다.: Exchange 2013 Help'
TOCTitle: IP 주소를 구성 합니다.
ms:assetid: 100541c1-2297-4c46-9602-b304736541a8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266940(v=EXCHG.150)
ms:contentKeyID: 50482526
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IP 주소를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-11_

UM(통합 메시징) IP 게이트웨이를 만들기 전에 먼저 사용 중인 VoIP 게이트웨이, IP PBX 또는 SBC(Session Border Controller)에 대해 IP 주소 또는 FQDN(정규화된 도메인 이름)을 설정해야 합니다. 그런 다음 UM IP 게이트웨이를 만들 때 IP 주소 또는 FQDN을 설정합니다. IP 주소 또는 FQDN을 나중에 변경할 수 있습니다.

IP 주소 또는 FQDN을 구성하려면 EAC 또는 셸을 사용합니다. EAC에서 **UM IP 게이트웨이** 페이지의 **주소** 상자에는 IPv4 IP 주소, IPv6 주소 또는 FQDN을 입력할 수 있습니다. 셸에서 **Set-UMIPGateway** cmdlet의 *Address* 매개 변수를 사용하여 IPv4 IP 주소, IPv6 주소 또는 FQDN을 설정할 수도 있습니다. FQDN을 사용하여 UM IP 게이트웨이를 만드는 경우 DNS 전달 조회 영역에 적절한 HOST A 레코드를 만들어야 합니다. UM IP 게이트웨이의 DNS 구성이 변경되는 경우 UM IP 게이트웨이의 구성 정보가 올바르게 업데이트되게 하려면 UM IP 게이트웨이를 사용하지 않도록 설정했다가 다시 사용하도록 설정해야 합니다.

UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md) 항목을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md) 항목을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM IP 게이트웨이에 IP 주소 구성

1.  EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동하고, 수정할 UM IP 게이트웨이를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM IP 게이트웨이** 페이지의 **주소** 상자에 VoIP 게이트웨이, IP PBX 또는 SBC(Session Border Controller)의 IP 주소를 입력합니다.

3.  **저장**을 클릭하여 변경 내용을 저장합니다.


> [!IMPORTANT]
> UM IP 게이트웨이의 IP 주소 대신 FQDN을 사용할 경우 올바른 DNS 레코드가 만들어졌는지 확인하십시오.



## 셸을 사용하여 UM IP 게이트웨이에 IP 주소 구성

이 예에서는 IP 주소 10.10.10.1의 `MyUMIPGateway`라는 UM IP 게이트웨이를 구성합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

이 예에서는 IP 주소가 10.10.10.10이고 TCP 포트 5061에서 SIP 요청을 수신하는 `MyUMIPGateway`라는 UM IP 게이트웨이를 구성합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.10 -Port 5061

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이가 수신 전화 및 발신 전화를 금지하고, IPv6 주소를 설정하고, UM IP 게이트웨이가 IPv4 및 IPV6 주소를 사용하도록 허용합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

