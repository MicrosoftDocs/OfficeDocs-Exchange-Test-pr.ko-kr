---
title: 'EdgeSync를 사용 하지 않고 Edge 전송 서버를 통해 인터넷 메일 흐름 구성: Exchange 2013 Help'
TOCTitle: EdgeSync를 사용 하지 않고 Edge 전송 서버를 통해 인터넷 메일 흐름 구성
ms:assetid: 6bb98d10-6f12-4b08-a58e-36375f605d65
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232082(v=EXCHG.150)
ms:contentKeyID: 61183424
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# EdgeSync를 사용 하지 않고 Edge 전송 서버를 통해 인터넷 메일 흐름 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-01-23_

Edge 구독 프로세스를 사용하여 Exchange 조직과 Edge 전송 서버 간의 메일 흐름을 설정하는 것이 좋습니다. 그러나 Edge 구독 프로세스를 사용하여 Exchange 조직에 Edge 전송 서버를 구독할 수 없는 상황도 있습니다. Exchange 조직과 Edge 전송 서버 간의 메일 흐름을 수동으로 설정하려면 Exchange 조직의 Edge 전송 서버와 사서함 서버에서 송신 커넥터와 수신 커넥터를 만들고 구성해야 합니다.

## 시작하기 전에

  - 이 작업의 예상 완료 시간: 30분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "송신 커넥터" 항목, "송신 커넥터 - Edge 전송" 항목 및 "수신 커넥터 - Edge 전송" 항목

  - 이 절차에서는 TLS(전송 계층 보안)를 통한 기본 인증을 사용하여 암호화 및 인증을 제공합니다. TLS를 통한 기본 인증을 사용할 경우 받는 서버에는 X.509 SSL(Secure Sockets Layer) 서버 인증서가 설치되어 있어야 합니다. 수신 커넥터에 구성된 FQDN(정규화된 도메인 이름) 값은 SSL 서버 인증서의 FQDN과 일치해야 합니다. 기본적으로 수신 커넥터의 FQDN 값은 수신 커넥터를 포함하는 서버의 FQDN입니다.

  - 외부 보안 인증 방법을 사용할 수도 있습니다. 그러나 이 경우 Edge 전송 서버와 사서함 서버 간의 통신은 Exchange에 의해 인증 또는 암호화되지 않습니다. 추가 암호화 방법도 사용하는 경우에만 외부 보안 인증 방법을 사용하는 것이 좋습니다. IPsec(인터넷 프로토콜 보안) 연결 또는 VPN(가상 사설망)을 암호화 방법으로 사용할 수 있습니다.

  - 일반적으로 Edge 전송 서버는 *멀티홈*입니다. 따라서 Edge 전송 서버에는 여러 네트워크 세그먼트에 연결된 네트워크 어댑터가 있습니다. 이러한 네트워크 어댑터마다 고유한 IP 구성을 가집니다. 외부 또는 공용 네트워크 세그먼트에 연결된 네트워크 어댑터는 이름 확인을 위해 공용 DNS(Domain Name System) 서버를 사용하도록 구성되어야 합니다. 이를 통해 서버는 MX 리소스 레코드에 대한 SMTP 도메인 이름을 확인하고 메일을 인터넷으로 라우트할 수 있습니다. 내부 또는 개인 네트워크 세그먼트에 연결된 네트워크 어댑터는 경계 네트워크의 DNS 서버를 사용하도록 구성하거나 호스트 파일을 사용할 수 있도록 해야 합니다.

  - Active Directory에서 사용자 계정을 만든 후 Exchange Server 컴퓨터의 유니버설 보안 그룹에 해당 계정을 추가해야 합니다. 이 계정은 Edge 전송 서버의 송신 커넥터에서 Exchange 조직의 대상 사서함 서버에 인증하는 데 사용합니다.
    

    > [!IMPORTANT]
    > 이 계정에는 Exchange Server를 실행하는 컴퓨터에 연결된 사용 권한이 부여됩니다. 계정이 오용되지 않도록 계정 자격 증명을 보호해야 합니다. 특정 컴퓨터에만 로그온할 수 있도록 계정을 구성할 수 있습니다.



## Edge 전송 서버 절차

Edge 전송 서버에 필요한 커넥터는 다음과 같습니다.

  - 인터넷으로 메시지를 보내도록 구성된 송신 커넥터

  - Exchange 조직의 사서함 서버로 메시지를 보내도록 구성된 송신 커넥터

  - Exchange 조직의 사서함 서버로부터만 메시지를 받도록 구성된 수신 커넥터

  - 인터넷에서 받은 메시지만 수락하도록 구성된 수신 커넥터

