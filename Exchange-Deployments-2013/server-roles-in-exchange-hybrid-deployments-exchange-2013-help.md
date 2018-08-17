---
title: 'Exchange 하이브리드 배포에서의 서버 역할: Exchange 2013 Help'
TOCTitle: Exchange 하이브리드 배포에서의 서버 역할
ms:assetid: 7a7eaf17-d2b0-4d62-90a2-45a0d2faca54
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ659051(v=EXCHG.150)
ms:contentKeyID: 50484632
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 하이브리드 배포에서의 서버 역할

 

_<strong>적용 대상:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong>2016-12-09_

Exchange 2013 및 Exchange 2016에 따라 하이브리드 배포를 구성할 수 있습니다. 하이브리드 배포를 지원하도록 구성해야 하는 역할은 사용 중인 Exchange 버전에 따라 달라집니다.

## Exchange 2016 하이브리드 배포

Exchange 2016 조직에서 하이브리드 배포를 구성하는 경우 기존 Exchange 조직에 Exchange 서버를 추가로 설치할 필요가 없습니다. 사서함 서버는 기존의 Exchange 2016 조직과 Exchange Online 조직 사이의 통신을 조정합니다. 이 통신에는 온-프레미스 조직과 Exchange Online 조직 사이의 메시지 전송 및 메시징 기능이 포함됩니다. 온-프레미스 조직에 Exchange 서버를 둘 이상 설치하여 하이브리드 배포 기능의 안정성과 가용성을 높이는 것이 좋습니다.

Exchange 2016에는 필수 서버 역할인 사서함 역할만 있습니다. 사서함 역할은 온-프레미스 받는 사람 사서함을 호스트하는 것 외에, Exchange Online으로 하이브리드 배포를 지원하는 데 필요한 모든 기능을 수행합니다. 여기에는 온-프레미스 조직과 Exchange Online 조직 간의 모든 보안 메일 메시지를 처리하는 것은 물론 전송 규칙, 저널링 정책, 그리고 하이브리드 배포에 있는 사용자 사서함으로의 메시지 배달도 포함됩니다. 모든 클라이언트 연결 및 조직 관계 기능(예: 약속 있음/없음 공유)도 사서함 서버에서 처리됩니다.

