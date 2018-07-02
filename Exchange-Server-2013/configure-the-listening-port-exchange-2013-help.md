---
title: '수신 대기 포트를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 수신 대기 포트를 구성 합니다.
ms:assetid: 200ecbd8-18c3-4594-9cc8-924b3ab4eca1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633457(v=EXCHG.150)
ms:contentKeyID: 50555957
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수신 대기 포트를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

UM(통합 메시징) IP 게이트웨이에서 SIP(Session Initiation Protocol) 요청을 수신 대기하는 데 사용되는 TCP 포트를 구성할 수 있습니다. 기본적으로, UM IP 게이트웨이를 만들 때 TCP SIP 수신 대기 포트 번호는 5060으로 설정됩니다. TCP SIP 수신 대기 포트는 EAC를 사용하여 구성하거나 변경할 수 없습니다. TCP SIP 수신 대기 포트 번호는 **Set-UMIPGateway** cmdlet을 사용하여 구성해야 합니다.

다음과 같이 하려는 경우 TCP 수신 대기 포트 번호를 5061로 구성해야 할 수 있습니다.

  - UM 다이얼 플랜에서 VoIP를 SIP 보안으로 설정

  - UM 다이얼 플랜에서 VoIP를 보안으로 설정

  - Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server와 통합

  - 상호 TLS(상호 전송 계층 보안)를 사용하여 Exchange 서버와 VoIP 게이트웨이, SIP 사용 가능 PBX(Private Branch Exchange), IP PBX 또는 SBC(Session Border Controller) 간의 네트워크 데이터를 암호화

SIP 보안 또는 보안 모드로 작동 중인 다이얼 플랜과 UM IP 게이트웨이 간에 상호 TLS를 사용하려면 UM IP 게이트웨이를 만들 때 FQDN(정규화된 도메인 이름)을 사용하여 구성한 다음 셸을 사용하여 TCP 포트 5061에서 수신 대기하도록 UM IP 게이트웨이를 구성해야 합니다. 또한 VoIP 게이트웨이, SIP 사용 가능 PBX, IP PBX 및 SBC가 포트 5061에서 상호 TLS 요청을 수신 대기하도록 구성되었는지 확인해야 합니다.


> [!IMPORTANT]
> FQDN을 사용하여 UM IP 게이트웨이를 만들 경우 DNS 정방향 조회 영역에 적절한 호스트 (A) 레코드를 만들어야 합니다. FQDN으로 UM IP 게이트웨이를 만든 경우 UM IP 게이트웨이의 DNS 구성이 변경되면 UM IP 게이트웨이를 사용하지 않도록 설정했다가 다시 사용하도록 설정하여 UM IP 게이트웨이의 구성 정보가 올바르게 업데이트되도록 해야 합니다.



UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인합니다. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 TCP 수신 대기 포트 구성

이 예에서는 mTLS.MyUMIPGateway.contoso.com이라는 FQDN을 가진 `MyUMIPGateway`라는 UM IP 게이트웨이를 구성하고 TCP 포트 5061에서 SIP 요청을 수신 대기합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address mTLS.MYUMIPGateway.contoso.com -Port 5061

이 예에서는 SIPSecured.MyUMIPGateway.contoso.com이라는 FQDN을 가진 `MyUMIPGateway`라는 UM IP 게이트웨이를 구성하고 TCP 포트 5061에서 SIP 요청을 수신 대기합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address SIPSecured.MyUMIPGateway.contoso.com -Port 5061

이 예에서는 MyOCSUMIPGateway.contoso.com이라는 FQDN을 가진 `MyUMIPGateway`라는 UM IP 게이트웨이를 구성하고 TCP 포트 5061에서 SIP 요청을 수신 대기합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address MyOCSUMIPGateway.contoso.com -Port 5061

