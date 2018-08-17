---
title: '아키텍처 변경 사항: Exchange 2013 Help'
TOCTitle: 아키텍처 변경 사항
ms:assetid: 55d5ca4a-b0cd-45f1-9f47-e745ef208698
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150516(v=EXCHG.150)
ms:contentKeyID: 50483138
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 아키텍처 변경 사항

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013 아키텍처는 Exchange Server 2007 및 Exchange Server 2010 아키텍처와는 다릅니다. Exchange 2007 및 Exchange 2010에서는 서버 유형이 클라이언트 액세스, 사서함, 허브 전송 및 통합 메시징이라는 역할로 구분되었습니다. Exchange 2013에서는 이러한 서버 역할이 두 가지 유형으로 결합되었으며 두 서버 역할의 모든 구성 요소나 서비스는 동일한 실제 서버에서 또는 클라이언트 액세스와 사서함이라는 별개의 두 서버에서 실행됩니다. 새 모델에서 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버는 들어오는 호출에서 생성된 SIP(Session Initialization Protocol) 트래픽을 사서함 서버로 리디렉션합니다. 그 다음에는 VoIP 게이트웨이나 IP PBX(Private Branch eXchange)에서 사용자 사서함을 호스트하는 사서함 서버로의 미디어(RTP(Realtime Transport Protocol) 또는 SRTP(보안 RTP)) 채널이 설정됩니다. Exchange 2013에서 사서함 서버의 프로세스는 Exchange 2007 및 Exchange 2010의 통합 메시징 서버 역할과 동일합니다. 사서함 서버는 Microsoft Exchange 통합 메시징 서비스와 UM 작업자 프로세스를 모두 실행합니다. 클라이언트 액세스 서버는 들어오는 호출을 받아 사서함 서버로 전달하는 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행합니다.

**목차**

Support for the new Exchange architecture

UM ports

UM dial plans

UM Call Router performance counters

## 새 Exchange 아키텍처에 대한 지원

Exchange 2013의 클라이언트 액세스 서버는 자동 검색, SSL(Secure Sockets Layer), 인증, 리디렉션 및 프록시를 담당합니다. 클라이언트 액세스 서버는 UM(통합 메시징)에 대한 인바운드 호출 또는 SIP 요청에 대한 진입점입니다. 라우팅 논리와 SIP REDIRECT는 서비스로 구현되어 클라이언트 액세스 서버에 자동으로 포함됩니다. 이 서비스를 Microsoft Exchange 통합 메시징 호출 라우터 서비스라고 합니다. 이 서비스는 조직의 각 클라이언트 액세스 서버에 설치되고 실행됩니다. 클라이언트 액세스 서버가 들어오는 호출에 대한 SIP INVITE를 받으면 Microsoft Exchange 통합 메시징 호출 라우터 서비스는 들어오는 호출을 사서함 서버로 라우팅합니다. 그 다음에는 VoIP 게이트웨이, IP PBX 또는 SBC(Session Border Controller) 간에 미디어 채널(RTP 또는 SRTP)이 만들어집니다. 클라이언트 액세스 서버는 SIP 리디렉터로 작동하기는 하지만 VoIP 게이트웨이, IP PBX 또는 SBC에서 받은 SIP 요청만 처리할 뿐 모든 미디어 트래픽을 받지는 않습니다. RTP 또는 SRTP를 사용하는 미디어 트래픽은 클라이언트 액세스 서버로 전달되는 것이 아니라 사서함 서버와 VoIP 게이트웨이, IP PBX 또는 SBC 같은 SIP 피어 간에 전달됩니다. Exchange 2013과 UM을 배포할 때, 설치된 클라이언트 액세스 서버를 가리키도록 VoIP 게이트웨이, IP PBX 또는 SBC를 구성하여 들어오는 호출이 UM에 대해 올바르게 라우팅되도록 해야 합니다.

