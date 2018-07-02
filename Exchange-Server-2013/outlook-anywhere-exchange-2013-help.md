---
title: 'Outlook Anywhere: Exchange 2013 Help'
TOCTitle: Outlook Anywhere
ms:assetid: 9026d461-ec6a-4ef5-ba9d-de33030858f3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123741(v=EXCHG.150)
ms:contentKeyID: 50483642
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Outlook Anywhere

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 Outlook Anywhere 기능(이전의 RPC over HTTP)은 MicrosoftOutlook 2013, Outlook 2010 또는 Outlook 2007을 사용하는 클라이언트가 회사 네트워크의 외부에서, 또는 RPC over HTTP Windows 네트워킹 구성 요소를 사용하여 인터넷을 통해 Exchange 서버에 연결할 수 있게 해줍니다. 이 항목에서는 Outlook Anywhere 기능 및 Outlook Anywhere를 사용하는 경우의 이점에 대해 설명합니다.

**목차**

Outlook Anywhere 및 Exchange 2013

Outlook Anywhere 사용을 통해 얻을 수 있는 이점

Outlook Anywhere 배포

Outlook Anywhere 관리

Outlook Anywhere 동시 사용

Outlook Anywhere 연결 테스트

## Outlook Anywhere 및 Exchange 2013

Outlook Anywhere 클라이언트가 연결하기 위해 사용하는 Windows RPC over HTTP 프록시 구성 요소는 HTTP 계층으로 RPC(원격 프로시저 호출)를 래핑합니다. 이렇게 하면 RPC 포트를 열지 않아도 트래픽이 네트워크 방화벽을 트래버스할 수 있습니다. Exchange 2013은 직접 RPC 연결을 허용하지 않으므로 Exchange 2013에서는 이 기능이 기본적으로 사용되도록 설정되어 있습니다.

## Outlook Anywhere 사용을 통해 얻을 수 있는 이점

Outlook Anywhere는 Outlook 2013, Outlook 2010 또는 Outlook 2007을 사용하여 Exchange 메시징 인프라에 액세스하는 고객에게 다음과 같은 이점을 제공합니다.

  - 사용자가 인터넷에서 Exchange 서버에 원격으로 액세스할 수 있습니다.

  - Outlook Web App 및 MicrosoftExchange ActiveSync에 사용하는 동일한 URL 및 네임스페이스를 사용할 수 있습니다.

  - Outlook Web App 및 Exchange ActiveSync에 모두 사용하는 동일한 SSL(Secure Sockets Layer) 서버 인증서를 사용할 수 있습니다.

  - Outlook에서 인증되지 않은 요청은 Exchange 서버에 액세스할 수 없습니다.

  - 인터넷을 통해 Exchange 서버에 액세스하기 위해 VPN(가상 사설망)을 사용할 필요가 없습니다.

  - SSL이 적용된 Outlook Web App 또는 SSL이 적용된 Exchange ActiveSync를 이미 사용하고 있는 경우 인터넷에서 추가로 포트를 열 필요가 없습니다.

  - **Test-OutlookConnectivity** cmdlet을 사용하여 Outlook Anywhere 및 TCP 기반 연결에 대한 종단 간 클라이언트 연결을 테스트할 수 있습니다.

## Outlook Anywhere 배포

Exchange 2013에서는 모든 Outlook 연결이 "Outlook Anywhere 사용"을 통해 발생하므로 "Outlook Anywhere 사용"이 기본적으로 사용되도록 설정됩니다. Outlook Anywhere를 성공적으로 사용하기 위해 수행해야 하는 배포 후 작업으로는 클라이언트 액세스 서버에 유효한 SSL 인증서를 설치하기만 하면 됩니다. 조직의 사서함 서버에만 기본 자체 서명된 SSL 인증서가 필요합니다.

## Outlook Anywhere 관리

Exchange 관리 센터나 Exchange 관리 셸을 사용하여 Outlook Anywhere를 관리할 수 있습니다.

## Outlook Anywhere 동시 사용

동시 사용 시나리오에서 이전 버전의 Exchange Server와 함께 Exchange 2013을 설치하려면 조직에 Outlook 2003 클라이언트가 있어야 합니다. Exchange 2013에 대해 Outlook 2003은 지원되는 클라이언트가 아닙니다.

