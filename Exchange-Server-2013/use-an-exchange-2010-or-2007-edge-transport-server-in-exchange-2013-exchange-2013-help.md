---
title: 'Exchange 2010 또는 2007 Edge 전송 서버에서 Exchange 2013 사용: Exchange 2013 Help'
TOCTitle: Exchange 2010 또는 2007 Edge 전송 서버에서 Exchange 2013 사용
ms:assetid: ce99b4bd-868c-4767-9009-e22c17ac0ac7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150569(v=EXCHG.150)
ms:contentKeyID: 50484182
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2010 또는 2007 Edge 전송 서버에서 Exchange 2013 사용

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Edge 전송 서버는 Microsoft Exchange Server 2013 SP1(서비스 팩 1)에서 제공됩니다. 그러나 경계 네트워크에 배포한 기존 Exchange Server 2007 또는 Exchange Server 2010 Edge 전송 서버는 계속 사용할 수 있습니다. 신규 또는 업그레이드된 Exchange 2013 조직의 경우에는 경계 네트워크에 새 Exchange 2007 또는 Exchange 2010 Edge 전송 서버를 설치할 수 있습니다.

다음은 사용자가 알아야 할 사항입니다.

  - Exchange 2007 또는 Exchange 2010 Edge 전송 서버를 허브 전송 서버와 연결해야 합니다. Exchange 2013에서 전송 서비스는 사서함 서버에 있습니다. 따라서 인터넷 메일 흐름은 사서함 서버의 전송 서비스와 Edge 전송 서버 간에 발생하며, Exchange 2013 클라이언트 액세스 서버를 효과적으로 우회합니다.

  - Exchange 2007 또는 Exchange 2010 Edge 전송 서버를 Exchange 2013 서버만 포함된 Active Directory 사이트에서 구독할 수 있습니다. Edge 구독 파일을 가져온 다음 독립 실행형 Exchange 2013 사서함 서버나, 동일한 컴퓨터에 사서함 서버와 클라이언트 액세스 서버가 설치된 서버에서 EdgeSync를 실행할 수 있습니다. 독립 실행형 Exchange 2013 클라이언트 액세스 서버에서 Edge 구독 파일을 가져오거나 EdgeSync를 실행할 수는 없습니다.

  - Exchange 2013 조직에 새 Exchange 2007 또는 Exchange 2010 Edge 전송 서버를 배포하는 절차는 기본적으로 이전 Exchange 버전과 동일합니다. 그러나 이전 버전의 허브 전송 서버에서 수행되는 절차가 Exchange 2013에서는 사서함 서버에서 수행됩니다. 해당 절차는 다음과 같습니다.
    
      - [구독 된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성](https://go.microsoft.com/fwlink/p/?linkid=275859)
    
      - [Edge 전송 서버와 EdgeSync를 사용 하지 않고 허브 전송 서버 간의 메일 흐름 구성](https://go.microsoft.com/fwlink/p/?linkid=276661)

