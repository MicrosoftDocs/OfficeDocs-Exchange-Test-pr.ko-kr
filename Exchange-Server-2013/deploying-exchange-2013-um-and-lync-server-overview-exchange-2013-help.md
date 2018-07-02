---
title: 'Exchange 2013 UM 및 Lync Server 배포 개요: Exchange 2013 Help'
TOCTitle: Exchange 2013 UM 및 Lync Server 배포 개요
ms:assetid: 96fcb0dd-79ee-4e55-9e59-3ee7fbe3c4a1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb676409(v=EXCHG.150)
ms:contentKeyID: 50483746
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 UM 및 Lync Server 배포 개요

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

UM(통합 메시징) 및 Microsoft Lync Server를 함께 배포하여 음성 메시징, 인스턴트 메시징, 향상된 사용자 현재 상태, 오디오/비디오 회의, 통합 전자 메일 및 메시징 환경 등을 조직의 사용자에게 제공할 수 있습니다. 통합 메시징은 음성 메일에 대한 전화 응답, Outlook Voice Access 및 자동 전화 교환 서비스를 제공하는 데 사용됩니다. Microsoft Lync Server에서는 IM(인스턴트 메시징), 회의, 인바운드 및 아웃바운드 호출과 같이 Enterprise Voice에 있는 고급 기능을 사용할 수 있습니다. 이 항목에서는 이러한 기능을 지원하기 위해 통합 메시징 및 Microsoft Lync Server를 구성하는 방법에 대해 설명합니다.


> [!TIP]
> Microsoft Office Communications Server 2007 R2를 통합 메시징과 함께 배포할 수도 있습니다. 이 항목에서 &amp;quot;Microsoft Lync Server&amp;quot;는 Microsoft Lync Server 2010 또는 Microsoft Lync Server 2013을 나타냅니다.



Microsoft Lync Server에 대 한 자세한 내용은 필요 하신가요? [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)를 참조 하십시오.

**목차**

Deploying Exchange UM and Lync Server overview

Certificate configuration recommendations

Deployment steps

For more information

## Exchange UM 및 Lync Server 배포 개요

통합 메시징은 음성 및 전자 메일 메시징을 단일 메시징 인프라로 통합합니다. Microsoft Lync Server Enterprise Voice는 UM 인프라를 활용하여 음성 메일, Outlook Voice Access, 전화 알림 및 자동 전화 교환 기능을 제공합니다.

다음 목록에서는 UM 및 Lync Server의 간소한 배포 단계를 보여 줍니다. 각 단계에 대한 자세한 내용은 이 항목의 뒷부분에 있습니다.

1.  Microsoft Exchange 통합 메시징 호출 라우터 서비스를 실행하는 클라이언트 액세스 서버와 Microsoft Exchange 통합 메시징 서비스를 실행하는 사서함 서버를 설치할 동일한 토폴로지에 Microsoft Lync Server를 설치합니다. Lync 풀이 하나 이상 만들어졌는지 확인합니다.

2.  개인 또는 정부 CA(인증 기관)에서 서명하고 Lync Server가 신뢰하는 유효한 인증서를 설치합니다.

3.  클라이언트 액세스 서버 및 사서함 서버를 설치합니다. 설치를 확인합니다.

4.  Lync 서버에 설치한 인증서와 동일한 CA에서 서명한 유효한 인증서를 설치합니다.

5.  SIP(Session Initiation Protocol) URI 다이얼 플랜을 만들고 구성합니다.

6.  모든 클라이언트 액세스 및 사서함 서버를 SIP URI 다이얼 플랜에 추가합니다. 그러나 SIP URI 다이얼 플랜이 여러 개 있는 경우 모든 SIP URl 다이얼 플랜에 모든 클라이언트 액세스 및 사서함 서버를 추가해야 합니다.

