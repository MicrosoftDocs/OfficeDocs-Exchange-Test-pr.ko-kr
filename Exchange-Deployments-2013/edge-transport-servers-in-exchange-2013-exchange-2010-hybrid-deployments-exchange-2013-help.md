---
title: 'Exchange 2013/Exchange 2010 하이브리드 배포의 Edge 전송 서버: Exchange 2013 Help'
TOCTitle: Exchange 2013/Exchange 2010 하이브리드 배포의 Edge 전송 서버
ms:assetid: 924f895e-5987-48d0-b113-9d26dcbcdae0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn393965(v=EXCHG.150)
ms:contentKeyID: 59635568
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 2013/Exchange 2010 하이브리드 배포의 Edge 전송 서버

이 항목은 진행 중입니다.  

_**적용 대상:**Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange의 Edge 전송 서버는 조직의 온-프레미스 경계 네트워크에 배포됩니다. 이러한 서버는 인터넷 연결 메일 흐름을 처리하고 내부 네트워크의 Exchange 서버에 대한 SMTP 릴레이 및 스마트 호스트 역할을 하는 도메인에 가입하지 않은 컴퓨터입니다.

Edge 전송 서버를 사용하려는 Exchange 2013 조직은 Exchange Server 2013 Edge 전송 서버 또는 Exchange 2010용 서비스 팩 3(SP3)을 실행하는 Exchange 2010 Edge 전송 서버를 배포할 수 있습니다. 내부 Exchange 2013 클라이언트 액세스 서버 또는 사서함을 인터넷에 직접 노출하지 않으려는 경우 Edge 전송 서버를 사용합니다.

Exchange 2013Edge 전송 서버 역할에 대한 자세한 내용은 [Edge 전송 서버](https://technet.microsoft.com/ko-kr/library/bb124701\(v=exchg.150\))를 참조하세요.

Exchange 2010 Edge 전송 서버 역할에 대한 자세한 내용은 [Edge 전송 서버 역할 개요](http://go.microsoft.com/fwlink/p/?linkid=183473)를 참조하십시오.

## Exchange 2013 기반 하이브리드 배포 조직의 Edge 전송 서버

하이브리드 배포에서 온-프레미스 조직과 Exchange Online 조직 간에 메시지를 라우팅하려면 Exchange Online 대신 Microsoft EOP(Exchange Online Protection) 서비스를 Exchange 2013 또는 Exchange 2010 SP3이 실행되는 Edge 전송 서버에 직접 연결해야 합니다.


> [!IMPORTANT]
> 하이브리드 전송을 처리하지 않는 다른 Exchange 2010Edge 전송 서버가 다른 위치에 있는 경우에는 해당 서버를 Exchange 2010 SP3으로 업그레이드할 필요가 없습니다. 그러나 나중에 EOP를 하이브리드 전송용 추가 Edge 전송 서버에 연결하려면 해당 서버를 Exchange 2010 SP3 또는 Exchange 2013 Edge 전송 서버로 업그레이드해야 합니다.



## 하이브리드 배포에 Edge 전송 서버 추가

하이브리드 배포를 구성할 때 온-프레미스 조직에 Edge 전송 서버를 배포하는 것은 옵션입니다. 하이브리드 배포를 구성할 때 하이브리드 구성 마법사를 사용하면 하이브리드 메일 전송용 클라이언트 액세스 및 사서함 서버를 하나 이상 선택할 수도 있고, 온-프레미스 Edge 전송 서버가 Exchange Online 조직에서 하이브리드 메일 전송을 처리하도록 선택할 수도 있습니다.

하이브리드 배포에 추가된 Edge 전송 서버는 내부 Exchange 2013 클라이언트 액세스 및 사서함 서버 대신 EOP와 통신합니다. Edge 전송 서버는 온-프레미스 조직에서 Exchange Online 조직으로 가는 아웃바운드 메시지에 대해 온-프레미스 사서함 서버와 EOP 간 릴레이 역할을 합니다. Edge 전송 서버는 또한 Exchange Online 조직에서 온-프레미스 조직으로 가는 인바운드 메시지에 대해 온-프레미스 클라이언트 액세스 서버와 EOP 간 릴레이 역할을 합니다. 이전에는 클라이언트 액세스 서버에서 처리되었던 모든 연결 보안이 Edge 전송 서버에서 처리됩니다. 받는 사람 조회, 규정 준수 정책 및 다른 메시지 검사는 계속해서 클라이언트 액세스 서버에서 수행됩니다.

## Edge 전송 서버를 사용하지 않는 메일 흐름

다음 프로세스 및 다이어그램에서는 Edge 전송 서버가 배포되지 않은 경우 온-프레미스 조직과 Exchange Online 간에 발생하는 경로 메시지에 대해 설명합니다.

1.  온-프레미스 조직에서 Exchange Online 조직의 받는 사람에게 보내는 메시지는 Exchange 2010 사서함 서버의 사서함에서 Exchange 2010 허브 전송 서버로 전송됩니다.

2.  Exchange 2010 허브 전송 서버는 메시지를 Exchange 2013 사서함 서버로 전송합니다.

3.  Exchange 2013 사서함 서버는 메시지를 직접 Exchange Online EOP 회사로 보냅니다.

4.  EOP는 메시지를 Exchange Online 조직으로 배달합니다. 이 예에서는 클라이언트 액세스 및 사서함 서버 역할이 동일한 Exchange 2013 서버에 설치됩니다.

Exchange Online 조직에서 온-프레미스 조직으로 보낸 메시지는 역방향 라우팅을 따릅니다.

**Edge 전송 서버가 배포되지 않은 하이브리드 배포에서의 메일 흐름**

![Edge 전송 서버가 없는 온-프레미스](images/Dn393965.37bbe430-b157-4f52-83da-6d44f4459425(EXCHG.150).png "Edge 전송 서버가 없는 온-프레미스")

## Edge 전송 서버를 사용하는 메일 흐름

다음 프로세스는 Edge 전송 서버가 배포된 경우 온-프레미스 조직과 Exchange Online 간의 경로 메시지를 보여줍니다. 온-프레미스 조직에서 Exchange Online 조직의 받는 사람에게 가는 메시지가 Exchange 2010 사서함 서버에서 전송됩니다.

1.  온-프레미스 조직에서 Exchange Online 조직의 받는 사람에게 보내는 메시지는 Exchange 2010 사서함 서버의 사서함에서 Exchange 2010 허브 전송 서버로 전송됩니다.

2.  Exchange 2010 허브 전송 서버는 메시지를 Exchange 2013 사서함 서버로 전송합니다.

3.  Exchange 2013 사서함 서버는 메시지를 Exchange 2013 또는 Exchange 2010 SP3 Edge 전송 서버로 보냅니다.

4.  Edge 전송 서버는 메시지를 Exchange Online EOP 회사로 보냅니다.

5.  EOP는 메시지를 Exchange Online 조직으로 배달합니다. 이 예에서는 클라이언트 액세스 및 사서함 서버 역할이 동일한 Exchange 2013 서버에 설치됩니다.

Exchange Online 조직에서 온-프레미스 조직으로 보낸 메시지는 역방향 라우팅을 따릅니다.

**Exchange 2013 또는 2010 SP3 Edge 전송 서버가 배포된 하이브리드 배포에서의 메일 흐름**

![Edge 전송 서버가 있는 온-프레미스](images/Dn393965.f1039133-249b-401d-bd39-3672442a06c9(EXCHG.150).png "Edge 전송 서버가 있는 온-프레미스")

