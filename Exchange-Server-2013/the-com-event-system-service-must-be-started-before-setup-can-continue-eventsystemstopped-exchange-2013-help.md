---
title: '설치 수 continue_EventSystemStopped 전에 COM + 이벤트 시스템 서비스를 시작 해야 합니다.: Exchange 2013 Help'
TOCTitle: 설치 수 continue_EventSystemStopped 전에 COM + 이벤트 시스템 서비스를 시작 해야 합니다.
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 50482895
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 설치 수 continue\_EventSystemStopped 전에 COM + 이벤트 시스템 서비스를 시작 해야 합니다.

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

대상 컴퓨터에서 COM + 이벤트 시스템 서비스가 시작 되지 않으므로 클라이언트 액세스 서버 또는 Edge 전송 서버 역할을 설치 하는 시도 실패 했기 때문에 Microsoft Exchange Server 2007 설치를 계속할 수는 없습니다.

Exchange 2007 설치 프로그램의 COM + 이벤트 시스템 서비스 상태가 **시작** 됨으로 설정 하도록 Microsoft Exchange를 설치 하는 컴퓨터가 필요 합니다.

COM + 이벤트 시스템 서비스 COM + 구성 요소, 구독 COM 구성 요소에 이벤트의 자동 배포를 제공 하는 시스템 이벤트 알림을 지원 합니다.

클라이언트 액세스 서버와 Edge 전송 서버 역할, COM + 이벤트 시스템 서비스를 구독 하는 COM + 구성 요소에 의존 하는 합니다.

이 문제를 해결 하려면 로컬 컴퓨터에서 COM + 이벤트 시스템 서비스 상태가 **시작** 됨으로 설정 되어있는지 확인 한 후 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

'시작'을 COM + 이벤트 시스템 서비스의 상태를 설정 하려면

1.  **내 컴퓨터** 마우스 오른쪽 단추로 클릭 한 다음 **관리** 를 클릭 합니다.

2.  **서비스 및 응용 프로그램** 노드를 확장 하 고 **서비스** 노드를 클릭 합니다.

3.  오른쪽 창에서 **Com + 이벤트 시스템** 을 찾습니다.

4.  **Com + 이벤트 시스템** 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 클릭 합니다.

5.  **시작 유형** **을 자동** 으로 **시작** 하는 **서비스 상태** 를 설정 합니다.

6.  **적용**을 클릭한 다음 **확인**을 클릭합니다.

