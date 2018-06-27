---
title: '통합 메시징의 IPv6 지원: Exchange 2013 Help'
TOCTitle: 통합 메시징의 IPv6 지원
ms:assetid: 91242c85-ce4e-422a-954e-ab623d3d6939
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150536(v=EXCHG.150)
ms:contentKeyID: 50483664
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 통합 메시징의 IPv6 지원

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-04-07_

IPv6(인터넷 프로토콜 버전 6)은 가장 최근 버전의 IP(인터넷 프로토콜)입니다. IPv6에서는 이전 버전의 IP인 IPv4의 많은 결점이 수정되었습니다. Microsoft Exchange Server 2010에서 IPv6은 IPv4도 함께 사용할 때만 지원됩니다. 순수 IPv6 Exchange 환경은 지원되지 않습니다. IPv6 주소 및 IP 주소 범위 사용은 Exchange 2010을 실행 중인 컴퓨터에서 IPv6과 IPv4가 모두 사용하도록 설정되어 있고 네트워크가 두 IP 주소 버전을 모두 지원하는 경우에만 지원됩니다. 그러나 IPv4와 IPv6이 완전히 다른 프로토콜이므로 IPv4 네트워크와 IPv6 네트워크는 서로 간에 직접 통신할 수 없습니다. 이 단점을 처리하려면 네트워크 관리자가 라우터와 같이 IPv4 네트워크와 IPv6 네트워크 간에 정보를 라우팅할 수 있는 장치를 배포해야 합니다. IPv4와 IPv6을 모두 사용하여 Exchange 2010을 배포하면 UM(통합 메시징)을 제외한 모든 서버 역할이 IPv6 주소를 사용하는 장치, 서버 및 클라이언트와 데이터를 주고받을 수 있습니다. Exchange 2013을 사용하는 경우 통합 메시징은 더 이상 Exchange 2007과 Exchange 2010의 전송 서버 역할, 클라이언트 액세스 서버 역할 및 사서함 서버 역할과 같은 별개의 서버 역할이 아닙니다. UM 관련 구성 요소와 음성 서비스는 클라이언트 액세스 서버와 사서함 서버에서만 실행됩니다.

Exchange 2013에서는 UM 아키텍처가 변경되어 이제 UCMA(Unified Communications Managed API) v4.0이 있어야 IPv4와 IPv6이 모두 지원되고 기타 Exchange 기능도 지원될 수 있습니다. 이에 따라 통합 메시징 구성 요소 및 서비스가 있는 클라이언트 액세스 서버와 사서함 서버가 모두 IPv6 네트워크를 완전히 지원합니다.

## IPv6 지원

Exchange 2010 서비스 팩 1 (SP1) 부터는 통합 메시징 서버 역할에 의존 UCMA 2.0의 기본 프로토콜 SIP (Session Initiation) 신호 및 음성에 대 한 처리 합니다. UCMA 2.0은 UM의 음성 기능에 대 한 주요 구성 요소입니다. UCMA 2.0 포함 되어 SIP 스택이, 미디어 스택에서, 및 음성 엔진에 대 한 음성 인식 ASR (자동), 텍스트 음성 변환 (TTS) 하 여 생성 되는 음성 합성 외에도 있습니다.

Exchange 2010 (IPv4 및 IPv6) 이중 스택 실행 된 필요 UM 제외 하 고 모든 서버 역할 UM UCMA 2.0 필요 하지만 IPv4, 하지 i p v 6을 지원 하기 때문에 합니다. Exchange 2013 대 한 UCMA 4.0은 UM 사용 하 고 클라이언트 액세스 및 사서함 서버에 Exchange 2013 를 설치 하는데 필요 합니다. UCMA 4.0은 새로운 기능을 지원 하 고 i p v 6을 지원 하기 위해 필요 합니다.

