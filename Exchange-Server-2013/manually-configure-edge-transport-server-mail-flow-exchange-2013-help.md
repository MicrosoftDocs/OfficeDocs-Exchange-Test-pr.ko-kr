---
title: 'Edge 전송 서버 메일 흐름 수동 구성: Exchange 2013 Help'
TOCTitle: Edge 전송 서버 메일 흐름 수동 구성
ms:assetid: cb4cc165-6c09-44ab-a95f-167ae8ed2485
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn606261(v=EXCHG.150)
ms:contentKeyID: 61183429
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버 메일 흐름 수동 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-02-21_

이 항목에서는 Edge 전송 서버에서 메일 흐름을 관리하는 방법과 관련한 구성을 수동으로 변경하는 절차에 대해 설명합니다. 이러한 절차는 특정 시나리오에 사용하기 위한 것입니다. 조직에서 구성을 반드시 수동으로 변경해야 하는 경우가 아니면 Edge 전송 서버 구독 시 기본 구성을 사용하는 것이 좋습니다.

**목차**

Manually configure Send connectors

Intra-Organization Send Connectors

Create additional Send connectors after Edge subscription

Reasons to suppress automatic creation of Send connectors

Partition mail flow

Route outbound email to a smart host

Configure Send connectors for external relay domains

## 송신 커넥터 수동 구성

송신 커넥터의 구성을 수동으로 수정할 수 있습니다. 예를 들어 스마트 호스트를 통해 아웃바운드 전자 메일을 라우팅해야 하는 경우 송신 커넥터가 자동으로 만들어지지 않도록 하고 인터넷으로의 송신 커넥터를 수동으로 구성할 수 있습니다.

## 조직 내 송신 커넥터

조직 내 송신 커넥터는 Exchange에 의해 자동으로 계산되며 같은 조직에 있는 사서함 서버의 전송 서비스가 명시적인 송신 커넥터를 사용하지 않고도 서로 메시지를 릴레이할 수 있도록 하는 암시적이며 숨겨진 송신 커넥터입니다. Active Directory 사이트와 연결된 구성 개체가 Edge 구독의 Active Directory에 있으므로 해당 Edge 전송 서버로 메시지를 릴레이하는 경우에도 조직 내 송신 커넥터가 사용됩니다.

구독된 Active Directory 사이트에 있는 사서함 서버만 구독된 Edge 전송 서버로 또는 Edge 전송 서버에서 전자 메일을 직접 전송할 수 있습니다. 다중 사이트 Active Directory 포리스트가 있고 둘 이상의 사이트에 Exchange가 배포되어 있으면 구독되지 않은 사이트의 사서함 서버는 구독된 사이트로 아웃바운드 전자 메일을 라우팅합니다. 구독된 사이트의 사서함 서버는 아웃바운드 전자 메일을 Edge 전송 서버로 라우팅합니다.

## Edge 구독 후 추가 송신 커넥터 만들기

Edge 전송 서버가 Active Directory 사이트에 구독되면 Edge 전송 서버에서 송신 커넥터를 만들거나 수정하는 데 사용되는 cmdlet을 사용할 수 없습니다. Edge 전송 서버가 원본 서버인 송신 커넥터를 만들려면 Exchange 조직 내에서 송신 커넥터를 만들면 됩니다. 송신 커넥터의 원본 서버로 하나 이상의 Edge 구독을 지정할 수 있습니다. 같은 송신 커넥터의 원본 서버로 사서함 서버와 Edge 구독을 모두 지정할 수는 없습니다. EdgeSync에서 다음에 구성 데이터를 동기화할 때 원본 서버로 구성된 Edge 전송 서버의 AD LDS 인스턴스로 송신 커넥터가 복제됩니다. 둘 이상의 Edge 구독을 원본 서버로 지정한 경우 구독된 Edge 전송 서버 간의 해당 송신 커넥터로의 연결 부하가 분산됩니다. 부하가 분산되려면 Edge 전송 서버가 동일한 Active Directory 사이트에 구독되어 있어야 합니다. 각기 다른 Active Directory 사이트의 Edge 구독이 동일한 송신 커넥터에서 원본 서버로 구성되면 Edge 전송 서버는 가장 가까운 원본 서버로만 라우팅됩니다.

다음과 같은 경우 송신 커넥터를 수동으로 만들어야 합니다.

  - 인터넷 또는 인바운드 송신 커넥터가 자동으로 만들어지지 않도록 설정한 경우

  - 외부 릴레이 도메인으로 구성된 허용 도메인이 조직에 있는 경우

## 송신 커넥터가 자동으로 만들어지지 않도록 설정하는 이유

