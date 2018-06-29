---
title: 'TLS 기능 및 관련 용어: Exchange 2013 Help'
TOCTitle: TLS 기능 및 관련 용어
ms:assetid: 294ba2a9-892d-4a90-beec-9d298426b5f4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb430753(v=EXCHG.150)
ms:contentKeyID: 52058061
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# TLS 기능 및 관련 용어

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-06-18_

Microsoft Exchange Server 2013에서는 TLS(전송 계층 보안)의 전체적인 관리를 향상시키는 관리 기능 및 기타 향상된 기능을 제공합니다. 이러한 기능을 사용할 때는 일부 TLS 관련 기능에 대해 파악해야 합니다. 일부 용어 및 개념은 여러 TLS 관련 기능에 적용됩니다. 이 항목에서는 TLS 및 도메인 보안 기능 집합과 관련된 일부 차이점과 일반 용어를 쉽게 이해할 수 있도록 각 기능에 대해 간단하게 설명합니다.

  - **전송 계층 보안   **TLS는 인터넷 또는 인트라넷에서 보안 웹 통신을 제공하는 데 사용되는 표준 프로토콜입니다. TLS를 사용하면 클라이언트가 서버를 인증하거나 선택적으로 서버가 클라이언트를 인증할 수 있습니다. 또한 TLS는 통신을 암호화하여 보안 채널을 제공하기도 합니다. TLS는 SSL(Secure Sockets Layer) 프로토콜의 최신 버전입니다.

  - **상호 TLS**   상호 TLS 인증은 일반적으로 배포되는 TLS와는 다릅니다. 일반적으로 배포되는 TLS는 기밀 정보를 암호화 형식으로 제공하는 데에만 사용됩니다. 보낸 사람과 받는 사람 간에 인증은 수행되지 않습니다. 또한 TLS를 배포할 때 받는 서버만 인증되는 경우가 있습니다. TLS의 HTTP 구현 작업을 할 때 이러한 TLS 배포가 일반적으로 적용됩니다. 받는 서버만 인증되는 이러한 구현을 SSL이라고 합니다.
    
    상호 TLS 인증을 사용하면 각 서버는 다른 서버에서 제공한 인증서의 유효성을 검사하여 해당 서버의 ID를 확인합니다. 이 시나리오에서는 Exchange 2013 환경에서 확인된 연결을 통해 외부 도메인으로부터 메시지를 받으며 Microsoft Outlook에 **도메인 보안** 아이콘이 표시됩니다.

  - **도메인 보안**   도메인 보안은 상호 TLS를 관리 가능한 유용한 기술로 사용할 수 있도록 하는 인증서 관리, 커넥터 기능 및 Outlook 클라이언트 동작 등의 기능 집합입니다. Exchange 2013 클라이언트 액세스 서버를 통해 아웃바운드 전자 메일을 라우팅할 때는 도메인 보안이 지원되지 않습니다.

  - **Opportunistic TLS**   Exchange 2013에서는 설치 과정에서 자체 서명된 인증서가 만들어집니다. 그리고 기본적으로 TLS가 사용됩니다. 따라서 보내는 시스템에서 Exchange로의 인바운드 SMTP 세션을 암호화할 수 있습니다. 기본적으로 Exchange 2013에서도 모든 원격 연결에 대해서도 TLS를 시도합니다.

  - **직접 신뢰**   기본적으로 Edge 전송 서버와 사서함 서버 간의 모든 트래픽은 인증 및 암호화됩니다. 게다가 인증 및 암호화를 위한 기본 메커니즘은 상호 TLS입니다. Exchange 2013에서는 X.509 유효성 검사 대신 직접 신뢰를 사용하여 인증서를 인증합니다. 직접 신뢰란 Active Directory 또는 AD LDS(Active Directory Lightweight Directory Services)의 인증서 존재 여부로 인증서 유효성을 검사하는 것입니다. Active Directory는 신뢰할 수 있는 저장소 메커니즘으로 간주됩니다. 직접 신뢰를 사용하는 경우 인증서가 자체 서명한 것인지 아니면 인증 기관에서 서명한 것인지는 관계가 없습니다. Exchange 조직에 Edge 전송 서버를 가입시키면 Edge 구독이 사서함 서버에 대한 Active Directory에 Edge 전송 서버 인증서를 게시하여 인증서의 유효성을 검사합니다. Microsoft Exchange EdgeSync 서비스는 Edge 전송 서버에 대한 사서함 서버 인증서 집합으로 AD LDS를 업데이트하여 인증서의 유효성을 검사합니다.