클라이언트 액세스 서버를 여러 개 배포하는 것이 요구 사항이며 클라이언트 액세스 서버가 사서함 서버와는 다른 실제 하드웨어에 별개로 배포되는 경우가 있습니다. L4나 L5 하드웨어 또는 소프트웨어 부하 분산 장치를 사용하여 클라이언트 액세스 서버를 배열로 그룹화할 수 있습니다. 하지만 Active Directory Exchange 개체 기반 클라이언트 액세스 서버 배열은 없습니다. 클라이언트 액세스 서버 앞에 하드웨어 또는 소프트웨어 부하 분산 장치를 사용하는 것은 대규모 Exchange 배포에서 적합한 방법입니다.

클라이언트 액세스 서버를 설치하면 Microsoft Exchange 통합 메시징 호출 라우터 서비스가 실행됩니다. 이 서비스가 수행하는 작업은 다음과 같습니다.

  - 초기화될 때 msexchangeumcallrouter.config라는 로컬 구성 파일을 읽습니다.

  - 조직의 중재 사서함을 사용하여 음성 문법을 생성합니다.

  - TCP(Transmission Control Protocol) 및/또는 TLS(전송 계층 보안) 연결을 지원합니다. 이 설정은 구성 가능합니다.

  - 구성 오류가 있거나 필요한 포트를 등록할 수 없는 경우에만 중지됩니다.

Exchange 2013에서 사서함 서버는 들어오는 호출의 SIP 요청에 대한 응답을 담당하지 않습니다. 클라이언트 액세스 서버에서 보낸 SIP 트래픽을 받은 다음 VoIP 게이트웨이, IP PBX 또는 SBC에 대한 RTP나 SRTP 연결을 설정하는 것만 담당합니다.

클라이언트 액세스 서버가 들어오는 호출을 사서함 서버로 리디렉션하면 VoIP 게이트웨이, IP PBX 또는 SBC와 사서함 서버 간에 미디어 채널이 설정됩니다. 미디어 채널이 설정되면 사서함 서버의 Microsoft Exchange 통합 메시징 서비스는 사용자의 음성 메일 인사말을 재생하고, 사용자의 전화 응답 규칙을 처리하고, 음성 메시지를 남기도록 발신자에게 알려 줍니다. 그 다음에는 사서함 서버가 음성 메시지를 녹음하고 메시지 녹음 내용을 만들어 사용자의 사서함에 저장합니다. 하지만 Exchange를 Office Communications Server 2007 R2 또는 Lync Server와 통합하는 경우에는 들어오는 호출에 대한 SIP 및 RTP 또는 SRTP 미디어 채널 모두가 Lync 서버 및 사서함 서버에 의해 처리됩니다. Lync 통합 환경에서는 VoIP 게이트웨이, IP PBX 또는 SBC를 사용하지 않습니다. Lync는 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버를 Exchange 2010 UM 서버처럼 인식합니다. 사서함 서버와 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버는 모두 SIP 다이얼 플랜에 추가되어야 하므로 신뢰할 수 있는 피어로 간주됩니다. Lync는 들어오는 호출을 인바운드 라우팅 구성 요소를 사용하여 라우팅합니다. 인바운드 라우팅 구성 요소는 SIP를 사용하여 클라이언트 액세스 서버와 통신한 다음 호출을 사서함 서버로 라우팅합니다.

