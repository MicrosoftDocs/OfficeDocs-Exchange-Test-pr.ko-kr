---
title: '메시지는 현재 하나 이상의 queues_MessagesInQueue에 있습니다: Exchange 2013 Help'
TOCTitle: 메시지는 현재 하나 이상의 queues_MessagesInQueue에 있습니다
ms:assetid: 3ffcdc7e-c1b7-49a7-8e5f-b30c0397908d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.messagesinqueue(v=EXCHG.150)
ms:contentKeyID: 50482949
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지는 현재 하나 이상의 queues\_MessagesInQueue에 있습니다

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

전송 역할을 제거 하는 시도 전송 큐에서 데이터가 손실 될 수 있으므로이 경고를 표시 하는 Microsoft® Exchange Server 2007 설치 합니다.

Exchange 2007 설치 프로그램에서는 해당 큐 관리와 관련 된 역할을 제거 하기 전에 전송 대기열이 비어 있는지 있는지 확인 합니다.

전송 큐에 여전히 메시지의 배달 전에 전송 역할을 제거 하는 경우 해당 메시지를 무기한 차단 될 수 있습니다.

이 문제를 해결 하는 비어 있는 메시지의 설치를 계속 하기 전에 되도록 참조 된 큐를 조사 합니다.

큐의 콘텐츠를 보려면

1.  Exchange 관리 콘솔을 엽니다.

2.  콘솔 트리에서 **도구 상자**를 클릭합니다.

3.  결과 창에서 **Exchange 큐 뷰어** 를 클릭 합니다.

4.  작업 창에서 **도구 열기**를 클릭합니다.

5.  큐 뷰어에서 **큐** 탭을 클릭 합니다. 연결 된 서버에 있는 모든 큐의 목록이 표시 됩니다.

6.  원하는 하 고 큐의 속성을 보려면 **속성** 선택 하는 큐를 마우스 오른쪽 단추로 클릭 합니다.

큐에서 메시지를 보려면

1.  1 ~ 4 단계를 수행 합니다.

2.  큐 뷰어에서 **메시지** 탭을 클릭 합니다. 연결 된 서버에 있는 모든 메시지의 목록이 표시 됩니다. 단일 큐에 보기를 조정 하려면 **큐** 탭을 클릭 하 고 큐 이름을 두번클릭 다음 표시 되 면 Server\\Queue 탭을 클릭 합니다.

3.  메시지에 대 한 자세한 정보를 보려면 메시지를 선택한 다음 작업창에서 **속성** 을 클릭 합니다.

