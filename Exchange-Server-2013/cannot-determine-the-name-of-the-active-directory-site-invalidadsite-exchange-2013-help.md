---
title: 'Active Directory site_InvalidADSite의 이름을 확인할 수 없음: Exchange 2013 Help'
TOCTitle: Active Directory site_InvalidADSite의 이름을 확인할 수 없음
ms:assetid: ef96e077-08a0-4108-9f7d-0d61758abcd4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.invalidadsite(v=EXCHG.150)
ms:contentKeyID: 50484491
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory site\_InvalidADSite의 이름을 확인할 수 없음

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

이 서버가 유효한 Active Directory® 디렉터리 서비스 사이트에 속하는 것으로 나타나지 않으면 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Microsoft Exchange 설치 Exchange 2007의 설치에 사용 되는 서버는 유효한 Active Directory 사이트에 속하는 필요 합니다.

이 문제를 해결 하려면 로컬 서버는 유효한 Active Directory 사이트의 구성원 인지 확인 하 고 Exchange Server 2007 설치 프로그램을 다시 실행 하십시오.

확인 하 고 사이트 멤버 자격을 표시 하려면 Nltest.exe 명령줄 도구의 **/DsGetSite** 옵션을 사용할 수 있습니다. 자세한 내용은 "도구 및 설정의 컬렉션에서" *Windows Server 2003에 대 한 기술 참조* ([https://go.microsoft.com/fwlink/?LinkId=27734](https://go.microsoft.com/fwlink/?linkid=27734)) "Nltest.exe:: NLTest 개요"를 참조 합니다.

Active Directory 문제를 해결 하는 방법에 대 한 자세한 내용은 "Active Directory 작업 문제를 해결"을 참조 *Windows Server 2003: 작업* (<https://go.microsoft.com/fwlink/?linkid=68099>).

