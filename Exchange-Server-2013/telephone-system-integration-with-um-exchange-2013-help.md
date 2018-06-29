---
title: 'Um 전화 시스템 통합: Exchange 2013 Help'
TOCTitle: Um 전화 시스템 통합
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50556074
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Um 전화 시스템 통합

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

UM(통합 메시징)을 배포하기 위해서는 기본적인 전화 통신 개념과 전화 통신 구성 요소에 대해 잘 알고 있어야 합니다. 기본적인 전화 통신 개념을 이해하면 UM을 Exchange 조직에 통합할 수 있습니다. 기본 개념과 구성 요소는 다음과 같습니다.

  - 회로 전환 네트워크와 패킷 전환 네트워크

  - PBX(Private Branch eXchange)

  - IP PBX

  - VoIP(Voice over Internet Protocol)

  - VoIP 게이트웨이

온-프레미스, 하이브리드 또는 Office 365 환경에서 필요한 전화 통신 구성 요소를 연결 및 구성하는 것은 Lync Server Enterprise Voice의 유무에 관계없이 UM을 올바르게 배포하는 데 있어서 가장 복잡하고도 중요한 단계입니다. Microsoft Lync Server 및 UM을 사용하려는 경우 기존 전화 통신 네트워크에 대해 VoIP 게이트웨이, 고급 VoIP 게이트웨이, PBX, IP PBX 및 SBC(Session Border Controller)를 연결 및 구성하고 전화 통신 네트워크에 연결해야 합니다.

