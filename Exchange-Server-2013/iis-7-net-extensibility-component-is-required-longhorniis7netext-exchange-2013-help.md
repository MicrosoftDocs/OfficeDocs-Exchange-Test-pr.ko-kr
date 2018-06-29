---
title: 'IIS 7.NET 확장성 구성 요소는 required_LonghornIIS7NetExt: Exchange 2013 Help'
TOCTitle: IIS 7.NET 확장성 구성 요소는 required_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 50483621
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IIS 7.NET 확장성 구성 요소는 required\_LonghornIIS7NetExt

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

Microsoft®대상 서버에 필요한 인터넷 정보 서버 (IIS) 7.NET 확장성 구성 요소 설치 되어있지 않은 Exchange Server 2010 설치를 계속할 수 없습니다.

Exchange 2010 Windows PowerShell 원격 작업을 사용할 수 있으려면 대상 서버에 IIS 7.NET 확장성 구성 요소를 설치 해야 합니다.

이 오류를 해결 하기 위해 서버 관리자를 사용 하 여이 서버에 IIS 7.NET 확장성 구성 요소를 설치 및 Exchange 2010 설치 프로그램을 다시 실행 하십시오.

서버 관리자 도구를 사용 하 여 Windows Server 2008 R2 또는 Windows Server 2008에 IIS 7.NET 확장성 구성 요소 설치

1.  **시작**, **관리 도구** 를 선택한 다음 **서버 관리자** 를 클릭 합니다.

2.  왼쪽 탐색 창에서 **역할**을 확장한 다음 **웹 서버(IIS)**를 마우스 오른쪽 단추로 클릭하고 **역할 서비스 추가**를 선택합니다.

3.  **역할 서비스 선택** 창에서 **응용 프로그램 개발** 까지 아래로 스크롤하십시오.

4.  **.NET 확장성** 아래에서 확인란을 선택 합니다.

5.  **역할 서비스 선택** 창에서 **다음** 을 클릭 하 고 **설치 선택 사항 확인** 창에서 **설치** 를 클릭 합니다.

6.  **Close** 역할 서비스 추가 마법사를 종료를 클릭 합니다.