Exchange 2010 UM 관리자는 각 UM 서버에서 통합 메시징 속성 집합을 구성할 수 있습니다. Exchange 2013에서는 UM 구성 요소와 UM 구성 설정이 클라이언트 액세스 서버와 사서함 서버 모두에 있습니다. Exchange 2010에서 통합 메시징 서버 역할을 실행하는 단일 컴퓨터에 적용된 모든 구성 설정을 계속 사용할 수 있습니다. 하지만 이러한 속성과 구성 설정 중 일부는 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버에서 설정하고 다른 일부는 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버에서 사용할 수 있습니다. 동일한 설정을 두 서버 모두에서 사용할 수 있는 경우도 있습니다. 다음 목록은 클라이언트 액세스 서버 및 사서함 서버에서 사용할 수 있는 cmdlet과 매개 변수 및 이전 버전의 통합 메시징을 사용하는 배포 시나리오를 지원하기 위해 cmdlet에서 변경된 곳을 보여 줍니다.

  - **Set-UMService -DialPlans \<MultiValuedProperty\>**    Exchange 2013 사서함 서버에서 사용할 수 있으며 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서도 작동합니다.

  - **Set-UMCallRouterSettings -DialPlans \<MultiValuedProperty\>**    Exchange 2013 클라이언트 액세스 서버에서는 사용할 수 있지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 사용할 수 없습니다.

  - **Set-UMService -MaxCallsAllowed \<Int32\>**    Exchange 2013 사서함 서버에서 사용할 수 있으며 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서도 작동합니다.

  - **Set-UMCallRouterSettings -MaxCallsAllowed \<Int32\>**   Exchange 2013 클라이언트 액세스 서버에서 사용할 수 없고 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서도 사용할 수 없습니다.

  - **Set-UMService -SipTcpListeningPort \<Int32\>**    Exchange 2013 사서함 서버에서는 구성할 수 없지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동합니다.

  - **Set-UMService -SipTlsListeningPort \<Int32\>**   Exchange 2013 사서함 서버에서는 구성할 수 없지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동합니다.

  - **Set-UMCallRouterSettings -SipTcpListeningPort \<Int32\>**   Exchange 2013 클라이언트 액세스 서버에서는 사용할 수 있지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동하지 않습니다.

  - **Set-UMCallRouterSettings -SipTlsListeningPort \<Int32\>**   Exchange 2013 클라이언트 액세스 서버에서는 사용할 수 있지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동하지 않습니다.

  - **Set-UMService - Status \<Enabled | Disabled | NoNewCalls\>**   Exchange 2013 사서함 서버에서는 사용할 수 없지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동합니다.

  - **Set-UMCallRouterSettings - Status \<Enabled | Disabled | NoNewCalls\>**   Exchange 2013 클라이언트 액세스 서버에서 사용할 수 없고 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서도 작동하지 않습니다.

  - **Set-UMService -UMStartupMode \<TCP | TLS | Dual\>**   Exchange 2013 사서함 서버에서 사용할 수 있으며 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서도 작동합니다.

  - **Set-UMCallRouterSettings - UMStartupMode \<TCP | TLS | Dual\>**   Exchange 2013 클라이언트 액세스 서버에서는 사용할 수 있지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동하지 않습니다.

  - **Enable-UMService**   Exchange 2013 사서함 서버에서는 사용할 수 없지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동합니다.

  - **Disable-UMService**   Exchange 2013 사서함 서버에서는 사용할 수 없지만 Exchange 2007 및 Exchange 2010 통합 메시징 서버에서는 작동합니다.

사서함 서버에서는 **Set/Get/Enable/Disable-UMService** cmdlet을 사용하여 Exchange 2013 사서함 서버나 Exchange 2007 또는 Exchange 2010 통합 메시징 서버의 Microsoft Exchange 통합 메시징 서비스에 대한 UM 속성을 보거나 구성합니다. 클라이언트 액세스 서버에서는 또 다른 cmdlet 집합인 **Set/Get-UMCallRouterSettings**를 사용하여 Microsoft Exchange 통합 메시징 호출 라우터 서비스 속성을 보거나 구성할 수 있습니다. 이렇게 하면 Exchange 2013 사서함 서버와의 공존성 배포에서 Exchange 2007 및 Exchange 2010의 기존 **Get-UMServer**, **Set-UMServer**, **Enable-UMServer** 및 **Disable-UMServer** cmdlet이 작동합니다. 사서함 서버와 클라이언트 액세스 서버가 동일한 서버에 설치되거나 서로 다른 서버에 설치된 경우에도 이러한 cmdlet이 작동합니다.

맨 위로 이동

## UM 포트