7.  사서함 서버의 \<Exchange 설치 폴더\>\\Exchange Server\\Script 폴더에서 ExchUcUtil.ps1 스크립트를 실행합니다.
    

    > [!IMPORTANT]
    > ExchUcUtil.ps1 스크립트는 Lync 통합 시 UM IP 게이트웨이를 하나 이상 만듭니다. 스크립트가 만들어진 한 게이트웨이를 제외한 모든 UM IP 게이트웨이에서 발신 전화를 사용하지 않도록 설정해야 합니다. 또한 스크립트를 실행하기 전에 만들어진 UM IP 게이트웨이에서도 발신 전화를 사용하지 않도록 설정합니다. UM IP 게이트웨이에서 발신 전화를 사용하지 않도록 설정하려면 <A href="disable-outgoing-calls-on-um-ip-gateways-exchange-2013-help.md">UM IP 게이트웨이에서 거는 전화를 사용 하지 않도록 설정</A>을 참조하세요.



8.  Lync Server의 %CommonProgramFiles%\\Microsoft Lync Server 2013\\Support 폴더에서 **OcsUmUtil.exe**를 실행합니다.

9.  중재 서버와 미디어 게이트웨이를 배포합니다.

10. Lync 서버에 설치한 인증서와 동일한 CA에서 서명한 유효한 인증서를 중재 서버에 설치합니다.

11. 사용자가 UM 및 Enterprise Voice를 사용할 수 있도록 설정합니다.

## 인증서 구성 권장 사항

Exchange를 실행하는 컴퓨터와 Lync Server를 실행하는 컴퓨터에서 모두 신뢰하는 인증서가 있어야 합니다. Lync Server 및 통합 메시징이 포함된 환경에서 다음 지침에 따라 신뢰할 수 있는 인증서를 배포합니다.

  - Lync 서버, 클라이언트 액세스 서버, 사서함 서버, 중재 서버 및 미디어 게이트웨이에서 민간 또는 정부 CA가 서명한 유효한 인증서를 가져옵니다. 이 인증서는 신뢰할 수 있는 타사 상용 인증서나 PKI(공개 키 인프라) 인증서여야 합니다.

  - 각 Exchange 서버에 동일한 타사 상용 또는 PKI 인증서를 가져오면 덜 복잡합니다. 또한 Microsoft Lync Server 및 중재 서버를 실행하는 각 컴퓨터에 이 신뢰할 수 있는 인증서를 설치합니다. 이렇게 하면 인증서 배포가 덜 복잡하게 되고 인증서 배포와 관련된 관리 오버헤드가 줍니다. 하지만 SAN(주체 대체 이름)을 지원하는 신뢰할 수 있는 인증서를 얻어야 합니다.
    
    UM과 함께 TLS(전송 계층 보안)를 배포하는 경우 클라이언트 액세스 서버 및 사서함 서버에서 사용되는 인증서 모두의 인증서 주체 이름에 로컬 컴퓨터의 FQDN(정규화된 도메인 이름)이 포함되어 있어야 합니다. 이 문제를 해결하려면 공용 인증서를 사용하고 모든 클라이언트 및 사서함 서버, 모든 VoIP 게이트웨이, IP PBX, 모든 Lync 서버에 인증서를 가져옵니다.
    
    배포에 VoIP 게이트웨이 또는 IP PBX가 포함되고 SIP 보안 또는 보안 다이얼 플랜을 사용하는 경우 클라이언트 액세스 및 사서함 서버와 VoIP 게이트웨이 또는 IP PBX 간에 신뢰할 수 있는 인증서가 필요합니다. 직접 SIP 연결을 사용하는 경우에도 신뢰할 수 있는 인증서가 필요합니다. SIP 보안 또는 보안 다이얼 플랜을 사용하는 경우 VoIP 게이트웨이 또는 IP PBX에서 사용되는 것과 동일한 신뢰할 수 있는 인증서를 Lync 및 Exchange 서버에서 사용할 수 있습니다.

  - Exchange 클라이언트 액세스 및 사서함 서버를 Microsoft Lync Server나 타사 SIP 게이트웨이 또는 PBX(Private Branch eXchange) 전화 통신 장비에 연결하는 경우 내부 또는 공용 타사 CA(인증 기관)에서 서명한 유효한 인증서를 사용하여 보안 세션을 설정해야 합니다. 인증서의 SAN 목록에 모든 클라이언트 액세스 및 사서함 서버의 FQDN이 포함된 경우 모든 클라이언트 액세스 및 사서함 서버에서 단일 인증서를 사용할 수 있습니다. 또는 각 클라이언트 액세스 및 사서함 서버마다 해당 서버의 주체 CN(일반 이름) 또는 SAN 목록에 있는 로컬 컴퓨터의 FQDN을 사용하여 각기 다른 인증서를 생성할 수 있습니다. Exchange UM은 Microsoft Lync Server에서 와일드카드 인증서를 지원하지 않습니다.
    
    Lync Server와 Exchange가 함께 작동하려면 와일드카드가 아닌 주체 이름이 필요합니다. UM과 Lync Server는 신뢰할 수 있는 SIP 피어임을 나타내는 방법으로 주체 이름을 사용합니다. Lync Server는 일부 호출 라우팅 시나리오에서도 와일드카드가 아닌 주체 이름을 필요로 합니다. FQDN은 "발급 대상" 값으로 사용되어야 합니다.
    
    Exchange UM의 경우 인증서 이름에 와일드카드를 사용할 수 없습니다. 그러나 SAN에는 와일드카드를 사용할 수 있습니다.

