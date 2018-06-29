---
title: '로컬 컴퓨터에는 Exchange Server_ExchangeAlreadyInstalled 이미 실행 중임: Exchange 2013 Help'
TOCTitle: 로컬 컴퓨터에는 Exchange Server_ExchangeAlreadyInstalled 이미 실행 중임
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 50482941
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 로컬 컴퓨터에는 Exchange Server\_ExchangeAlreadyInstalled 이미 실행 중임

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

로컬 컴퓨터에 이전 Microsoft Exchange 구성 요소가 설치 되어 있기 때문에 Microsoft® Exchange Server 2007 설치를 계속할 수는 없습니다.

Exchange 2007 설치는 로컬 컴퓨터에 없는 설치 하는 기존 Microsoft Exchange 구성 요소는 필요 합니다.

이 문제를 해결 하려면 모든 Microsoft Exchange Server 2003 또는 Microsoft Exchange 2000 Server 구성 요소를 제거 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

Microsoft Exchange 구성 요소를 제거 하려면

1.  **시작** 을 클릭 하 고 **설정** 을 가리킨 다음 **제어판** 을 차례로 클릭 합니다.

2.  **프로그램 추가/제거**를 두 번 클릭합니다.

3.  **현재 설치 된 프로그램** 목록에서 **Microsoft Exchange** 클릭 한 다음 **변경/제거** 를 클릭 합니다.

4.  Microsoft Exchange 설치 마법사에서 **다음** 을 클릭 합니다.

5.  구성 요소 선택 페이지에서 작업 목록에서 설치 된 각 구성 요소 옆에 있는 아래쪽 화살표를 클릭 한 다음 **제거** 를 클릭 합니다.
    

    > [!NOTE]
    > 설치 된 구성 요소 작업 목록에서 확인 표시가 있어야 합니다. <STRONG>제거</STRONG> 를 클릭 하면 확인 표시가 <STRONG>제거</STRONG> word로 대체 됩니다.



6.  **다음** 을 두 번 클릭 합니다.

7.  **마침**을 클릭합니다.

