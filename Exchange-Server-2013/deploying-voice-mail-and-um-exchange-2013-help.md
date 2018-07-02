---
title: '음성 메일 및 UM 배포: Exchange 2013 Help'
TOCTitle: 음성 메일 및 UM 배포
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 50482925
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일 및 UM 배포

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange UM(통합 메시징)을 사용하면 조직 내 사용자에게 음성 사서함 서비스를 제공할 수 있습니다. 통합 메시징을 배포할 때는 Exchange Server 배포를 조직의 기존 전화 통신 시스템과 통합하거나 Microsoft Lync Server와 통합해야 합니다. 배포를 적절하게 수행하려면 기존 전화 통신 인프라를 주의 깊게 분석해야 하며, 통합 메시징에서 음성 메일을 배포 및 관리하기 위한 정확한 계획 단계를 수행해야 합니다. Exchange를 Lync Server와 통합하는 경우 Lync Server에 익숙해야 합니다.

통합 메시징을 배포하는 경우 조직에 있는 전화 통신 하드웨어에 따라 여러 옵션이 있습니다. 전화 통신 네트워크에 UM을 연결하는 경우에는 조직에 다음 전화 통신 구성 중 하나가 있는 것입니다.

  - PBX 하나 또는 여러 개를 사용하는 VoIP 게이트웨이 하나 또는 여러 개

  - IP PBX 하나 또는 여러 개

  - SIP 사용이 가능한 PBX 하나 또는 여러 개

  - Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server 2010 또는 2013

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>호스트 또는 하이브리드 환경에 Exchange UM을 배포하는 경우 SBC(Session Border Controller)를 배포해야 합니다. SBC는 전화 통신 네트워크에 연결하거나 조직에 발신음을 제공하기 위해 UM을 사용하지 않습니다. 그러나 공용 또는 사설 WAN을 통해 IP 프로토콜을 사용하여 온-프레미스 UM 배포를 데이터 센터에 연결합니다.</td>
</tr>
</tbody>
</table>


**전화 통신 게이트웨이** 올바른 VoIP 게이트웨이, IP PBX 또는 SBC를 선택하는 일은 전화 통신 네트워크와 UM을 통합할 때 첫 번째 단계에 불과합니다. 이러한 장치를 UM과 함께 작동하도록 구성하고, 필요한 클라이언트 액세스 및 사서함 서버를 배포하고, 모든 필요한 UM 구성 요소를 만들고 구성해야 합니다. 이러한 구성 요소를 통해 회로 기반 프로토콜 네트워크를 IP 데이터 네트워크에 연결하고 조직의 사용자가 음성 메일을 사용하도록 설정할 수 있습니다. 자세한 내용은 [Exchange 2013에 대 한 전화 통신 관리자](telephony-advisor-for-exchange-2013-exchange-2013-help.md)를 참조하십시오.

**Microsoft Lync Server**   통합 메시징은 Microsoft Lync Server를 사용하여 음성 메시징, 인스턴트 메시징, 향상된 현재 상태, 오디오/비디오 회의 및 전자 메일을 익숙하고 통합된 통신 환경으로 결합할 수 있습니다. UM과 Lync Server를 통합하면 다음과 같은 이점이 있습니다.

  - 다양한 응용 프로그램에서 향상된 현재 상태 알림으로 사용자에게 연락처의 가용성을 지속적으로 알려줍니다.

  - 인스턴트 메시징, 음성 메시징, 회의, 전자 메일 및 기타 통신 방법이 통합되어 사용자가 작업에 가장 알맞은 방법을 선택할 수 있습니다. 필요에 따라 한 방법에서 다른 방법으로 전환할 수도 있습니다.

  - 인터넷 연결이 가능한 모든 곳에서 대체 통신을 사용할 수 있습니다.

  - 전화 통신, 인스턴트 메시징 및 회의용 스마트 클라이언트(Microsoft Lync).

  - 여러 장치에서 사용자 환경의 연속성.

Lync Server에 대 한 자세한 내용은 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)를 참조 하십시오.

## 배포 단계

통합 메시징에 대해 많은 배포 옵션을 사용할 수 있습니다. 각 옵션에는 많은 수의 사용자를 지원할 수 있도록 확장 가능하고 가용성이 높은 시스템을 만들기 위해 필요한 공통된 여러 단계가 있습니다. 해당 단계는 다음과 같습니다.

1.  통합 메시징으로 전화 통신 구성 요소 또는 Microsoft Lync Server를 배포 및 구성합니다.

2.  통합 메시징에 필요한 클라이언트 액세스 및 사서함 서버를 올바르게 설치했는지 확인합니다.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td>Exchange 2013 클라이언트 액세스 서버로 UM SIP 및 RTP 트래픽을 보내도록 VoIP 게이트웨이 또는 IP PBX를 구성하기 전에 조직에 Exchange 2013 사서함 서버를 하나 이상 배포해야 합니다.</td>
    </tr>
    </tbody>
    </table>


3.  UM 다이얼 플랜, UM IP 게이트웨이, UM 헌트 그룹 및 UM 사서함 정책을 포함한 필수 통합 메시징 구성 요소를 만들고 구성합니다.

4.  상호 TLS를 위한 인증서를 배포하고 UM 자동 전화 교환 및 클라이언트 기능을 만드는 등의 사후 배포 작업을 수행합니다.

통합 메시징 배포에 대한 자세한 내용은 [Exchange 2013 UM 배포](deploy-exchange-2013-um-exchange-2013-help.md)를 참조하십시오.

통합 메시징 환경을 Microsoft Lync Server와 통합하는 경우 계획과 관련하여 추가로 고려해야 할 사항이 있습니다. 자세한 내용은 [Exchange 2013 UM 및 Lync Server 배포 개요](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md) 항목을 참조하십시오.

