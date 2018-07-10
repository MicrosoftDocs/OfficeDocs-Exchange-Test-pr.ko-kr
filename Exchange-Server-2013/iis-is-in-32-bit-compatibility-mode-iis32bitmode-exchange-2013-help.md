---
title: 'IIS가 32 비트 호환성 mode_IIS32BitMode: Exchange 2013 Help'
TOCTitle: IIS가 32 비트 호환성 mode_IIS32BitMode
ms:assetid: 742dfc32-353c-46a2-830e-68aed6a68ce0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.iis32bitmode(v=EXCHG.150)
ms:contentKeyID: 50483427
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS가 32 비트 호환성 mode\_IIS32BitMode

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft 인터넷 정보 서비스 (IIS)이 64 비트 컴퓨터에서 32 비트 모드에서 실행 중인 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007을 사용 하려면 64 비트 컴퓨터에서 실행 하는 경우 IIS 완전 한 64 비트 모드에서 있어야 합니다.

이 문제를 해결 하려면 IIS 64 비트 모드 전환한 후 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

IIS 64 비트 모드로 전환 하려면

1.  명령 프롬프트를 엽니다.

2.  다음을 입력 합니다.
    
    **cscript c:\\inetpub\\adminscripts\\adsutil.vbs SET /w3svc/AppPools/Enable32BitAppOnWin64 False**

3.  Enter 키를 누릅니다.

