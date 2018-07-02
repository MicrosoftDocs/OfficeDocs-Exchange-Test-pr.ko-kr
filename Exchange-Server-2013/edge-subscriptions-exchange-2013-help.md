---
title: 'Edge 구독: Exchange 2013 Help'
TOCTitle: Edge 구독
ms:assetid: 3addd71a-4165-401f-a009-002bcd8baba6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997438(v=EXCHG.150)
ms:contentKeyID: 61183421
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 구독

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Edge 전송 서버는 모든 인터넷 연결 메일 흐름을 처리하고 Exchange 조직에 대해 SMTP 릴레이 및 스마트 호스트 서비스를 제공하여 공격 영역을 최소화합니다. 조직 경계 네트워크의 Edge 전송 서버에서 실행되는 일련의 에이전트에 의해 추가적인 메시지 보호 및 보안 계층이 제공됩니다. 이러한 에이전트는 바이러스 및 스팸 방지 기능을 제공하고 메시지 흐름을 제어하는 전송 규칙을 적용합니다.

Edge 구독은 Edge 전송 서버의 AD LDS(Active Directory Lightweight Directory Services) 인스턴스를 Active Directory 데이터로 채우는 데 사용됩니다. ‏Edge 구독을 반드시 만들어야 하는 것은 아니지만 Edge 전송 서버를 Exchange 조직에 구독하면 관리 환경이 간소해지고 스팸 방지 기능이 향상됩니다. 받는 사람 조회 또는 수신 허용 목록 집계를 사용하려는 경우 또는 MTLS(상호 전송 계층 보안)를 사용하여 파트너 도메인과의 SMTP 통신을 보호하려는 경우에는 Edge 구독을 만들어야 합니다.

**목차**

Edge Subscription Process

Microsoft Exchange EdgeSync Service

Managing Edge Subscriptions

## Edge 구독 프로세스

Edge 전송 서버는 Active Directory에 직접 액세스할 수 없습니다. Edge 전송 서버가 메시지를 처리하는 데 사용하는 구성 및 받는 사람 정보는 AD LDS에 로컬로 저장됩니다. Edge 구독을 만들면 Active Directory의 정보가 AD LDS로 안전하게 자동 복제됩니다. Edge 구독 프로세스는 Exchange 2013 사서함 서버와 구독된 Edge 전송 서버 간의 보안 LDAP 연결을 설정하는 데 사용되는 자격 증명을 프로비전합니다. 사서함 서버에서 실행되는 Microsoft Exchange EdgeSync 서비스(EdgeSync)가 주기적인 단방향 동기화를 수행하여 최신 데이터를 AD LDS로 전송합니다. 따라서 사서함 서버를 구성한 다음 해당 정보를 Edge 전송 서버에 동기화할 수 있으므로 경계 네트워크에서 수행하는 관리 작업이 줄어듭니다.

Edge 전송 서버에서/서버로 메시지를 전송하는 사서함 서버가 포함된 Active Directory 사이트에 Edge 전송 서버를 구독합니다. Edge 구독 프로세스를 통해 해당 Edge 전송 서버에 대한 Active Directory 사이트 구성원 정보도 만들어집니다. 이 사이트 정보를 사용하면 Exchange 조직의 사서함 서버가 명시적인 송신 커넥터를 구성하지 않고도 인터넷 배달용으로 Edge 전송 서버에 메시지를 릴레이할 수 있습니다.

하나 이상의 Edge 전송 서버를 단일 Active Directory 사이트에 구독할 수 있습니다. 그러나 Edge 전송 서버 하나를 여러 Active Directory 사이트에 구독할 수는 없습니다. 여러 Edge 전송 서버를 배포하는 경우 각 서버를 서로 다른 Active Directory 사이트에 구독할 수 있습니다. 각 Edge 전송 서버에는 개별 Edge 구독이 필요합니다.

Edge 전송 서버를 배포하여 Active Directory 사이트에 구독하려면 다음 단계를 수행합니다.

1.  Edge 전송 서버 역할을 설치합니다.

2.  DNS 이름 확인을 사용하여 사서함 서버와 Edge 전송 서버가 서로를 찾을 수 있는지 확인합니다.

3.  사서함 서버에서 Edge 전송 서버로 복제할 개체 및 설정을 구성합니다.

