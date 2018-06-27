---
title: '로컬 컴퓨터가 그룹 membership_ServerIsDynamicGroupExpansionServer 확장을 담당: Exchange 2013 Help'
TOCTitle: 로컬 컴퓨터가 그룹 membership_ServerIsDynamicGroupExpansionServer 확장을 담당
ms:assetid: f6fdd8e1-fda1-45be-b8a2-0d356dbe7d83
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.serverisdynamicgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 50484554
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 로컬 컴퓨터가 그룹 membership\_ServerIsDynamicGroupExpansionServer 확장을 담당

 

_**적용 대상:**Exchange Server_

_**마지막으로 수정된 항목:**2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

그룹 구성원 자격을 확장 하는 일을 담당 하는 허브 전송 역할을 제거 하려면 해당 시도가 실패 했기 때문에 Microsoft® Exchange Server 2007 설치를 계속할 수 없습니다.

Exchange 2007 설치 전에 허브 전송 역할을 제거할 수 있는 메일 그룹 확장 현재 브리지 헤드 서버에서 제거할 필요 합니다.

메일 그룹을 확장 하 게 식별할 수, 메일 그룹에 속한 개별 받는 사람을 식별 하거나 확장에 대 한 추가 메일 그룹의 id를 나열 합니다. 확장 된 메일 그룹에는 모든 필수 배달 상태 알림 (DSN)에 대 한 경로 반환할 수 있습니다. Microsoft Exchange 관리자 또는 특정 전자 메일 메시지의 상태를 전자 메일 보낸 사람이 Dsn에 게 알려야합니다. 또한 메일 그룹 확장 부재중 메시지 또는 자동으로 생성 된 회신 원본 메시지의 보낸사람에 게 보내야 하는지 여부를 식별 합니다.

이 문제를 해결 하려면 메일 그룹 확장을 다른 서버로 이동 하 고 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

메일 그룹 또는 동적 메일 그룹 확장 서버를 변경 하려면

1.  Exchange 관리 콘솔을 엽니다.

2.  콘솔 트리에서 **받는 사람 구성** 을 확장 합니다.

3.  콘솔 트리에서 **메일 그룹** 을 클릭 합니다.

4.  모든 메일 그룹 및 동적 메일 그룹 확장 서버와 현재 브리지 헤드 서버를 사용 하는 보기에 필터를 만듭니다.
    
    1.  동작 창에서 **필터 만들기** 를 클릭 합니다.
    
    2.  속성 드롭다운 목록에서 **확장 서버** 를 클릭 합니다.
    
    3.  연산자 드롭다운 목록에서 **같음** 를 클릭 합니다.
    
    4.  값 상자에 현재 서버 역할을 확장 하는 브리지 헤드 서버를 선택 하려면 **찾아보기** 단추를 클릭 합니다.


> [!NOTE]
> 다음 단계는 선택 사항입니다.



1.  추가 필터 조건을 지정 하려면 **식 추가** 클릭 합니다. 모든 필터 조건을 만족 하는 메시지에만 표시 됩니다.

2.  **필터 적용** 을 클릭 합니다. 필터 조건을 만족 하는 결과가 표시 됩니다.

<!-- end list -->

1.  결과 창에서 메일 그룹 확장 서버를 변경 하려면를 클릭 한 다음 작업창에서 **속성** 을 클릭 합니다.

2.  **속성** **고급** 탭을 클릭 합니다.

3.  확장 서버 드롭다운 목록에서 목록에서 특정 서버를 선택 하거나 **조직에서 모든 서버** 를 선택 합니다.

4.  자신의 확장 서버로 브리지 헤드 서버를 사용 하는 동적 메일 그룹 또는 모든 메일 그룹에 대 한 5-7 단계를 반복 합니다.