클라이언트 액세스 서버에 있는 Microsoft Exchange 통합 메시징 호출 라우터 서비스는 TCP(Transmission Control Protocol) 또는 상호 TLS(Transport Layer Security)를 통한 SIP를 사용하여 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버와 통신합니다. TCP/UDP(User Datagram Protocol) 포트 충돌을 방지하기 위해 Microsoft Exchange 통합 메시징 호출 라우터 서비스와 Microsoft Exchange 통합 메시징 서비스는 기본적으로 서로 다른 TCP 포트에서 수신 대기합니다. SIP 및 RTP 트래픽에 상호 TLS를 사용하는지 여부에 따라 두 서비스는 비보안 연결과 보안 연결을 모두 수락할 수 있습니다. 상호 TLS를 사용하는 경우 클라이언트 액세스 서버는 기본적으로 TCP 포트 5060(비보안 모드)과 TCP 포트 5061(SIP 보안 모드)에서 모두 SIP 요청을 수신 대기합니다. 이러한 포트는 **Set-UMCallRouterSettings** cmdlet을 사용하여 구성할 수 있습니다. 클라이언트 액세스 서버에 있는 Microsoft Exchange 통합 메시징 호출 라우터 서비스는 미디어(RTP 또는 SRTP) 트래픽을 처리하지 않으므로 TCP 포트만 사용되고 UDP 포트는 사용되지 않습니다. 상호 TLS를 사용하는 경우 사서함 서버는 기본적으로 TCP 포트 5062(비보안 모드)와 TCP 포트 5063(SIP 보안 모드)에서 모두 SIP 요청을 수신 대기합니다. 이러한 포트는 Exchange 관리 셸 cmdlet을 사용하여 구성할 수 없습니다. Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버에서는 셸을 사용하거나 레지스트리에서 설정을 구성하는 방법으로는 Exchange 서버에 대한 TCP 포트를 구성할 수 없습니다. 사서함 서버의 Microsoft Exchange 통합 메시징 서비스는 SIP 포트 5062 및 5063에서 클라이언트 액세스 서버로부터의 연결을 수락합니다. 클라이언트 액세스 서버가 SIP 요청을 사서함 서버로 리디렉션하면 VoIP 게이트웨이, IP PBX 또는 SBC와 사서함 서버의 Microsoft Exchange 통합 메시징 작업자 프로세스를 사용하여 RTP 또는 SRTP 미디어 채널이 만들어집니다.

다음 표에서는 Exchange 2013 포트 및 프로토콜과 포트 변경 가능 여부를 요약하여 보여 줍니다.

### UM 수신 대기 포트

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>프로토콜</th>
<th>TCP 포트</th>
<th>UDP 포트</th>
<th>포트 변경 가능 여부</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SIP(클라이언트 액세스 서버 - Microsoft Exchange 통합 메시징 통화 라우터 서비스)</p></td>
<td><p>5060(비보안), 5061(보안) 서비스가 두 포트 모두에서 수신합니다.</p></td>
<td><p>해당 없음</p></td>
<td><p>예(<strong>Set-UMCallRouterSettings</strong> cmdlet 사용)</p></td>
</tr>
<tr class="even">
<td><p>SIP(사서함 서버 - Microsoft Exchange 통합 메시징 서비스)</p></td>
<td><p>5062(비보안), 5063(보안) 서비스가 두 포트 모두에서 수신합니다.</p></td>
<td><p>해당 없음</p></td>
<td><p>포트를 변경할 수 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p>SIP(사서함 서버 - UM 작업자 프로세스)</p></td>
<td><p>TCP의 경우 5065와 5067(보안되지 않음). 상호 TLS의 경우 5066과 5068(보안됨). <em>UMStartupMode</em>가 <em>Dual</em>로 설정된 경우에 해당합니다. <em>UMStartUpMode</em>가 <em>TCP</em> 또는 <em>TLS</em>로 설정되어 있으면 포트 5065와 5066이 사용됩니다. 기본 <em>UMStartupMode</em>는 <em>TCP</em>입니다.</p></td>
<td><p>해당 없음</p></td>
<td><p>포트를 변경할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>RTP(사서함 서버 - UM 작업자 프로세스)</p></td>
<td><p>해당 없음</p></td>
<td><p>1024와 65535 사이의 포트</p></td>
<td><p>레지스트리에서 포트 범위를 변경할 수는 있지만 지원되는 구성 방법은 아닙니다.</p>
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMinPort</p>
<p>HKLM\SOFTWARE\Microsoft\Microsoft Speech Server\2.0\AudioConnectionMaxPort</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## UM 다이얼 플랜