4.  Edge 전송 서버에서 Edge 구독 파일을 만들고 내보냅니다.

5.  Edge 구독 파일을 사서함 서버나 사서함 서버가 포함된 Active Directory 사이트에서 액세스할 수 있는 파일 공유로 복사합니다.

6.  Active Directory 사이트로 Edge 구독 파일을 가져옵니다.

## 새 Edge 구독을 만드는 경우 수행되는 작업

Edge 전송 서버에서 **New-EdgeSubscription** cmdlet을 실행하여 Edge 구독 파일을 만들면 다음 작업이 수행됩니다.

  - ESBRA(EdgeSync 부트스트랩 복제 계정)라는 AD LDS 계정이 만들어집니다. 이러한 ESBRA 자격 증명은 첫 번째 EdgeSync 연결을 Edge 전송 서버에 대해 인증할 때 사용됩니다. 이 계정은 작성 시점에서 24시간 후에 만료되도록 구성됩니다. 따라서 이전 섹션에서 설명한 6단계 구독 프로세스를 24시간 내에 완료해야 합니다. Edge 구독 프로세스가 완료되기 전에 ESBRA가 만료되면 **New-EdgeSubscription** cmdlet을 다시 실행하여 새 Edge 구독 파일을 만들어야 합니다.

  - ESBRA 자격 증명은 AD LDS에서 검색되어 Edge 구독 파일에 기록됩니다. 이때 Edge 전송 서버의 자체 서명 인증서용 공개 키도 Edge 구독 파일로 내보내집니다. Edge 구독 파일에 작성되는 자격 증명은 파일을 내보낸 서버에만 적용됩니다.

  - Edge 전송 서버에서 이전에 만들어졌으며 이제 Active Directory에서 AD LDS로 복제될 구성 개체는 AD LDS에서 삭제되며 이러한 개체를 구성하는 데 사용된 Exchange 관리 셸 cmdlet은 사용할 수 없도록 설정됩니다. 그러나 계속해서 **Get-\*** cmdlet을 사용하여 이러한 개체를 볼 수는 있습니다. **New-EdgeSubscription** cmdlet을 실행하면 Edge 전송 서버에서 다음 cmdlet이 사용하지 않도록 설정됩니다.
    
      - **Set-SendConnector**
    
      - **New-SendConnector**
    
      - **Remove-SendConnector**
    
      - **New-AcceptedDomain**
    
      - **Set-AcceptedDomain**
    
      - **Remove-AcceptedDomain**
    
      - **New-MessageClassification**
    
      - **Set-MessageClassification**
    
      - **Remove-MessageClassification**
    
      - **New-RemoteDomain**
    
      - **Set-RemoteDomain**
    
      - **Remove-RemoteDomain**

사서함 서버에서 **New-EdgeSubscription** cmdlet을 실행하여 사서함 서버로 Edge 구독 파일을 가져오면 다음 작업이 수행됩니다.

  - Edge 구독이 만들어지며 Edge 전송 서버가 Exchange 조직에 구독됩니다. EdgeSync는 구성 데이터를 이 Edge 전송 서버로 전파하여 Active Directory에 Edge 구성 개체를 만듭니다.

  - Active Directory 사이트의 각 사서함 서버는 새 Edge 전송 서버가 구독되었다는 알림을 Active Directory로부터 받습니다. 그러면 사서함 서버가 Edge 구독 파일에서 ESBRA를 검색합니다. 그런 다음 이 사서함 서버는 Edge 전송 서버 자체 서명 인증서의 공개 키를 사용하여 ESBRA를 암호화합니다. 이렇게 암호화된 자격 증명은 Edge 구성 개체에 기록됩니다.

  - 또한 각 사서함 서버는 자체 공개 키를 사용하여 ESBRA를 암호화한 다음 해당 자격 증명을 자체 구성 개체에도 저장합니다.

  - 각 Edge 전송 서버와 사서함 서버 쌍에 대한 ESRA(EdgeSync 복제 계정)가 Active Directory에 만들어집니다. 각 사서함 서버는 해당 ESRA 자격 증명을 사서함 서버 구성 개체의 특성으로 저장합니다.

  - Edge 전송 서버에서 인터넷으로 보내는 아웃바운드 메시지와 Edge 전송 서버에서 Exchange 조직으로 보내는 인바운드 메시지를 릴레이하기 위해 송신 커넥터가 자동으로 만들어집니다.

  - 사서함 서버에서 실행되는 Microsoft Exchange EdgeSync 서비스는 ESBRA 자격 증명을 사용하여 사서함 서버와 Edge 전송 서버 간에 보안 LDAP 연결을 설정하며 초기 데이터 복제를 수행합니다. AD LDS로 복제되는 데이터는 다음과 같습니다.
    
      - 토폴로지 데이터
    
      - 구성 데이터
    
      - 받는 사람 데이터
    
      - ESRA 자격 증명

  - Edge 전송 서버에서 실행되는 Microsoft Exchange 자격 증명 서비스가 ESRA 자격 증명을 설치합니다. 이러한 자격 증명은 이후 동기화 연결을 인증하고 안전하게 연결되도록 하는 데 사용됩니다.

  - EdgeSync 동기화 일정이 설정됩니다.

