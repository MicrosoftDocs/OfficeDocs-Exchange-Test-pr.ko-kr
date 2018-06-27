---
title: 'UM 프로토콜, 포트 및 서비스: Exchange 2013 Help'
TOCTitle: UM 프로토콜, 포트 및 서비스
ms:assetid: 5997ce29-1755-48bb-8ff4-b08da549482a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998265(v=EXCHG.150)
ms:contentKeyID: 54651815
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 프로토콜, 포트 및 서비스

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-03-09_

Microsoft Exchange 2013 통합된 메시징 (UM) 여러 TCP 및 사용자 데이터 그램 프로토콜 (UDP) 포트 Exchange 2013 및 다른 장치를 실행 하는 서버 간의 통신을 설정 하는데 사용할 필요 합니다. 이러한 IP 포트를 통해 액세스를 허용 하 여 제대로 작동 하도록 통합 메시징을 사용 하도록 설정 합니다. 이 항목에서는 Exchange 2013 에 사용 되는 TCP 및 UDP 포트에 설명 통합 메시징 합니다.

## 통합된 메시징 프로토콜 및 서비스

Exchange 2013 통합 메시징 기능 및 서비스는 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 하는 클라이언트 액세스 서버와 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버의 올바른 작동을 위해 TCP 및 UDP 포트를 정적 및 동적에 의존 합니다. Exchange 2013 를 설치할 때 정적 인바운드 Windows 방화벽 규칙은 Exchange 에 대 한 추가 됩니다. 클라이언트 액세스 및 사서함 서버에서 사용 되는 TCP 포트를 변경 하는 경우에 제대로 작동 하도록 통합 메시징을 허용 하려면 Windows 방화벽 규칙을 다시 구성 해야할 수 있습니다.


> [!IMPORTANT]
> Exchange 2013 에서 클라이언트 액세스 및 사서함이 UM 구성 요소 및 서비스를 실행 하는 서버, Exchange 설치 프로그램을 만듭니다 인바운드 방화벽 규칙 하는 TCP 포트 제한 없이 인바운드 통신을 허용 합니다. UM 서비스에 대 한 다음 인바운드 규칙 추가 됩니다.



1.  **SESWorker (GFW) (TCP In)**

2.  **UMCallRouter (GFW) (TCP In)**

3.  **UMCallRouter (TCP In)**

4.  **UMService (GFW) (TCP In)**

5.  **UMService (TCP In)**

6.  **UMWorkerProcess-RPC (TCP In)**

7.  **UMWorkerProcess (GFW) (TCP In)**

8.  **UMWorkerProcess (TCP In)**

## Session Initiation Protocol

Session Initiation Protocol (SIP)은 시작 하거나, 수정 하 고, 끝, 비디오, 음성, 인스턴트 메시징, 온라인 게임 및 가상 현실 등의 멀티미디어 요소를 포함 하는 대화형 사용자 세션에 사용 되는 프로토콜입니다. H.323와 함께 IP (VoIP)를 통한 음성에 대 한 프로토콜 신호 앞에 오는 중 하나입니다. 대부분 VoIP 표준 기반 솔루션 H.323 또는 SIP를 사용 합니다. 그러나 몇가지 독점 설계 하 고 프로토콜도 존재 합니다. 일반적으로 VoIP 프로토콜 통화 대기, 회의 통화와 같은 기능을 지원 하 고 호출 전송 합니다.

VoIP 게이트웨이 및 IP Private Branch Exchange (Pbx)과 같은 SIP 클라이언트 TCP 및 UDP 포트 5060를 사용 하 여 Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행 하는 클라이언트 액세스 서버를 포함 하는 SIP 서버에 연결할 수 있습니다. SIP은 설정 하 고 음성 또는 화상 통화를 해제에 대해서만 사용 됩니다. 모든 음성 및 비디오 통신에는 실시간 전송 프로토콜 (RTP)을 통해 발생 합니다.

## 실시간 전송 프로토콜

RTP은 인터넷 등의 특정 네트워크를 통해 오디오 및 비디오를 제공 하기 위한 표준 패킷 형식을 정의 합니다. RTP는 네트워크를 통해 음성/화상 데이터만 실행합니다. 통화 설정 및 정리 SIP가 일반적으로 수행 됩니다.

RTP에 표준 또는 정적 TCP 또는 UDP 포트와 통신 하는데 필요 하지 않습니다. RTP 통신에서 발생할 수 있습니다는 짝수 UDP 포트 및 TCP 통신에 더 높은 다음 홀수 번호 포트를 사용 합니다. RTP 1024 포트를 사용 하도록 구성 된 일반적으로 표준 포트 범위 배정이 없는 되지만,-65535, 및 Microsoft Exchange 통합 메시징 서비스 팔 로우가이 규칙을 실행 하는 사서함 서버입니다. 동적 포트 범위를 사용 하기 때문에 방화벽을 통과 하는 RTP 어렵습니다.

## 통합된 메시징 웹 서비스

사서함 서버에 설치 된 통합 메시징 웹 서비스는 클라이언트, 사서함 서버 및 다른 Exchange 2013 서버 역할을 실행 하는 컴퓨터 간의 네트워크 통신에 대 한 IP를 사용 합니다. 여러 Exchange 2013Outlook Web App 및 Outlook 2013 클라이언트 기능이 올바르게 작동 하려면 통합 메시징 웹 서비스에 의존 합니다.

통합 메시징 웹 서비스에서는 다음과 같은 통합 메시징 클라이언트 기능을 사용합니다.

  - 음성 메일 옵션 Exchange 2013Outlook Web App, PIN 다시 설정 하는 기능 및 전화 기능에서 재생을 포함 하 여을 사용할 수 있습니다.

  - 전화에서 재생 기능 Outlook 클라이언트에서 찾을 수 있습니다.

