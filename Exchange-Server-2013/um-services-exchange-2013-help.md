---
title: 'UM 서비스: Exchange 2013 Help'
TOCTitle: UM 서비스
ms:assetid: f36835f2-1e5f-4e5a-88bc-0672af1e3498
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125191(v=EXCHG.150)
ms:contentKeyID: 50556112
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 서비스

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-18_

Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 하는 클라이언트 액세스 서버 및 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버를 통해 UM (통합 메시징) 및 조직의 사용자에 대 한 음성 메일 기능을 배포할 수 있습니다.

UM 서비스와 관련 된 관리 작업에 대 한 자세한 내용은? [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조 하십시오.

**목차**

클라이언트 액세스 및 사서함 서버

서버 구성 설정

서버 작업

## 클라이언트 액세스 및 사서함 서버

Exchange 2013 서버 역할 발견에서 Exchange 2007 및 Exchange 2010 두 종류의 서버를 결합 하 고 모든 구성 요소 또는 해당 서버 역할의 서비스를 동일한 실제 서버 또는 클라이언트 액세스 및 사서함 이라는 두 별도 서버에서 실행 됩니다.

이 새 모델에 대 한 클라이언트 액세스 서버는 자동 검색, Secure Sockets Layer (SSL), 인증, 리디렉션 및 프록시 사용 하는 일을 담당 합니다. 클라이언트 액세스 서버는 모든 인바운드 호출에 대 한 진입점 또는 통합 메시징에 대 한 프로토콜 SIP (Session Initiation) 요청입니다. 라우팅 논리 및 리디렉션 SIP 클라이언트 액세스 서버에 자동으로 포함 된 서비스로 구현 됩니다. 이 서비스는 Microsoft Exchange 통합 메시징 호출 라우터 서비스 라고 합니다. 조직에서 각 클라이언트 액세스 서버에서 실행 됩니다.

SIP INVITE 수신 전화에 대 한 클라이언트 액세스 서버를 받으면 Microsoft Exchange 통합 메시징 호출 라우터 서비스에서 사서함 서버에 수신 전화를 리디렉션합니다. 다음은 VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러 (SBC)와 사용자의 사서함을 호스트 하는 사서함 서버 간의 미디어 채널 (RTP 또는 SRTP) 만들어집니다. 클라이언트 액세스 서버는 SIP 리디렉터 역할을 하지만 VoIP 게이트웨이, IP Pbx 또는 Sbc에서 SIP 요청을 처리 합니다. 모든 미디어 트래픽을 수신 하지 못합니다. 사서함 서버와 VoIP 게이트웨이, IP Pbx 또는 Sbc와 같은 SIP 피어 간에 RTP 또는 SRTP를 사용 하 여 미디어 트래픽을 전달만 됩니다. Exchange 2013 및 UM을 배포 하면 VoIP 게이트웨이, IP Pbx 또는 Sbc UM에 대 한 수신 전화를 제대로 라우팅되는 수 있도록 설치 했을 때 클라이언트 액세스 서버를 가리키도록 구성 해야 합니다.

Exchange 2013 사서함 서버는 Exchange 2007 및 Exchange 2010 에서 처리 하는 통합 메시징 서버 역할을 동일한 프로세스를 처리 합니다. 사서함 서버에서 Microsoft Exchange 통합 메시징 서비스와 UM 작업자 프로세스를 실행 합니다.

클라이언트 액세스 및 사서함 서버를 설치 하 고 통합 메시징 배포 하려는 연결 하거나 클라이언트 액세스를 추가할 필요가 없습니다 또는 사서함 서버에서 UM 다이얼 플랜 합니다. 클라이언트 액세스 및 사서함 서버 들어오는 모든 수신 전화에 응답 하 고 UM 다이얼 플랜을 사용 하 여 사용자를 찾을 수 있습니다.

그러나 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server와 통합 메시징 통합 중인, 경우 SIP 및 RTP 또는 SRTP 미디어 채널 걸려오는 전화에 대 한 모두 Lync 서버와 사서함 서버에 의해 처리 됩니다. Lync 통합 된 환경에서 VoIP 게이트웨이, IP Pbx 또는 Sbc 않아도 됩니다. Lync를 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버는 Exchange 2010 UM 서버와 마찬가지로 찾습니다. 사서함 서버 및 클라이언트 액세스 서버는 SIP 다이얼 플랜에 두 서버를 추가 해야 하기 때문에 신뢰할 수 있는 피어에 간주 됩니다. Lync를 사용 하 여 SIP 클라이언트 액세스 서버와 통신 하 고 다음 사서함 서버에 대 한 호출을 라우팅할는 인바운드 라우팅 구성 요소를 사용 하 여 들어오는 호출을 라우팅합니다.

맨 위로 이동

## 서버 구성 설정

Exchange 2013 모든 UM 구성 요소 및 Exchange 2010 에서 통합 메시징 서버 역할을 실행 하는 단일 컴퓨터에 적용 되는 구성 설정을 사용할 수 있습니다. 그러나 클라이언트 액세스 서버에서 발견 되는 이러한 구성 요소 및 구성 설정의 일부 및 다른 사용자는 사서함 서버에서 사용할 수 있습니다. 경우에 따라 동일한 설정을 모두에서 제공 됩니다. 다음 목록에는 매개 변수 및 클라이언트 액세스 서버와 사서함 서버에서 사용할 수 있는 설정을 보여줍니다.

  - \[-DialPlans \<MultiValuedProperty\>\]

  - \[-MaxCallsAllowed \< Int32 \>\]

  - \[-SipTcpListeningPort \< Int32 \>\]

  - \[-SipTlsListeningPort \< Int32 \>\]

  - \[-상태 \< 사용 | 비활성화 된 | NoNewCalls \>\]

  - \[-UMStartupMode \< TCP | TLS | 이중 \>\]

사서함 서버에 대 한 보기 또는 Microsoft Exchange 통합 메시징 서비스에 대 한 UM 속성을 구성 하는 **Set-UMService**, **Get-UMService**, **Enable-UMService**및 **Disable-UMService** cmdlet를 사용 합니다. 다양 한 cmdlet, **Set-UMCallRouterSettings** 및 **Get-UMCallRouterSettings**보기 또는 클라이언트 액세스 서버에서 Microsoft Exchange 통합 메시징 호출 라우터 서비스 속성을 구성 하는데 사용 됩니다. 이렇게 하면 기존 **Get-UMServer**, Exchange 2007 및 Exchange 2010 에서 **Set-UMServer**, **Enable-UMServer**및 **Disable-UMServer** cmdlet Exchange 2013 사서함 서버와의 동시 사용 배포에서 작동 합니다. 이렇게 하면 사서함 및 클라이언트 액세스 서버는 동일한 컴퓨터나 다른 컴퓨터에 설치 되 면 cmdlet은 작동 합니다.

맨 위로 이동

## 서버 작업

클라이언트 액세스 및 사서함 서버를 설치 하는 경우 자동으로 활성화 된 즉시 수신 대답할 수 하 고 보내는 음성 전화를 걸고 Exchange 조직에서 의도 한 받는 사람에 게 음성 메일 메시지를 라우팅합니다.

사서함 서버에서 Microsoft Exchange 통합 메시징 서비스 또는 새 호출에 응답 하도록 하는 클라이언트 액세스 서버에서 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 허용 하거나 이렇게에서 방지 수 있습니다. 기본적으로 사서함 또는 클라이언트 액세스 서버가 설치 된 후 활성된 상태로 설정입니다. 들어오는 음성, 팩스, 자동 전화 교환 및 Outlook Voice Access 호출을 수락 하도록 사서함 또는 클라이언트 액세스 서버를 설정 하는 경우 **Set-ServerComponentState** cmdlet을 사용 합니다.

Exchange 2013 사서함 또는 클라이언트 액세스 서버에 대 한 유지 관리 모드를 구성 서비스가 중단 서버 걸릴 수 있습니다. 사서함 서버에 대 한 서비스의 아웃 바운드 있음을 나타내고 모든 활성 데이터베이스를 호스트할 되지 않음, 모든 전송 큐는 비어는 서버에 클라이언트 액세스 서버, VoIP 게이트웨이, IP Pbx, SIP 사용 가능 Pbx 또는 Sbc의 모든 들어오는 호출을 수락 하지 않습니다. 클라이언트 액세스 서버에 대 한 서비스의 아웃 바운드 서버 VoIP 게이트웨이, IP Pbx, SIP 사용 가능 Pbx 또는 Sbc에서 들어오는 호출을 수락 되지 않음 의미 합니다.

Exchange 2007 및 Exchange 2010 에서 통합 메시징 서버의 작동 상태를 제어 하는데 사용할 수 있는 상태 매개 변수를 사용 했습니다. Exchange 2013 사서함 서버에 대 한 **Set-UMService** cmdlet 또는 클라이언트 액세스 서버에서 **Set-UMCallRouterSettings** cmdlet에서 해당 목적을 위해 없음 status 매개 변수를 사용 하 여 제공 됩니다.

클라이언트 액세스 및 사서함 서버는 로설정하면 자신이 설치 된 경우에 사용할 수 있지만 둘다 서버 올바르게 처리할 수 있습니다 및 UM 다이얼 플랜 때까지 UM 사용이 가능한 사용자에 게 걸려오는 전화 경로 하나 이상의 UM IP 게이트웨이와 연결 됩니다.

다이얼 플랜은 UM IP 게이트웨이 사용한 연결 된, 후 클라이언트 액세스 및 사서함 서버는 UM 다이얼 플랜 및 VoIP 게이트웨이, IP Pbx 및 Sbc와 연결 된 모든 UM IP 게이트웨이 찾습니다. 검색 하 고 UM 다이얼 플랜 또는 UM IP 게이트웨이 구성 변경 내용을 확인 하려면 클라이언트 액세스 또는 사서함 서버 10 분 마다 구성을 확인 합니다.

UM IP 게이트웨이 구성에 변경 내용을 식별 하는 경우에서 적절 하 게 대응 하는 클라이언트 액세스 또는 사서함 서버와 하나를 사용 하 여 시작 하거나 적절 한 VoIP 게이트웨이, IP PBX 또는 SBC를 사용 하 여 중지 합니다. 클라이언트 액세스 및 사서함 서버에 들어오는 응답 한 후 UM 다이얼 플랜과 연결 된 사용자에 대 한 호출 및 VoIP 게이트웨이, IP Pbx 및 Sbc와 통신 올바르게 하 자신이 정상적으로 작동 하 고 해당 연결 Exchange 서버와 VoIP 게이트웨이, IP Pbx 또는 Sbc 간의 정상적으로 작동 합니다. 확인 하려면 진단 작업 집합을 실행할 수 있습니다.

맨 위로 이동

