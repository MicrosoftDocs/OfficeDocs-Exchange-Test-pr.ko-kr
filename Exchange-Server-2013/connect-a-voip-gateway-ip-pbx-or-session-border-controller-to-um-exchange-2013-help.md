---
title: 'Um VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러에 연결: Exchange 2013 Help'
TOCTitle: Um VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러에 연결
ms:assetid: a7cecf59-b93a-413b-bb88-29f2669ef2cf
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124084(v=EXCHG.150)
ms:contentKeyID: 50556056
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Um VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러에 연결

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

IP Private Branch 교환 (Pbx) 올바르게 조직에 대 한 UM (통합 메시징)을 배포 하는 경우 및 (VoIP) IP 게이트웨이 통해 음성 구성 해야 합니다. 하이브리드 환경에서 UM을 배포 하는 경우 올바르게 세션 테두리 컨트롤러 (반자)를를 구성 해야 합니다. 이 작업을 수행 하는 인터페이스 또는 VoIP 게이트웨이, IP Pbx 및 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 하는 클라이언트 액세스 서버 및 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버와 통신 하는 Sbc의 인터페이스를 구성 해야 합니다.


> [!IMPORTANT]
> VoIP 게이트웨이, IP PBX 또는 웹 브라우저를 사용 하 여 SBC에 대 한 관리 작업을 수행 하는 경우에 네트워크를 통해 전송 되는 HTTP 요청 암호화 되지 않습니다. VoIP 게이트웨이, IP Pbx 또는 Sbc 사용자 네트워크에 대 한 보안 수준을 높이 데 관리 자격 증명 및 네트워크를 통해 전송 되는 데이터를 보호 하려면 인터넷 프로토콜 보안 (IPsec) 또는 Secure Sockets Layer (SSL)를 사용 합니다. 또한 장치에 대 한 관리 자격 증명을 보호 하기 위해 강력한 인증 메커니즘 및 복잡 한 관리 암호를 활용 하는 것이 좋습니다.



## 전화 통신 IP 장치 인터페이스

여러 유형의 포트 또는 PBX, VoIP 게이트웨이, IP PBX 또는 SBC 및 네트워크에 대 한 클라이언트 액세스 및 사서함 서버 간의 통신을 사용 하도록 구성 해야 하는 인터페이스 있습니다. VoIP 게이트웨이, IP PBX 또는 SBC를 구성할 때 아날로그, 디지털, 또는 아날로그 및 디지털 장치 인지 여부를 고려해 야 합니다.

PBX에 연결 하는 VoIP 게이트웨이 인터페이스 아날로그 있으면 클라이언트 액세스 및 사서함 서버와 통신 하도록 VoIP 게이트웨이 사용 하도록 설정 하 고 적절 한 설정을 올바르게 구성 해야 합니다. IP Pbx 및 Sbc 모두에 대 한 이러한 장치에 대 한 클라이언트 액세스 및 사서함 서버와 통신할 수 있도록 IP 인터페이스를 올바르게도 구성 해야 합니다. 이러한 모든 장치는 서로 다른 유형의 연결 또는 장치 모델 및 공급 업체에 따라 사용할 수 있는 포트 합니다.

네트워크에 대 한 클라이언트 액세스 및 사서함 서버와의 통신 수 있도록 합니다.

  - VoIP 게이트웨이 대 한 사용자의 Pbx와 통신에 대 한 전화 통신 인터페이스를 구성 해야 하며, 장치에 대 한 IP 인터페이스를 구성 해야 합니다.

  - IP Pbx에 대 한 회로 기반을 구성 하 고 해야 네트워크 또는 IP 기반 연결 합니다.

  - Sbc에 대 한 네트워크와 인터넷 또는 전용된 WAN 연결을 통해 연결 하는 다른 인터페이스에 대 한 두 IP 인터페이스를 구성 해야 합니다.

다음은 VoIP 게이트웨이, IP Pbx 및 Sbc를 올바르게 구성 하는데 도움이 되는 정보를 제공 하는 Exchange TechCenter에서 발견 된 자원의 목록입니다.

  - **지원 되는 IP 게이트웨이, IP PBX 및 PBX 설명서** [Exchange 2013에 대 한 전화 통신 관리자](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013) 구성 파일 및 VoIP 게이트웨이, IP Pbx, Pbx 및 Sbc를 구성할 때 사용할 수 있는 설치 정보를 포함 합니다.   

  - **구성 및 기술 정보** [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways) 구성 파일 및 VoIP 게이트웨이, IP Pbx 및 Pbx를 구성 하는 경우 사용할 수 있는 설치 정보를 포함 합니다.   

  - **Exchange UM online에 대 한 구성 참고 사항** [지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-session-border-controllers) 구성 파일 및 Sbc를 구성할 때 사용할 수 있는 설치 정보를 포함 합니다.   