Exchange 2007 및 Exchange 2010과는 달리 Exchange 2013에서는 UM 다이얼 플랜을 UM 서버에 매핑하거나 연결할 필요가 없습니다. 모든 클라이언트 액세스 서버와 사서함 서버는 VoIP 게이트웨이, IP PBX 또는 SBC에서 들어오는 모든 호출을 받아야 하므로 UM 서비스를 실행하는 클라이언트 액세스 서버나 사서함 서버에 다이얼 플랜을 연결할 필요가 없습니다. 예외적으로 Lync 2013, Lync Server 2010 및 Office Communications Server 2007 R2에 사용되는 SIP 다이얼 플랜은 배포한 클라이언트 액세스 서버 및 사서함 서버에 연결해야 합니다. 두 유형의 Exchange 서버를 모두 SIP 다이얼 플랜에 추가하여 Communications Server 2007 R2 또는 Lync Server의 신뢰할 수 있는 피어에 포함되도록 해야 합니다. 그렇지 않으면 Communications Server 2007 R2나 Lync Server가 사용자의 아웃바운드 호출을 거부하게 됩니다.

다음 표에서는 클라이언트 액세스 서버 및 사서함 서버와 UM 다이얼 플랜 간의 관계를 요약하여 보여 줍니다.

### UM 다이얼 플랜 연결

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>토폴로지</th>
<th>다이얼 플랜</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>클라이언트 액세스 서버와 사서함 서버가 동일한 서버에 있는 경우(Communications Server 2007 R2 또는 Lync Server 2010 비 SIP 다이얼 플랜이 없음)</p></td>
<td><p>다이얼 플랜을 클라이언트 액세스 서버나 사서함 서버에 연결할 필요가 없습니다. 클라이언트 액세스 서버나 사서함 서버를 다이얼 플랜에 추가하는 것이 허용되지 않습니다. <strong>Set-UMService</strong> cmdlet을 실행하면 사서함 서버를 SIP 이외의 다이얼 플랜에 연결하려고 할 때 오류가 생성됩니다.</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 서버와 사서함 서버가 서로 다른 서버에 있는 경우(Communications Server 2007 R2 또는 Lync Server 2010 비 SIP 다이얼 플랜이 없음)</p></td>
<td><p>더 이상 다이얼 플랜을 클라이언트 액세스 서버나 사서함 서버에 연결할 필요가 없습니다. 클라이언트 액세스 서버나 사서함 서버를 다이얼 플랜에 추가하는 것이 허용되지 않습니다. <strong>Set-UMService</strong> cmdlet을 실행하면 사서함 서버를 SIP 이외의 다이얼 플랜에 연결하려고 할 때 오류가 생성됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 액세스 서버와 사서함 서버가 동일한 실제 서버에 있는 경우(Communications Server 2007 R2 또는 Lync Server 2010 SIP 다이얼 플랜이 있음)</p></td>
<td><p>단일 SIP 다이얼 플랜의 경우 모든 클라이언트 액세스 및 사서함 서버를 SIP 다이얼 플랜에 추가하십시오. 다중 SIP 다이얼 플랜의 경우 모든 클라이언트 액세스 및 사서함 서버를 각 SIP 다이얼 플랜에 추가하십시오. 이렇게 하면 두 서버는 Office Communications Server 2007 R2 또는 Lync Server의 신뢰할 수 있는 피어가 됩니다. 각 클라이언트 액세스 서버 및 사서함 서버에서 동일한 인증서를 사용한 것처럼 Office Communications Server 2007 R2 또는 Lync Server 배포에서도 동일한 인증서를 사용해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 서버와 사서함 서버가 서로 다른 실제 서버에 있는 경우(Communications Server 2007 R2 또는 Lync Server 2010 SIP 다이얼 플랜이 있음)</p></td>
<td><p>단일 SIP 다이얼 플랜의 경우 모든 클라이언트 액세스 및 사서함 서버를 SIP 다이얼 플랜에 추가하십시오. 다중 SIP 다이얼 플랜의 경우 모든 클라이언트 액세스 및 사서함 서버를 각 SIP 다이얼 플랜에 추가하십시오. 이렇게 하면 두 서버는 Office Communications Server 2007 R2 또는 Lync Server의 신뢰할 수 있는 피어가 됩니다. 클라이언트 액세스 서버와 사서함 서버에서 사용하는 인증서가 서로 다를 경우에는 조직의 각 클라이언트 액세스 서버 및 사서함 서버에서 동일한 인증서를 사용한 것처럼 Office Communications Server 2007 R2 또는 Lync Server 배포에서도 동일한 인증서를 사용해야 합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## UM 호출 라우터 성능 카운터