이제 UM이 UCMA 4.0을 사용하여 IPv6을 포함한 Exchange 2013의 새로운 기능을 지원하는 이유는 다음과 같습니다.

  - 일부 정부 기관에서 사용하는 제품에 대한 IPv6 지원이 필요합니다.

  - 이제 UM을 사용하려면 이중 스택(IPv4 및 IPv6)을 실행하거나 IPv6만 실행하는 라우터, IP 게이트웨이, IP PBX 및 SBC(Session Border Controller)와 같은 하드웨어 장치와의 호환성이 필요합니다.

  - Exchange 2013의 경우 Microsoft Exchange 통합 메시징 서비스는 사서함 서버에서 실행되고 Microsoft Exchange 통합 메시징 호출 라우터 서비스는 클라이언트 액세스 서버에서 실행됩니다. Exchange 2013에서 사서함 서버 역할과 클라이언트 액세스 서버 역할을 사용하려면 IPv4와 IPv6이 모두 필요합니다.

  - 온라인 서비스를 사용하면 클라이언트가 IPv4나 IPv6을 통해 해당 서비스에 연결할 수 있습니다.

  - 공용 IPv4 주소 공간이 부족합니다. Exchange Server 2013 Enterprise의 경우 UM이 항상 개인 IPv4 주소 공간과 함께 배포할 수 있는 내부 SIP 피어와 통신하므로 이 문제는 사실상 UM에 해당하는 문제가 아닙니다. 그러나 호스트된 Exchange UM의 경우에는 고객의 장비가 IPv4와 IPv6을 사용하여 호스트된 UM을 지원해야 합니다.

UM과 일부 전송 부분의 경우를 제외하고 Exchange 2013은 클라이언트 액세스 또는 사서함 서버가 IPv4와 IPv6을 사용하도록 설정한 상태에서 이중 스택 모드로 실행될 때 조직의 Exchange 2010 서버에 연결할 수 있습니다. 즉, 고객은 IPv4 스택 주소와 IPv6 스택 주소를 구성한 상태로 실행 중인 컴퓨터에 Exchange 2013을 설치할 수 있습니다. 이를 통해 IPv6 클라이언트와 Exchange Server 2010을 포함한 기타 Exchange 서버에서 Exchange 2013에 직접 연결할 수 있습니다.

UM은 이중 스택 모드로 실행 중인 Windows 서버에서 작동합니다. 이는 HTTP와 같은 프로토콜이 전송 유형을 무시하고, UM이 상호 종속되지 않는 VoIP(Voice over IP) 프로토콜(SIP/RTP/STUN/TURN/ICE 포함)을 사용하기 때문입니다. 여기에는 UM이 IP 게이트웨이, IP PBX 또는 SBC와 같은 SIP 피어에게 IP 주소 목록을 보급하고 전달하는 미디어 협상(RTP/SRTP)이 포함됩니다.

## UM에 대한 IPv6 지원은 무엇을 뜻합니까?

Exchange 2013 UM이 IPv6을 지원할 수 있으려면 라우터, IP 게이트웨이, IP PBX, Office Communications Server 2007 R2 및 Microsoft Lync Server와 같은 장치를 포함한 IPv6 사용 가능 장치에 UM을 연결할 때 엔터프라이즈 및 온라인 UM 관리자가 모두 IPv6을 이용할 수 있어야 합니다. 그러나 이전 Exchange 버전과의 상호 운용성 및 호환성을 위해 IPv6을 사용할 수 없는 경우 관리자는 구성을 추가로 변경할 필요없이 IPv4를 대신 사용할 수 있습니다.

Exchange 2013 Enterprise의 경우 UM은 해당 소프트웨어나 펌웨어에서 IPv6을 지원하지 않을 수도 있는 SIP 피어(IP 게이트웨이, IP PBX 및 SBC)와 직접 통신해야 합니다. 따라서 UM은 IPv4를 지원하는 SIP 피어와 직접 통신할 수 있어야 할 뿐 아니라 특히 IPv6와도 직접 통신할 수 있어야 합니다. 호스트된 Exchange 2013의 경우 UM은 SBC나 Lync Server 2010 또는 Lync Server 15를 통해 고객 장비와 통신합니다. 호스트된 Exchange 2013 환경에서는 SBC 및 Lync Server와 같은 IPv6 SIP 인식 클라이언트를 잠재적으로 배포할 수 있으므로 해당 클라이언트를 통해 IPv6-IPv4 변환 프로세스를 처리할 수 있습니다.

## IPv6에 대한 UM 장치 지원

