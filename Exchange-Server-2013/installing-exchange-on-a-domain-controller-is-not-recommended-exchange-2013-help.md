---
title: '도메인 컨트롤러에서 Exchange 설치 하지 않기: Exchange 2013 Help'
TOCTitle: 도메인 컨트롤러에서 Exchange 설치 하지 않기
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 50483018
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 도메인 컨트롤러에서 Exchange 설치 [WarningInstallExchangeRolesOnDomainController] 하지 않기

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2013-03-22_

Microsoft Exchange Server 2013 설치 프로그램에서 Exchange 2013을 설치하려는 컴퓨터가 Active Directory 도메인 컨트롤러에 있음을 감지했습니다. Exchange 2013을 도메인 컨트롤러에 설치하는 것은 권장되지 않습니다.

Exchange 2013을 도메인 컨트롤러에 설치하는 경우 다음 문제를 고려하십시오.

  - Exchange 2013을 Active Directory 사용 권한 분할로 구성하는 것은 지원되지 않습니다.

  - Exchange를 도메인 컨트롤러에 설치하면 Exchange Trusted Subsystem USG(유니버설 보안 그룹)가 Domain Admins 그룹에 추가됩니다. 이렇게 되면 도메인의 모든 Exchange 서버에 해당 도메인에 대한 도메인 관리자 권한이 부여됩니다.

  - Exchange Server와 Active Directory는 모두 리소스를 많이 사용하는 응용 프로그램입니다. 한 대의 컴퓨터에서 두 프로그램을 모두 실행할 경우에는 성능 문제를 고려해야 합니다.

  - 도메인 컨트롤러 Exchange 2013은 글로벌 카탈로그 서버에 설치해야 합니다.

  - 도메인 컨트롤러가 곧 글로벌 카탈로그 서버인 경우 Exchange 서비스가 정상적으로 시작되지 않을 수 있습니다.

  - 서버를 종료하거나 다시 시작하기 전에 Exchange 서비스를 중지하지 않으면 시스템이 종료되는 데 상당히 오래 걸립니다.

  - 도메인 컨트롤러를 구성원 서버로 강등하는 것은 지원되지 않습니다.

  - Active Directory 도메인 컨트롤러이기도 한 클러스터된 노드에서 Exchange 2013을 실행하는 것은 지원되지 않습니다.

Exchange 2013은 구성원 서버에 설치하는 것이 좋습니다.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

