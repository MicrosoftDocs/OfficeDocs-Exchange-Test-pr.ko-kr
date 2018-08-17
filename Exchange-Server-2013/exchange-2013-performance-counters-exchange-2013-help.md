---
title: 'Exchange 2013 성능 카운터: Exchange 2013 Help'
TOCTitle: Exchange 2013 성능 카운터
ms:assetid: 9143dd77-7c30-4769-8de1-28c717cfa9e9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn904093(v=EXCHG.150)
ms:contentKeyID: 63913017
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 성능 카운터

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-02-06_

## Exchange 2013 성능 카운터

다음 섹션에서는 Exchange 2013의 성능 문제를 해결할 때 사용할 수 있는 유용한 성능 카운터를 나열 합니다.

## Exchange 도메인 컨트롤러 연결 카운터

다음 표에서 적절 한 임계값 및 Exchange 도메인 컨트롤러 연결 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>카운터</th>
<th>설명</th>
<th>임계값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MSExchange ADAccess 도메인 컨트롤러 (*) \LDAP 읽기 시간</p></td>
<td><p>표시 (ms) LDAP 보낼 시간 지정 된 도메인 컨트롤러에 대 한 요청 읽고 응답이 수신 합니다.</p></td>
<td><p>해야 50ms 아래 평균 합니다. 급격히 증가 하는 (최대 값)이 100ms 보다 더 높은 아니어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess 도메인 컨트롤러 (*) \LDAP 검색 시간</p></td>
<td><p>LDAP 검색 요청을 보내고 응답을 받지 (밀리초) 시간을 표시 합니다.</p></td>
<td><p>해야 50ms 아래 평균 합니다. 급격히 증가 하는 (최대 값)이 100ms 보다 더 높은 아니어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ADAccess \LDAP 읽기 시간 (*)를 처리합니다.</p></td>
<td><p>LDAP 읽기 지정 된 도메인 컨트롤러에 대 한 요청을 보내고 응답을 받을 (밀리초) 시간을 표시 합니다.</p></td>
<td><p>해야 50ms 아래 평균 합니다. 급격히 증가 하는 (최대 값)이 100ms 보다 더 높은 아니어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ADAccess \LDAP 검색 시간 (*)를 처리합니다.</p></td>
<td><p>LDAP 검색 요청을 보내고 응답을 받지 (밀리초) 시간을 표시 합니다.</p></td>
<td><p>해야 50ms 아래 평균 합니다. 급격히 증가 하는 (최대 값)이 100ms 보다 더 높은 아니어야 합니다.</p></td>
</tr>
</tbody>
</table>


## 프로세서 및 프로세스 카운터

다음 표에서 적절 한 임계값 및 프로세서 및 프로세스 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>카운터</th>
<th>설명</th>
<th>임계값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processor (_Total) \ % 프로세서 시간</p></td>
<td><p>응용 프로그램 또는 운영 체제 프로세스는 프로세서 실행 중인 시간의 백분율을 보여줍니다. 프로세서 유휴 상태가 아닐 때입니다.</p></td>
<td><p>75% 미만 평균 이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>Processor (_Total) \ 사용자 시간 (%)</p></td>
<td><p>사용자 모드에 소요 된 프로세서 시간의 백분율을 보여줍니다. 사용자 모드는 응용 프로그램, 환경 하위 시스템 및 전체 하위 시스템으로 설계 된 제한 된 처리 모드입니다.</p></td>
<td><p>75% 미만 평균 이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Processor (_Total) \ % 시스템 시간</p></td>
<td><p>권한 있는 모드에 소요 된 프로세서 시간의 백분율을 보여줍니다. 권한 있는 모드는 운영 체제 구성 요소 및 드라이버 하드웨어 조작 하기 위한 처리 모드입니다. 하드웨어 및 모든 메모리에 직접 액세스할 수 있습니다.</p></td>
<td><p>75% 미만 평균 이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>시스템 \ 프로세서 큐 길이 (모든 인스턴스)</p></td>
<td><p>각 프로세서를 서비스 하는 스레드 수를 나타냅니다. 프로세서 큐 길이 프로세서 경합 또는 CPU 사용률이 높은 프로세서 용량에 할당 된 작업 부하를 처리 하기에 충분 없는 것으로 인해 발생 하는 경우를 식별 하는데 사용할 수 있습니다. 프로세서 큐 길이 프로세서 준비 된 큐에 해당 작업을 지연 되 고 실행을 예약할 수 대기 중인 스레드 수를 표시 합니다. 나열 된 값은 측정 수행 된 시간에는 마지막 관찰 된 값입니다.</p></td>
<td><p>프로세서 당 5 보다 클 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>프로세스 (*) \ % 프로세서 시간</p></td>
<td><p>하는데 사용할 수 CPU를 사용 하는 특정 프로세스를 식별 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## 메모리 카운터

