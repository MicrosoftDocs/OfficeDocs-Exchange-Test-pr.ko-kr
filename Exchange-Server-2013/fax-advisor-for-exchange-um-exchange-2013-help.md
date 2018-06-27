---
title: 'Exchange UM에 대 한 팩스 advisor: Exchange 2013 Help'
TOCTitle: Exchange UM에 대 한 팩스 advisor
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52058010
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange UM에 대 한 팩스 advisor

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft UM(통합 메시징)은 송신 팩스 또는 팩스 라우팅 같은 향상된 팩스 기능을 위해 인증된 팩스 파트너 솔루션을 사용합니다. 기본적으로 사용자는 수신 팩스 메시지를 UM 사용 가능 사용자에게 배달할 수 있도록 구성되지 않습니다. Exchange 서버는 팩스 요청을 인증된 팩스 파트너 솔루션으로 전송합니다. 팩스 파트너의 서버는 팩스 데이터를 받은 후 이 팩스가 .tif 첨부 파일로 포함된 전자 메일 메시지로 받는 사람의 사서함에 보냅니다. 자세한 내용은 [음성 메일 사용자가 팩스를 받을 수 있도록](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)을 참조하십시오.


> [!IMPORTANT]
> 통합 메시징 배포를 계획 하는 모든 고객은 통합 메시징 전문가의 도움을 얻을 것이 좋습니다. 통합 메시징 전문가 레거시 음성 메일 시스템에서 통합 메시징에 원활 하 게 전환 있는지 확인 하는데 도움이 됩니다. 새 배포를 수행 하거나 레거시 음성 메일 시스템을 업그레이드에 Pbx와 통합 메시징에 대 한 중요 한 지식이 필요 합니다. 통합 메시징 전문가 게 문의 하는 방법에 대 한 자세한 내용은 <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 통합 메시징 (UM) 전문가</A> 나 <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">통합 메시징에 대 한 Microsoft 적절치</A>를 참조 하십시오.



## Exchange 통합 메시징 팩스 파트너 프로그램

Exchange UM과의 상호 운용성에 대해 인증된 팩스 파트너가 되려면 파트너는 팩스 파트너 상호 운용성 사양에 포함된 요구 사항을 구현하고 팩스 솔루션은 독립적인 인증 공급업체의 인증을 받아야 합니다. Exchange 통합 메시징과 함께 작동하도록 팩스 제품을 인증하는 방법에 대해 알아보려면 [통합 메시징 팩스 파트너](mailto:fax-part@microsoft.com)로 요청을 제출하십시오.

## 통합 메시징과 상호 운용되도록 인증된 팩스 파트너 솔루션

했을 때 이미 Exchange 통합 메시징을 배포 하 고 조직에 대 한 수신 되는 팩스를 사용할 수 있는 팩스 파트너에 대 한 자세한 내용은 되는 경우 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=190238)를 참조 하십시오. 이러한 소프트웨어 공급 업체 Exchange 서버와 상호 운용으로 인증 된 및 통합 메시징에 대 한 인증 된 소프트웨어 솔루션을 포함 합니다.

## VoIP, 미디어 게이트웨이 및 IP PBX 지원

조직에 대해 VoIP 게이트웨이를 올바르게 구성하는 일은 수신 팩스에 대해 Exchange 통합 메시징을 배포하기 위해 완료해야 하는 어려운 배포 작업입니다. 질문에 대한 대답과 최신 VoIP 게이트웨이 구성 정보를 얻으려면 [Exchange 2013에 대 한 전화 통신 관리자](telephony-advisor-for-exchange-2013-exchange-2013-help.md)를 참조하십시오. [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)에서는 조직의 VoIP 게이트웨이, IP PBX 및 SBC가 Exchange 통합 메시징과 호환되도록 올바르게 구성하는 데 필요한 VoIP 게이트웨이 구성 참고 사항과 파일을 제공합니다.

VoIP 게이트웨이가 포함된 Exchange 통합 메시징의 상호 운용성 테스트가 이제는 Microsoft Unified Communications Open Interoperability Program에 통합되었습니다. 자세한 내용은 [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722)을 참조하십시오.

VoIP 게이트웨이 및 IP PBX용 [Microsoft Unified Communications Open Interoperability Program](http://go.microsoft.com/fwlink/p/?linkid=140722) 인증 프로그램을 통해 고객이 Microsoft 통합 통신 소프트웨어와 함께 공인 전화 통신 게이트웨이 및 IP-PBX를 사용할 때 원활한 설치 및 지원 환경에서 작업할 수 있도록 할 수 있습니다.


> [!IMPORTANT]
> 통합 메시징, Communications Server 2007 R2 또는 Microsoft Lync Server가 통합된 환경에서는 T.38 또는 G.711을 사용하여 팩스를 보내고 받을 수 없습니다.



## 팩스 배포 및 구성

UM이 수신 팩스 호출을 전용 팩스 파트너 솔루션으로 전달하면, 이 솔루션에서는 팩스 호출과 팩스를 보낸 사람을 연결하고 UM 사용 가능한 사용자를 대신하여 팩스를 수신합니다. 하지만 UM 사용 가능 사용자가 자신의 사서함에서 팩스 메시지를 받도록 하려면 팩스 파트너 서버를 구성한 다음, UM 다이얼 플랜 및 UM 사서함 정책을 구성하고 UM 사용 가능 사용자가 팩스를 받을 수 있도록 해야 합니다. 자세한 내용은 [수신 팩스 설정](setting-up-incoming-faxing-exchange-2013-help.md)을 참조하십시오.

