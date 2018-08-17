---
title: '최신 누적 업데이트 또는 서비스 팩으로 Exchange 2013 업그레이드: Exchange 2013 Help'
TOCTitle: 최신 누적 업데이트 또는 서비스 팩으로 Exchange 2013 업그레이드
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52058115
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 최신 누적 업데이트 또는 서비스 팩으로 Exchange 2013 업그레이드

 

_**적용 대상:** Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-09-04_

Microsoft Exchange Server 2013을 설치한 경우 최신 Exchange 2013 누적 업데이트 또는 서비스 팩으로 업그레이드할 수 있습니다. Exchange 2013 설치 마법사를 사용하여 현재 Exchange 2013 버전을 업그레이드할 수 있습니다. 최신 Exchange 2013 누적 업데이트 또는 서비스 팩에 대한 자세한 내용은 [Exchange 2013용 업데이트](updates-for-exchange-2013-exchange-2013-help.md)를 참조하세요. Exchange 2013에 대한 자세한 내용은 [Exchange 2013의 새로운 기능](what-s-new-in-exchange-2013-exchange-2013-help.md)를 참조하세요.

> [!CAUTION]
> Exchange 2013을 최신 누적 업데이트 또는 서비스 팩으로 업그레이드한 후에는 새 버전을 제거하여 이전 버전으로 되돌릴 수 없습니다. 새 버전을 제거할 경우 서버에서 Exchange가 제거됩니다.


## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 60분

  - Exchange 2013을 설치하기 전에 릴리스 정보를 읽어 보십시오. 자세한 내용은 [Exchange Server 2013 릴리스 정보](release-notes-for-exchange-2013-exchange-2013-help.md)를 참조하십시오.

  - 누적 업데이트 또는 서비스 팩을 설치하려는 서버가 시스템 요구 사항 및 필수 구성 요소를 충족하는지 확인합니다. 자세한 내용은 [Exchange 2013 시스템 요구 사항](exchange-2013-system-requirements-exchange-2013-help.md) 및 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)를 참조하십시오.
    
    > [!CAUTION]
    > Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.


  - 누적 업데이트 또는 서비스 팩을 설치한 후 변경 내용이 레지스트리 및 운영 체제에 적용될 수 있도록 컴퓨터를 다시 시작해야 합니다.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Exchange 2013 누적 업데이트 또는 서비스 팩 설치

설치 마법사를 사용하거나 무인 모드를 통해 Exchange 2013용 누적 업데이트 또는 서비스 팩을 설치할 수 있습니다. 자세한 지침은 다음 항목을 참조하십시오.

  - [설치 마법사를 사용하여 Exchange 2013 설치](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [무인 모드로 Exchange 2013 설치](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

경우에 서비스 팩 또는 누적 업데이트를 설치 했을 때 컴퓨터가 (DAG) 데이터베이스 가용성 그룹의 구성원 [데이터베이스 가용성 그룹 관리](managing-database-availability-groups-exchange-2013-help.md) 항목의 [DAG 구성원에서 유지 관리 수행](managing-database-availability-groups-exchange-2013-help.md) 섹션의 단계를 수행 합니다.