UM 구성 요소 및 서비스를 실행하는 Exchange 2013 사서함 서버와 클라이언트 액세스 서버가 IPv6을 지원하므로 IP 게이트웨이, IP PBX 및 SBC 공급업체도 IPv6을 지원할 수 있어야 합니다. 다음과 같이 IPv6에 대한 장치 지원에 영향을 주는 몇 가지 문제가 있습니다.

  - IPv6을 지원할 수도 있는 IP 게이트웨이, IP PBX 및 SBC가 있지만 이러한 장치는 아직 IPv6 및 UM 관련 테스트를 거치지 않았습니다. 이 지원이 나중에 추가될 수도 있지만, 이는 하드웨어 공급업체에 따라 다릅니다.

  - 일부 IP 게이트웨이는 현재 IPv6을 지원하지 않습니다.

  - 일부 SBC의 경우 IPv4-IPv6 기능이 있지만 SRTP(Secure Real-time Transport Protocol)/SDES(Session Description Protocol Security)를 지원하지 않으므로 현재 UM에 대해 작동하지 않습니다.

  - 이중 스택과 순수 IPv6을 지원하지 않는 IP PBX가 있지만 이러한 장치는 아직 Exchange 2013 관련 테스트를 거치지 않았습니다.

현재 UCMA 4.0은 IPv6을 사용할 수 있습니다. 즉, UCMA 4.0이 IPv6 연결을 받아들일 수 있지만, 이중 모드로 작동하거나 아웃바운드 연결을 설정하는 경우 IPv4도 받아들일 수 있습니다. 이중 모드로 실행하면 이전 버전의 Exchange UM에 연결해야 할 때 IPv4 연결을 설정할 수 있습니다. Lync 설치의 경우 이 작업은 Active Directory에서 최신 버전의 Exchange Server에 대한 버전 정보를 가져오는 Lync Server를 통해 수행됩니다. IP 게이트웨이, IP PBX 및 SBC를 포함한 일반 전화 통신 장치의 경우 IPv4와 함께 IPv6 연결을 지원하려면 두 유형의 연결을 모두 수신 대기해야 합니다. 각 SIP 피어가 이전 Exchange UM 버전과의 호환성을 위해 두 유형의 연결을 모두 받아들일 수 있어야 하기 때문입니다. 이는 두 유형의 연결 모두에 대해 외부로 전화 걸기를 지원할 때도 필요합니다.

## IPv6을 지원하기 위한 UM 구성

