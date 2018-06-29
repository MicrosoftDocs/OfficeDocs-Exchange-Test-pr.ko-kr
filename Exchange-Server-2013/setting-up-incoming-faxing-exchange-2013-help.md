---
title: '수신 팩스 설정: Exchange 2013 Help'
TOCTitle: 수신 팩스 설정
ms:assetid: 5d3cae58-1690-424d-9bef-011911d0b608
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633468(v=EXCHG.150)
ms:contentKeyID: 52057925
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수신 팩스 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange UM(통합 메시징)은 아웃바운드 팩스 또는 팩스 라우팅 같은 향상된 팩스 기능을 위해 인증된 팩스 파트너 솔루션을 사용합니다. 기본적으로 Exchange 서버는 UM 사용 가능 사용자에게 수신되는 팩스를 배달하도록 구성되지 않습니다. 대신에 Exchange 서버는 수신 팩스 호출을 인증된 팩스 파트너 솔루션으로 리디렉션합니다. 팩스 파트너의 서버는 팩스 데이터를 받은 후 이 팩스가 .tif 첨부 파일로 포함된 전자 메일 메시지로 사용자의 사서함에 보냅니다.

팩스 파트너에 대 한 자세한 내용은 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238)

## 팩스 배포 및 구성

UM이 수신 팩스 호출을 전용 팩스 파트너 솔루션으로 전달하면, 이 솔루션에서는 팩스 호출과 팩스를 보낸 사람을 연결하고 UM 사용 가능한 사용자를 대신하여 팩스를 수신합니다. 단, UM 사용 가능한 사용자가 사서함에서 팩스 메시지를 받도록 하려면 먼저 수신 팩스를 사용하도록 설정하고 UM 사용 가능한 사용자에게 연결된 UM 사서함 정책에 대해 팩스 파트너 URI를 설정해야 합니다. UM 사용 가능한 사용자에 대해 UM 다이얼 플랜, UM 사서함 정책 및 사서함에서 수신 팩스를 허용하거나 금지할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [사용자가 팩스를 받을 동일한 다이얼 플랜의 수 있게 합니다.](allow-users-in-the-same-dial-plan-to-receive-faxes-exchange-2013-help.md)

  - [팩스를 받을에서 동일한 다이얼 플랜에 사용자를 방지](prevent-users-in-the-same-dial-plan-from-receiving-faxes-exchange-2013-help.md)

  - [사용자 그룹에 대 한 팩스를 사용 하도록 설정](enable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [사용자 그룹에 대 한 팩스를 사용 하지 않도록 설정](disable-faxing-for-a-group-of-users-exchange-2013-help.md)

  - [팩스를 받을 수 있도록 설정](enable-a-user-to-receive-faxes-exchange-2013-help.md)

  - [사용자 팩스를 받지 않도록 방지](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)

## 1단계: 통합 메시징 배포

온-프레미스나 하이브리드 조직에 대해 팩스를 설정하려면 클라이언트 액세스 및 사서함 서버를 배포하고 팩스를 허용하도록 지원되는 VoIP(Voice over IP) 게이트웨이를 구성해야 합니다. UM을 배포하는 방법에 대한 자세한 내용은 [Exchange 2013 UM 배포](deploy-exchange-2013-um-exchange-2013-help.md)를 참조하십시오. VoIP 게이트웨이 및 IP PBX(Private Branch eXchanges)를 배포하는 방법에 대한 자세한 내용은 [UM 전화 시스템에 연결](connect-um-to-your-telephone-system-exchange-2013-help.md)을 참조하십시오.


> [!IMPORTANT]
> 통합 메시징, MicrosoftOffice Communications Server 2007 R2 또는 Microsoft Lync Server가 통합된 환경에서는 T.38 또는 G.711을 사용하여 팩스를 보내고 받을 수 없습니다.



## 2단계: 팩스 파트너 서버 구성

다음으로, 수신 팩스를 활성화 하 고 조직에 필요한 각 UM 사서함 정책에서 팩스 파트너의 URI를 구성 해야 합니다. 수신 팩스를 성공적으로 배포 하려면 Exchange 통합 메시징이 있는 인증 된 팩스 파트너 솔루션을 통합 해야 합니다. 자세한 내용은 [Exchange UM에 대 한 팩스 advisor](fax-advisor-for-exchange-um-exchange-2013-help.md)를 참조 합니다. 인증 된 팩스 파트너 목록을, [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238) 을 참조 하십시오.


> [!NOTE]
> 팩스 파트너 서버는 조직 외부에 있으므로 IP 기반 네트워크를 통해 팩스를 사용하도록 설정하는 T.38 프로토콜 포트를 허용하도록 방화벽 포트를 구성해야 합니다. 기본적으로 T.38 프로토콜은 TCP 포트 6004를 사용합니다. UDP(사용자 데이터그램 프로토콜) 포트 6044도 사용할 수 있지만 이 포트는 하드웨어 제조업체에 의해 정의됩니다. TCP 또는 UDP 포트나 제조업체에서 정의한 포트 범위를 사용하는 팩스 데이터를 허용하도록 방화벽 포트를 구성해야 합니다.



## 3단계: 통합 메시징에 대해 팩스를 사용하도록 설정

사용자가 통합 메시징을 사용하여 팩스를 수신하도록 하려면 다음 구성 요소를 올바르게 구성해야 합니다.

  - UM 다이얼 플랜

  - UM 사서함 정책

  - UM 사서함

UM 다이얼 플랜, UM 사서함 정책 또는 개별 UM 사용 가능 사용자의 사서함에 대해 팩스를 사용하거나 사용하지 않도록 설정할 수 있습니다. UM 사서함 정책은 EAC(Exchange 관리 센터)나 Exchange 관리 셸을 사용하여 팩스에 대해 사용하도록 설정하거나 사용하지 않도록 설정할 수 있습니다. 다이얼 플랜 및 개별 UM 사용 가능 사용자를 사용하도록 설정하고 사용하지 않도록 설정하는 작업은 Exchange 관리 셸을 사용하여 수행해야 합니다. 다음 표에는 팩스를 사용하도록 설정하고 사용하지 않도록 설정하는 데 사용되는 cmdlet 및 매개 변수와 사용 가능한 옵션이 나와 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>UM 구성 요소</th>
<th>EAC를 사용하여 사용하도록 설정하거나 사용하지 않도록 설정할 수 있는지 여부</th>
<th>팩스를 사용하도록 설정하는 셸의 예</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>다이얼 플랜</p></td>
<td><p>아니요</p></td>
<td><p><code>Set-UMDialPlan -id MyUMDialPlan -faxenabled $true</code></p></td>
</tr>
<tr class="even">
<td><p>UM 사서함 정책</p></td>
<td><p>예</p></td>
<td><p><code>Set-UMMaiboxPolicy -id MyPolicy -AllowFax $true</code></p></td>
</tr>
<tr class="odd">
<td><p>UM 사용 가능 사용자</p></td>
<td><p>아니요</p></td>
<td><p><code>Set-UMMailbox -id tonysmith -faxenabled $true</code></p></td>
</tr>
</tbody>
</table>


기본적으로 UM 다이얼 플랜 및 사용자의 사서함이 수신 팩스를 허용하더라도 먼저 UM 사용 가능 사용자에게 할당된 UM 사서함 정책에 대해 인바운드 팩스를 사용하도록 설정하고 팩스 파트너 서버의 URI를 입력해야 합니다.

UM 사용 가능 사용자가 팩스를 받을 수 있도록 설정하려면 다음을 수행해야 합니다.

  - UM 다이얼 플랜에 연결된 사용자가 각 UM 다이얼 플랜을 통해 팩스를 받을 수 있는지 확인합니다. 기본적으로 다이얼 플랜과 연결된 모든 사용자는 팩스를 받을 수 있습니다. UM 사용 가능 사용자가 자신의 사서함에서 팩스 메시지를 수신하려면 수신 팩스 호출을 수락하도록 각 VoIP 게이트웨이나 IP PBX를 구성해야 합니다. 또한 다이얼 플랜과 연결된 사용자가 팩스 메시지를 받을 수 있도록 설정해야 합니다. 다이얼 플랜에 연결된 사용자가 팩스를 수신하도록 하거나 팩스를 수신하지 못하도록 설정하는 방법에 대한 자세한 내용은 [팩스를 받을 수 있도록 설정](enable-a-user-to-receive-faxes-exchange-2013-help.md)을 참조하십시오.
    

    > [!NOTE]
    > 다이얼 플랜에서 팩스 메시지를 받지 못하도록 차단하면 해당 다이얼 플랜과 연결된 모든 사용자는 팩스를 받지 못하게 됩니다. 팩스 수신을 허용하도록 개별 사용자의 속성을 구성하는 경우에도 마찬가지입니다. UM 다이얼 플랜에서 팩스를 사용하거나 사용하지 않도록 설정하는 것은 개별 UM 사용 가능 사용자에 대한 설정보다 우선합니다.



  - UM 사용 가능 사용자와 연결된 UM 사서함 정책을 구성합니다. UM 사서함 정책은 팩스 파트너의 URI 및 팩스 파트너 서버 이름을 비롯하여 수신 팩스를 허용하도록 구성되어야 합니다. *FaxServerURI* 매개 변수의 형식은 다음과 같아야 합니다. sip:\<*팩스 서버 URI*\>:\<*포트*\>;\<*전송*\>, 여기서 "팩스 서버 URI"는 팩스 파트너 서버의 FQDN(정규화된 도메인 이름) 또는 IP 주소이고 "포트"는 팩스 서버가 수신 팩스 호출을 수신 대기하는 포트이며 "전송"은 수신 팩스에 사용되는 전송 프로토콜입니다(UDP, TCP 또는 TLS(전송 계층 보안)). 예를 들어 다음과 같이 팩스를 수신하도록 UM 사서함 정책을 구성할 수 있습니다.
    
        Set-UMMailboxPolicy MyUMMailboxPolicy -AllowFax $true -FaxServerURI "sip:faxserver.abc.com:5060;transport=tcp"

  - 자세한 내용은 [팩스 서버 팩스를 허용 하는 URI 파트너를 설정 합니다.](set-the-partner-fax-server-uri-to-allow-faxing-exchange-2013-help.md)을 참조하십시오.
    
    <table>
    <thead>
    <tr class="header">
    <th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><em>FaxServerURI</em> 형식에는 세미콜론으로 구분된 여러 항목을 포함할 수 있지만 하나의 항목만 사용됩니다. 이 매개 변수는 하나의 항목만 사용하도록 하며 여러 항목을 추가하면 팩스 요청의 부하를 분산시킬 수 없습니다.</td>
    </tr>
    </tbody>
    </table>


  - UM 사용 가능 사서함이 팩스 메시지를 받을 수 있는지 확인합니다. 기본적으로 다이얼 플랜과 연결된 모든 사용자는 팩스를 받을 수 있습니다. 하지만 사서함에서 팩스 수신 기능이 사용하지 않도록 설정되어 사용자가 팩스를 받을 수 없는 경우도 있습니다. UM 사용 가능 사용자가 팩스를 받도록 설정하는 방법에 대한 자세한 내용은 [팩스를 받을 수 있도록 설정](enable-a-user-to-receive-faxes-exchange-2013-help.md)을 참조하십시오.
    
    다이얼 플랜과 연결된 개별 사용자가 팩스 메시지를 받지 못하도록 차단할 수 있습니다. 이렇게 하려면 셸에서 **Set-UMMailbox** cmdlet을 사용하여 사용자에 대해 속성을 구성합니다. **Set-UMMailboxPolicy** cmdlet을 사용하여 여러 사용자가 팩스 메시지를 받지 못하도록 차단할 수도 있습니다. 한 명 이상의 사용자가 팩스 메시지를 받지 못하도록 차단하는 방법에 대한 자세한 내용은 [사용자 팩스를 받지 않도록 방지](prevent-a-user-from-receiving-faxes-exchange-2013-help.md)을 참조하십시오.

## 4단계: 인증 구성

UM 다이얼 플랜, UM 사서함 정책 및 UM 사용 가능 사용자를 구성하는 것 외에도 Exchange 서버와 팩스 파트너 서버 간 인증을 구성해야 합니다. Exchange 서버는 팩스 파트너 서버에서 들어오는 것으로 주장하는 메시지의 출처를 인증할 수 있어야 합니다. 팩스 파트너 서버에서 들어오는 것으로 주장하지만 인증되지 않은 모든 메시지는 Exchange 서버에서 처리되지 않습니다.

팩스 파트너 서버에서 Exchange 서버로의 연결을 인증하려면 다음을 사용할 수 있습니다.

  - 상호 TLS

  - 보낸 사람 ID 유효성 검사

  - 전용 수신 커넥터

수신 커넥터는 조직에 배포된 팩스 파트너 서버를 인증할 수 있어야 합니다. 수신 커넥터는 Exchange 서버가 팩스 파트너 서버에서 들어오는 모든 트래픽을 인증된 것으로 취급하는지 확인합니다.

수신 커넥터는 SMTP 팩스 메시지를 전송하기 위해 팩스 파트너 서버에서 사용하는 Exchange 서버에 구성되며 다음 값으로 구성되어야 합니다.

  - *AuthMechanism: ExternalAuthoritative*

  - *PermissionGroups: ExchangeServers, PartnersFax*

  - *RemoteIPRanges: {the fax server's IP address}*

  - *RequireTLS: False*

  - *EnableAuthGSSAPI: False*

  - *LiveCredentialEnabled: False*

자세한 내용은 [커넥터](connectors-exchange-2013-help.md)를 참조하십시오.

팩스 파트너 서버가 공용 네트워크를 통해 네트워크 트래픽을 Exchange 서버로 보내는 경우(예: 클라우드에서 호스트된 서비스 기반의 팩스 파트너) 보낸 사람 ID 검사를 통해 팩스 파트너 서버를 인증하는 것이 좋습니다. 이러한 인증 유형은 팩스 메시지가 들어왔음을 주장하는 팩스 파트너 도메인 대신 해당 메시지를 수신한 IP 주소에서 전자 메일 메시지를 보내도록 인증되었는지 확인합니다. DNS는 보낸 사람 ID 레코드(또는 SPF(보낸 사람 정책 프레임워크) 레코드)를 저장하는 데 사용되며, 팩스 파트너는 DNS 정방향 조회 영역에 자신의 SPF 레코드를 게시해야 합니다. Exchange는 DNS를 쿼리하여 IP의 유효성을 검사합니다. 단, DNS 쿼리를 수행하려면 보낸 사람 ID 에이전트가 사서함 서버에서 실행 중이어야 합니다.

TLS를 사용하여 네트워크 트래픽을 암호화하거나 상호 TLS를 사용하여 팩스 파트너 서버와 Exchange 서버 간 암호화 및 인증을 수행할 수도 있습니다.

