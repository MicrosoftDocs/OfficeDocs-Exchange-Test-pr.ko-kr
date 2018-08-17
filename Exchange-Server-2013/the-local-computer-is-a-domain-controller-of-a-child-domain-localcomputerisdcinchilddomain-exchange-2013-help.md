---
title: '로컬 컴퓨터가 하위 domain_LocalComputerIsDCInChildDomain의 도메인 컨트롤러: Exchange 2013 Help'
TOCTitle: 로컬 컴퓨터가 하위 domain_LocalComputerIsDCInChildDomain의 도메인 컨트롤러
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 50483503
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 로컬 컴퓨터가 하위 domain\_LocalComputerIsDCInChildDomain의 도메인 컨트롤러

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

로컬 컴퓨터에 하위 도메인에 대 한 도메인 컨트롤러는 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007 설치 프로그램에서 도메인 컨트롤러는 글로벌 카탈로그 서버 하지 않으면 자식 도메인에 대 한 도메인 컨트롤러에 로그온 할 설치 되지 않습니다.

이 문제를 해결 하려면 글로벌 카탈로그 서버에는 도메인 컨트롤러를 승격 또는 비 도메인 컨트롤러, 자식 도메인의 구성원 서버에 Exchange 2007을 설치 하 고 후 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

Exchange 서버를 글로벌 카탈로그 서버를 만들어서이 경고를 해결 하려면

1.  도메인 컨트롤러에서 **시작**, 하 고 **프로그램**, **관리 도구** 를 클릭 한 다음 **Active Directory 사이트 및 서비스를** 클릭 합니다.

2.  콘솔 트리에서 **사이트** 를 두번클릭 하 고 해당 사이트의 이름을 두번클릭 **서버** 를 차례로 두번클릭 합니다.

3.  대상 도메인 컨트롤러를 두번클릭 합니다.

4.  결과 창에서 **NTDS 설정** 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 클릭 합니다.

5.  **일반** 탭에서 **글로벌 카탈로그** 확인란을 선택 하려면 클릭 합니다.

6.  도메인 컨트롤러를 다시 시작 합니다.

