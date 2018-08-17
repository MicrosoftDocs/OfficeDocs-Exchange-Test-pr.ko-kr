---
title: 'UM IP 게이트웨이: Exchange 2013 Help'
TOCTitle: UM IP 게이트웨이
ms:assetid: 991d77e0-3995-44ab-bedf-52ff7a0301ab
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123890(v=EXCHG.150)
ms:contentKeyID: 50483730
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM IP 게이트웨이

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2014-06-24_

UM(통합 메시징) IP 게이트웨이는 실제 VoIP(Voice over IP) 게이트웨이, IP PBX(Private Branch eXchange) 또는 SBC(Session Border Controller) 하드웨어 장치를 나타냅니다. 음성 메일 사용자가 수신 전화를 받고 발신 전화를 거는 데 VoIP 게이트웨이, IP PBX 또는 SBC를 사용하려면 디렉터리 서비스에 UM IP 게이트웨이가 생성되어 있어야 합니다.

**목차**

Overview of UM IP gateways

UM IP gateways

IPv6 support for UM IP gateways

Enabling and disabling a UM IP gateway

## UM IP 게이트웨이 개요

일반적으로 *게이트웨이*는 서로 호환되지 않는 두 네트워크를 연결하는 실제 장치입니다. Exchange 통합 메시징 및 기타 통합 메시징 솔루션을 사용할 경우 VoIP 게이트웨이는 PSTN(공중 전화망)/TDM(Time Division Multiplex) 또는 회로 전환 기반 전화 통신 네트워크와 IP 또는 패킷 전환 데이터 네트워크 사이의 변환에 사용됩니다. IP PBX는 PSTN 네트워크와 패킷 전환 네트워크 간의 변환도 수행하므로 IP PBX를 사용할 때는 VoIP 게이트웨이가 필요하지 않습니다. VoIP 게이트웨이는 레거시 PBX 하드웨어 장치를 UM 배포에 연결하는 경우에만 필요합니다.


> [!NOTE]
> 패킷 전환 네트워크는 패킷(메시지 또는 메시지 조각)이 라우터, 스위치, VoIP 게이트웨이, IP PBX 및 SBC와 같은 장치 간에 개별적으로 라우팅되는 네트워크입니다. 이와 달리 회로 전환 네트워크에서는 두 노드 사이에 통신하는 동안 단독으로 사용되는 전용 연결을 설정합니다.



Exchange 통합 메시징은 VoIP 게이트웨이 기능에 의존하여 ISDN(Integrated Services Digital Network) 또는 QSIG 같은 TDM 또는 전화 통신 회로 전환 기반 프로토콜을 PBX에서 SIP(Session Initiation Protocol), RTP(Realtime Transport Protocol) 또는 실시간 팩스 전송용 T.38과 같은 VoIP 또는 IP 기반 프로토콜로 변환합니다.

IP PBX는 회로 전환 전화 통신 네트워크를 데이터 또는 패킷 전환 네트워크에 연결할 때도 사용됩니다. 또한 회로 전환 프로토콜을 SIP, RTP 및 SRTP(Secure RTPC)와 같은 VoIP 또는 IP에 기반한 프로토콜로 전환하는 데도 사용됩니다.

SBC(Session Border Controllers)는 VoIP 게이트웨이 및 IP PBX와 약간 다릅니다. SBC는 회로 전환 네트워크를 패킷 전환 네트워크에 연결하는 대신 인터넷과 같은 공개 네트워크 또는 사설 WAN 연결을 통해 두 데이터 네트워크를 연결하는 데 사용됩니다. 통합 메시징에서 SBC는 UM이 온-프레미스에 있는 일부 구성 요소와 클라우드에 있는 사서함 등의 다른 구성 요소를 사용하는 하이브리드 UM 배포에 사용됩니다.

## VoIP 장치 구성

PBX, VoIP 게이트웨이 IP PBX 및 SBC의 경우 제조업체와 유형이 다양하지만 VoIP 장치 구성에는 기본적으로 다음과 같은 세 가지 유형이 있습니다.

  - **IP PBX**   PSTN/TDM 또는 회로 전환 기반 전화 통신 네트워크와 IP 또는 패킷 전환 데이터 네트워크 간에 변환하는 단일 장치입니다.

  - **PBX(레거시) 및 VoIP 게이트웨이**   PSTN/TDM 또는 회로 전환 전화 통신 네트워크와 IP 또는 패킷 전환 데이터 네트워크 간에 전환하는 두 개의 개별적인 구성 요소입니다.

  - **SBC**   LAN 및 데이터 센터와 같은 두 유형의 IP 기반 네트워크를 연결하는 하나 또는 여러 개의 장치입니다.