구독된 Active Directory 사이트의 사서함 서버에서 실행되는 Microsoft Exchange EdgeSync 서비스가 정기적인 일정에 따라 Active Directory에서 AD LDS로의 단방향 데이터 복제를 수행합니다. **Start-EdgeSynchronization** cmdlet을 사용하여 EdgeSync 동기화 일정을 재정의하고 동기화를 즉시 시작할 수도 있습니다.

ESRA 계정 및 이러한 계정을 사용하여 안전한 EdgeSync 동기화 프로세스를 수행하는 방법에 대한 자세한 내용은 [Edge 구독 자격 증명](edge-subscription-credentials-exchange-2013-help.md)를 참조하세요.

이 예에서는 Edge 전송 서버를 지정된 사이트에 구독하고 인터넷 송신 커넥터 및 Edge 전송 서버에서 사서함 서버로의 송신 커넥터를 자동으로 만듭니다.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -CreateInternetSendConnector $true -CreateInboundSendConnector $true -Site "Default-First-Site-Name" 


> [!NOTE]
> <EM>CreateInternetSendConnector</EM> 및 <EM>CreateInboundSendConnector</EM> 매개 변수의 기본값은 모두 <CODE>$true</CODE>이며, 여기서는 예시용으로만 표시됩니다.



이 예에서는 Edge 구독 파일을 내보냅니다.

    New-EdgeSubscription -FileName "C:\EdgeSubscriptionInfo.xml"


> [!NOTE]
> Edge 전송 서버에서 <STRONG>New-EdgeSubscription</STRONG> cmdlet을 실행하면 사용하지 않도록 설정할 명령과 Edge 전송 서버에서 덮어쓸 구성을 확인하라는 메시지가 표시됩니다. 이 확인 메시지를 무시하려면 <EM>Force</EM> 매개 변수를 사용해야 합니다. 이 매개 변수는 <STRONG>New-EdgeSubscription</STRONG> cmdlet을 스크립팅하는 경우에 유용합니다. <EM>Force</EM> 매개 변수는 Edge 전송 서버를 다시 구독할 때 만들어지는 파일과 이름이 같은 기존 파일을 덮어쓰는 데에도 사용됩니다.