Exchange 조직의 토폴로지에 따라 송신 커넥터가 자동으로 만들어지지 않도록 설정할 수 있습니다. 다음 예에서는 송신 커넥터가 자동으로 만들어지지 않도록 설정해야 하는 시나리오에 대해 설명합니다.

## 메일 흐름 분할

두 Edge 전송 서버 간에 인바운드 및 아웃바운드 메일 처리를 분할하는 경우 Edge 전송 서버 하나는 아웃바운드 메일 흐름을 처리하고 두 번째 Edge 전송 서버는 인바운드 메일 흐름을 처리합니다. 이처럼 메일 흐름을 분할하려면 Edge 구독을 다음과 같이 구성합니다.

  - 아웃바운드 Edge 전송 서버의 경우 사서함 서버에서 다음 명령을 실행합니다.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $false -CreateInternetSendConnector $true

  - 인바운드 Edge 전송 서버의 경우 사서함 서버에서 다음 명령을 실행합니다.
    
        New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInboundSendConnector $true -CreateInternetSendConnector $false

## 스마트 호스트로 아웃바운드 전자 메일 라우팅

Exchange 조직이 모든 아웃바운드 전자 메일을 스마트 호스트를 통해 라우팅할 경우 자동으로 만들어진 송신 커넥터가 올바르게 구성되지 않습니다.

인터넷 송신 커넥터를 자동으로 만들지 않도록 설정하려면 사서함 서버에서 다음 명령을 실행합니다.

    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "C:\EdgeServerSubscription.xml" -Encoding Byte -ReadCount 0)) -Site "Site-A" -CreateInternetSendConnector $false

Edge 구독 프로세스가 완료되면 인터넷 송신 커넥터를 수동으로 만듭니다. Exchange 조직 내에서 송신 커넥터를 만든 후 커넥터의 원본 서버로 Edge 구독을 선택합니다. `Custom` 사용 유형을 선택하고 하나 이상의 스마트 호스트를 구성합니다. 새 송신 커넥터는 다음에 EdgeSync가 구성 데이터를 동기화할 때 Edge 전송 서버의 AD LDS 인스턴스로 복제됩니다. 사서함 서버에서 **Start-EdgeSynchronization** cmdlet을 실행하여 EdgeSync 동기화를 즉시 강제로 시작할 수 있습니다.

예: 셸을 사용하여 구독된 Edge 전송 서버의 송신 커넥터가 스마트 호스트를 통해 모든 인터넷 주소 공간으로의 메시지를 라우팅하도록 구성합니다. Edge 전송 서버가 아닌 Exchange 조직 내의 사서함 서버에 대해 이 작업을 실행합니다.

    New-SendConnector -Name "EdgeSync - Site-A to Internet" -Usage Custom -AddressSpaces SMTP:*;100 -DNSRoutingEnabled $false -SmartHosts 192.168.10.1 -SmartHostAuthMechanism None -SourceTransportServers EdgeSubscriptionName


> [!IMPORTANT]
> 이 예에서는 스마트 호스트 인증 메커니즘을 지정하지 않습니다. 따라서 사용자 Exchange 조직에서 실제로 스마트 호스트 커넥터를 만들 때 올바른 인증 메커니즘을 구성하고 필요한 모든 자격 증명을 제공해야 합니다.



## 외부 릴레이 도메인용 송신 커넥터 구성

Exchange 조직에 외부 릴레이 도메인으로 구성된 허용 도메인이 있는 경우 해당 주소 공간의 송신 커넥터를 수동으로 만들어야 합니다. 외부 릴레이 도메인으로 전달되는 메시지는 Edge 전송 서버에 의해 릴레이됩니다. Edge 구독 프로세스는 외부 릴레이 도메인 송신 커넥터를 자동으로 만들고 구성하지 않습니다. 따라서 해당 도메인에 대해 송신 커넥터를 구성하고 하나 이상의 Edge 구독을 해당 송신 커넥터의 원본 서버로 지정해야 합니다.

외부 릴레이 도메인의 DNS MX 리소스 레코드는 Edge 전송 서버로 해석됩니다. 전자 메일을 외부 릴레이 도메인으로 릴레이하는 송신 커넥터가 라우팅에 스마트 호스트를 사용하도록 구성할 수 있습니다. 외부 릴레이 도메인용 송신 커넥터가 DNS 라우팅을 사용하도록 구성하면 라우팅 루프가 발생합니다. 외부 릴레이 도메인에 대한 자세한 내용은 [허용 도메인](accepted-domains-exchange-2013-help.md)를 참조하세요.

맨 위로 이동

