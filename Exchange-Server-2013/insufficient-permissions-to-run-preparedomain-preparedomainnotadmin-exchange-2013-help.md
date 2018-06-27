---
title: '/PrepareDomain_PrepareDomainNotAdmin 실행에 있는 권한이 없습니다.: Exchange 2013 Help'
TOCTitle: /PrepareDomain_PrepareDomainNotAdmin 실행에 있는 권한이 없습니다.
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 50484089
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# /PrepareDomain\_PrepareDomainNotAdmin 실행에 있는 권한이 없습니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

**/PrepareDomain** 프로세스를 실행 하지 못했습니다 Microsoft Exchange Server 2007 설치를 계속할 수 없습니다. 로그온된 한 사용자가 **/PrepareDomain** 프로세스를 수행할 수 있는 권한이 없습니다.

Exchange 2007 설치 프로그램을 사용 하려면 **/PrepareDomain** 프로세스를 실행 하는 경우 로그온 한 사용자 준비, 도메인에 대 한 Domain Admins 그룹의 구성원 및 Enterprise Admins 그룹의 구성원 있어야 합니다.

이 문제를 해결 하려면 Domain Admins 그룹 준비 하는 도메인에 대 한 사용 권한 및 Enterprise Admins 그룹에서이 등록 또는 Exchange 2007 설치 프로그램을 다시 실행 하 고 이러한 사용 권한이 있는 계정을 사용 하 여 로그온에서 로그온 한 사용자에 게 부여 합니다.

Microsoft Exchange와 필요한 Active Directory 사용 권한에 대 한 자세한 내용은 "(영문)와 Active Directory 사용 권한에서 Exchange 서버" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))을 참조 하십시오.

