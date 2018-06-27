---
title: '읽기 전용 도메인 controller_ComputerRODC에 Exchange를 설치할 수 없습니다.: Exchange 2013 Help'
TOCTitle: 읽기 전용 도메인 controller_ComputerRODC에 Exchange를 설치할 수 없습니다.
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 50483033
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 읽기 전용 도메인 controller\_ComputerRODC에 Exchange를 설치할 수 없습니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

대상 컴퓨터는 읽기 전용 도메인 컨트롤러 (RODC) 때문에 Microsoft Exchange Server 2007 설치 프로그램에서 설치를 계속할 수 없습니다.

읽기 전용 도메인 컨트롤러는 Windows Server 2008에 대 한 Active Directory의 기능입니다. RODC는 도메인 컨트롤러의 형식을 더 낮은 수준의 물리적 보안 포함 될 수 있는 원격 사이트에 설치할 수 있는 옵션을 설치 합니다.

Exchange 설치 대상 설치 컴퓨터에 대 한 쓰기 액세스 필요합니다.

이 문제를 해결 하려면는 RODC로 지정 되지 않은 대상 설치 컴퓨터를 선택 하 고 설치 프로그램을 다시 실행 하십시오.

