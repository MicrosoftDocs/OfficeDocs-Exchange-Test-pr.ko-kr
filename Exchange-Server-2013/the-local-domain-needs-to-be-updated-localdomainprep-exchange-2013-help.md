---
title: '로컬 도메인에서 updated_LocalDomainPrep 해야합니다: Exchange 2013 Help'
TOCTitle: 로컬 도메인에서 updated_LocalDomainPrep 해야합니다
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 50484526
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 로컬 도메인에서 updated\_LocalDomainPrep 해야합니다

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

로그온된 한 사용자의 계정을 있지 않은 때문에 Microsoft Exchange Server 2007 설치를 계속할 수 도메인 준비에 필요한 권한이 나와 있습니다.

Exchange 설치 하려면 도메인 관리자와 Exchange 조직 관리자 그룹 또는 Enterprise Admins 그룹의 구성원 **Setup /PrepareDomain** 을 실행 하는 경우 로그온 한 사용자에 있어야 합니다.

이 문제를 해결 하려면 로그온된 한 사용자 Domain Admins 및 Exchange 조직 관리자 권한을 부여, Enterprise Admins 그룹에서이 등록 또는 Exchange 2007 설치 프로그램을 다시 실행 하 고 이러한 사용 권한이 있는 계정으로 로그온 합니다.

Microsoft Exchange와 필요한 Active Directory 사용 권한에 대 한 자세한 내용은 "(영문)와 Active Directory 사용 권한에서 Exchange 서버" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))을 참조 하십시오.