기본적으로 단일 수신 커넥터는 Edge 전송 서버 역할을 설치하는 동안 만들어집니다. 이 커넥터는 인터넷에서 받는 메시지와 사서함 서버에서 받는 메시지 둘 다에 사용할 수 있습니다. 일반적으로 Edge 구독 프로세스는 기본 수신 커넥터에서 올바른 사용 권한 및 인증을 자동으로 구성합니다. Edge 구독 프로세스를 사용하지 않을 경우 Edge 전송 서버의 기본 수신 커넥터가 인터넷의 메시지만 수락하도록 수정하는 것이 좋습니다. 그런 다음 내부 사서함 서버의 메시지만 수락하도록 구성된 수신 커넥터를 Edge 전송 서버에 만들어야 합니다.

다음 섹션에서는 Exchange 조직과 통신하도록 Edge 전송 서버를 준비하는 데 필요한 모든 구성 단계를 설명합니다.


> [!NOTE]
> Edge 전송 서버에서 다음 절차를 수행하려면 셸을 사용해야 합니다.



## 1단계: 인터넷으로 메시지를 보내도록 구성된 송신 커넥터 만들기

이 송신 커넥터에는 다음 구성이 필요합니다.

  - **이름**   To Internet 또는 커넥터를 설명하는 이름

  - **사용 유형**   인터넷

  - **주소 공간**   "\*"(모든 도메인)

  - **네트워크 설정**   DNS MX 레코드를 사용하여 메일을 자동으로 라우팅 네트워크 구성에 따라 스마트 호스트를 통해 메일을 라우팅할 수도 있습니다. 그러면 스마트 호스트에서 메일을 인터넷으로 라우팅합니다.