조직에서 새 UM을 계획하고 배포하거나 기존 음성 메일 시스템을 업그레이드하는 작업은 어려운 문제일 수 있습니다. 이를 위해서는 VoIP 게이트웨이, PBX, IP PBX, Microsoft Lync Server 및 통합 메시징에 대해 잘 알고 있어야 합니다. Exchange 및 음성 메일 시스템에 대한 사용자의 기술 경험에 따라 통합 메시징 전문가의 지원을 받을 수 있습니다. 통합 메시징 전문가는 레거시 또는 타사 음성 메일 시스템에서 Exchange 통합 메시징으로 원활하게 전환할 수 있도록 지원합니다. 통합 메시징 전문가에게 문의하는 방법에 대한 자세한 내용은 [Microsoft Exchange Server 2013 UM(통합 메시징) 전문가](http://go.microsoft.com/fwlink/p/?linkid=262708)(영문)를 참조하십시오.

## 전화 통신 네트워크 통합

통합 메시징에서는 Exchange Server 배포를 기존 전화 통신 네트워크와 통합하거나 UM을 조직의 Microsoft Lync Server와 통합해야 합니다. 기존 전화 통신 인프라나 Microsoft Lync Server Enterprise Voice 배포를 주의 깊게 분석한 다음 필요한 계획 단계를 따라야만 UM 음성 메일을 배포하고 관리할 수 있습니다.

## VoIP 게이트웨이

Exchange 조직에 UM을 배포할 경우 전화 통신 네트워크의 PBX에 연결할 VoIP 게이트웨이를 하나 또는 여러 개 설치, 배포 및 구성하거나 SIP(Session Initiation Protocol) 사용 가능 PBX 또는 IP PBX를 설치, 배포 및 구성해야 합니다.

VoIP IP 게이트웨이는 레거시 PBX를 LAN에 연결하는 타사 하드웨어 장치입니다. VoIP 게이트웨이를 통해 PBX 시스템은 조직의 Exchange 서버와 통신할 수 있습니다.

UM은 VoIP 게이트웨이의 기능을 사용하여 ISDN 및 QSIG와 같은 TDM(Time Division Multiplexing) 또는 회로 전환 기반 프로토콜을 PBX에서 SIP, RTP(Realtime Transport Protocol) 또는 실시간 팩스 전송용 T.38과 같은 IP 기반 또는 VoIP 기반 프로토콜로 전환하거나 변환합니다. VoIP 게이트웨이는 UM의 기능과 작동에 필수적인 요소입니다. VoIP 게이트웨이는 PSTN(공중 전화망) 회로 전환 프로토콜 대신 VoIP를 사용하는 PBX 시스템에도 연결할 수 있습니다.

올바른 VoIP 게이트웨이, IP PBX, SIP 사용 가능 PBX 또는 SBC를 선택하는 일은 전화 통신 네트워크와 UM을 통합할 때 첫 번째 단계에 불과합니다. 이러한 장치가 UM에서 작동하도록 구성해야 합니다. 온-프레미스 및 하이브리드 배포 둘 다에서 필요한 클라이언트 액세스 서버와 사서함 서버를 배포하고, 필요한 모든 UM 구성 요소를 만들고 구성해야 합니다. 호스트된 음성 메일을 사용하는 Office 365의 경우에는 서버를 설치 및 구성할 필요가 없습니다. 이러한 구성 요소를 통해 회로 전환 전화 통신 네트워크와 IP 데이터 네트워크를 연결하고 조직의 사용자가 음성 메일을 사용할 수 있도록 설정할 수 있습니다. 자세한 내용 및 지원되는 전화 통신 장치는 다음 리소스를 참조하십시오.

  - [Exchange 2013에 대 한 전화 통신 관리자](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

통합 메시징은 Microsoft Lync Server를 사용하여 음성 메시징, 인스턴트 메시징, 현재 상태 사용자 지정, 오디오/비디오 회의 및 전자 메일을 익숙하고 통합된 통신 환경에 결합할 수 있습니다. UM과 Microsoft Lync Server를 통합하여 조직의 사용자에게 Enterprise Voice 기능을 제공하면 다음과 같은 이점이 있습니다.

  - 다양한 응용 프로그램에서 향상된 현재 상태 알림으로 사용자에게 연락처의 가용성을 지속적으로 알려줍니다.

  - 인스턴트 메시징, 음성 메시징, 회의, 전자 메일 및 기타 통신 모드가 통합되어 사용자가 작업에 가장 알맞은 모드를 선택할 수 있습니다. 필요에 따라 한 모드에서 다른 모드로 전환할 수도 있습니다.

  - 인터넷 연결이 가능한 모든 곳에서 대체 통신을 사용할 수 있습니다.

  - 전화 통신, 인스턴트 메시징 및 회의용 스마트 클라이언트(Microsoft Lync).

  - 여러 장치에서 사용자 환경의 연속성.

Exchange UM 라우팅 구성 요소는 Lync Server와 Exchange 서버 간의 음성 메일 라우팅을 처리하여 Lync Server를 통합 메시징 기능과 통합합니다. 또한 Exchange 서버를 사용할 수 없는 경우에는 Lync Server에 있는 Exchange UM 라우팅 구성 요소가 PSTN을 통해 음성 메일을 다시 라우팅하는 작업을 처리합니다. Enterprise Voice가 지사 사이트에 배포되었으며 해당 사이트에 중앙 사이트에 대한 복구 WAN 연결이 없는 경우 WAN 연결이 중단되면 지사 사이트에 배포된 SBA(Survivable Branch Appliance)가 지사 사용자에게 음성 메일 기능을 제공합니다. WAN 연결을 사용할 수 없는 경우 SBA는 다음을 수행합니다.

  - 응답하지 않는 전화를 PSTN을 통해 중앙 사이트에 있는 Exchange 서버로 다시 라우팅합니다.

  - 사용자에게 PSTN을 통해 음성 메시지를 검색하는 기능을 제공합니다.

  - 부재 중 통화 알림을 큐에 넣은 다음 WAN 연결이 복원되면 Exchange 서버에 업로드합니다.

Microsoft Lync Server에 대 한 자세한 내용은 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)을 참조 하십시오.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>온-프레미스 또는 하이브리드 배포에서 통합 메시징 및 Lync Server를 통합하는 경우 Exchange 2007 또는 Exchange 2010 사서함 서버에 사서함이 있는 사용자는 부재 중 전화 알림을 사용할 수 없습니다. 부재 중 전화 알림은 전화가 사서함 서버에 전송되기 전에 사용자의 연결이 끊기는 경우 생성됩니다.</td>
</tr>
</tbody>
</table>