통합된 메시징 전문가 전화 통신 및 IP 기반 네트워크 장치 구성에 도움이 될 수 있습니다. 통합 메시징 전문가 레거시에서 통합 메시징에 원활 하 게 전환 방법이 또는 타사 음성 메일 시스템 또는 계획 및 Exchange 통합 메시징이 있는 새 음성 메일 시스템을 배포할 수 있는지 확인 하는 데 도움이 됩니다. 새 음성 메일 시스템 배포 또는 업그레이드 하는 레거시 하나에는 VoIP 게이트웨이, IP Pbx, Pbx 및 통합 메시징에 대 한 중요 한 지식이 필요 합니다. 통합 메시징 전문가 게 문의 하는 방법에 대 한 자세한 내용은 [Microsoft Exchange Server 2013 통합 메시징 (UM) 전문가](http://go.microsoft.com/fwlink/p/?linkid=262708) 또는 [Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=261951)에서 인증 된 UM 파트너를 참조 하십시오.

VoIP 게이트웨이, IP PBX 또는 SBC IP 인터페이스를 구성한 후에 만들기 하 고 배포한 각 장치를 나타내려면 UM IP 게이트웨이 구성 해야 합니다. UM IP 게이트웨이를 만드는 방법에 대 한 자세한 내용은 [UM IP 게이트웨이 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway)을 참조 하십시오.

UM IP 게이트웨이 만든 후에 연결 된 UM IP 게이트웨이, 클라이언트 액세스 및 사서함 서버는 VoIP 게이트웨이, IP PBX 또는 응답 인지 확인 하는 SBC 옵션 SIP 요청을 보냅니다. VoIP 게이트웨이, IP PBX 또는 SBC 응답 하지 않으면 사서함 서버 요청이 실패 하는 ID 1088 되었다는와 이벤트를 기록 합니다. 이 문제를 해결 하려면 VoIP 게이트웨이, IP PBX 또는 SBC가 사용 가능 하 고 온라인 하 고 통합 메시징 구성이 올바른지 확인 합니다.

클라이언트 액세스 서버 및 사서함 서버 VoIP 게이트웨이, IP PBX 또는 신뢰할 수 있는 프로토콜 SIP (Session Initiation) 피어도 나열 된 SBC와만 통신할 됩니다. 여러 DNS 호스트 동일한 IP 주소를 공유 하는 경우 ID 1175를 사용 하 여 이벤트를 기록 됩니다. 이 이벤트는 네트워크에서 VoIP 게이트웨이 대 한 DNS 영역 Fqdn을 가진 구성 했는지 하는 경우 발생할 수 있습니다. 통합 메시징 사서함 서버에 있는 통합 메시징 웹 서비스 가상 디렉터리의 내부 URL을 검색 하 여 무단으로 요청을 보호 하 고 피어 다음 URL을 사용 하 여 신뢰할 수 있는 SIP에 대 한 Fqdn의 목록을 작성 합니다. 두 Fqdn 동일한 IP 주소로 확인 되 면이 이벤트가 기록 됩니다.


> [!NOTE]
> Microsoft Exchange 통합 메시징 서비스 하는 경우 VoIP 게이트웨이, IP PBX를 다시 시작 해야 또는 SBC FQDN 및 VoIP 게이트웨이, IP PBX의 DNS 레코드를 포함 하도록 구성 된 또는 SBC 서비스가 시작 된 후 변경 됩니다. 서비스를 다시 시작 하지는 사서함 서버는 VoIP 게이트웨이, IP PBX 또는 SBC를 찾을 수 없습니다. 이 사서함 서버 메모리에 모든 VoIP 게이트웨이, IP Pbx 또는 Sbc에 대 한 캐시를 유지 관리 및 서비스를 다시 시작 하는 경우에 DNS 확인을 수행 하기 때문에 또는 VoIP 게이트웨이, IP PBX 또는 SBC의 구성을 변경 될 때 발생 합니다.