네임스페이스를 Exchange 2013으로 이동하기 전에 모든 Outlook 클라이언트가 지원되는 최소 버전으로 업그레이드되었는지 확인해야 합니다. Exchange 2013에 Outlook Anywhere를 연결하려면 Outlook 2007 이상이 필요합니다(대상 사서함이 Exchange 2007 또는 Exchange 2010에 있는 경우에도 마찬가지임).

현재 Exchange 2007 또는 2010 환경에서 Outlook Anywhere를 사용하는 경우 Exchange 2013 클라이언트 액세스 서버에서 Exchange 2007/2010 서버로 프록시 연결을 수행할 수 있게 하려면, 조직의 모든 Exchange 2007/2010 CAS에서 Outlook Anywhere를 사용하도록 설정하고 구성해야 합니다. 그렇지만 현재 Exchange 2007/2010 환경에서 Outlook Anywhere를 사용하고 있지 않으며 사용하지 않으려는 경우에는 기존 환경에서 Outlook Anywhere를 사용하도록 설정할 필요가 없습니다. Exchange Server 2007에서 실행되는 클라이언트 액세스 서버에 대해 Outlook Anywhere를 사용하도록 설정하기 위한 지침에 대해서는 [Outlook Anywhere를 사용하도록 설정하는 방법](https://go.microsoft.com/fwlink/p/?linkid=510497)을 참조하세요. Exchange Server 2010에서 실행되는 클라이언트 액세스 서버에 대해 Outlook Anywhere를 사용하도록 설정하기 위한 지침에 대해서는 [Outlook Anywhere 사용](https://go.microsoft.com/fwlink/p/?linkid=510502)을 참조하세요.

클라이언트 액세스 서버에서 Outlook Anywhere를 사용하도록 설정하는 경우 IIS 인증에 대해 NTLM을 선택해야 합니다.

마지막으로 Exchange 2013 Outlook Anywhere 호스트 이름을 가리키도록 Outlook Anywhere 외부 호스트 이름을 구성합니다. Exchange Server 2007에 대한 지침을 보려면 [Outlook Anywhere에 대해 외부 호스트 이름을 구성하는 방법](https://go.microsoft.com/fwlink/p/?linkid=510530)을 참조하세요. Exchange Server 2010에 대한 지침을 보려면 [Outlook Anywhere에 대해 외부 호스트 이름 구성](https://go.microsoft.com/fwlink/p/?linkid=510531)을 참조하세요.

## Outlook Anywhere 연결 테스트

다음 중 한 가지 방법으로 종단 간 클라이언트 Outlook 연결을 테스트할 수 있습니다.

  - **Test-OutlookConnectivity** cmdlet 실행. 이 cmdlet은 Outlook Anywhere(RPC over HTTP) 연결을 테스트합니다. 이 cmdlet 테스트가 실패하면 실패한 단계가 출력에 표시됩니다. 구문과 매개 변수에 대한 자세한 내용은 [Test-OutlookConnectivity](https://technet.microsoft.com/ko-kr/library/dd638082\(v=exchg.150\))를 참조하세요.

  - ExRCA(Exchange Remote Connectivity Analyzer)를 사용하여 Outlook Anywhere 연결 테스트를 실행. 이 테스트를 실행하면 어느 지점에서 테스트가 실패했는지, 그리고 문제 해결을 위해 어떤 단계를 수행해야 할지 알려주는 상세 요약이 반환됩니다. 자세한 내용은 [Exchange 원격 연결 분석기](exchange-remote-connectivity-analyzer-exchange-2013-help.md)를 참조하세요.

두 가지 테스트 모두 Autodiscover 서비스에서 서버 설정을 가져온 후 Outlook Anywhere를 통해 로그인을 시도합니다. 종단 간 확인에는 다음 내용이 포함됩니다.

  - 자동 검색 연결 테스트

  - DNS 확인

  - 인증서 확인(인증서 이름이 웬 사이트와 일치하는지, 인증서가 만료되었는지, 인증서를 신뢰할 수 있는지 여부)

  - 방화벽이 올바르게 설정되어 있는지 확인(ExRCA가 전반적인 방화벽 설정을 확인하고, 이 cmdlet이 Windows 방화벽 구성을 테스트합니다.)

  - 사용자의 사서함에 로그인하여 클라이언트 연결 확인

