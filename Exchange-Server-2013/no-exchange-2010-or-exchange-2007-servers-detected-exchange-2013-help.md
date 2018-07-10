---
title: 'Exchange 2010 또는 Exchange 2007 서버 없음 감지: Exchange 2013 Help'
TOCTitle: Exchange 2010 또는 Exchange 2007 서버 없음 감지
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 50483494
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2010 또는 Exchange 2007 서버 없음 감지

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-11-08_

조직에 Exchange Server 2010 또는 Exchange Server 2007 서버 역할이 없기 때문에 Microsoft Exchange Server 2013 설치 시 이 경고가 표시됩니다.


> [!WARNING]
> Exchange Server 2013 설치를 계속하더라도 Exchange 2010 또는 Exchange 2007 서버를 나중에도 조직에 추가할 수 없습니다.



Exchange 2013을 배포하기 전에 Exchange 2013 배포 전 Exchange 2010 또는 Exchange 2007 서버 배포에 필요할 수 있는 다음 요인을 고려하십시오.

  - **타사 또는 내부 개발 응용 프로그램**   이전 버전의 Exchange용으로 개발한 응용 프로그램은 Exchange 2013과 호환되지 않을 수 있습니다. 해당 응용 프로그램을 지원하려면 Exchange 2010 또는 Exchange 2007 서버를 유지 관리해야 할 수 있습니다.

  - **동시 사용 또는 마이그레이션 요구 사항**   사서함을 조직으로 마이그레이션하려는 경우 일부 솔루션에서는 Exchange 2010 또는 Exchange 2007 서버 사용이 필요할 수 있습니다.

Exchange 2010 또는 Exchange 2007 서버를 배포해야 한다면 Exchange 2013 배포 전에 해당 작업을 먼저 수행해야 합니다. Active Directory는 다음 순서대로 Exchange 버전마다 준비해야 합니다.

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