## UM 포트

클라이언트 액세스 서버에 있는 Microsoft Exchange 통합 메시징 호출 라우터 서비스 SIP를 사용 하 여 전송 제어 프로토콜 (TCP) 또는 상호 중 하나를 통해 전송 계층 보안 (mutual TLS)는 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버와 통신할 수 있습니다. 충돌을 피하기 위해 TCP/사용자 데이터 그램 프로토콜 (UDP) 포트, Microsoft Exchange 통합 메시징 호출 라우터 서비스 및 Microsoft Exchange 통합 메시징 서비스 기본값으로 설정 하 고 서로 다른 TCP 포트에서 수신 대기 합니다. 보안 되지 않은 및 보안 된 SIP 및 RTP 트래픽 mutual TLS를 사용 하는 여부에 따라 연결을 모두를 수락할 수 있습니다. 기본적으로 mutual TLS를 사용 하는 경우 클라이언트 액세스 서버는 모두 TCP 포트 5060 보안 되지 않은 모드로 및 SIP 보안 모드에서 TCP 포트 5061에서 SIP 요청에 대 한 수신 합니다. 이러한 포트 **Set-UMCallRouterSettings** cmdlet을 사용 하 여 구성할 수 있습니다. 유일한 TCP 포트 및 없음 UDP 포트를 사용 하는 클라이언트 액세스 서버에서 Microsoft Exchange 통합 메시징 호출 라우터 서비스 미디어 (RTP 또는 SRTP) 트래픽을 처리할 하지 않습니다입니다. 기본적으로 mutual TLS를 사용 하는 경우 사서함 서버는 5062 보안 되지 않은 모드에서 모두 TCP 포트 및 TCP 포트 5063 SIP 보안 모드에서 SIP 요청에 대 한 수신 합니다. 이러한 포트 Exchange 관리 셸 cmdlet을 사용 하 여 구성할 수 없습니다. 사서함 서버에서 Microsoft Exchange 통합 메시징 서비스에는 SIP 포트 5062 및 5063에서 클라이언트 액세스 서버에서 연결을 수락 합니다. 클라이언트 액세스 서버에서 사서함 서버를 SIP 요청을 리디렉션합니다, VoIP 게이트웨이, IP PBX 또는, SBC 및 Microsoft Exchange 통합 메시징 작업자 프로세스를 사용 하 여 사서함 서버에는 RTP 또는 SRTP 미디어 채널 파일이 만들어집니다.

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
<td><p>SIP (클라이언트 액세스 서버-Microsoft 통합 메시징 호출 라우터 서비스)</p></td>
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
<td><p>5065 및 TCP (보안 되지 않음)에 대 한 5067 합니다. 5065 및 5067 (보안) mutual TLS에 대 한 합니다. 이중 모드 5066 설정한 경우 5068도 사용 됩니다.</p></td>
<td><p>해당 없음</p></td>
<td><p>포트를 변경할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>RTP(사서함 서버 - UM 작업자 프로세스)</p></td>
<td><p>해당 없음</p></td>
<td><p>1024와 65535 사이의 포트</p></td>
<td><p>Msexchangeum.config 구성 파일에서 포트를 변경할 수 있습니다. Msexchangeum.config 파일은 Exchange 2013 통합 메시징 서버에서 \Program Files\Microsoft\Exchange\V15\bin 폴더에 있습니다.</p></td>
</tr>
</tbody>
</table>


## Lync Server 및 UM 포트

Exchange 2013 통합된 메시징 네트워크 주소 변환 (NAT) 통과 지원할 뿐 이며 NAT 방화벽을 통해 터널링 되 수를 사서함 서버로 RTP 미디어에 대 한 수 있도록 허용 합니다. 그러나이 작업을 수행 하려면 또한 해야 Microsoft Office Communications Server 2007 R2 및 Microsoft Lync Server 2010 또는 Microsoft Lync 2013 환경에 배포 합니다. 네트워크에 모두 Exchange 2013 및 Communications Server 2007 R2 또는 Microsoft Lync Server 2010 또는 Lync 2013 를 배포 하는 경우이 배포 NAT 방화벽 외부의 끝점와 통신 하는 Microsoft Exchange 통합 메시징 서비스를 실행 하는 사서함 서버 사용 하도록 설정 됩니다. 사서함 서버는 Communications Server 2007 R2, Microsoft Lync Server 2010 또는 Lync 2013 풀에 연결 하 고 A에서 적절 한 인증 토큰을 가져옵니다 / V 인증 서비스는 컴퓨터에는 특정 Communications Server 2007 또는 Lync Server 풀을 처리 합니다.

A / V 인증 서비스를 사용 하 여 RTP 음성 미디어 NAT 장치 및 방화벽을 통과를 허용 하 여 합니다. 이 미디어 게이트웨이 신호를 처리 하 고 NAT 장치 또는 방화벽을 통해 음성을 안전 하 게 전송할 수 없습니다 필요 합니다. A를 지정 하는 Communications Server 2007 R2, Lync Server 2010 또는 Lync 2013 에서 중재 서버를 구성할 때 / V에 지 서버를 A / V 인증 서비스를 중재 서버는 들어오는 미디어 패킷을 전달 하는 위치를 파악할 수 있도록 실행 됩니다.

Communications Server 2007 R2 또는 Lync Server 2010 또는 2013을 배포 하는 방법 및 Exchange 2013 하는 방법에 대 한 자세한 내용은 통합 메시징, 다음을 참조 하십시오.

  - [Exchange 2013 UM 및 Lync Server 배포 개요](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [검사 목록: Lync Server와 Exchange 2013 UM 통합](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)

