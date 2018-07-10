---
title: '설치 수 continue_MSDTCStopped 전에 분산 트랜잭션 코디네이터 서비스를 시작 해야 합니다.: Exchange 2013 Help'
TOCTitle: 설치 수 continue_MSDTCStopped 전에 분산 트랜잭션 코디네이터 서비스를 시작 해야 합니다.
ms:assetid: 96e33c94-348e-4a0b-9585-9bee81be4355
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.msdtcstopped(v=EXCHG.150)
ms:contentKeyID: 50483721
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 설치 수 continue\_MSDTCStopped 전에 분산 트랜잭션 코디네이터 서비스를 시작 해야 합니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2012-06-05_

Microsoft Exchange Server 2013의 경우 이 항목의 내용이 업데이트되지 않았습니다. 아직 업데이트되지 않았지만 Exchange 2013에 계속 적용할 수 있습니다. 여전히 도움이 필요하면 아래 커뮤니티 리소스를 확인하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

분산 트랜잭션 코디네이터 서비스가 대상 컴퓨터에서 시작 되지 않으므로 클라이언트 액세스 서버 또는 통합 메시징 서버 역할을 설치 하는 시도 실패 했기 때문에 Microsoft Exchange Server 2007 설치를 계속할 수는 없습니다.

Exchange 2007 설치 프로그램의 분산 트랜잭션 코디네이터 서비스 상태가 **시작** 됨으로 설정 하도록 Microsoft Exchange를 설치 하는 컴퓨터가 필요 합니다.

분산 트랜잭션 코디네이터 서비스 시스템 오류, 프로세스 오류 및 통신 오류와도 성공 하 고 완전 트랜잭션을 확인 하도록 설계 하는 서비스를 제공 합니다.

분산된 트랜잭션에 참가 하는 각 컴퓨터 자체 리소스 및 데이터를 관리 하 고 트랜잭션에서 다른 컴퓨터와 동시에도 작동 합니다. 무엇 보다 분산된 트랜잭션을 커밋하거나 전적으로 참여 하는 모든 컴퓨터에 해당 작업을 중단 해야 합니다. 분산 트랜잭션 코디네이터 거래를 관리 하는 각 컴퓨터에 대 한 트랜잭션 관리자 얻을 수 있으며 관련 된 구성 요소에 대 한 트랜잭션 조정 역할을 수행 합니다.

클라이언트 액세스 서버와 통합 메시징 서버 역할 분산 트랜잭션 코디네이터 서비스에 의존 하는 합니다.

이 문제를 해결 하려면 로컬 컴퓨터에 분산 트랜잭션 코디네이터 서비스 상태가 **시작** 됨으로 설정 되었는지 확인 한 후 Microsoft Exchange 설치 프로그램을 다시 실행 하십시오.

'시작'을 분산 트랜잭션 코디네이터 서비스의 상태를 설정 하려면

1.  **내 컴퓨터** 마우스 오른쪽 단추로 클릭 한 다음 **관리** 를 클릭 합니다.

2.  **서비스 및 응용 프로그램** 노드를 확장 하 고 **서비스** 노드를 클릭 합니다.

3.  오른쪽 창에서 **분산 트랜잭션 코디네이터** 를 찾습니다.

4.  **분산 트랜잭션 코디네이터** 마우스 오른쪽 단추로 클릭 하 고 **속성** 을 클릭 합니다.

5.  **시작 유형** **을 자동** 으로 **시작** 하는 **서비스 상태** 를 설정 합니다.

6.  **적용**을 클릭한 다음 **확인**을 클릭합니다.