인터넷으로 메시지를 보내도록 구성된 송신 커넥터를 만들려면 다음 명령을 실행합니다.

    New-SendConnector -Name "To Internet" -AddressSpaces * -Usage Internet -DNSRoutingEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [New-SendConnector](https://technet.microsoft.com/ko-kr/library/aa998936\(v=exchg.150\))를 참조하십시오.

## 2단계: Exchange 조직에 메시지를 보내도록 구성된 송신 커넥터 만들기

송신 커넥터를 만들려면 **New-SendConnector** cmdlet을 사용합니다.


> [!NOTE]
> 송신 커넥터를 만들기 전에 먼저 <STRONG>Get-Credential</STRONG> 명령을 실행하여 임시 변수에 사용할 사용자 이름과 암호를 저장해야 합니다. <STRONG>New-SendConnector</STRONG> cmdlet에서는 일반 텍스트로 된 사용자 자격 증명을 사용할 수 없으므로 이 작업을 수행해야 합니다.



이 송신 커넥터에는 다음 구성이 필요합니다.

  - **Name**   To Internal Org 또는 커넥터를 설명하는 이름

  - **사용 유형**   내부

  - **주소 공간**   Exchange 조직에 대한 모든 허용 도메인(예: \*.contoso.com)

  - DNS 라우팅 사용 안 함(스마트 호스트 라우팅 사용)

  - **스마트 호스트**   스마트 호스트로 사용할 사서함 서버 하나 이상의 FQDN(예: mbxserver01.contoso.com 및 mbxserver02.contoso.com)

  - **스마트 호스트 인증 방법**   TLS 통한 기본 인증

  - **스마트 호스트 인증 자격 증명**   내부 도메인의 사용자 계정용 자격 증명. **New-SendConnector** cmdlet에서는 일반 텍스트로 된 사용자 자격 증명을 사용할 수 없으므로 먼저 사용자 이름과 암호를 임시 변수에 저장해야 합니다.

Exchange 조직에 메시지를 보내도록 구성된 송신 커넥터를 만들려면 다음 명령을 실행합니다.

    $MailboxCredentials = Get-Credential
    New-SendConnector -Name "To Internal Org" -Usage Internal -AddressSpaces *.contoso.com -DNSRoutingEnabled $false -SmartHosts mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $MailboxCredentials

구문과 매개 변수에 대한 자세한 내용은 [New-SendConnector](https://technet.microsoft.com/ko-kr/library/aa998936\(v=exchg.150\))를 참조하세요.

## 3단계: 기본 수신 커넥터를 인터넷에서 받은 메시지만 수락하도록 수정

기본 수신 커넥터 구성을 다음과 같이 변경해야 합니다.

  - 커넥터가 인터넷에서 전자 메일을 받는 데만 사용됨을 반영하도록 이름을 수정합니다. 기본 수신 커넥터의 이름은 "기본 내부 수신 커넥터 \<Edge 전송 서버 이름\>"입니다.

  - 인터넷에서 액세스할 수 있는 네트워크 어댑터의 메시지만 수락하도록 네트워크 바인딩을 변경합니다. 예를 들어 10.1.1.1 및 표준 SMTP TCP 포트 값인 25를 사용할 수 있습니다.

인터넷의 메시지만 수락하도록 기본 수신 커넥터를 수정하려면 다음 명령을 실행합니다.

    Set-ReceiveConnector "Default internal Receive connector Edge01" -Name "From Internet" -Bindings 10.1.1.1:25

구문과 매개 변수에 대한 자세한 내용은 [Set-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125140\(v=exchg.150\))를 참조하십시오.

## 4단계: Exchange 조직에서 받은 메시지만 수락하도록 구성된 수신 커넥터 만들기

이 수신 커넥터에는 다음 구성이 필요합니다.

  - **Name**   From Internal Org 또는 커넥터를 설명하는 이름

  - **사용 유형**   내부

  - **로컬 네트워크 바인딩**   내부 네트워크 연결 네트워크 어댑터(예: 10.1.1.2 및 표준 SMTP TCP 포트 값 25)

  - **원격 네트워크 설정**   Exchange 조직에 있는 사서함 서버 하나 이상의 IP 주소(예: 192.168.5.10 및 192.168.5.20)

  - **인증 방법**   TLS, 기본 인증, TLS를 통한 기본 인증 및 Exchange Server 인증

Exchange 조직의 메시지만 수락하도록 구성된 수신 커넥터를 만들려면 다음 명령을 실행합니다.

    New-ReceiveConnector -Name "From Internal Org" -Usage Internal -AuthMechanism TLS,BasicAuth,BasicAuthRequireTLS,ExchangeServer -Bindings 10.1.1.2:25 -RemoteIPRanges 192.168.5.10,192.168.5.20

구문과 매개 변수에 대한 자세한 내용은 [New-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125139\(v=exchg.150\))를 참조하십시오.

## 단계를 정상적으로 수행했는지 확인하는 방법

필요한 송신 커넥터와 수신 커넥터를 정상적으로 구성했는지 확인하려면 Edge 전송 서버에서 다음 명령을 실행하여 구성한 값이 제대로 표시되는지 확인합니다.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,SourceTransportServers,DSNRoutingEnabled,SmartHosts,SmartHostAuthMechanism
    Get-ReceiveConnector | Format-List Name,Usage,AuthMechanism,Bindings,RemoteIPRanges

## 사서함 서버 절차

조직의 사서함 서버에는 인터넷으로 릴레이하기 위해 Edge 전송 서버로 메시지를 보내도록 구성된 송신 커넥터가 필요합니다.

기본적으로 사서함 서버 역할을 설치하는 동안 두 개의 수신 커넥터가 만들어집니다. 이름이 Client *서버 이름*인 커넥터는 모든 POP3 및 IMAP 메시징 클라이언트의 메시지를 수락하도록 구성되며 Default *서버 이름* 커넥터는 Edge 전송 서버의 메시지를 수락하도록 구성됩니다. 이러한 커넥터를 수정할 필요는 없습니다.

## 5단계: 보내는 메시지를 Edge 전송 서버로 보내도록 구성된 송신 커넥터 만들기

이 송신 커넥터에는 다음 구성이 필요합니다.

  - **이름**   To Edge 또는 커넥터를 설명하는 이름

  - **사용 유형**   내부

  - **주소 공간**   "\*"(모든 도메인)

  - DNS 라우팅 사용 안 함(스마트 호스트 라우팅 사용)

  - **Smart hosts**   Edge 전송 서버의 IP 주소 또는 FQDN(예: edge01.contoso.net)

  - **원본 사서함 서버**   사서함 서버 하나 이상의 FQDN(예: mbxserver01.contoso.com 및 mbxserver02.contoso.com)

  - **스마트 호스트 인증 방법**   TLS 통한 기본 인증 합니다.

  - **스마트 호스트 인증 자격 증명**   Edge 전송 서버에 있는 사용자 계정의 자격 증명. **New-SendConnector** cmdlet에서는 일반 텍스트로 된 사용자 자격 증명을 사용할 수 없으므로 먼저 사용자 이름과 암호를 임시 변수에 저장해야 합니다.

Edge 전송 서버로 보내는 메시지를 보내도록 구성된 송신 커넥터를 만들려면 다음 명령을 실행합니다.

    $EdgeCredentials = Get-Credential
    New-SendConnector -Name "To Edge" -Usage Internal -AddressSpaces * -DNSRoutingEnabled $false -SmartHosts edge01.contoso.com -SourceTransportServers mbxserver01.contoso.com,mbxserver02.contoso.com -SmartHostAuthMechanism BasicAuthRequireTLS -AuthenticationCredential $EdgeCredentials

구문과 매개 변수에 대한 자세한 내용은 [New-SendConnector](https://technet.microsoft.com/ko-kr/library/aa998936\(v=exchg.150\))를 참조하세요.

## 이 단계의 작동 여부는 어떻게 확인합니까?

Edge 전송 서버로 보내는 메시지를 보내도록 구성된 송신 커넥터를 정상적으로 만들었는지 확인하려면 사서함 서버에서 다음 명령을 실행하여 구성한 값이 제대로 표시되는지 확인합니다.

    Get-SendConnector | Format-List Name,Usage,AddressSpaces,DSNRoutingEnabled,SmartHosts,SourceTransportServers,SmartHostAuthMechanism