구문과 매개 변수에 대한 자세한 내용은 [New-EdgeSubscription](https://technet.microsoft.com/ko-kr/library/bb123800\(v=exchg.150\))를 참조하세요.

## Edge 구독 프로세스 중에 만들어진 송신 커넥터

기본적으로 Edge 구독 파일을 사서함 서버로 가져와 권장 Edge 구독 프로세스를 완료하면 인터넷과 Exchange 조직 간의 종단 간 메일 흐름을 사용하는 데 필요한 송신 커넥터가 자동으로 만들어지고 Edge 전송 서버의 기존 송신 커넥터는 삭제됩니다. 송신 커넥터를 자동으로 만들지 않도록 설정하고 수동으로 송신 커넥터를 구성하는 시나리오도 있습니다. 송신 커넥터를 수동으로 구성하는 방법에 대한 자세한 내용은 [Edge 전송 서버 메일 흐름 수동 구성](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md) 및 [EdgeSync를 사용 하지 않고 Edge 전송 서버를 통해 인터넷 메일 흐름 구성](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)을 참조하세요.

Edge 구독 프로세스는 다음과 같은 송신 커넥터를 프로비전합니다.

  - Exchange 조직에서 인터넷으로 전자 메일 메시지를 릴레이하도록 구성된 송신 커넥터

  - Edge 전송 서버에서 Exchange 조직으로 전자 메일 메시지를 릴레이하도록 구성된 송신 커넥터

또한 Edge 전송 서버를 Exchange 조직에 구독하면 구독된 Active Directory 사이트의 사서함 서버가 조직 내 송신 커넥터를 사용하여 해당 Edge 전송 서버로 메시지를 릴레이할 수 있습니다.

## 인터넷에서 메시지를 받는 인바운드 송신 커넥터 자동 생성

기본적으로 사서함 서버에서 **New-EdgeSubscription** cmdlet을 실행하면 인바운드 송신 커넥터 매개 변수 *CreateInboundSendConnector*의 값이 `$true`로 설정됩니다. 그러면 Exchange 조직으로 메시지를 보내는 데 필요한 송신 커넥터가 만들어집니다. 다음 표에서는 이 송신 커넥터의 구성을 보여줍니다.

### 인바운드 송신 커넥터 자동 구성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>속성</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - Inbound to &lt;<em>사이트 이름</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:--;1</code></p>
<p>주소 공간의 <code>--</code> 값은 Exchange 조직의 모든 신뢰할 수 있는 도메인 및 내부 릴레이 허용 도메인을 나타냅니다. 이러한 허용 도메인에 대해 Edge 전송 서버가 수신하는 모든 메시지는 이 송신 커넥터로 라우팅되고 스마트 호스트로 릴레이됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Edge 구독 이름</em>&gt;</p></td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>False</p></td>
</tr>
<tr class="even">
<td><p><em>SmartHosts</em></p></td>
<td><p><code>--</code></p>
<p>스마트 호스트 목록의 <code>--</code> 값은 구독된 Active Directory 사이트의 모든 사서함 서버를 나타냅니다. Edge 구독을 설정한 후 구독된 Active Directory 사이트에 추가하는 모든 사서함 서버는 EdgeSync 동기화 프로세스에 포함되지 않습니다. 하지만 자동으로 만들어진 인바운드 송신 커넥터의 스마트 호스트 목록에는 자동으로 추가됩니다. 둘 이상의 사서함 서버가 구독된 Active Directory 사이트 내에 있으면 스마트 호스트 간에 인바운드 연결 부하가 분산됩니다.</p></td>
</tr>
</tbody>
</table>


자동으로 작성되는 인바운드 송신 커넥터에 대해 작성 시에 주소 공간이나 스마트 호스트 목록을 수정할 수는 없습니다. 그러나 Edge 구독을 만들 때 *CreateInboundSendConnector* 매개 변수의 값을 `$false`로 설정할 수는 있습니다. 그러면 Edge 전송 서버에서 Exchange 조직으로 연결되는 송신 커넥터를 수동으로 구성할 수 있습니다.

## 인터넷으로 메시지를 보내는 아웃바운드 송신 커넥터 자동 생성

기본적으로 사서함 서버에서 **New-EdgeSubscription** cmdlet을 실행하면 아웃바운드 송신 커넥터 매개 변수 *CreateInternetSendConnector*의 값이 `$true`로 설정됩니다. 그러면 인터넷으로 메시지를 보내는 데 필요한 송신 커넥터가 만들어집니다. 다음 표에서는 이 송신 커넥터의 기본 구성을 보여줍니다.

### 인터넷 송신 커넥터 자동 구성

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>속성</th>
<th>값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Name</em></p></td>
<td><p>EdgeSync - &lt;<em>사이트 이름</em>&gt; to Internet</p></td>
</tr>
<tr class="even">
<td><p><em>AddressSpaces</em></p></td>
<td><p><code>SMTP:*;100</code></p></td>
</tr>
<tr class="odd">
<td><p><em>SourceTransportServers</em></p></td>
<td><p>&lt;<em>Edge 구독 이름</em>&gt;</p>

> [!NOTE]
> Edge 구독의 이름은 가입된 Edge 전송 서버의 이름과 같습니다.


</td>
</tr>
<tr class="even">
<td><p><em>Enabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="odd">
<td><p><em>DNSRoutingEnabled</em></p></td>
<td><p>True</p></td>
</tr>
<tr class="even">
<td><p><em>DomainSecureEnabled</em></p></td>
<td><p>True</p></td>
</tr>
</tbody>
</table>


둘 이상의 Edge 전송 서버가 동일한 Active Directory 사이트에 구독되면 추가적인 인터넷 송신 커넥터가 만들어지지 않습니다. 대신 모든 Edge 구독이 원본 서버와 동일한 송신 커넥터에 추가됩니다. 그러면 구독된 Edge 전송 서버 간에 인터넷으로의 아웃바운드 연결 부하가 분산됩니다.

아웃바운드 송신 커넥터는 Exchange 조직에서 모든 원격 SMTP 도메인으로 전자 메일 메시지를 보내도록 구성되며, DNS 라우팅을 사용하여 MX 리소스 레코드에 대해 도메인 이름을 확인합니다. 커넥터의 구성을 수동으로 구성하는 방법에 대한 자세한 내용은 [Edge 전송 서버 메일 흐름 수동 구성](manually-configure-edge-transport-server-mail-flow-exchange-2013-help.md)을 참조하세요.

## Microsoft Exchange EdgeSync 서비스

Edge 전송 서버를 Active Directory 사이트에 구독하고 나면 EdgeSync에서 구성 및 받는 사람 데이터를 Edge 전송 서버에 복제합니다. 이 서비스는 다음 데이터를 Active Directory에서 AD LDS로 복제합니다.

  - 송신 커넥터 구성

  - 허용 도메인

  - 원격 도메인

  - 메시지 분류

  - 수신 허용 - 보낸 사람 목록

  - 수신 거부 목록

  - 받는 사람

  - 파트너와의 도메인 보안 통신에 사용되는 송신 및 수신 도메인 목록

  - 조직의 전송 구성에서 내부 서버로 나열되는 SMTP 서버의 목록

  - 구독된 Active Directory 사이트의 사서함 서버 목록

AD LDS로 복제되는 데이터와 그 사용 방법에 대한 자세한 내용은 [EdgeSync 복제 데이터](edgesync-replication-data-exchange-2013-help.md)를 참조하세요.

EdgeSync는 상호 인증되었으며 권한이 부여된 보안 LDAP 채널을 사용하여 사서함 서버에서 Edge 전송 서버로 데이터를 전송합니다.

AD LDS으로 데이터를 복제하기 위해 사서함 서버는 글로벌 카탈로그 서버를 바인딩하여 업데이트된 데이터를 검색합니다. EdgeSync 서비스는 비표준 TCP 포트 50636을 통해 사서함 서버와 구독된 Edge 전송 서버 사이에 보안 LDAP 세션을 시작합니다.

Edge 전송 서버를 Active Directory 사이트에 처음 구독하면 디렉터리 서비스에 있는 데이터의 양에 따라 AD LDS에 Active Directory의 데이터를 입력하는 초기 복제가 5분 이상 걸릴 수 있습니다. 초기 복제 이후 EdgeSync는 새 개체와 변경된 개체만 동기화하며 삭제된 개체는 제거합니다.

## 동기화 일정

각 일정에서는 서로 다른 형식의 데이터가 동기화됩니다. EdgeSync 동기화 일정은 EdgeSync 동기화 간의 최대 간격을 지정합니다. EdgeSync 동기화는 다음과 같은 간격으로 수행됩니다.

  - 구성 데이터: 3분

  - 받는 사람 데이터: 5분

  - 토폴로지 데이터: 5분

이러한 간격을 변경하려면 **Set-EdgeSyncServiceConfig** cmdlet을 사용합니다. 사서함 서버에서 **Start-EdgeSynchronization** cmdlet을 사용하여 Edge 구독 동기화를 강제로 수행하면 예약된 다음 EdgeSync 동기화의 타이머가 재정의되고 EdgeSync가 즉시 시작됩니다.

## 사서함 서버 선택

구독된 각 Edge 전송 서버는 특정 Active Directory 사이트와 연결됩니다. 해당 사이트에 여러 개의 사서함 서버가 있는 경우 어떤 사서함 서버에서나 구독된 Edge 전송 서버로 데이터를 복제할 수 있습니다. 동기화가 수행될 때 사서함 서버 간의 경합을 방지하기 위해 다음과 같이 기본 설정 사서함 서버가 선택됩니다.

1.  토폴로지 검색을 수행하고 새 Edge 구독을 검색하는 Active Directory 사이트의 첫 번째 사서함 서버에서 초기 복제가 수행됩니다. 이 검색 작업은 토폴로지 검색 시간을 기반으로 수행하므로 사이트에 있는 모든 사서함 서버에서 초기 복제를 수행할 수 있습니다.

2.  초기 복제를 수행하는 사서함 서버가 EdgeSync 임대 옵션을 설정하고 Edge 구독에 대해 잠금을 설정합니다. 임대 옵션은 해당 사서함 서버를 Edge 전송 서버에 대해 동기화 서비스를 제공하는 기본 설정 서버로 지정합니다. 이 잠금 설정은 다른 사서함 서버에서 실행되는 EdgeSync가 임대 옵션을 소유하지 못하도록 합니다.

3.  EdgeSync 임대 옵션은 한 시간 동안 지속됩니다. 해당 시간이 종료되기 전에 수동 동기화를 시작하는 경우가 아니면 이 시간 동안에는 다른 EdgeSync 서비스가 임대 옵션을 소유할 수 없습니다. 수동 동기화를 시작할 때 기본 사서함 서버에서 EdgeSync 서비스를 제공할 수 없는 경우 5분 동안 대기한 다음 잠금이 해제되며, 그러면 다른 EdgeSync 서비스에서 임대 옵션을 소유하여 동기화를 수행할 수 있습니다.

4.  수동 동기화를 시작하는 경우가 아니면 EdgeSync 동기화 일정에 따라 동기화가 수행됩니다. 예약된 동기화가 수행될 때 기본 설정 서버를 사용할 수 없는 경우 5분 동안 대기한 다음 잠금이 해제되며, 그러면 다른 EdgeSync 서비스가 임대 옵션을 소유하여 동기화를 수행할 수 있습니다.

이러한 잠금 및 임대 방식을 사용하면 여러 EdgeSync 인스턴스가 데이터를 동시에 같은 Edge 전송 서버로 전달하지 못하도록 할 수 있습니다.


> [!NOTE]
> 구독된 Active Directory 서비스에 Exchange 2010 또는 Exchange 2007 사서함 서버도 있는 경우에는 Exchange 2013 사서함 서버가 항상 우선적으로 사용되며 복제를 수행합니다.




> [!NOTE]
> Edge 전송 서버를 Active Directory 사이트에 구독하면 구독 시 해당 Active Directory 사이트에 설치되어 있는 모든 사서함 서버가 EdgeSync 동기화 프로세스에 참여할 수 있습니다. 이 서버 중 하나를 제거하면 나머지 사서함 서버에서 실행 중인 EdgeSync 서비스에서 데이터 동기화 프로세스를 계속 진행합니다. 그러나 나중에 Active Directory 사이트에 새로 설치하는 사서함 서버는 EdgeSync 동기화에 자동으로 참여하지 않습니다. 이러한 새 사서함 서버가 EdgeSync 동기화에 참여하도록 하려면 Edge 전송 서버를 다시 구독해야 합니다.



다음 표에는 잠금 및 임대와 관련된 EdgeSync 속성이 나와 있습니다. **Set-EdgeSyncServiceConfig** cmdlet을 사용하여 이러한 속성을 구성합니다.

### EdgeSync 임대 속성

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>기본값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>LockDuration</em></p></td>
<td><p><code>00:05:00</code>(5분)</p></td>
<td><p>이 설정은 특정 EdgeSync 서비스가 잠금을 획득한 상태를 유지하는 시간을 결정합니다. 이 잠금을 획득한 사서함 서버의 EdgeSync 서비스가 응답하지 않으면 다른 사서함 서버의 EdgeSync 서비스가 5분 후에 임대 옵션을 소유하게 됩니다. EdgeSync 동기화를 즉시 강제로 실행해도 이 설정은 재정의되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>OptionDuration</em></p></td>
<td><p><code>01:00:00</code>(1시간)</p></td>
<td><p>이 설정은 EdgeSync 서비스가 Edge 전송 서버에서 임대 옵션을 선언한 상태를 유지할 수 있는 시간을 결정합니다. 임대 옵션을 소유한 EdgeSync 서비스를 사용할 수 없으며 이 옵션 기간 동안 서비스가 다시 시작되지 않아도 EdgeSync 동기화를 강제로 수행하는 경우가 아니면 다른 Exchange EdgeSync 서비스가 임대 옵션을 소유하지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>LockRenewalDuration</em></p></td>
<td><p><code>00:01:00</code>(1분)</p></td>
<td><p>이 설정은 EdgeSync 서비스가 Edge 전송 서버에 대한 잠금을 획득한 경우 잠금 필드가 업데이트되는 빈도를 결정합니다.</p></td>
</tr>
</tbody>
</table>


## EdgeSync 서비스 실행 준비

Edge 전송 서버를 Exchange 조직에 구독하려면 먼저 인프라 및 사서함 서버가 EdgeSync 서비스에 맞게 준비되어 있는지 확인해야 합니다. EdgeSync 동기화를 준비하려면 다음을 수행해야 합니다.

  - Edge 전송 서버와 Exchange 조직을 분리하는 경계 네트워크 방화벽이 올바른 포트를 통해 통신할 수 있도록 구성되어 있는지 확인합니다. Edge 전송 서버는 비표준 LDAP 포트를 사용합니다. 환경에서 특정 포트를 사용해야 하는 경우에는 Exchange에서 제공하는 ConfigureAdam.ps1 스크립트를 사용하여 AD LDS에 사용되는 포트를 수정할 수 있습니다. 자세한 내용은 [AD LDS 구성 수정](modify-ad-lds-configuration-exchange-2013-help.md)를 참조하십시오. Edge 구독을 만들기 전에 포트를 수정합니다. Edge 구독을 만든 후에 포트를 수정하는 경우에는 Edge 구독을 제거한 다음 새 Edge 구독을 만들어야 합니다. 기본적으로 다음 LDAP 포트를 사용하여 AD LDS에 액세스합니다.
    
      - **LDAP   **AD LDS 인스턴스에 바인딩하기 위해 포트 50389/TCP가 로컬로 사용됩니다. 경계 네트워크 방화벽에서는 이 포트를 열 필요가 없습니다.
    
      - **보안 LDAP**   사서함 서버에서 AD LDS로 디렉터리를 동기화하는 데 포트 50636/TCP를 사용합니다. EdgeSync 동기화에 성공하려면 방화벽에서 이 포트를 열어야 합니다.

  - Edge 전송 서버에서 사서함 서버로, 그리고 사서함 서버에서 Edge 전송 서버로의 DNS 호스트 이름 확인이 수행되는지 확인합니다.

  - Edge 전송 서버의 사용을 허가합니다. Edge 구독을 만들 때 Edge 전송 서버에 대한 라이선스 정보가 캡처됩니다. 라이선스 키를 Edge 전송 서버에 적용한 후 구독된 Edge 전송 서버를 Exchange 조직에 구독해야 합니다. Edge 구독 프로세스를 수행한 후 라이선스 키를 Edge 전송 서버에 적용하는 경우에는 Exchange 조직에서 라이선스 정보가 업데이트되지 않으므로 Edge 전송 서버를 다시 구독해야 합니다.

  - Edge 전송 서버 역할에 전파할 다음과 같은 전송 설정을 구성합니다.
    
      - **내부 SMTP 서버**   **Set-TransportConfig** cmdlet에서 *InternalSMTPServers* 매개 변수를 사용하여 Edge 전송 서버의 보낸 사람 ID 및 연결 필터링 에이전트가 무시하도록 할 내부 SMTP 서버 IP 주소 또는 IP 주소 범위의 목록을 지정합니다.
    
      - **허용 도메인**   모든 트러스트할 수 있는 도메인, 내부 릴레이 도메인 및 외부 릴레이 도메인을 구성합니다.
    
      - **원격 도메인**   원격 도메인 설정을 구성합니다.

맨 위로 이동

## Edge 구독 관리

Edge 구독 관리 작업의 단계별 지침은 [Edge 구독 관리](manage-edge-subscriptions-exchange-2013-help.md)를 참조하세요.

