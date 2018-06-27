---
title: '도메인 준비 required_DomainPrepRequired: Exchange 2013 Help'
TOCTitle: 도메인 준비 required_DomainPrepRequired
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 50484519
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 도메인 준비 required\_DomainPrepRequired

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

서버 역할을 설치 하지 못했습니다 Microsoft Exchange Server 2007 설치를 계속할 수 없습니다.

Microsoft Exchange 설치 하려면 Exchange Server 2007에 특정 서버 역할을 설치 하기 전에 로컬 도메인을 준비 해야 합니다.

Exchange Server 2007에 대 한 도메인 준비는 다음 작업 이루어져 있습니다.

  - Exchange 서버, Exchange 조직 관리자, 사용자 인증 및 Exchange 사서함 관리자에서 도메인 컨테이너 사용 권한을 설정 합니다.

  - 존재 하지 않는 경우 Microsoft Exchange System Objects 컨테이너를 만들고이 컨테이너 Exchange 서버, Exchange 조직 관리자 및 인증 된 사용자에 대 한 사용 권한을 설정 합니다.

  - 현재 도메인에서 새 도메인 글로벌 그룹을 만들고 Exchange Install Domain Servers 호출 됩니다.

  - 루트 도메인에서 Exchange Servers USG에 Exchange Install Domain Servers 그룹을 추가 합니다.

이 문제를 해결 하려면 **setup /PrepareDomain** 로컬 도메인을 준비 하 고 서버를 다시 시도 하 역할 설치를 실행 합니다.

PrepareDomain 프로세스를 수행 하는 방법에 대 한 자세한 내용은 "방법 하 준비 Active Directory 및 도메인" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453))을 참조 하십시오.

