---
title: 'Active Directory 사이트 간의 TLS를 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: Active Directory 사이트 간의 TLS를 사용 하지 않도록 설정
ms:assetid: 1e1a0acf-24e7-4f94-9b33-603a4e0a812c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876856(v=EXCHG.150)
ms:contentKeyID: 52058058
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 사이트 간의 TLS를 사용 하지 않도록 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2013-02-19_

Microsoft Exchange Server 2013에서는 SMTP 트래픽을 압축하는 WOC(WAN 최적화 컨트롤러) 장치가 사용되는 특정 토폴로지에서 사서함 서버 간의 SMTP 통신에 대해 TLS를 사용하지 않도록 설정할 수 있습니다.

이 항목에서는 TLS를 사용하지 않도록 해당하는 사서함 서버의 전송 서비스를 구성하는 방법과, Active Directory 라우팅 토폴로지가 메시지를 올바르게 라우팅하도록 구성되어 있는지 확인하는 방법에 대한 단계별 지침을 제공합니다. 이 시나리오에 대한 자세한 내용은 [시나리오: WAN 최적화 컨트롤러를 지원 하도록 Exchange 구성](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 60분

  - 이 시나리오의 개별 구성 단계는 더 적은 권한으로도 완료할 수 있지만, 전체 종단 간 시나리오 작업을 완료하려면 계정이 Organization Management 역할 그룹의 구성원이어야 합니다.

  - WOC 장치를 통과하는 연결에 대해서만 TLS를 사용하지 않도록 설정해야 합니다.

  - 이 절차를 수행하려면 Exchange 2013을 여러 Active Directory 사이트에 배포해야 하며, 하나 이상의 사이트가 WAN 링크를 통해 다른 사이트에 연결되어 있어야 합니다.

  - 이 절차를 수행하려면 WAN 링크를 통과하는 SMTP 트래픽을 압축하기 위한 WOC 장치를 배포해야 합니다.

  - 이 절차를 수행하려면 WOC 장치가 배포된 WAN 링크를 Exchange가 통과하기 위한 논리적 메시지 흐름 경로가 있어야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 1단계: 셸을 사용하여 다운그레이드된 Exchange Server 인증을 사용하도록 사서함 서버의 전송 서비스 구성

다운그레이드된 Exchange Server 인증을 사용하도록 사서함 서버의 전송 서비스를 구성하려면 다음 명령을 실행합니다.

    Set-TransportService <ServerIdentity> -UseDowngradedExchangeServerAuth $true

이 예에서는 Mailbox01이라는 서버에서 구성을 이와 같이 변경합니다.

    Set-TransportService Mailbox01 -UseDowngradedExchangeServerAuth $true

## 2단계: 대상 Active Directory 사이트에 대해 사서함 서버에서 전용 수신 커넥터 만들기

## EMC를 사용하여 수신 커넥터 만들기

1.  EAC(Exchange 관리 센터)에서 **메일 흐름** \> **수신 커넥터**를 클릭한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 수신 커넥터** 마법사의 첫 페이지에서 다음 값을 입력합니다.
    
      - **이름**   설명 값을 입력합니다.
    
      - **유형**   내부
    
    완료되면 **다음**을 클릭합니다.

3.  **새 수신 커넥터** 마법사의 두 번째 페이지에 있는 **원격 설정** 섹션에서 대상 Active Directory 사이트에 대한 IP 주소 또는 IP 주소 범위를 입력합니다. 작업을 마치면 **마침**을 클릭합니다.

## 셸을 사용하여 수신 커넥터 만들기

사서함 서버에서 수신 커넥터를 만들려면 다음 명령을 실행합니다.

    New-ReceiveConnector -Name <Name> -Server <ServerIdentity> -RemoteIPRanges <IPAddressRange> -Internal

이 예에서는 다음 설정을 사용하여 Mailbox01 서버에서 WAN이라는 수신 커넥터를 만듭니다.

  - *RemoteIPRanges* 매개 변수는 10.0.2.0/24로 설정됩니다. 이 IP 주소 범위는 해당 수신 커넥터가 암호화되지 않은 연결을 수신할 원격 Active Directory 사이트와 일치해야 합니다. 원격 사이트에 둘 이상의 IP 서브넷이 있는 경우 쉼표로 구분하여 모두를 입력할 수 있습니다.

  - 사용 유형을 내부로 설정합니다.

<!-- end list -->

    New-ReceiveConnector -Name WAN -Server Hub01 -RemoteIPRanges 10.0.2.0/24 -Internal

## 3단계: 셸을 사용하여 전용 수신 커넥터에 대해 TLS를 사용하지 않도록 설정

수신 커넥터에 대해 TLS를 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

    Set-ReceiveConnector <ReceiveConnectorIdentity> -SuppressXAnonymousTLS $true

이 예에서는 Mailbox01이라는 사서함 서버에서 WAN이라는 수신 커넥터에 대해 TLS를 사용하지 않도록 설정합니다.

    Set-ReceiveConnector Mailbox01\WAN -SuppressXAnonymousTLS $true

## 4단계: 셸을 사용하여 Active Directory 사이트를 허브 사이트로 지정

Active Directory 사이트를 허브 사이트로 지정하려면 다음 명령을 실행합니다.

    Set-AdSite <ADSiteIdentity> -HubSiteEnabled $true

암호화되지 않은 트래픽에 참가하는 사서함 서버가 포함된 각 Active Directory 사이트에서 이 절차를 한 번씩 수행해야 합니다.

이 예에서는 Central Office Site 1이라는 Active Directory 사이트를 허브 사이트로 구성합니다.

    Set-AdSite "Central Office Site 1" -HubSiteEnabled $true

## 5단계: 셸을 사용하여 WAN 연결을 통과하는 최저 비용 라우팅 경로 구성

Active Directory에서 IP 사이트 링크 비용을 구성하는 방법에 따라 이 단계를 수행하지 않아도 될 수 있습니다. WOC 장치가 배포된 네트워크 링크가 최저 비용 라우팅 경로에 있는지 확인해야 합니다. Active Directory 사이트 링크 비용 및 Exchange 관련 사이트 링크 비용을 확인하려면 다음 명령을 실행합니다.

    Get-AdSiteLink

WOC 장치가 배포된 네트워크 링크가 최저 비용 라우팅 경로에 있지 않으면 메시지가 올바르게 라우팅되도록 Exchange 관련 비용을 특정 IP 사이트 링크에 할당해야 합니다. 이 특정 문제에 대한 자세한 내용은 [시나리오: WAN 최적화 컨트롤러를 지원 하도록 Exchange 구성](scenario-configure-exchange-to-support-wan-optimization-controllers-exchange-2013-help.md)의 "Exchange 관련 Active Directory 사이트 링크 비용 구성" 섹션을 참조하십시오.

이 예에서는 Branch Office 2-Branch Office 1이라는 IP 사이트 링크에 대해 Exchange 관련 비용을 15로 구성합니다.

    Set-AdSiteLink "Branch Office 2-Branch Office 1" -ExchangeCost 15