클라이언트 액세스 서버와 사서함 서버를 설치한 후 통합 메시징 다이얼 플랜, 자동 전화 교환, IP 게이트웨이 및 헌트 그룹을 만들어야 합니다. UM이 IPv6을 지원하도록 허용하려면 다음을 수행해야 합니다.

  - 새 UM IP 게이트웨이를 만들거나 네트워크의 각 IP 게이트웨이, IP PBX 또는 SBC의 IPv6 주소로 기존 UM IP 게이트웨이를 구성합니다. 필요한 UM IP 게이트웨이를 만들고 구성하는 경우 UM IP 게이트웨이에 대한 IPv6 주소 또는 FQDN(정규화된 도메인 이름)을 추가해야 합니다. UM IP 게이트웨이에 FQDN을 추가하는 경우 UM IP 게이트웨이 FQDN을 IPv6 주소로 확인할 수 있도록 올바른 DNS 레코드를 만들었어야 합니다. 기존 UM IP 게이트웨이가 있는 경우 **Set-UMIPgateway** cmdlet을 사용하여 IPv6 주소 또는 FQDN을 구성할 수 있습니다. UM IP 게이트웨이를 만들거나 구성한 후 **Get-UMIPgateway** cmdlet을 통해 UM IP 게이트웨이 속성을 확인하여 IPv6 설정이 올바른지 파악할 수 있습니다.

  - 각 UM IP 게이트웨이에 대해 *IPAddressFamily* 매개 변수를 구성합니다. IP 게이트웨이가 IPv6 패킷을 받아들일 수 있도록 하려면 **Set-UMIPgateway** cmdlet을 통해 *IPAddressFamily* 매개 변수를 다음 중 하나로 설정하여 IPv4 연결과 IPv6 연결을 모두 받아들이거나 IPv6 연결만 받아들이도록 UM IP 게이트웨이를 설정해야 합니다.
    
      - *IPv4* – 기본값이며 다른 값이 구성되지 않은 경우에 사용됩니다.
    
      - *IPv6* - IPv6을 사용하도록 설정합니다. 그러나 IPv4는 사용되지 않습니다.
    
      - *Any* – IPv6을 사용하도록 허용하지만, 장치가 IPv6을 지원하지 않는 경우 IPv4가 대신 사용됩니다.

  - UM IP 게이트웨이를 구성한 후 네트워크의 IP 게이트웨이, IP PBX 및 SBC도 IPv6을 지원하도록 구성해야 합니다. 자세한 내용을 알아보려면 하드웨어 공급업체에 IPv6을 지원하는 장치 목록과 올바른 구성 방법을 문의하십시오.

  - 선택적으로, 두 서버 중 하나가 IPv4 트래픽만 수신하도록 설정된 경우 IPv6 트래픽을 받아들이도록 클라이언트 액세스 서버와 사서함 서버를 설정해야 할 수도 있습니다. 그러나 기본 설정을 사용하면 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 중인 클라이언트 액세스 서버와 Microsoft Exchange 통합 메시징 서비스를 실행 중인 사서함 서버가 모두 IPv4 트래픽과 IPv6 트래픽을 받아들입니다. 클라이언트 액세스 서버와 사서함 서버의 IPv6 설정 구성에 대한 자세한 내용은 [Set-UMCallRouterSettings](https://technet.microsoft.com/ko-kr/library/jj215758\(v=exchg.150\)) 및 [Set-UMService](https://technet.microsoft.com/ko-kr/library/jj552412\(v=exchg.150\)) 항목을 참조하십시오.
    
    IPv6을 지원하기 위해 클라이언트 액세스 서버와 사서함 서버에서 구성해야 할 수 있는 두 가지 매개 변수가 있습니다. *IPAddressFamily*와 *IPAddressFamilyConfigurable*가 이에 해당합니다. 클라이언트 액세스 서버와 사서함 서버가 IPv6 패킷을 받아들이도록 하려면 IPv4 연결과 IPv6 연결을 모두 받아들이거나 IPv6 연결만 받아들이도록 클라이언트 액세스 서버와 사서함 서버를 설정해야 합니다. *IPAddressFamily* 매개 변수를 구성하려면 *IPAddressFamilyConfigurable* 매개 변수를 `$true`로 설정해야 합니다.

## UM IP 주소 지정 논리

Exchange 2013에서 UM에 대한 IPv6 지원을 뒷받침하는 논리는 다음과 같습니다.

  - 이중 스택이 사용하도록 설정되어 있고 클라이언트 액세스 서버와 사서함 서버가 *IPv6*이나 *Any*로 설정되어 있는 경우 클라이언트 액세스 서버와 사서함 서버는 IPv4 인터페이스와 IPv6 인터페이스 모두에서 수신 대기합니다. 그렇지 않으면 IPv4만 사용됩니다.

  - 보내는 호출의 경우 UM IP 게이트웨이, 클라이언트 액세스 서버 및 사서함 서버의 *IPAddressFamily* 매개 변수가 *IPv6*이나 *Any*로 설정되어 있으면 UM이 이중 모드를 사용합니다. 그렇지 않으면 IPv4만 사용됩니다.

이중 모드에서 보내는 호출을 설정할 때 *IPAddressFamily* 매개 변수가 *IPv6*이나 *Any*로 설정되어 있는 경우

  - UCMA는 연결을 시도 중인 SIP 피어의 FQDN에 있는 주소 목록을 가져옵니다.

  - UCMA는 모든 IPv6 주소(있는 경우)를 시도합니다.

  - UCMA가 주소를 사용할 수 없다고 확인하면 해당 주소를 목록에 포함하고 구성한 간격을 기준으로 다시 시도하지 않습니다. 따라서 UM이 잘못된 것으로 알려진 주소를 불필요하게 다시 시도하지 않게 됩니다.

  - 사용 가능한 IPv6 주소가 없으면 UCMA가 SIP 피어의 주소 목록에 있는 IPv4 주소로 변경합니다.

