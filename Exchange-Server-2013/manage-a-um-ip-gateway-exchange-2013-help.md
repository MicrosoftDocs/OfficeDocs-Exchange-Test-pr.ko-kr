---
title: 'UM IP 게이트웨이 관리: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이 관리
ms:assetid: 387e540f-8c59-42d2-a423-99fcf97e00aa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997283(v=EXCHG.150)
ms:contentKeyID: 50482881
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMIPGatewayGeneralPropertyPageControl
ms.translationtype: MT
---

# UM IP 게이트웨이 관리

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-21_

UM(통합 메시징) IP 게이트웨이를 만든 후 다양한 설정을 보거나 구성할 수 있습니다. 예를 들어 IP 주소 또는 FQDN(정규화된 도메인 이름)과 발신 전화 설정을 구성하고 MWI(Message Waiting Indicator)를 사용하거나 사용하지 않도록 설정할 수 있습니다.

UM IP 게이트웨이와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM IP 게이트웨이 절차](um-ip-gateway-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM IP 게이트웨이" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM IP 게이트웨이를 만들었는지 확인하십시오. 자세한 단계는 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM IP 게이트웨이 속성 보기 또는 구성

1.  EAC에서 **통합 메시징** \> **UM IP 게이트웨이**로 이동합니다. 목록 보기에서 관리하려는 UM IP 게이트웨이를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  
    
    **UM IP 게이트웨이** 페이지를 사용하여 UM IP 게이트웨이에 대한 설정을 보고 구성합니다. 다음 설정을 보거나 구성할 수 있습니다.
    
      - **상태**   이 표시 전용 필드에는 UM IP 게이트웨이의 상태가 표시됩니다.
    
      - **이름**   이 상자에 UM IP 게이트웨이의 고유 이름을 지정합니다. 이 이름은 EAC에 나타나는 표시 이름입니다. UM IP 게이트웨이를 만든 후 표시 이름을 변경해야 하는 경우 먼저 기존 UM IP 게이트웨이를 삭제한 다음 적합한 이름으로 다른 UM IP 게이트웨이를 만들어야 합니다. UM IP 게이트웨이 이름은 필수 항목이지만 표시 목적으로만 사용됩니다. 조직에서 여러 UM IP 게이트웨이를 사용할 수 있기 때문에 UM IP 게이트웨이에 의미 있는 이름을 사용하는 것이 좋습니다. UM IP 게이트웨이 이름의 최대 길이는 64자이며 공백을 포함할 수 있습니다.
    
      - **주소**   IP 주소나 FQDN(정규화된 도메인 이름)으로 UM IP 게이트웨이를 구성할 수 있습니다. 이 상자에 VoIP 게이트웨이, SIP 사용 PBX, IP PBX 또는 SBC에 구성된 IP 주소나 FQDN을 지정합니다.
        
        이 상자에는 영문자와 숫자를 입력할 수 있습니다. IPv4 주소, IPv6 주소 및 FQDN을 사용할 수 있습니다. FQDN을 사용하는 경우 호스트 이름이 올바른 IP 주소로 확인되도록 VoIP 게이트웨이의 DNS 호스트 레코드가 올바르게 구성되었는지도 확인해야 합니다. 또한 IP 주소 대신 FQDN을 사용하고 UM IP 게이트웨이에 대한 DNS 구성이 변경된 경우 UM IP 게이트웨이의 구성 정보가 올바르게 업데이트되려면 UM IP 게이트웨이를 사용하지 않도록 설정한 후 사용하도록 다시 설정해야 합니다.
        
        SIP 보안이나 보안 모드에서 작동하는 다이얼 플랜과 UM IP 게이트웨이 간에 상호 TLS(상호 전송 계층 보안)를 사용하려는 경우 FQDN으로 UM IP 게이트웨이를 구성해야 합니다. 또한 포트 5061에서 수신 대기하도록 UM IP 게이트웨이를 구성하고, IP 게이트웨이 또는 IP PBX도 포트 5061에서 상호 TLS 요청을 수신 대기하도록 구성되었는지 확인해야 합니다. `Set-UMIPGateway -identity MyUMIPGateway -Port 5061`.
    
      - **이 UM IP 게이트웨이를 통해 나가는 호출 허용**   UM IP 게이트웨이가 나가는 호출을 받아들이고 처리할 수 있도록 하려면 이 확인란을 선택합니다. 이 설정은 VoIP 게이트웨이에서 들어오는 호출이나 호출 전송에 영향을 주지 않습니다.
        
        기본적으로 UM IP 게이트웨이를 만들 때 이 설정을 사용합니다. 이 설정을 사용하지 않도록 설정하면 다이얼 플랜과 연결된 사용자가 **주소** 필드에 정의된 VoIP 게이트웨이, IP PBX 또는 SBC를 통해 나가는 호출을 만들 수 없습니다.
    
      - **MWI(Message Waiting Indicator) 허용**   UM IP 게이트웨이가 받은 호출에 대해 사용자에게 음성 메일 알림을 보낼 수 있도록 하려면 이 확인란을 선택합니다. 이 설정을 사용하면 UM IP 게이트웨이가 사용자에 대해 SIP NOTIFY 메시지를 보내고 받을 수 있습니다. 이 설정은 기본적으로 사용하도록 설정되며 사용자에게 메시지 대기 알림을 보낼 수 있습니다.
        
        MWI(Message Waiting Indicator)는 새 메시지나 듣지 않은 메시지가 있음을 나타내는 모든 메커니즘을 참조할 수 있습니다. Outlook 및 Outlook Web App와 같은 클라이언트의 받은 편지함에는 새 음성 메시지가 도착했다는 표시가 나타납니다. 등록된 휴대폰으로 SMS(Short Messaging Service) 또는 문자 메시지가 전송되거나, Exchange 서버에서 미리 구성된 번호로 아웃바운드 통화이 수행되거나, 사용자가 볼 수 있도록 데스크톱 전화 램프가 켜질 수 있습니다.

## 셸을 사용하여 UM IP 게이트웨이 속성 구성

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이의 IP 주소를 수정합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이가 들어오는 호출을 수락하지 않도록 하고 나가는 호출을 차단합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address voipgateway.contoso.com -Status 2 -OutcallsAllowed $false

이 예는 UM IP 게이트웨이가 VoIP 게이트웨이 시뮬레이터로 작동할 수 있도록 하며, **Test-UMConnectivity** cmdlet과 함께 사용할 수 있습니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Simulator $true


> [!IMPORTANT]
> UM IP 게이트웨이의 구성에 대한 모든 변경 내용이 UM IP 게이트웨이와 같은 UM 다이얼 플랜의 모든 Exchange 서버로 복제될 때까지는 일정한 대기 시간이 있습니다.



이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이가 수신 전화를 받지 못하게 하고 발신 전화를 방지하며 IPv6 주소를 설정하고 UM IP 게이트웨이가 IPv4 및 IPV6 주소를 사용하도록 허용합니다.

    Set-UMIPGateway -Identity MyUMIPGateway -Address fe80::39bd:88f7:6969:d223%11 -IPAddressFamily Any -Status Disabled -OutcallsAllowed $false

## 셸을 사용하여 UM IP 게이트웨이 속성 보기

이 예에서는 Active Directory 포리스트의 모든 UM IP 게이트웨이를 서식 있는 목록으로 표시합니다.

    Get-UMIPGateway |Format-List

이 예에서는 `MyUMIPGateway`라는 UM IP 게이트웨이의 속성을 표시합니다.

    Get-UMIPGateway -Identity MyUMIPGateway

이 예에서는 Active Directory 포리스트의 VoIP 게이트웨이 시뮬레이터를 포함하여 모든 UM IP 게이트웨이를 표시합니다.

    Get-UMIPGateway -IncludeSimulator $true

