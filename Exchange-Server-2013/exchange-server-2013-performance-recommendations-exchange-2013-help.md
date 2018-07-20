---
title: 'Exchange Server 2013 성능 권장 사항: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 성능 권장 사항
ms:assetid: 6d0aea68-10d5-4a18-b632-a814ce3daa43
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn879084(v=EXCHG.150)
ms:contentKeyID: 63806350
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Server 2013 성능 권장 사항

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

사용자 환경에 적절 하 게 크기 조정 및 계획 된 Exchange Server 2013 성능 조정 하 고 문제를 해결 가장 효과적입니다. Exchange 2013의 기반이 되는 리소스 인프라를 단순화 하기 위해를 디자인 하는 동안 많은 양의 CPU 용량, 메모리 및 저장소 용량 등의 시스템 리소스를 계속 사용할 수 있습니다 것입니다.

이 섹션의 문서는 Exchange 성능 팀으로 작성 되었습니다. 포함 Exchange 제품 그룹에서 전문 지식을 잘 사례 고객 지원 사례에서 습득 합니다. 이러한 문서 목적이 Exchange 2013 및 Exchange 2013 인프라를 적절 하 게 크기의 중요성에 도입 된 변경의 영향을 파악할 수 있습니다. 또한 권장된 최적화 및 성능 문제를 식별 하에 대 한 지침 포함 했습니다.

## Exchange 2013 및 기타 리소스의 아키텍처 변경 사항

[Exchange 팀 블로그 (영문)](https://go.microsoft.com/fwlink/p/?linkid=35786)및 technet에 이미 Exchange 2013의 아키텍처 변경 사항 설명 되어있습니다. 성능을 더 잘 이해 하기 위해 고려해 야 하는 몇가지 높은 수준의 변경 내용에 따라 먼저 터치 하는 비용 및 크기 조정 합니다. 그런 다음 아래 추가 제공 하기 위해 상황에 맞 및 이러한 중요 한 영역에 배경 권장된 참조의 목록을 포함 했습니다.


> [!NOTE]
> 가상화 된 환경에서 Exchange Server 2013을 배포 하는 방법에 대 한 성능 최적화 지침에 대 한 <A href="exchange-2013-virtualization-exchange-2013-help.md">Exchange 2013 가상화</A> 참조 하십시오.



Exchange 2013 클라이언트 액세스 서버 역할 상태 비저장 프록시 서버입니다. 클라이언트 액세스 서버 역할의 기본 책임 각 요청을 적절 한 사서함 서버로 들어오는 요청 및 프록시를 인증 하는 것, 이제는 사용자 사서함의 활성 복사본을 호스트 한 합니다. 즉, 클라이언트 액세스 서버 사이의 선호도 구성 하 고 부하 분산 장치 특정 프로토콜에 대 한 필요가 하는 것이 더 이상.

Exchange 2013의 다른 주목할 만한 변경 정보 저장소에 됩니다. 이제 두 유형의 프로세스 정보 저장소에 이루어져: 호스트 및 작업자 합니다. 각 데이터베이스 인스턴스는 자체 Microsoft.Exchange.Store.Worker.exe 프로세스와 연결 합니다. 이 문제가 있는 데이터베이스 문제를 더 나은 격리를 허용 하 고 해당 데이터베이스에 대 한 하나의 작업자 인스턴스에 방금 데이터베이스 문제가 발생 한 성능 영향을 줄일 수 있습니다.

Microsoft Exchange Replication service는 사서함 서버 역할에 관련 된 모든 고가용성 서비스에 대 한 책임을 집니다. 이 복제 서비스가 오류를 모니터링 하 고 수정 조치를 수행 하는 일을 담당 하는 활성 관리자 구성 요소를 호스팅합니다.

[Exchange 2013 서버 역할 아키텍처](https://go.microsoft.com/fwlink/p/?linkid=523735)에서 다시 이전 버전에서 Exchange 2013 환경 크기에 영향을 포함 하 여 아키텍처 변경 사항에 유용한 게시물을 확인할 수 있습니다.

Exchange 2013 아키텍처 변경 사항 및 기타 관련 영역에 대 한 배경 정보에 대 한 자세한 다음에서 찾을 수 있습니다.

[Exchange Server 2013의 아키텍처](https://go.microsoft.com/fwlink/p/?linkid=523769)

[계획 하 고 적절 한 방법으로: 시나리오의 크기를 조정 하는 Exchange Server 2013](https://go.microsoft.com/fwlink/p/?linkid=523773)

[모니터링 및 튜닝 Microsoft Exchange Server 2013 성능](https://go.microsoft.com/fwlink/p/?linkid=523774)

[Exchange Server 2013 구현: (01) 업그레이드 및 Exchange Server 2013 배포](https://go.microsoft.com/fwlink/p/?linkid=523775)

[Exchange Server 2013 구현: (02) 계획 하 고 오른쪽 방법: Exchange Server 2013 크기 조정](https://go.microsoft.com/fwlink/p/?linkid=523776)

[Exchange Server 2013 구현: (03) Exchange Server 2013 가상화 모범 사례](https://go.microsoft.com/fwlink/p/?linkid=523777)

[Exchange Server 2013 구현: (04) Exchange 아키텍처: 고가용성 및 사이트 복원 력](https://go.microsoft.com/fwlink/p/?linkid=523779)

[Exchange Server 2013 구현: (05) Outlook 연결](https://go.microsoft.com/fwlink/p/?linkid=523781)

[기본 아키텍처](https://go.microsoft.com/fwlink/p/?linkid=523782)

[Exchange 2013 클라이언트 액세스 서버 역할](https://go.microsoft.com/fwlink/p/?linkid=386373)

[Exchange Server 2013 가상화 모범 사례](https://go.microsoft.com/fwlink/p/?linkid=523783)

[부하 분산](load-balancing-exchange-2013-help.md)

[Exchange Server 업데이트: 빌드 번호 및 릴리스 날짜](https://technet.microsoft.com/ko-kr/library/hh135098\(v=exchg.150\))

[Exchange Server 2013 릴리스 정보](release-notes-for-exchange-2013-exchange-2013-help.md)

[Exchange 2013용 업데이트](updates-for-exchange-2013-exchange-2013-help.md)

[IIS 7.5, IIS 6.0 및 IIS 7.0에서 ASP.NET 스레드 사용](https://go.microsoft.com/fwlink/p/?linkid=169626)