통합 메시징을 지원하기 위해서는 전화 통신 네트워크 인프라를 데이터 네트워크 인프라에 연결하거나 온-프레미스 배포를 클라우드의 UM 배포와 연결할 때 IP/VoIP 장치 구성의 유형 중 하나 또는 두 가지가 모두 사용됩니다.

## UM IP 게이트웨이

UM IP 게이트웨이에는 하나 이상의 UM 헌트 그룹과 구성 설정이 포함됩니다. UM 헌트 그룹은 UM IP 게이트웨이를 UM 다이얼 플랜에 연결하는 데 사용됩니다. UM IP 게이트웨이와 UM 헌트 그룹의 조합으로 VoIP 게이트웨이, IP PBX 또는 SBC와 UM 다이얼 플랜 간의 연결이 설정됩니다. 여러 UM 헌트 그룹을 만들면 단일 UM IP 게이트웨이를 여러 UM 다이얼 플랜과 연결할 수 있습니다.

UM IP 게이트웨이를 만든 후에는 UM IP 게이트웨이에 연결된 Exchange 서버가 SIP OPTIONS 요청을 VoIP 게이트웨이, IP PBX 또는 SBC로 전송하여 장치가 응답하는지 확인합니다. VoIP 게이트웨이, IP PBX 또는 SBC가 요청에 응답하지 않으면 Exchange 서버는 요청이 실패했음을 알리는 ID 1400을 사용하여 이벤트를 기록합니다. 이 경우에는 VoIP 게이트웨이, IP PBX 또는 SBC를 사용할 수 있고 온라인 상태이며 통합 메시징 구성이 올바른지 확인하십시오.

사서함 서버는 신뢰할 수 있는 SIP 피어로 나열된 VoIP 게이트웨이, IP PBXs 또는 SBC와의 통신만 수행합니다. 경우에 따라 두 개의 VoIP 게이트웨이, IP PBX 또는 SBC가 동일한 IP 주소를 사용하도록 구성되어 있으면 ID 1175 이벤트가 기록됩니다. 통합 메시징은 통합 메시징 웹 서비스 가상 디렉터리의 내부 URL을 검색함으로써 무단 요청을 차단하며, 그런 다음 URL을 사용하여 신뢰할 수 있는 SIP 피어의 FQDN 목록을 작성합니다. 두 개의 FQDN이 동일한 IP 주소로 확인되면 이 이벤트가 기록됩니다.

## UM IP 게이트웨이에 대한 IPv6 지원

IPv6(인터넷 프로토콜 버전 6)은 가장 최근 버전의 IP(인터넷 프로토콜)입니다. IPv6에서는 이전 버전의 IP인 IPv4의 많은 결점이 수정되었습니다. Microsoft Exchange Server 2010 온-프레미스 및 하이브리드 배포에서 IPv6는 IPv4도 사용되는 경우에만 지원되었습니다.

Exchange 2013 온-프레미스 및 하이브리드 배포에서는 UM 관련 구성 요소와 음성 서비스가 클라이언트 액세스 및 사서함 서버에서만 실행됩니다. 이제 UM 아키텍처가 변경되어 IPv4 및 IPv6과 기타 Exchange 기능을 지원하기 위해서는 UCMA(Unified Communications Managed API) v4.0이 필요하므로, 통합 메시징 구성 요소와 서비스가 있는 클라이언트 액세스 및 사서함 서버는 IPv6 네트워크를 완전히 지원하며 IPv4가 필요하지 않습니다.

온-프레미스, 하이브리드 및 Exchange Online 배포에서 엔터프라이즈 및 Exchange Online UM 관리자는 라우터, IP 게이트웨이, IP PBX, Microsoft Office Communications Server 2007 R2 및 Microsoft Lync Server와 같은 장치를 포함한 IPv6 지원 장치에 UM을 연결할 때 IPv6를 사용할 수 있습니다. 하지만 이전 버전과의 호환성과 상호 운용성을 위해 UM IP 게이트웨이에서 *IPAddressFamily* 매개 변수를 `Any`로 설정하면 추가적인 구성 변경 없이 IPv4를 대신 사용할 수 있습니다.