다음 표에서 적절 한 임계값 및 메모리 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>Memory\Available Mbytes</p></td>
<td><p>실제 메모리의 양을 메가바이트 (MB) 또는 시스템에서 사용 하는 프로세스에 대 한 할당에 대 한 즉시 사용할 수 있는 단위로 표시합니다. 대기 (캐시 된), 비어 있거나에 할당 된 메모리의 합계와 같은 이며 0 이면 페이지를 나열 합니다. 메모리 관리자의 한 전체 설명을 네트워크 MSDN (Microsoft Developer) 또는 &quot;시스템 성능 및 문제해결 가이드&quot; Windows Server 2003 Resource kit에서를 참조 하십시오.</p></td>
<td><p>총 RAM의 5% 이상이 값을 유지 해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Memory\% 커밋된 사용 되 고 있는 바이트</p></td>
<td><p>Memory\Commit 제한 Memory\Committed 바이트의 비율을 표시 합니다. 커밋된 메모리 사용 하는 작업에 대 한 공간이 예약 된 페이징 파일에 기록 될 필요는 실제 메모리는 디스크에 있습니다. 커밋 제한 페이징 파일의 크기에 따라 결정 됩니다. 페이징 파일은 하는 경우 커밋 제한 증가 확대 하 고 비율 감소 됩니다. 이 카운터를 표시 하는 현재 백분율 값만 사용 합니다. 평균 없습니다.</p></td>
<td><p>이 값은 80% 이상, 하는 경우 시스템에서 더 많은 메모리를 제공 하는 스트레스 될 가능성은 합니다.</p></td>
</tr>
</tbody>
</table>


## .NET framework 카운터

