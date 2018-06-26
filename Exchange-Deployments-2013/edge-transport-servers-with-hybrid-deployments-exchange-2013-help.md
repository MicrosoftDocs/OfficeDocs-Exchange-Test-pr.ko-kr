---
title: '하이브리드 배포의 Edge 전송 서버: Exchange 2013 Help'
TOCTitle: 하이브리드 배포의 Edge 전송 서버
ms:assetid: 166b1490-5c56-40df-a17b-e8bb36224fd9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh134662(v=EXCHG.150)
ms:contentKeyID: 50484626
ms.date: 04/27/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 배포의 Edge 전송 서버

 

_<strong>적용 대상:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong>2018-04-16_

Edge 전송 서버 역할은 일반적으로 Exchange 조직의 경계 네트워크에 있는 컴퓨터에 배포되며 조직의 공격 영역을 최소화하도록 설계되었습니다. Edge 전송 서버 역할은 조직의 내부 온-프레미스 Exchange 서버에 대한 SMTP 릴레이 및 스마트 호스트 서비스를 제공하는 모든 인터넷 연결 메일 흐름을 처리합니다.

## Exchange 기반 하이브리드 배포 조직의 Edge 전송 서버

Edge 전송 서버를 사용하려는 Exchange 2016 조직은 Exchange 2016 이상, Exchange 2013 또는 Exchange 2010의 최신 릴리스를 실행하는 Edge 전송 서버를 배포할 수 있습니다. 내부 Exchange 서버를 인터넷에 직접 노출하지 않으려면 Edge 전송 서버를 사용합니다. 하이브리드 배포에서 Edge 전송 서버를 배포하면 Exchange Online이 Exchange Online Protection 서비스를 통해 Edge 전송 서버에 연결하여 메시지를 배달합니다. 그러면 Edge 전송 서버에서 받는 사람 사서함이 있는 온-프레미스 Exchange 사서함 서버로 메시지를 배달합니다.


> [!IMPORTANT]
> 모든 서버, 서비스 또는 장치를 SMTP 트래픽을 처리하거나 수정하는 온-프레미스 Exchange 서버와 Office 365 사이에 두지 마십시오. 온-프레미스 Exchange 조직과 Office 365 간의 보안 메일 흐름은 조직 간 전송된 메시지에 포함된 정보에 따라 다릅니다. 수정하지 않고 TCP 포트 25에서 SMTP 트래픽을 허용하는 방화벽이 지원됩니다. 서버, 서비스 또는 장치가 온-프레미스 Exchange 조직과 Office 365 간에 보낸 메시지를 처리하는 경우 이 정보가 제거됩니다. 이 경우 메시지가 더 이상 조직 내부로 간주되지 않으며 및 스팸 방지 필터링, 전송 및 저널 규칙, 적용되지 않을 수 있는 기타 정책을 따르게 됩니다.




> [!IMPORTANT]
> 하이브리드 전송을 처리하지 않는 다른 Exchange Edge 전송 서버가 다른 위치에 있는 경우에는 해당 서버를 하이브리드 배포로 업그레이드할 필요가 없습니다. 그러나 나중에 EOP를 하이브리드 전송용 추가 Edge 전송 서버에 연결하려면 해당 서버를 최신 릴리스의 Exchange 2016 이상, Exchange 2010 또는 Exchange 2013를 실행해야 합니다.



## 하이브리드 배포에 Edge 전송 서버 추가

하이브리드 배포를 구성할 때 온-프레미스 조직에 Edge 전송 서버를 배포하는 것은 옵션입니다. 하이브리드 배포를 구성할 때 하이브리드 구성 마법사를 사용하면 내부 온-프레미스 Exchange 서버를 하나 이상 선택할 수도 있고, 하나 이상의 온-프레미스 Edge 전송 서버가 Exchange Online 조직에서 하이브리드 메일 전송을 처리하도록 선택할 수도 있습니다.

하이브리드 배포에 추가된 Edge 전송 서버는 내부 Exchange 서버 대신 EOP와 통신합니다. Edge 전송 서버는 온-프레미스 조직에서 Exchange Online 조직으로 가는 아웃바운드 메시지에 대해 내부 Exchange 서버 간 릴레이 역할을 합니다. Edge 전송 서버는 또한 Exchange Online 조직에서 온-프레미스 조직으로 가는 인바운드 메시지에 대해 내부 Exchange 서버 간 릴레이 역할도 합니다. 이전에는 내부 Exchange 서버에서 처리되었던 모든 연결 보안이 Edge 전송 서버에서 처리됩니다. 받는 사람 조회, 규정 준수 정책 및 다른 메시지 검사는 계속해서 내부 Exchange 서버에서 수행됩니다.

하이브리드 배포에 Edge 전송 서버를 추가하는 경우 온-프레미스 사용자와 인터넷 받는 사람 간에 전송되는 메일을 라우팅할 필요는 없습니다. 온-프레미스와 Exchange Online 조직 간에 전송되는 메시지만 Edge 전송 서버를 통해 라우팅됩니다.

## Edge 전송 서버를 사용하지 않는 메일 흐름

다음 프로세스 및 다이어그램에서는 Edge 전송 서버가 배포되지 않은 경우 온-프레미스 조직과 Exchange Online 간에 발생하는 메시지 경로에 대해 설명합니다.

1.  온-프레미스 조직에서 Exchange Online 조직의 받는 사람에게 전송되는 아웃바운드 메시지는 내부 Exchange 서버의 사서함에서 전송됩니다.

2.  Exchange 서버에서 EOP에 직접 메시지를 보냅니다.

3.  EOP는 Exchange Online 조직으로 메시지를 배달합니다.

Exchange Online 조직에서 온-프레미스 조직으로 보낸 메시지는 역방향 라우팅을 따릅니다.

**Edge 전송 서버가 배포되지 않은 하이브리드 배포에서의 메일 흐름**

![Edge 전송 서버를 사용하지 않는 하이브리드 메일 흐름](images/Hh134662.a95b4d1e-fd4a-4952-b891-22f84c9e71a3(EXCHG.150).png "Edge 전송 서버를 사용하지 않는 하이브리드 메일 흐름")

## Edge 전송 서버를 사용하는 메일 흐름

다음 프로세스는 Edge 전송 서버가 배포된 경우 온-프레미스 조직과 Exchange Online 간의 경로 메시지를 보여줍니다. 온-프레미스 조직에서 Exchange Online 조직의 받는 사람에게 전송되는 메시지가 내부 Exchange 사서함 서버에서 전송됩니다.

1.  온-프레미스 조직에서 Exchange Online 조직의 받는 사람에게 전송되는 메시지는 내부 Exchange 서버의 사서함에서 전송됩니다.

2.  Exchange 서버는 지원되는 버전 및 릴리스의 Exchange를 실행하는 Edge 전송 서버에 메시지를 보냅니다.

3.  Edge 전송 서버는 EOP로 메시지를 보냅니다.

4.  EOP는 Exchange Online 조직으로 메시지를 배달합니다.

Exchange Online 조직에서 온-프레미스 조직으로 보낸 메시지는 역방향 라우팅을 따릅니다.

**Edge 전송 서버가 배포된 하이브리드 배포에서의 메일 흐름**

![Edge 전송 서버를 사용하는 하이브리드 메일 흐름](images/Hh134662.821fe099-56f5-4501-8e1a-e184ba07a653(EXCHG.150).png "Edge 전송 서버를 사용하는 하이브리드 메일 흐름")

