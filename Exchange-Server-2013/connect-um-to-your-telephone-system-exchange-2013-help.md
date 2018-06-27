---
title: 'UM 전화 시스템에 연결: Exchange 2013 Help'
TOCTitle: UM 전화 시스템에 연결
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50556039
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 전화 시스템에 연결

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-30_

UM(통합 메시징)은 음성 메시징과 전자 메일 메시징을 다양한 장치에서 액세스할 수 있는 사서함 하나로 결합합니다. 따라서 사용자가 전자 메일 받은 편지함에서 또는 전화기에서 Outlook Voice Access를 사용하여 음성 사서함 메시지를 들을 수 있습니다.

Microsoft Exchange 조직에 UM을 배포할 경우 전화 통신 네트워크의 PBX(Private Branch eXchange)에 연결할 VoIP(Voice over IP) 게이트웨이를 하나 또는 여러 개 설치, 배포 및 구성하거나 SIP(Session Initiation Protocol) 사용 PBX 또는 IP PBX를 설치, 배포 및 구성해야 합니다. 현재 음성 사서함 시스템을 업그레이드할 경우 전화 통신 네트워크에 연결할 장치를 배포하고 Exchange 클라이언트 액세스 및 사서함 서버를 설치한 후 전화 통신 네트워크에서 데이터 네트워크에 연결할 수 있도록 필요한 UM 구성 요소를 만들어야 합니다. 이렇게 하면 전화 통신 네트워크에서 들어오는 호출이 VoIP 게이트웨이, IP PBX 또는 SIP 사용 PBX로 연결되고 이러한 장치는 Exchange 조직으로 연결됩니다.

Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server를 설치, 배포 및 구성할 경우에는 Exchange 통합 메시징에 직접 연결하기 위해 VoIP 게이트웨이, IP PBX 또는 SIP 사용 PBX를 사용하지 않습니다. 대신 Lync 중재 서버와 VoIP 게이트웨이를 사용하거나 중재 서버 기능과 VoIP 게이트웨이 기능이 모두 있는 고급 VoIP 게이트웨이를 사용하여 Exchange UM에 연결할 수 있습니다. Enterprise Voice를 사용할 수 있는 UM 사용자는 음성 메시지를 검색하고 듣고 응답할 수 있으며 아웃바운드 호출을 할 수 있습니다. Office Communicator나 Lync 클라이언트를 사용하여 현재 상태 및 IM(인스턴트 메시징)을 비롯한 다른 Lync 관련 기능에 액세스할 수도 있습니다.

다음은 조직에서 UM을 설치 및 배포하고 사용자가 음성 사서함 기능을 사용할 수 있도록 설정하는 데 도움이 되는 정보입니다.

  - [Um VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러에 연결](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)   VoIP 게이트웨이 또는 IP PBX를 UM에 연결하는 방법에 대해 알아봅니다.

  - [Exchange 2013에 대 한 전화 통신 관리자](telephony-advisor-for-exchange-2013-exchange-2013-help.md)   지원되는 VoIP 게이트웨이, IP PBX 및 PBX에 대해 알아봅니다.

  - [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)  VoIP 게이트웨이, IP PBX 및 PBX를 설정하는 방법에 대해 알아봅니다.