다음 표에서 적절 한 임계값 및.NET Framework 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR 메모리 (*) \ GC에서 시간 (%)</p></td>
<td><p>가비지 수집 발생 했을 때 표시 합니다. 임계값을 초과 하는 카운터, CPU를 정리 하 고 부하에 대 한 효율적으로 사용 되지 않습니다 나타냅니다. 서버에 메모리를 추가 하면이 상황을 향상 됩니다.</p></td>
<td><p>해야 10% 미만 평균 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>.NET CLR 예외 (*) \의 # Excepts throw 된 / sec</p></td>
<td><p>초당 throw 하는 예외를 표시 합니다. .NET Framework 예외 및 비관리 예외 변환 되는.NET Framework 예외를 모두 포함 됩니다. 예는 null 포인터 참조 (영문) 비관리 코드에는 가져올 예외가 발생 다시 관리 되는 코드에서.NET Framework System.NullReferenceException으로. 이 카운터는 처리 및 처리 되지 않은 예외를 포함합니다.</p></td>
<td><p>총 요청 수 (RPS) 초당 5% 미만 이어야 합니다 (웹 서버 (_Total) \Connection 시도/초 *.05.</p></td>
</tr>
<tr class="even">
<td><p>.NET CLR 메모리 (*) \ # 모든 힙 바이트</p></td>
<td><p>4 개의 다른 카운터의 표시 하는: 생성 0 힙 크기, 생성 1 힙 크기, 생성 2 힙 크기 및 큰 개체 힙 크기입니다. 이 카운터는 바이트 GC 힙에 할당 된 현재 메모리를 나타냅니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## 네트워크 카운터

다음 표에서 적절 한 임계값 및 일반적인 네트워크 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>네트워크 인터페이스 (*) \Packets 아웃 바운드 오류</p></td>
<td><p>오류로 인해 전송 될 수 없으며는 아웃 바운드 패킷 수를 나타냅니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connection 오류</p></td>
<td><p>인터넷 사용자의 현재 상태 설정 되었음 또는 닫기를 대기를는 TCP 연결의 수를 표시 합니다. TCP 연결을 설정할 수 있는 수가 페이지 되지 않은 풀의 크기에 따라 제한 됩니다. 페이지 되지 않은 풀 소진 되 면 하는 경우에 없는 새 연결을 설정할 수 있습니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>TCPv4\Connections 재설정</p></td>
<td><p>TCP 연결의 연결 상태 또는 닫기 대기 상태에서 닫힌된 상태에 직접 전환에 대 한 횟수를 표시 합니다.</p></td>
<td><p>재설정 수가 증가 함 또는 일관 되 게 증가 속도 재설정의 대역폭 부족 하다는 나타낼 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>TCPv6\Connections 재설정</p></td>
<td><p>TCP 연결의 연결 상태 또는 닫기 대기 상태에서 닫힌된 상태에 직접 전환에 대 한 횟수를 표시 합니다.</p></td>
<td><p>재설정 수가 증가 함 또는 일관 되 게 증가 속도 재설정의 대역폭 부족 하다는 나타낼 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## Netlogon 카운터

다음 표에서 적절 한 임계값 및 NTLM 인증 문제 및 MaxConcurrentAPI 문제를 모니터링 하는 것에 대 한 일반적인 카운터에 대 한 정보를 표시 합니다. Microsoft 기술 자료 문서 2688798 [MaxConcurrentAPI 설정을 사용 하 여 NTLM 인증의 성능 조정 하는 방법](https://go.microsoft.com/fwlink/p/?linkid=389728) 에 대 한 자세한 내용은 참조 하십시오.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore 대기 자가</p></td>
<td><p>세마포 토 대기 중인 스레드 수입니다.</p></td>
<td><p>Microsoft 기술 자료 문서 2688798 <a href="https://go.microsoft.com/fwlink/p/?linkid=389728">MaxConcurrentAPI 설정을 사용 하 여 NTLM 인증의 성능 조정 하는 방법</a></p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore 소유자</p></td>
<td><p>세마포를 보유 하는 스레드의 수입니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Semaphore 획득</p></td>
<td><p>세마포 _Total에 대 한 보안 채널 연결의 또는 시스템 시작 된 이후 수명 주기 동안 가져온 번의 총 수입니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>\Netlogon\Semaphore 제한 시간</p></td>
<td><p>스레드가 해당 하는 동안 시간이 초과 되었습니다 하는 총 횟수 _Total에 대 한 보안 채널 연결의 또는 시스템 시작 된 이후 수명 주기 동안 세마포에 대 한 대기 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>\Netlogon\Average 세마포 대기 시간</p></td>
<td><p>평균 시간 (초) 마지막 샘플을 통해 세마포 소유 하 고 있는 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## 데이터베이스 카운터

다음 표에서 활성 로그 I/O 대기 시간 요구 사항 카운터와 적절 한 임계값을 보여줍니다. 임계값이 초과 되 면 클라이언트 환경이 떨어집니다. 예, 사용자가 메시지 배달 지연이 발생할 수도 있습니다 느린 시스템 성능을 합니다.


> [!NOTE]
> 일반 저장소 대기 시간 지침 Exchange 2013는 매우 비슷합니다 지침 Exchange 2010에서. <A href="https://go.microsoft.com/fwlink/p/?linkid=525622">사서함 서버 카운터</A>에서 추가 데이터베이스 카운터를 확인할 수 있습니다.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 데이터베이스 = = &gt; \I/O 데이터베이스 인스턴스 (*) 읽습니다 (연결 된) 평균 대기 시간</p></td>
<td><p>데이터베이스 읽기 작업 당 시간을 밀리초 (ms) 단위로 평균 길이 표시 합니다.</p></td>
<td><p>평균 미만 20ms 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 데이터베이스 = = &gt; \I/O 데이터베이스 인스턴스 (*) 기록 (연결 된) 평균 대기 시간</p></td>
<td><p>데이터베이스 쓰기 작업별 평균 대기 시간을 밀리초(ms) 단위로 나타냅니다.</p></td>
<td><p>평균 미만 50ms 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 데이터베이스 = = &gt; 인스턴스 (*) \I/O 로그 쓰기 평균 대기 시간</p></td>
<td><p>Ms 당 로그 쓰기 작업의에서 시간의 평균 길이 표시합니다.</p></td>
<td><p>평균 미만 10ms 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 데이터베이스 = = &gt; \I/O 데이터베이스 인스턴스 (*) 평균 대기 시간 (복구)를 읽습니다.</p></td>
<td><p>수동 데이터베이스 읽기 작업 당 ms에서 시간의 평균 길이 표시 합니다.</p></td>
<td><p>평균 미만 200ms 있어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 데이터베이스 = = &gt; \I/O 데이터베이스 인스턴스 (*) 쓰기 평균 대기 시간 (복구)</p></td>
<td><p>수동 데이터베이스 쓰기 작업당 ms에서 시간의 평균 길이 표시 합니다.</p></td>
<td><p>해야 수 = = 미만으로 동일한 인스턴스에 대 한 읽기 대기 시간 MSExchange 데이터베이스로 측정 된 &gt; 인스턴스 (*) \I/O 데이터베이스 읽습니다 (복구) 평균 대기 시간 카운터 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 데이터베이스 = = &gt; 인스턴스 (연결) (*) \I/O 데이터베이스 읽기 / sec</p></td>
<td><p>데이터베이스 읽기 각 연결 된 데이터베이스 인스턴스에 대 한 초당 작업 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>MSExchange 데이터베이스 = = &gt; 인스턴스 (연결) (*) \I/O 데이터베이스 쓰기 / sec</p></td>
<td><p>각 연결 된 데이터베이스 인스턴스에 대 한 초당 데이터베이스 쓰기 작업의 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 데이터베이스 = = &gt; 인스턴스 (*) \I/O 로그 초당 쓰기</p></td>
<td><p>각 데이터베이스 인스턴스에 대 한 초당 쓰기 로그 횟수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>탑재 MSExchange 활성 관리자 (_total) \Database</p></td>
<td><p>서버에서 활성 데이터베이스 복사본의 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## ASP.NET

다음 표에서 적절 한 임계값 및 ASP.NET 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Application 다시 시작</p></td>
<td><p>웹 서버의 작동 기간 동안 응용 프로그램 다시 시작 된 횟수를 표시 합니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET\Worker 프로세스를 다시 시작</p></td>
<td><p>컴퓨터에서 작업자 프로세스를 다시 시작 되는 횟수를 표시 합니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET\Request 대기 시간</p></td>
<td><p>큐에서 가장 최근의 요청이 대기 하 고 ms 수를 표시 합니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>응용 프로그램 큐에서 ASP.NET 응용 프로그램 (*) \Requests</p></td>
<td><p>응용 프로그램 요청 큐의 요청 수를 표시 합니다.</p></td>
<td><p>항상 0이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET 응용 프로그램 (*) \Requests 실행</p></td>
<td><p>현재 실행 중인 요청 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>ASP.NET 응용 프로그램 (*) \Requests/Sec</p></td>
<td><p>초당 실행 되는 요청의 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## RPC 클라이언트 액세스 카운터

다음 표에서 적절 한 임계값 및 RPC 클라이언트 액세스 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC 평균 대기 시간을 계산합니다.</p></td>
<td><p>대기 시간을 표시, 밀리초 (ms)에서 이전에 대 한 평균 1, 024 패킷을 합니다.</p></td>
<td><p>250ms 아래 이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\RPC 요청</p></td>
<td><p>RPC 클라이언트 액세스 서비스에서 현재 처리 중인 클라이언트 요청 수를 표시 합니다.</p></td>
<td><p>40 개 이상의 아니어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\Active 사용자 수</p></td>
<td><p>마지막 2 분의 일부 작업이 있는 고유 사용자 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\Connection 수</p></td>
<td><p>유지 관리 하는 연결 클라이언트의 총 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>MSExchange RpcClientAccess\RPC 작업/초</p></td>
<td><p>속도 표시는 RPC에서 작업이 발생 초당 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange RpcClientAccess\User 수</p></td>
<td><p>서비스에 연결 된 사용자 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## HTTP 프록시 카운터

다음 표에서 HTTP 프록시 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy (*) \MailboxServerLocator 평균 대기 시간</p></td>
<td><p>MailboxServerLocator 웹 서비스 호출의 평균 대기 시간 (밀리초)을 표시합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy (*) \Average 인증 대기 시간</p></td>
<td><p>평균 시간 표시 마지막 200 샘플을 통해 인증 CAS 요청에 소요 된 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy (*) \Average ClientAccess 서버 처리 대기 시간</p></td>
<td><p>마지막 200 요청을 통해 CAS 처리 시간 (시간에 소요 된 프록시를 포함 하지 않음)의 평균 대기 시간 (밀리초)을 표시 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy (*) \Mailbox 서버 프록시 실패율</p></td>
<td><p>연결의 백분율을 표시 마지막 200 샘플을 통해이 클라이언트 액세스 서버와 MBX 서버 간의 오류와 관련 된 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange HttpProxy (*) \Outsanding 프록시 요청</p></td>
<td><p>해결 되지 않은 프록시 동시 요청 수를 표시 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange HttpProxy (*) \Proxy 요청/초</p></td>
<td><p>초당 처리 된 프록시 요청 수를 표시 합니다.</p></td>
</tr>
<tr class="even">
<td><p>\Requests/Sec MSExchange HttpProxy (*)</p></td>
<td><p>초당 처리 된 요청 수를 표시 합니다.</p></td>
</tr>
</tbody>
</table>


## 정보 저장소 카운터

다음 표에서 적절 한 임계값 및 정보 저장소 카운터에 대 한 정보를 표시 합니다.


> [!NOTE]
> 일반 저장소 대기 시간 지침 Exchange 2013는 매우 비슷합니다 지침 Exchange 2010에서. <A href="https://go.microsoft.com/fwlink/p/?linkid=525622">사서함 서버 카운터</A>에서 추가 정보 저장소 카운터를 확인할 수 있습니다.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
<td><p>임계값</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 저장소 (*) \RPC 요청</p></td>
<td><p>정보 저장소 프로세스에서 현재 실행되는 전체 RPC 요청을 나타냅니다.</p></td>
<td><p>항상 70 미만이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS 클라이언트 형식 (*) \RPC 평균 대기 시간</p></td>
<td><p>특정 클라이언트 프로토콜의 이전 1,024개 패킷에 대한 평균 서버 RPC 대기 시간을 밀리초 단위로 나타냅니다.</p></td>
<td><p>각 클라이언트에 대해 평균적으로 50밀리초 미만이어야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 저장소 (*) \RPC 평균 대기 시간</p></td>
<td><p>RPC 대기 시간 (밀리초) 평균은 데이터베이스당 RPC 요청의 시간 (밀리초)의 평균 대기 시간입니다. 평균은 exrpc32를 로드 한 후 모든 Rpc over 계산 됩니다.</p></td>
<td><p>있어야 미만 50ms 스파이크 항상 100ms 미만입니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeIS 저장소 (*) \RPC 작업/초</p></td>
<td><p>각 데이터베이스 인스턴스에 대 한 초당 RPC 작업 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeIS 클라이언트 형식 (*) \RPC 작업/초</p></td>
<td><p>각 클라이언트 유형 연결에 대 한 초당 RPC 작업 수를 표시 합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


## 클라이언트 액세스 서버 카운터

다음 표에서 클라이언트 연결 카운터 및 인터넷 정보 서비스 (IIS) 카운터에 대 한 정보를 표시 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Requests/초</p></td>
<td><p>초당 ASP.NET 통해 클라이언트에서 받은 HTTP 요청 수를 표시 합니다. 현재 Exchange ActiveSync 요청 속도 결정합니다. 현재 사용자 부하를 결정에 사용 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange ActiveSync\Ping 보류 중인 명령</p></td>
<td><p>큐에서 현재 보류 중인 ping 명령 수를 표시 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange ActiveSync\Sync 명령/초</p></td>
<td><p>초당 처리 된 동기화 명령 수를 표시 합니다. 클라이언트에서는이 명령을 사용 하 여 폴더 내의 항목을 동기화 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange 가용성 Service\Availability 요청 (초)</p></td>
<td><p>초당 처리 하는 요청 수를 표시 합니다. 요청 수 있는 약속 있음 / 없음 정보에 대해서만 이거나 추천 단어를 포함 합니다. 하나의 요청 여러 사서함이 포함 될 수 있습니다. 가용성 서비스 요청의 같은 발생 하는 속도 결정 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange OWA\Current 고유 사용자</p></td>
<td><p>현재 Outlook Web App에 로그온 하는 고유 사용자 수를 표시 합니다. 이 값 고유 활성 사용자 세션의 모니터링 하므로 사용자가 로그 하거나 세션이 제한 시간이 초과 된 후에이 카운터에서 제거 됩니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange OWA\Requests/초</p></td>
<td><p>Outlook Web App에서 처리 하는 초당 요청 수를 표시 합니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeAutodiscover\Requests/sec</p></td>
<td><p>초당 처리 된 자동 검색 서비스 요청 수를 표시 합니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeWS\Requests/sec</p></td>
<td><p>초당 처리 된 요청 수를 표시 합니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="even">
<td><p>웹 서비스 (_Total) \Current 연결</p></td>
<td><p>웹 서비스 설정 된 연결의 현재 수를 표시 합니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>웹 서비스 (기본 웹사이트) \Current 연결</p></td>
<td><p>프런트엔드 최종 CAS 서버 역할을 방문 하는 연결 수에 해당 하는 기본 웹사이트에 설정 된 연결의 현재 수를 표시 합니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="even">
<td><p>WebService (_Total) \Connection 시도/초</p></td>
<td><p>웹 서비스에 대 한 연결을 시도 하 고 있는 속도 표시 합니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>웹 서비스 (_Total) \Other 요청 방법/초</p></td>
<td><p>속도 HTTP 요청 사항이 표시 옵션을 사용 하지, 가져오기, 향해, 게시, 배치, 삭제, 추적, 이동, 복사, MKCOL, PROPFIND, PROPPATCH, 검색, 잠금 또는 잠금해제 방법입니다. 현재 사용자 부하를 결정합니다.</p></td>
</tr>
</tbody>
</table>


## 작업 부하 관리 카운터

다음 표에서 Exchange 작업 부하 관리 카운터에 대 한 정보를 표시 합니다. 이러한 카운터는 작업 부하 관리 사용량이 많지 않은 시간 동안 백그라운드에서 작업을 실행할 수 있으므로 모니터링 하는 것이 중요 합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>카운터</p></td>
<td><p>설명</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement 작업 (*) \ActiveTasks</p></td>
<td><p>작업 관리에 대 한 배경에서 현재 실행 중인 활성 작업의 수를 표시 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>MSExchange WorkloadManagement 작업 (*) \CompletedTasks</p></td>
<td><p>관리 작업을 완료 된 작업의 수를 표시 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MSExchange WorkloadManagement 작업 (*) \QueuedTasks</p></td>
<td><p>현재 대기 처리 대기 하는 관리 작업 작업의 수를 표시 합니다.</p></td>
</tr>
</tbody>
</table>

