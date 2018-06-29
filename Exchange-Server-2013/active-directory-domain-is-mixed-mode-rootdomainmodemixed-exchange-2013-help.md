---
title: 'Active Directory 도메인 mode_RootDomainModeMixed 혼합: Exchange 2013 Help'
TOCTitle: Active Directory 도메인 mode_RootDomainModeMixed 혼합
ms:assetid: 9f60096e-3eaa-40d8-bde5-13ada5855702
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.rootdomainmodemixed(v=EXCHG.150)
ms:contentKeyID: 50483799
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Active Directory 도메인 mode\_RootDomainModeMixed 혼합

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft® Exchange Server 2007 설치 Microsoft Windows® ° 2000 Server에 대 한 기본 모드에 있는 기존 Active Directory 도메인 설정 되지 않은 때문에 계속 하거나 더 나은 수 없습니다.

Exchange 2007 설치 프로그램에서는 Windows 2000 Server 기본 모드 또는 아주 좋음, 도메인에만 있을 수 있는 유니버설 보안 그룹을 만듭니다.

이 문제를 해결 하려면 도메인 기능 수준에 적어도 Windows 2000 Server 네이티브 수준 올리기, 다음이 단계를 수행 하 고 Exchange 2007 설치 프로그램을 다시 실행 하십시오.

도메인 기능 수준 올리기

1.  Active Directory 도메인 및 트러스트를 엽니다.

2.  콘솔 트리에서 기능을 발생 시킬 하려는 도메인을 마우스 오른쪽 단추로 클릭 하 고 **도메인 기능 수준 올리기** 를 클릭 합니다.

3.  **사용 가능한 도메인 기능 수준 선택** 에서 다음 절차 중 하나를 사용 합니다.
    
      - 네이티브 Windows 2000 Server로 도메인 기능 수준 올리기 **Windows 2000 기본** 클릭 한 다음 **수준 올리기** 를 클릭 합니다.
    
      - Windows Server® 2003에 도메인 기능 수준을 발생 시킬 **Windows Server 2003** 클릭 하 고 다음을 클릭 **발생 시킵니다.**


> [!WARNING]
> <BR>또는 Windows NT® 4.0을 실행 하는 모든 도메인 컨트롤러가 있고 경우 이전에 도메인 기능 수준이 Windows 2000 Server 네이티브를 발생 시 키 지 않습니다. 도메인 기능 수준이 Windows 2000 Server 네이티브 로설정하면 서버로 다시 Windows 2000 혼합 변경할 수 없습니다.<BR>했거나 Windows NT 4.0 및 이전 버전 또는 Windows 2000 Server를 실행 하는 모든 도메인 컨트롤러를 포함 하는 경우에 Windows Server 2003 도메인 기능 수준을 발생 하지 않습니다. 도메인 기능 수준이 Windows Server 2003으로 설정 된 후에 Windows 2000 Server 네이티브 또는 혼합 Windows 2000 Server를 다시 변경할 수 없습니다.


