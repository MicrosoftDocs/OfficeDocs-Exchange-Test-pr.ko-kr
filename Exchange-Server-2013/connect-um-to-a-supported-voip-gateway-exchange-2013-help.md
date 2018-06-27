---
title: '지원 되는 VoIP 게이트웨이를 UM에 연결: Exchange 2013 Help'
TOCTitle: 지원 되는 VoIP 게이트웨이를 UM에 연결
ms:assetid: b8dfc8bd-2ee5-418d-b0a4-4fa2ec7e2a2e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124360(v=EXCHG.150)
ms:contentKeyID: 50556072
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 지원 되는 VoIP 게이트웨이를 UM에 연결

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-04-19_

UM(통합 메시징)을 설정할 경우 Exchange 조직에서 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버 및 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버와 통신할 수 있도록 네트워크에 VoIP(Voice over IP) 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC(Session Border Controller)를 구성해야 합니다. 또한 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC와 통신할 수 있도록 클라이언트 액세스 서버 및 사서함 서버를 구성해야 합니다.


> [!NOTE]
> 클라이언트 액세스 서버 및 사서함 서버를 데이터 네트워크의 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC에 연결한 후에는 필요한 UM 구성 요소를 만들고 사용자가 통합 메시징을 사용할 수 있도록 설정해야 합니다. 그래야 음성 메일 시스템을 사용할 수 있습니다.



## 단계

VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC를 클라이언트 액세스 서버 및 사서함 서버에 연결하기 위한 기본 단계는 다음과 같습니다.

1단계: 조직에 클라이언트 액세스 서버 및 사서함 서버를 설치합니다.

2단계: 내선 번호, SIP URI 또는 E.164 UM 다이얼 플랜을 만들고 구성합니다.

3단계: UM IP 게이트웨이를 만들고 구성합니다. 수신 전화를 수락하고 발신 전화를 보낼 각 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC에 대해 UM IP 게이트웨이를 만들고 구성해야 합니다.

4단계: 필요한 경우 새 UM 헌트 그룹을 만듭니다. UM IP 게이트웨이를 만들 때 UM 다이얼 플랜을 지정하지 않은 경우 UM 헌트 그룹이 자동으로 만들어집니다.

각 단계에 대한 내용은 다음 섹션을 참조하십시오.

## 1단계: 클라이언트 액세스 서버 및 사서함 서버 설치

조직에 Exchange 서버를 배포할 때 클라이언트 액세스 서버와 사서함 서버를 동일한 컴퓨터에 설치하거나 클라이언트 액세스 서버를 사서함 서버와는 별개의 컴퓨터에 설치할 수 있습니다. 클라이언트 액세스 서버를 설치하려면 설치 미디어에서 Setup.exe를 실행합니다. 클라이언트 액세스 서버를 사서함 서버와는 별개의 컴퓨터에 설치하거나 동일한 컴퓨터에 설치할 때 모두 동일한 명령을 사용합니다. 자세한 내용은 [설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)를 참조하십시오. 기존 Exchange 서버에 기능을 추가하려는 경우 **프로그램 및 기능**이나 Setup.exe를 사용합니다.

## 2단계: UM 다이얼 플랜 만들기 및 구성

필요한 서버를 설치했으면 먼저 UM 다이얼 플랜을 만들어야 합니다. UM 다이얼 플랜은 단일 또는 여러 UM IP 게이트웨이에 연결하여 전화 통신 네트워크에 연결할 수 있도록 하는 구성 설정을 포함합니다. UM IP 게이트웨이와 UM 헌트 그룹은 UM 다이얼 플랜에 바로 연결되며 이 두 항목 역시 필요한 요소입니다. 자세한 내용은 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

UM 다이얼 플랜은 사용자의 내선 전화 번호에서 UM 사용 가능 사서함으로의 링크를 설정합니다. UM 다이얼 플랜을 만들 때 다이얼 플랜에 대한 내선 번호 자릿수, URI(Uniform Resource Identifier) 유형 및 VoIP 보안 설정을 구성할 수 있습니다.

다이얼 플랜 유형에는 내선 번호, SIP(Session Initiation Protocol) URI 및 E.164의 세 가지가 있습니다. UM 다이얼 플랜을 만들고 구성할 때 IP PBX, SIP 사용 가능 PBX 또는 PBX에서 전송되는 정보의 유형을 결정하고, 통화를 클라이언트 액세스 서버 또는 사서함 서버로 전송할 때 내선 번호 형식을 사용할지 E.164 형식을 사용할지 결정해야 합니다. Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 배포할 경우 SIP URI 다이얼 플랜을 만들고 구성해야 합니다.

## 3단계: UM IP 게이트웨이 만들기 및 구성

UM 다이얼 플랜을 만들었으면 네트워크의 각 VoIP 게이트웨이, IP PBX 또는 SBC를 나타내기 위해 UM IP 게이트웨이를 만들어야 합니다. UM IP 게이트웨이를 만들 때 UM IP 게이트웨이가 IP 주소 또는 FQDN(정규화된 도메인 이름)을 사용하도록 구성할 수 있습니다. FQDN을 사용하는 경우에는 호스트 이름이 올바른 IP 주소로 확인되도록 IP 게이트웨이의 DNS 호스트 레코드가 올바르게 구성되어 있어야 합니다.