[Exchange 2016 배포 크기 조정](http://go.microsoft.com/fwlink/p/?linkid=301990)에서 Exchange 2016 용량 계획에 대해 자세히 알아보세요.

## Exchange 2013 하이브리드 배포

Exchange 2013 조직에서 하이브리드 배포를 구성하는 경우 기존 Exchange 조직에 Exchange 서버를 추가로 설치할 필요가 없습니다. 클라이언트 액세스 및 사서함 서버는 기존의 Exchange 2013 조직과 Exchange Online 조직 사이의 통신을 조정합니다. 이 통신에는 온-프레미스 조직과 Exchange Online 조직 사이의 메시지 전송 및 메시징 기능이 포함됩니다. 온-프레미스 조직에 Exchange 서버를 둘 이상 설치하여 하이브리드 배포 기능의 안정성과 가용성을 높이는 것이 좋습니다.

다음은 하이브리드 배포에서 Exchange 2013 서버 역할에 대한 간단한 개요입니다.

  - **클라이언트 액세스 서버 역할**   클라이언트 액세스 서버 역할은 기본적으로 Exchange 2013 조직의 클라이언트 액세스 서버가 제공하는 것과 동일한 기능을 계속 제공하면서 하이브리드 배포를 지원하는 데 필요한 몇 가지 기능도 추가로 제공합니다. 클라이언트 액세스 서버는 또한 온-프레미스 조직과 Exchange Online 조직 간에 전송되는 모든 보안 메일 메시지를 처리하는 것은 물론 전송 규칙, 저널링 정책, 그리고 하이브리드 배포에 있는 사용자 사서함으로의 메시지 배달도 처리합니다. 기본적으로 보안 하이브리드 메일 전송을 지원하기 위해 클라이언트 액세스 서버에 전용 수신 커넥터가 구성됩니다. Outlook 클라이언트 액세스, Outlook Web App 및 외부에서 Outlook 사용을 비롯한 모든 클라이언트 연결은 클라이언트 액세스 서버 역할을 통과합니다. 약속 있음/없음 공유와 같은 온-프레미스 조직과 Exchange Online 조직 간의 조직 관계 기능도 클라이언트 액세스 서버 역할에 의해 처리됩니다.
    
    자세한 내용은 [클라이언트 액세스 서버](https://technet.microsoft.com/ko-kr/library/dd298114\(v=exchg.150\))를 참조하십시오.

  - **사서함 서버 역할**   사서함 서버 역할은 온-프레미스 받는 사람 사서함을 호스트하고, 온-프레미스 클라이언트 액세스 서버를 통해 프록시 단위로 Exchange Online 조직과 통신합니다. 기본적으로 보안 하이브리드 메일 전송을 지원하기 위해 사서함 서버 역할에 전용 송신 커넥터가 구성됩니다.
    
    자세한 내용은 [사서함 서버](https://technet.microsoft.com/ko-kr/library/jj150491\(v=exchg.150\))를 참조하십시오.

원하는 하이브리드 배포 구성에 따라 Exchange 2013 서버에 서버 역할 하나 또는 둘 모두를 설치해야 합니다.

  - **단일 Exchange 서버**   온-프레미스 조직에 단일 Exchange 서버를 설치하도록 선택하는 경우 단일 서버에 클라이언트 액세스 및 사서함 서버 역할을 모두 설치해야 합니다.

  - **둘 이상의 Exchange 서버**   온-프레미스 조직에 Exchange 서버를 둘 이상 설치하도록 선택하는 경우에는 온-프레미스 조직의 개별 서버마다 서버 역할을 설치할 수 있습니다. 예를 들어 사서함 및 클라이언트 액세스 역할이 설치되어 있는 Exchange 서버 하나를 설치하고, 클라이언트 액세스 서버 역할만 설치되어 있는 또 다른 Exchange 서버를 설치할 수도 있습니다. 그러나 모범 사례 및 권장되는 서버 구성은 온-프레미스 조직에 배포된 서버 *각각*에 클라이언트 액세스 및 사서함 서버 역할을 설치하는 것입니다.

[용량 계획에서의 다중 서버 역할 구성 이해](http://go.microsoft.com/fwlink/?linkid=266576)에서 Exchange 2013 용량 계획에 대한 자세한 내용을 참조하십시오.

## 하이브리드 배포에서 Exchange 서버의 기능

Exchange 서버는 하이브리드 배포에서 온-프레미스 조직에 몇 가지 중요한 기능을 제공합니다.

  - **페더레이션**Exchange 서버를 사용하면 Microsoft 페더레이션 게이트웨이를 통해 온-프레미스 조직용 페더레이션 트러스트를 만들 수 있습니다. Microsoft 페더레이션 게이트웨이는 Microsoft에서 제공하는 무료, 클라우드 기반 서비스로서 온-프레미스 조직과 Office 365 조직 사이에서 트러스트 브로커 역할을 합니다. 페더레이션은 온-프레미스 조직과 Exchange Online 조직 간 조직 관계를 만들기 위한 요구 사항입니다.
    
    자세한 내용은 [페더레이션](https://technet.microsoft.com/ko-kr/library/dd335047\(v=exchg.150\))를 참조하십시오.

  - **조직 관계**   클라이언트 액세스 서버 역할이 있는 Exchange 2013 서버와 사서함 역할이 있는 Exchange 2016 서버를 사용하면 온-프레미스 조직과 Exchange Online 조직 간에 조직 관계를 만들 수 있습니다. 일정 약속 있음/없음 정보 공유, 메시지 추적, 온-프레미스 조직과 Exchange Online 조직 간의 사서함 이동 등 하이브리드 배포의 여러 다른 서비스를 사용하려면 조직 관계가 필요합니다.
    
    자세한 내용은 [공유](https://technet.microsoft.com/ko-kr/library/dd638083\(v=exchg.150\))를 참조하십시오.

  - **메시지 전송**   클라이언트 액세스 및 사서함 서버 역할이 설치되어 있는 Exchange 서버는 하이브리드 배포에서 메시지 전송을 담당합니다. 이러한 서버는 송신 및 수신 커넥터를 사용하여, 들어오는 외부 메시지의 연결 끝점 역할을 하면서 아웃바운드 메시지를 인터넷과 Exchange Online 조직으로 배달하는 기능도 제공합니다.
    
    자세한 내용은 [Exchange 하이브리드 배포의 전송 옵션](transport-options-in-exchange-hybrid-deployments-exchange-2013-help.md)를 참조하십시오.

  - **메시지 전송 보안**   클라이언트 액세스 및 사서함 서버 역할이 설치되어 있는 Exchange 서버는 Exchange의 도메인 보안 기능을 사용하여 온-프레미스 조직과 Exchange Online 조직 간의 메시지 통신을 보호할 수 있도록 지원합니다. 메시지 통신에 상호 전송 레이어 보안 인증 및 암호화를 사용하여 보안을 강화할 수 있습니다.
    
    자세한 내용은 [도메인 보안 이해](http://go.microsoft.com/fwlink/p/?linkid=266581)를 참조하십시오.

  - **웹의 Outlook(Exchange 2013에서는 Outlook 웹앱)**   클라이언트 액세스 서버 역할이 있는 Exchange 2013 서버와 사서함 역할이 있는 Exchange 2016 서버는 온-프레미스 사서함과 Exchange Online 사서함에 대한 외부 연결용으로 단일 URL 끝점을 구성할 수 있도록 지원합니다. 온-프레미스 사서함의 경우 Exchange 서버는 웹에서 Outlook 요청을 처리하도록 구성됩니다. Exchange Online 조직 사서함의 경우 Exchange 서버는 Exchange Online 조직의 웹에서 Outlook 끝점으로 연결되는 링크를 자동으로 표시하도록 구성됩니다.
    
    자세한 내용은 [Outlook Web App](https://technet.microsoft.com/ko-kr/library/jj657718\(v=exchg.150\))를 참조하십시오.

