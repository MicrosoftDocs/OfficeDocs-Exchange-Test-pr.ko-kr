---
title: '현재 Directory_DomainPrepWithoutADUpdate 준비에 있는 권한이 없습니다.: Exchange 2013 Help'
TOCTitle: 현재 Directory_DomainPrepWithoutADUpdate 준비에 있는 권한이 없습니다.
ms:assetid: 4283c4b9-983f-460e-a5de-42b2772eae0d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.domainprepwithoutadupdate(v=EXCHG.150)
ms:contentKeyID: 50482964
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 현재 Directory\_DomainPrepWithoutADUpdate 준비에 있는 권한이 없습니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

시도한 도메인 준비 실패 했기 때문에 Microsoft Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 설치 하려면 Exchange Server 2007에 Active Directory에서 도메인을 준비할 수 있습니다 전에 Active Directory 디렉터리 서비스를 수정 해야 합니다.

**Setup /PrepareAD** 명령을 실행 하는 데 사용 되는 계정에 Enterprise Admins 그룹에 속하는 것으로 표시 하는 경우에이 명령을 실행할 수 있는 권한이 있습니다. 계정이 만료 될 수 있습니다.

이 문제를 해결 하려면 로그온 한 사용자 계정이 유효 하 고 **setup /PrepareAD를** 다시 실행 하 고 이러한 사용 권한이 있는 계정으로에서 Enterprise Admins 그룹 또는 로그에 속하는 확인 합니다.

PrepareAD 프로세스를 수행 하는 방법에 대 한 자세한 내용은 "방법을 준비 Active Directory 및 도메인" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453))을 참조 하십시오.

Microsoft Exchange와 필요한 Active Directory 사용 권한에 대 한 자세한 내용은 "(영문)와 Active Directory 사용 권한에서 Exchange 서버" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592))을 참조 하십시오.