VoIP 게이트웨이, IP PBX 또는 SBC를 설치했으면 실제 하드웨어 장치를 나타내기 위해 UM IP 게이트웨이를 만들어야 합니다. UM IP 게이트웨이가 생성되면, UM IP 게이트웨이를 사용하는 클라이언트 액세스 서버는 VoIP 게이트웨이, IP PBX 또는 SBC가 응답하는지 확인하기 위해 SIP OPTIONS 요청을 보냅니다. VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC가 응답하지 않으면 클라이언트 액세스 서버는 요청이 실패했음을 알리는 ID 1088을 사용하여 이벤트를 기록합니다. 이 문제를 해결하려면 VoIP 게이트웨이, IP PBX 또는 SBC가 사용 가능하고 온라인 상태이며 통합 메시징 구성이 올바른지 확인하십시오.

클라이언트 액세스 서버 및 사서함 서버는 신뢰할 수 있는 SIP 피어로 나열된 VoIP 게이트웨이, IP PBX 또는 SBC와만 통신합니다. 경우에 따라 두 개의 VoIP 게이트웨이, IP PBX 또는 SBC가 동일한 IP 주소를 사용하도록 구성되어 있으면 ID 1175 이벤트가 기록됩니다. 이 이벤트는 네트워크에 있는 VoIP 게이트웨이의 FQDN(정규화된 도메인 이름)을 사용하여 DNS 영역을 구성한 경우에 발생할 수 있습니다. 통합 메시징은 사서함 서버에 있는 통합 메시징 웹 서비스 가상 디렉터리의 내부 URL을 검색한 다음 이 URL을 사용하여 신뢰할 수 있는 SIP 피어의 FQDN 목록을 작성하는 방법으로 무단 요청을 차단합니다. 두 FQDN이 동일한 IP 주소로 확인되면 이 이벤트가 로깅됩니다.

UM IP 게이트웨이가 FQDN을 사용하도록 구성되어 있고, MicrosoftExchange 통합 메시징 서비스가 시작된 이후 UM IP 게이트웨이의 DNS 레코드가 변경된 경우에는 이 서비스를 다시 시작해야 합니다. 서비스를 다시 시작하지 않으면 사서함 서버가 UM IP 게이트웨이를 찾을 수 없게 됩니다. 사서함 서버에서는 모든 UM IP 게이트웨이에 대한 캐시가 메모리에서 유지 관리되며, 서비스가 다시 시작되거나 VoIP 게이트웨이, IP PBX 또는 SBC의 구성이 변경된 경우에만 DNS 확인이 수행되기 때문입니다.

Exchange 통합 메시징은 다양한 VoIP 게이트웨이 공급업체뿐 아니라 그 밖의 IP PBX, SIP 사용 가능 PBX 및 SBC 공급업체도 지원합니다. 지원되는 각 VoIP 게이트웨이는 다양한 타사 PBX 시스템에 연결하도록 설계되었습니다.

VoIP 게이트웨이에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md)

  - [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Um VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러에 연결](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)

자세한 내용은 [음성 메일 시스템 전화 네트워크에 연결](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)을 참조하십시오.

## 4단계: 새 UM 헌트 그룹 만들기(필요한 경우)

헌트 그룹이란 사용자 간에 공유되는 PBX(Private Branch Exchange) 또는 IP PBX 내선 번호 그룹을 설명하는 데 사용되는 용어입니다. 이러한 헌트 그룹은 특정 사업부로 들어오고 발신 전화를 효율적으로 분배하는 데 사용됩니다. 헌트 그룹을 만들고 정의하면 전화가 걸려 올 때 발신자가 통화 중 신호음을 받을 가능성이 최소화됩니다.

UM 헌트 그룹은 PBX 및 IP PBX에서 사용되는 헌트 그룹을 미러링합니다. PBX 또는 IP PBX를 구성할 때 UM 헌트 그룹을 하나 이상 만들고 구성해야 합니다. UM 헌트 그룹은 UM IP 게이트웨이와 UM 다이얼 플랜 간의 링크 역할을 합니다.

UM IP 게이트웨이를 만드는 방법에 따라 새 UM 헌트 그룹을 하나 또는 여러 개 만들어야 할 수 있습니다. UM IP 게이트웨이를 만들 때 UM IP 게이트웨이를 다이얼 플랜과 연결하지 않으면 기본적으로 단일 UM 헌트 그룹이 만들어집니다. UM IP 게이트웨이를 만들 때 UM IP 게이트웨이를 UM 다이얼 플랜에 연결하면 모든 수신 전화가 UM IP 게이트웨이를 통해 전송되고 클라이언트 액세스 서버 및 사서함 서버는 이러한 수신 전화를 수락합니다. UM IP 게이트웨이를 만들 때 UM IP 게이트웨이를 UM 다이얼 플랜에 연결하지 않은 경우에는 수신 전화가 UM IP 게이트웨이에서 다이얼 플랜으로 전달될 수 있도록 올바른 파일럿 식별자를 사용하여 UM 헌트 그룹을 만들어야 합니다.

Outlook Voice Access 및 자동 전화 교환 번호를 여러 개 사용하고 UM IP 게이트웨이를 다이얼 플랜에 연결한 경우에는 기본적으로 만들어진 UM 헌트 그룹을 삭제하고 여러 UM 헌트 그룹을 만들어야 합니다. UM 헌트 그룹을 만드는 방법에 대한 자세한 내용은 [UM 헌트 그룹 만들기](create-a-um-hunt-group-exchange-2013-help.md)를 참조하십시오.