Exchange UM은 여전히 SIP 피어(VoIP 게이트웨이, IP PBX 및 SBC)와 직접 통신해야 하는데 이러한 피어는 자체 소프트웨어 또는 펌웨어에서 IPv6를 지원하지 않을 수 있습니다. IPv6를 지원하지 않는 경우 UM은 IPv4를 사용하는 SIP 피어와 직접 통신할 수 있어야 합니다. 호스트된 음성 메일의 경우 UM은 SBC, Lync Server 2010 또는 Lync Server 2013을 통해 고객 장비와 통신합니다. 호스트된 환경에서는 IPv6에서 IPv4로의 변환 프로세스를 처리하기 위해 SBC 및 Lync 서버와 같은 IPv6 SIP 인식 클라이언트를 배포할 수 있습니다.

클라이언트 액세스 서버 및 사서함 서버를 설치한 후 온-프레미스 및 하이브리드 배포의 경우 그리고 Exchange Online UM 배포의 경우 UM IP 게이트웨이를 만들어야 합니다. UM IP 게이트웨이에서 IPv6을 지원해야 하는 경우 다음 작업도 수행해야 합니다.

1.  새 UM IP 게이트웨이를 만들거나 네트워크의 각 IP 게이트웨이, IP PBX 또는 SBC의 IPv6 주소로 기존 UM IP 게이트웨이를 구성합니다. 필요한 UM IP 게이트웨이를 만들고 구성하는 경우 UM IP 게이트웨이에 대한 IPv6 주소 또는 FQDN(정규화된 도메인 이름)을 추가해야 합니다. UM IP 게이트웨이에 FQDN을 추가하는 경우 UM IP 게이트웨이 FQDN을 IPv6 주소로 확인할 수 있도록 올바른 DNS 레코드를 만들었어야 합니다. 기존 UM IP 게이트웨이가 있는 경우 **Set-UMIPgateway** cmdlet을 사용하여 IPv6 주소 또는 FQDN을 구성할 수 있습니다.

2.  각 UM IP 게이트웨이에 대해 *IPAddressFamily* 매개 변수를 구성합니다. VoIP 게이트웨이가 IPv6 패킷을 수락할 수 있도록 하려면 **Set-UMIPgateway** cmdlet을 사용하여 UM IP 게이트웨이가 IPv4 및 IPv6 연결을 모두 수락하거나 IPv6 연결만 수락하도록 설정해야 합니다.

3.  UM IP 게이트웨이를 구성한 후에는 네트워크의 VoIP 게이트웨이, IP PBX 및 SBC가 IPv6을 지원하도록 구성해야 합니다. 자세한 내용을 알아보려면 하드웨어 공급업체에 IPv6을 지원하는 장치 목록과 올바른 구성 방법을 문의하십시오.


> [!NOTE]
> 다이얼 플랜당 최대 UM IP 게이트웨이 수는 200입니다. 200개 넘게 만들 경우 UM 서비스가 시작되지 않습니다.



## UM IP 게이트웨이 사용 또는 사용 안 함

기본적으로 UM IP 게이트웨이를 만들고 나면 사용할 수 있는 상태가 되지만 UM IP 게이트웨이를 사용하거나 사용하지 않도록 설정할 수 있습니다. UM IP 게이트웨이를 사용하지 않도록 설정하는 경우 모든 Exchange 서버가 기존 통화를 삭제하도록 설정할 수 있습니다. 또는 UM IP 게이트웨이와 연관된 Exchange 서버가 VoIP 게이트웨이, IP PBX 또는 SBC에서 보내는 모든 새 통화의 처리를 중지하도록 설정할 수 있습니다.

통합 메시징을 Office Communications Server R2 또는 Microsoft Lync Server와 통합하는 경우에는 하나의 UM IP 게이트웨이만 사용자의 발신 전화를 처리하도록 허용하고 SIP URI 다이얼 플랜과 연결된 다른 모든 UM IP 게이트웨이에서는 아웃바운드 통화를 사용하지 않도록 설정해야 합니다. 셸 또는 EAC를 사용하여 아웃바운드 통화를 사용하지 않도록 설정합니다.

온-프레미스 및 하이브리드 배포에 대해 발신 전화를 허용할 UM IP 게이트웨이를 선택할 때는 가장 많은 트래픽을 처리할 가능성이 있는 게이트웨이를 선택합니다. Lync Server Director 풀에 연결되는 UM IP 게이트웨이를 통해 트래픽이 나가도록 허용하지 마십시오. 이는 외부 사용자에게 보내는 아웃바운드 통화가 회사 방화벽을 안정적으로 통과하는 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버에 의해 수행되도록 하기 위해서입니다(예: 전화에서 재생 시나리오).

