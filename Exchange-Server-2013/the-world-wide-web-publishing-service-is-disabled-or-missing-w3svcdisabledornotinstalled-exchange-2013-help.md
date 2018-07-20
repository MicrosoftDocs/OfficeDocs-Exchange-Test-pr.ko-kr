---
title: 'World Wide Web 게시 서비스를 사용할 수 없거나 missing_W3SVCDisabledOrNotInstalled: Exchange 2013 Help'
TOCTitle: World Wide Web 게시 서비스를 사용할 수 없거나 missing_W3SVCDisabledOrNotInstalled
ms:assetid: 2d26d778-ddf1-4225-b5e2-f6b49d819c94
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.w3svcdisabledornotinstalled(v=EXCHG.150)
ms:contentKeyID: 50482767
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# World Wide Web 게시 서비스를 사용할 수 없거나 missing\_W3SVCDisabledOrNotInstalled

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

사서함 서버 또는 클라이언트 액세스 역할을 설치 하는 시도 발견는 World Wide Web 게시 서비스를 사용 하지 않도록 설정 되거나 설치 되지 않은이 컴퓨터에 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007 설치 World Wide Web 게시 서비스 설치 되어 있고 사용 하지 않도록 이외의 다른 값으로 설정 하려면 Microsoft Exchange를 설치 하는 컴퓨터가 필요 합니다.

이 문제를 해결 하려면 World Wide Web 게시 서비스 설치 및 로컬 컴퓨터에서 해제 하지 않은 확인 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

World Wide Web 게시 서비스 설치 및 사용 하지 않도록 설정 되었는지 확인 하려면

1.  바탕 화면에서 **내 컴퓨터** 를 마우스 오른쪽 단추로 클릭 한 다음 **관리** 를 클릭 합니다.

2.  **서비스 및 응용 프로그램** 노드를 확장 하 고 **서비스** 노드를 클릭 합니다.

3.  오른쪽 창에서 **World Wide Web 게시 서비스** 를 찾습니다.
    
    **World Wide Web 게시 서비스** 설치 서비스 목록에 표시 되지 않으면, 설치 하는 아래의 절차의 단계를 수행 합니다.

4.  **World Wide Web 게시 서비스** 표시 되 고 상태가 **시작 됨** 이 아닌를 마법사를 시작 하려면 다음 단계를 계속 합니다.

5.  **World Wide Web 게시 서비스** 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 클릭 합니다.

6.  **시작 유형** **을 자동** 이며 **서비스 상태가시작** 됨으로 설정 확인 합니다.

7.  **적용**을 클릭한 다음 **확인**을 클릭합니다.

World Wide Web 게시 서비스를 설치 하려면

1.  **시작** 메뉴에서 **설정**, **제어판** 을 선택 하 고 **프로그램 추가 / 제거** 를 클릭 한 다음

2.  **Windows 구성 요소 추가/제거** 를 클릭 합니다.

3.  **구성 요소** 목록에서 **응용 프로그램 서버** 확인란을 선택한 다음 **자세히** 를 클릭 합니다.

4.  **인터넷 정보 서비스 관리자** 를 선택한 다음 **자세히** 를 클릭 합니다.

5.  **World Wide Web 서비스** 를 선택한 다음 확인란을 선택 합니다.

6.  **구성 요소** 목록으로 돌아가려면 **확인** 을 두 번 클릭 하 고 을 클릭 합니다.

7.  IIS 서비스를 설치 하면 **완료** 를 클릭 합니다.

