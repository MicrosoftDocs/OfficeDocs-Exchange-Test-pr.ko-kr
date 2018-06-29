---
title: 'UM IP 게이트웨이 만들기: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이 만들기
ms:assetid: 542d6b50-147b-4cec-b54d-61c7b8fc0fc7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998045(v=EXCHG.150)
ms:contentKeyID: 50483127
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.CreateUMIPGatewayWizardForm.CreateUMIPGatewayWizardPage
ms.translationtype: MT
---

# UM IP 게이트웨이 만들기

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-04-16_

UM(통합 메시징) IP 게이트웨이를 만들 때 Exchange 서버가 새 VoIP(Voice over IP) 게이트웨이, SIP(Session Initiation Protocol) 사용 가능 PBX(Private Branch eXchange), IP PBX 또는 SBC(Session Border Controller)에 연결하도록 설정합니다. UM IP 게이트웨이를 만든 직후에 새 UM 헌트 그룹을 만들어 UM IP 게이트웨이에 연결해야 합니다. 이때 하나 이상의 UM 헌트 그룹을 만들어 UM IP 게이트웨이를 하나 이상의 UM 다이얼 플랜과 연결할 수 있습니다.

UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM IP 게이트웨이 만들기

1.  
    
    EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동한 다음 **새로 만들기**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 UM IP 게이트웨이**에서 다음 정보를 입력합니다.
    
      - **이름**   이 상자에 UM IP 게이트웨이의 고유 이름을 지정합니다. 이 이름은 EAC에 나타나는 표시 이름입니다. UM IP 게이트웨이를 만든 후 표시 이름을 변경해야 하는 경우 먼저 기존 UM IP 게이트웨이를 삭제한 다음 원하는 이름으로 다른 UM IP 게이트웨이를 만들어야 합니다. UM IP 게이트웨이 이름은 필수 항목이지만 표시 목적으로만 사용됩니다. 조직에서 여러 UM IP 게이트웨이를 사용할 수 있기 때문에 UM IP 게이트웨이에 의미 있는 이름을 사용하는 것이 좋습니다. UM IP 게이트웨이 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다. 그러나 다음 문자는 사용할 수 없습니다. " / \\ \[ \] : ; | = , + \* ? \< \>.
    
      - **주소**   IP 주소나 FQDN(정규화된 도메인 이름)으로 UM IP 게이트웨이를 구성할 수 있습니다. 이 상자에 VoIP 게이트웨이, SIP 사용 PBX, IP PBX 또는 SBC에 구성된 IP 주소나 FQDN을 지정합니다. 이 상자에는 올바른 형식의 유효한 FQDN만 입력할 수 있습니다.
        
        이 상자에는 영문자와 숫자를 입력할 수 있습니다. IPv4 주소, IPv6 주소 및 FQDN을 사용할 수 있습니다. SIP 보안이나 보안 모드에서 작동하는 다이얼 플랜과 UM IP 게이트웨이 간에 상호 TLS(상호 전송 계층 보안)를 사용하려는 경우 FQDN으로 UM IP 게이트웨이를 구성해야 합니다. 또한 포트 5061에서 수신 대기하도록 UM IP 게이트웨이를 구성하고, VoIP 게이트웨이 또는 IP PBX도 포트 5061에서 상호 TLS 요청을 수신 대기하도록 구성되었는지 확인해야 합니다. UM IP 게이트웨이를 구성하려면 다음 명령을 실행합니다. `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
        
        FQDN을 사용하는 경우 호스트 이름이 올바른 IP 주소로 확인되도록 VoIP 게이트웨이의 DNS 호스트 레코드가 올바르게 구성되었는지도 확인해야 합니다. 또한 IP 주소 대신 FQDN을 사용하고 UM IP 게이트웨이에 대한 DNS 구성이 변경된 경우 UM IP 게이트웨이의 구성 정보가 올바르게 업데이트되려면 UM IP 게이트웨이를 사용하지 않도록 설정한 후 사용하도록 다시 설정해야 합니다.
    
      - **UM 다이얼 플랜**   **찾아보기**를 클릭하여 UM IP 게이트웨이와 연결할 UM 다이얼 플랜을 선택합니다. UM IP 게이트웨이와 연결할 UM 다이얼 플랜을 선택하면 기본 UM 헌트 그룹도 만들어져 선택한 UM 다이얼 플랜과 연결됩니다. UM 다이얼 플랜을 선택하지 않는 경우 UM 헌트 그룹을 수동으로 만든 다음 해당 UM 헌트 그룹을 만든 UM IP 게이트웨이와 연결해야 합니다.

3.  
    
    **저장**을 클릭합니다.

## 셸을 사용하여 UM IP 게이트웨이 만들기

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이를 만듭니다. 이 게이트웨이는 Exchange 서버가 VoIP 게이트웨이, SIP 사용 가능 PBX, IP PBX 또는 IP 주소가 10.10.10.1인 SBC에서 걸려오는 전화를 받을 수 있도록 합니다.

    New-UMIPGateway -Name MyUMIPGateway -Address 10.10.10.1

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이를 만듭니다. 이 게이트웨이는 Exchange 서버가 VoIP 게이트웨이, SIP 사용 가능 PBX, IP PBX 또는 FQDN이 MyUMIPGateway.contoso.com이고 포트 5061에서 수신 대기하는 SBC에서 걸려오는 전화를 받을 수 있도록 합니다.

    New-UMIPGateway -Name MyUMIPGateway -Address "MyUMIPGateway.contoso.com" -Port 5061

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이를 만들고 UM IP 게이트웨이가 수신 전화를 받지 못하게 하고 발신 전화를 방지하며 IPv6 주소를 설정하고 UM IP 게이트웨이가 IPv4 및 IPV6 주소를 사용하도록 허용합니다.

    New-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