다음 표에서는 Exchange UM에 대한 인증서 설치 및 구성을 위한 인증서 요구 사항을 보여 줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>토폴로지</th>
<th>인증서 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>클라이언트 액세스 및 사서함이 동일한 서버에 있음(Lync 2010 또는 2013 없음, 비 SIP 다이얼 플랜)</p></td>
<td><p>클라이언트 액세스 및 사서함 서버 간에 인증서가 필요합니다. 이 인증서는 클라이언트 액세스 및 사서함 서버와 VoIP 게이트웨이, IP PBX 또는 SBC 간에 사용되는 것과 동일합니다.</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 및 사서함이 다른 서버에 있음(Lync 2010 또는 2013 없음, 비 SIP 다이얼 플랜)</p></td>
<td><p>인증서가 필요합니다. 이 인증서는 클라이언트 액세스 및 사서함 서버에서 일치해야 합니다. 클라이언트 액세스 및 사서함 서버와 VoIP 게이트웨이, IP PBX 또는 SBC 간에도 인증서가 필요합니다. 이 인증서는 클라이언트 액세스 및 사서함 서버 간에 사용되는 인증서와 동일하거나 다를 수 있습니다. 클라이언트 액세스 및 사서함 서버의 경우 어느 서버에서든 <strong>Create-ExchangeCertificate</strong> cmdlet을 실행할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 액세스 및 사서함이 동일한 서버에 있음(Lync 2010 또는 2013 있음, SIP 다이얼 플랜)</p></td>
<td><p>인증서가 필요 합니다. 클라이언트 액세스 및 사서함 서버는 동일한 루트 인증서로 Lync 2010 또는 2013 서버 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>클라이언트 액세스 및 사서함이 다른 서버에 있음(Lync 2010 또는 2013 있음, SIP 다이얼 플랜)</p></td>
<td><p>인증서가 필요 합니다. 클라이언트 액세스 및 사서함 서버는 동일한 루트 인증서로 Lync 2010 또는 2013 서버 있어야 합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 배포 단계

조직에서 필요한 서버를 설치한 후 사용자에게 Enterprise Voice를 올바로 배포하기 위해 Exchange 통합 메시징 및 Lync Server 배포에서 수행해야 하는 일련의 권장 단계가 있습니다.

Microsoft Lync Server에 대 한 자세한 내용은, [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)을 참조 하십시오.

다음 단계를 수행하여 통합 메시징이 Lync Server의 Enterprise Voice 기능과 함께 작동하도록 구성해야 합니다.

1.  각각 해당하는 Lync Server 위치 프로필에 매핑되는 하나 이상의 통합 메시징 SIP URI 다이얼 플랜을 만듭니다. 각 Exchange UM 다이얼 플랜에 대해 Enterprise Voice 위치 프로필이 만들어져야 합니다. **Get-UMDialPlan** cmdlet을 사용하여 SIP URI 다이얼 플랜의 FQDN을 가져올 수 있습니다. SIP URI 다이얼 플랜을 만드는 방법에 대한 자세한 내용은 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md) 항목을 참조하십시오.
    

    > [!IMPORTANT]
    > Exchange UM과 Lync Server를 통합할 경우 Exchange UM에서 전화 걸기 규칙 또는 전화 걸기 규칙 그룹을 구성할 필요가 없을 것입니다. Lync Server는 조직의 사용자를 위해 호출 라우팅과 번호 변환을 수행할 수 있도록 설계되었으며 통합 메시징에서 사용자를 대신하여 전화를 건 경우에도 동일한 작업을 수행합니다.