이전 버전 Exchange에는 Microsoft Exchange 통합 메시징 서비스를 실행하는 통합 메시징 서버 역할이 있었습니다. Exchange 2013의 아키텍처 변경에 따라 이제 클라이언트 액세스 서버가 Microsoft Exchange 통합 메시징 통화 라우터 서비스를 실행하고 사서함 서버가 Microsoft Exchange 통합 메시징 서비스를 실행합니다. 관리자는 이전 버전 Exchange UM과 동일한 성능 카운터를 Microsoft Exchange 통합 메시징 서비스에 사용할 수 있습니다. 이 외에도 Microsoft Exchange 통합 메시징 통화 라우터 서비스의 상태를 확인하고 문제를 해결하기 위해 클라이언트 액세스 서버에서 사용할 수 있는 추가 성능 카운터가 있습니다.

Exchange 2013의 새 클라이언트 액세스 통합 메시징 호출 라우터 서비스를 지원하는 데 사용할 수 있는 성능 카운터는 다음과 같습니다.

### 성능 카운터

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>성능 카운터 범주</th>
<th>카운터 이름</th>
<th>설명</th>
<th>임계값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% of Inbound Calls Rejected by the Microsoft Exchange Unified Messaging Call Router Service over the Last Hour</p></td>
<td><p>Microsoft Exchange 통합 메시징 호출 라우터 서비스에 의해 지난 한 시간 동안 거부된 인바운드 호출의 백분율을 나타냅니다.</p></td>
<td><p>항상 5% 미만이어야 하지만 항상 0이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Calls Disconnected on Irrecoverable Internal Error for the Microsoft Exchange Unified Messaging Call Router Service</p></td>
<td><p>내부 시스템 오류가 발생한 후에 연결이 끊어진 호출 수를 나타냅니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total Inbound Calls Rejected by the Microsoft Exchange Unified Messaging Call Router Service</p></td>
<td><p>서비스가 시작된 이후 Microsoft Exchange 통합 메시징 호출 라우터 서비스에 의해 거부된 총 인바운드 호출 수를 나타냅니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>Total number of calls received by the Microsoft Exchange Unified Messaging Call Router Service</p></td>
<td><p>서비스가 시작된 이후 Microsoft Exchange 통합 메시징 호출 라우터 서비스에 의해 수신된 총 인바운드 호출 수를 나타냅니다.</p></td>
<td><p>0 이상이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeUMRouterAvailability</p></td>
<td><p>% of Inbound Calls Rejected by the Microsoft Exchange Unified Messaging Call Router Service Over the Last Hour</p></td>
<td><p>Microsoft Exchange 통합 메시징 호출 라우터 서비스에 의해 지난 한 시간 동안 거부된 인바운드 호출의 백분율을 나타냅니다.</p></td>
<td><p>5% 미만이어야 합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