2.  민간 또는 정부 CA에서 서명한 유효한 인증서를 클라이언트 액세스 및 사서함 서버에 설치합니다. 이 CA는 Lync Server에서 사용된 것과 동일합니다.

3.  SIP URI 다이얼 플랜을 SIP 보안 또는 보안으로 구성하여 VoIP(Voice over IP) 트래픽을 암호화합니다.
    

    > [!WARNING]
    > SIP 트래픽에 대해서만 암호화가 필요하도록 보안 설정을 SIP 보안으로 지정하면 프런트 엔드 풀이 암호화가 필요하도록 구성된 경우(즉 프런트 엔드 풀에서 SIP 및 RTP 트래픽 모두에 암호화가 필요함) 다이얼 플랜의 이 설정으로는 부족합니다. 다이얼 플랜과 풀 보안 설정이 호환되지 않으면 프런트 엔드 풀에서의 모든 Exchange UM 호출이 실패하고 "보안 설정이 호환되지 않습니다."라는 오류가 표시됩니다.

    
    UM 다이얼 플랜을 SIP 보안 또는 보안으로 구성할 수 있지만 Lync Phone Edition 장치가 올바르게 작동하도록 하려면 다이얼 플랜을 보안으로 구성하는 것이 좋습니다. 이는 Lync Server에 구성된 기본 암호화 수준 설정 때문입니다. Lync Phone Edition 장치는 암호화 설정이 다음 표에 나온 대로 구성된 경우에만 작동합니다. 다음 표에서는 Lync Server 및 UM 다이얼 플랜의 암호화 설정 간의 관계를 보여 줍니다.
    
    **Lync Phone Edition의 암호화 설정**
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Lync Server</th>
    <th>UM 다이얼 플랜</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>암호화 필수(기본값)</p></td>
    <td><p>보안</p></td>
    </tr>
    <tr class="even">
    <td><p>암호화 선택적</p></td>
    <td><p>SIP 보안/보안</p></td>
    </tr>
    <tr class="odd">
    <td><p>암호화 안 함</p></td>
    <td><p>SIP 보안</p></td>
    </tr>
    </tbody>
    </table>


4.  모든 클라이언트 액세스 및 사서함 서버를 SIP 다이얼 플랜에 추가합니다. 서버가 들어오는 호출에 응답할 수 있게 하려면 Lync Server의 호출에 응답하도록 할 모든 Exchange 서버를 다이얼 플랜에 추가해야 합니다.

5.  SIP URI 다이얼 플랜에 추가한 클라이언트 액세스 및 사서함 서버에서 시작 모드 및 TLS 수신 포트는 이중으로 설정한 다음 각 사서함 서버의 MicrosoftExchange 통합 메시징 서비스 및 각 클라이언트 서버의 MicrosoftExchange 통합 메시징 호출 라우터 서비스를 다시 시작합니다.

6.  UM 자동 전화 교환을 만들고 구성합니다. 자세한 내용은 [UM 자동 전화 교환을 설정합니다](set-up-a-um-auto-attendant-exchange-2013-help.md) 항목을 참조하십시오.

7.  사용자가 음성 메일을 사용할 수 있도록 설정할 때 Enterprise Voice를 사용할 사용자에 대한 SIP 주소를 만듭니다. 대부분의 경우 이 SIP 주소는 사용자가 Enterprise Voice를 사용할 수 있도록 설정할 때 사용하는 SIP 주소와 동일합니다. 자세한 내용은 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md) 항목을 참조하십시오.
    

    > [!IMPORTANT]
    > SIP URI 다이얼 플랜과 연결된 사용자는 수신 팩스를 받을 수 없습니다. 이는 들어오는 음성 및 팩스 호출이 중재 서버를 통해 라우팅되며 중재 서버가 사용될 경우 팩스가 지원되지 않기 때문입니다.



8.  Exchange 관리 셸을 열고 %Program Files%\\Microsoft\\Exchange Server\\V15\\Scripts 폴더에 있는 exchucutil.ps1 스크립트를 실행합니다. exchucutil.ps1 스크립트는 다음을 수행합니다.
    
      - Lync Server 읽을 수 있는 권한을 Exchange UM Active Directory 구성 요소, 특히 이전 작업에서 만든 SIP URI 다이얼 플랜을 부여 합니다. Active Directory 에서 사용 권한을 구성 하는 방법에 대 한 자세한 내용은, [사용 권한을 적용할 하려면 ADSI 편집을 사용 하는 방법](https://go.microsoft.com/fwlink/p/?linkid=82751)을 참조 하십시오.
    
      - 각 Lync Server 풀이나 Enterprise Voice를 사용하도록 설정할 사용자를 호스트하고 Lync Server Standard Edition을 실행하는 각 서버에 대해 UM IP 게이트웨이를 만듭니다. 자세한 내용은 [UM IP 게이트웨이 만들기](create-a-um-ip-gateway-exchange-2013-help.md) 항목을 참조하십시오.
    
      - 각 UM IP 게이트웨이에 대해 Exchange UM 헌트 그룹을 만듭니다. 헌트 그룹 파일럿 식별자는 해당하는 UM IP 게이트웨이와 연관된 다이얼 플랜의 이름이 됩니다. 헌트 그룹은 UM IP 게이트웨이에서 사용되는 UM SIP 다이얼 플랜을 지정해야 합니다.

9.  사용자가 음성 메일을 사용할 수 있도록 설정합니다. 이때 사용자의 유효한 SIP 주소를 입력하고 사용자를 SIP 다이얼 플랜에 연결해야 합니다. 자세한 내용은 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md) 항목을 참조하십시오.

또한 다음 작업을 수행하여 Lync Server가 통합 메시징과 함께 작동하도록 구성해야 합니다.

  - 위치 프로필 또는 Lync 다이얼 플랜을 만듭니다. 위치 프로필 이름은 해당 UM 다이얼 플랜의 FQDN과 일치하지 않아도 됩니다.

  - 위치 프로필을 Lync Server 풀에 할당합니다.

  - 미디어 게이트웨이 또는 중재 서버를 배포 및 구성합니다. 또한 클라이언트 액세스 및 사서함 서버와 Lync Server의 인증서에 사용된 것과 동일한 신뢰할 수 있는 CA에서 인증서를 가져와야 합니다.

  - 전화 사용을 정의하고 음성 정책 및 아웃바운드 호출 경로를 만들어 할당합니다.

  - Enterprise Voice의 사용자를 구성하고 TEL URI 및 SIP 식별자를 추가합니다.

  - Outlook Voice Access 및 자동 전화 교환에 대한 연락처 개체를 만드는 **ocsumutil.exe**를 실행합니다.
    

    > [!NOTE]
    > Lync Server를 설치하면 <STRONG>msRTC-SIPLine</STRONG> 특성이 Active Directory에 추가됩니다. 사용자 환경에 Lync Server를 설치하지 않은 경우 이 특성은 Active Directory에 추가되지 않습니다. 따라서 UM을 사용할 수 없는 사용자에 대해 통합 메시징 프록시 주소를 구성하지 않을 경우 단일 포리스트 및 포리스트 간 시나리오에서 다이얼 플랜 간의 발신자 번호 이름 확인이 올바로 이루어지지 않습니다.



Lync Server 및 통합 메시징 서버를 구성한 후 사용자가 Lync Server를 사용하고 사용자의 클라이언트 컴퓨터에 Lync를 설치할 수 있게 해야 합니다.


> [!IMPORTANT]
> 통합 메시징 및 Lync Server를 통합하는 경우 Exchange 2007 또는 Exchange 2010 사서함 서버에 사서함이 있는 사용자는 부재 중 전화 알림을 사용할 수 없습니다. 부재 중 전화 알림은 전화가 사서함 서버에 전송되기 전에 사용자의 연결이 끊기는 경우 생성됩니다.



맨 위로 이동

## 자세한 내용

Microsoft Lync Server에 대 한 완료 되어야 하는 작업을 수행 하는 방법에 대 한 자세한 내용은 [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752)을 참조 하십시오.

