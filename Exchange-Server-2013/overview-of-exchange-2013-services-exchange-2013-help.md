---
title: 'Exchange 2013 서비스 개요: Exchange 2013 Help'
TOCTitle: Exchange 2013 서비스 개요
ms:assetid: 2ed45d18-2ff3-4099-b841-050eb16a416b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423542(v=EXCHG.150)
ms:contentKeyID: 74479251
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 서비스 개요

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-10-20_

Exchange Server 2013 를 설치 하는 동안 설치 프로그램을 Microsoft Windows 에서 새 서비스를 설치 하는 작업의 집합을 실행 합니다. 서비스는 Windows 서비스 제어 관리자 서버를 시작 하는 동안 시작할 수 있는 백그라운드 프로세스입니다. 서비스는 실행 파일 독립적으로 및 관리 작업을 수행 하지 않고 작동 하도록 설계 되었습니다. 서비스는 그래픽 사용자 인터페이스 (GUI) 모드 또는 콘솔 모드를 사용 하 여 실행할 수 있습니다.

Exchange 의 이전 버전을 모두 서비스로 구현 되는 구성 요소를 포함 합니다. 각 Exchange 서버 역할 서비스의 일부인 (또는 하 여 필요할 수)를 포함 서버 역할을 해당 기능을 수행 합니다. 메모는 일부 서비스가 활성 상태가 특정 기능을 사용 하는 경우입니다.

이 항목의 섹션에서는 사서함 서버, 클라이언트 액세스 서버 및 Edge 전송 서버에서 Exchange 2013 통해 설치 되는 다양 한 서비스에 설명 합니다. 선택적으로 레이블이 지정 된 서비스에 대 한 조직에는 서비스에 의해 제공 되는 기능이 필요 하지 않습니다 판단 되 면 서비스를 비활성화할 수 있습니다.

## Exchange Exchange 2013 사서함 서버 제공 서비스

다음 표에서 사서함 서버에 설치 된 Exchange 서비스를 설명 합니다.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>서비스 이름</th>
<th>서비스 약식 이름</th>
<th>설명 및 종속성</th>
<th>기본 시작 유형</th>
<th>보안 컨텍스트</th>
<th>종속성</th>
<th>필수/선택</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Exchange 서비스에 Active Directory 토폴로지 정보를 제공합니다. 이 서비스를 중지 하는 경우 대부분의 Exchange 서비스를 시작할 수 없습니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Net.TCP 포트 공유 서비스</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 스팸 방지 업데이트</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Exchange SmartScreen 스팸 정의 업데이트를 제공 합니다.</p>

> [!NOTE]
> 2016년 11월 1일, Microsoft가 Exchange 및 Outlook에서 SmartScreen 필터에 대한 스팸 정의 업데이트 생성을 중지했습니다. 기존 SmartScreen 스팸 정의는 제자리에 남게 되지만 시간 경과에 따라 효율성이 저하될 가능성이 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 및 Exchange에서 SmartScreen에 대한 지원 삭제</A>를 참조하세요.


</td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange DAG 관리</p></td>
<td><p>MSExchangeDagMgmt</p></td>
<td><p>데이터베이스 가용성 그룹 (Dag)의 사서함 서버에 대 한 저장소 및 데이터베이스 레이아웃 관리를 제공합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p>
<p>Net.TCP 포트 공유 서비스</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 진단</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Exchange 서버 상태를 모니터링 하는 에이전트를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>없음</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange EdgeSync</p></td>
<td><p>MSExchangeEdgeSync</p></td>
<td><p>보안 LDAP 채널을 통해 UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) 가입 된 Edge 전송 서버에서 사서함 서버와 구성 및 받는 사람 데이터를 복제합니다.</p>
<p>모든 구독 된 Edge 전송 서버를 설치 하지 않은 경우에이 서비스를 비활성화할 수 있습니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 상태 관리자</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Exchange 서버의 핵심 구성 요소 상태를 모니터링 하는 관리 되는 가용성의 일부입니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Windows 이벤트 로그</p>
<p>Windows 관리 계측</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4 백엔드</p></td>
<td><p>MSExchangeIMAP4BE</p></td>
<td><p>프록시 클라이언트 연결을 수신 된 클라이언트 액세스 서버에서 IMAP4 서비스에서. 기본적으로이 서비스가 실행 중이 아닌 되므로이 서비스를 시작할 때까지 IMAP4 클라이언트 Exchange 서버에 연결할 수 없습니다.</p>
<p>모든 IMAP4 클라이언트를 설치 하지 않은 경우에이 서비스를 비활성화할 수 있습니다.</p></td>
<td><p>수동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 정보 저장소</p></td>
<td><p>MSExchangeIS</p></td>
<td><p>서버에서 사서함 데이터베이스를 관리합니다. 이 서비스를 중지 하는 경우에 서버에서 사서함 데이터베이스는 사용할 수 없습니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p>
<p>원격 프로시저 호출 (RPC)</p>
<p>서버</p>
<p>Windows 이벤트 로그</p>
<p>워크스테이션</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 사서함 도우미</p></td>
<td><p>MSExchangeMailboxAssistants</p></td>
<td><p>서버에서 사서함 데이터베이스에서 사서함의 백그라운드 처리를 수행합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 사서함 복제</p></td>
<td><p>MSExchangeMailboxReplication</p></td>
<td><p>프로세스 사서함 이동 및 요청을 이동 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p>
<p>Net.TCP 포트 공유 서비스</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 사서함 전송 배달</p></td>
<td><p>MSExchangeDelivery</p></td>
<td><p>Microsoft Exchange (로컬 또는 원격 사서함 서버)에서 전송 서비스 SMTP 메시지를 받아서 RPC를 사용 하 여 로컬 사서함 데이터베이스로 전달 합니다.</p></td>
<td><p>자동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 사서함 전송 제출</p></td>
<td><p>MSExchangeSubmission</p></td>
<td><p>로컬 사서함 데이터베이스에서 RPC 메시지를 받아서 SMTP를 통해 Microsoft Exchange (로컬 또는 원격 사서함 서버)에서 전송 서비스 전송 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange POP3 백엔드</p></td>
<td><p>MSExchangePOP3BE</p></td>
<td><p>클라이언트 액세스 서버에서 POP3 서비스에서 프록시 클라이언트 연결을 받습니다. 기본적으로이 서비스가 실행 중이 아닌 되므로이 서비스를 시작할 때까지 POP3 클라이언트가 Exchange 서버에 연결할 수 없습니다.</p></td>
<td><p>수동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 복제 서비스</p></td>
<td><p>MSExchangeRepl</p></td>
<td><p>가용성 그룹 (Dag) 데이터베이스에서 사서함 데이터베이스에 대 한 복제 기능을 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange RPC 클라이언트 액세스</p></td>
<td><p>MSExchangeRPC</p></td>
<td><p>Exchange 에 대 한 클라이언트 RPC 연결을 관리합니다.</p></td>
<td><p>자동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 검색</p></td>
<td><p>MSExchangeFastSearch</p></td>
<td><p>콘텐츠 검색의 성능이 향상 되는 사서함 콘텐츠 인덱싱를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 검색 호스트 컨트롤러</p></td>
<td><p>HostControllerService</p></td>
<td><p>로컬 Exchange 서버에서 응용 프로그램에 대 한 배포 및 관리 서비스를 제공합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>HTTP 서비스</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Windows Server 백업을 위한 Microsoft Exchange Server 확장 기능</p></td>
<td><p>WSBExchange</p></td>
<td><p>Windows Server Exchange 서버 데이터 백업 및 복원 하는 백업 수 있습니다.</p></td>
<td><p>수동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>없음</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 서비스 호스트</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>자신의 서비스를 설치 하지 않은 Exchange 구성 요소에 대 한 서비스 호스트를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 조정</p></td>
<td><p>MSExchangeThrottling</p></td>
<td><p>(이전의 사용자 제한) 사용자 작업의 속도 제한 하는 사용자 작업 부하 관리를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 전송</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>SMTP 서버와 전송 스택을 제공합니다.</p></td>
<td><p>자동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p>
<p>Microsoft 관리 서비스를 필터링합니다.</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 전송 로그 검색</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>전송 로그 파일 (예: 추적 메시지)에 대 한 원격 검색 기능을 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 통합 메시징</p></td>
<td><p>MSExchangeUM</p></td>
<td><p>UM (통합 메시징) 기능을 제공: Exchange 에 저장할 음성 및 팩스 메시지를 허용 하 고 전자 메일, 음성 메일, 일정, 연락처 또는 자동 전화 교환에 사용자가 전화 액세스를 제공 합니다. 이 서비스를 중지 하는 경우 통합 메시징을 사용할 수 없습니다.</p>
<p>UM을 사용 하지 않는 경우에이 서비스를 비활성화할 수 있습니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>CNG 키 격리</p>
<p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 클라이언트 액세스 서버에서 Exchange 서비스

다음 표에서 클라이언트 액세스 서버에 설치 된 Exchange 서비스를 설명 합니다.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>서비스 이름</th>
<th>서비스 약식 이름</th>
<th>설명 및 종속성</th>
<th>기본 시작 유형</th>
<th>보안 컨텍스트</th>
<th>종속성</th>
<th>필수/선택</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>MSExchangeADTopology</p></td>
<td><p>Exchange 서비스에 Active Directory 토폴로지 정보를 제공합니다. 이 서비스를 중지 하는 경우 대부분의 Exchange 서비스를 시작할 수 없습니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Net.TCP 포트 공유 서비스</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 진단</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Exchange 서버 상태를 모니터링 하는 에이전트를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>없음</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange Frontend 전송</p></td>
<td><p>MSExchangeFrontEndTransport</p></td>
<td><p>Microsoft Exchange 사서함 서버의 전송 서비스 외부 호스트에서 프록시 SMTP 연결 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 상태 관리자</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Exchange 서버의 핵심 구성 요소 상태를 모니터링 하는 관리 되는 가용성의 일부입니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Windows 이벤트 로그</p>
<p>Windows 관리 계측</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange IMAP4</p></td>
<td><p>MSExchangeIMAP4</p></td>
<td><p>프록시 IMAP4 클라이언트에 대 한 연결 사서함 서버에 있는 IMAP4 서비스입니다. 기본적으로이 서비스가 실행 중이 아닌 되므로이 서비스를 시작할 때까지 IMAP4 클라이언트 Exchange 서버에 연결할 수 없습니다.</p>
<p>모든 IMAP4 클라이언트를 설치 하지 않은 경우에이 서비스를 비활성화할 수 있습니다.</p></td>
<td><p>수동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange POP3</p></td>
<td><p>MSExchangePOP3</p></td>
<td><p>프록시 POP3 클라이언트에 대 한 연결 사서함 서버에 있는 IMAP4 서비스입니다. 기본적으로이 서비스가 실행 중이 아닌 되므로이 서비스를 시작할 때까지 POP3 클라이언트가 Exchange 서버에 연결할 수 없습니다.</p></td>
<td><p>수동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 검색 호스트 컨트롤러</p></td>
<td><p>HostControllerService</p></td>
<td><p>로컬 Exchange 서버에서 응용 프로그램에 대 한 배포 및 관리 서비스를 제공합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>HTTP 서비스</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 서비스 호스트</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>자신의 서비스를 설치 하지 않은 Exchange 구성 요소에 대 한 서비스 호스트를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 통합 메시징 통화 라우터</p></td>
<td><p>MSExchangeUMCR</p></td>
<td><p>사서함 서버에서 통합 메시징 서비스에 대 한 UM 클라이언트 연결을 리디렉션합니다.</p>
<p>UM을 사용 하지 않는 경우에이 서비스를 비활성화할 수 있습니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>CNG 키 격리</p>
<p>Microsoft Exchange Active Directory 토폴로지</p></td>
<td><p>옵션</p></td>
</tr>
</tbody>
</table>


## Exchange 2013 Edge 전송 서버에서 Exchange 서비스

다음 표에서 Edge 전송 서버에 설치 된 Exchange 서비스를 설명 합니다.


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>서비스 이름</th>
<th>서비스 약식 이름</th>
<th>설명</th>
<th>기본 시작 유형</th>
<th>보안 컨텍스트</th>
<th>종속성</th>
<th>필수/선택</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>ADAM_MSExchange</p></td>
<td><p>Edge 전송 서버에 구성 데이터 및 받는 사람 데이터를 저장합니다. 이 서비스는 UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS) Exchange 설치 하 여 자동으로 만들어지는의 명명 된 인스턴스를 나타냅니다.</p></td>
<td><p>자동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>COM + 이벤트 시스템</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 스팸 방지 업데이트</p></td>
<td><p>MSExchangeAntispamUpdate</p></td>
<td><p>Exchange SmartScreen 스팸 정의 업데이트를 제공 합니다.</p>

> [!NOTE]
> 2016년 11월 1일, Microsoft가 Exchange 및 Outlook에서 SmartScreen 필터에 대한 스팸 정의 업데이트 생성을 중지했습니다. 기존 SmartScreen 스팸 정의는 제자리에 남게 되지만 시간 경과에 따라 효율성이 저하될 가능성이 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=835894">Outlook 및 Exchange에서 SmartScreen에 대한 지원 삭제</A>를 참조하세요.


</td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>옵션</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 자격 증명 서비스</p></td>
<td><p>MSExchangeEdgeCredential</p></td>
<td><p>UNRESOLVED_TOKEN_VAL(exADLDS_1st) (AD LDS)에서 자격 증명의 변경 내용을 모니터링 하 고 Edge 전송 서버에서 변경 된 내용을 설치 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 진단</p></td>
<td><p>MSExchangeDiagnostics</p></td>
<td><p>Exchange 서버 상태를 모니터링 하는 에이전트를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>없음</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 상태 관리자</p></td>
<td><p>MSExchangeHM</p></td>
<td><p>Exchange 서버의 핵심 구성 요소 상태를 모니터링 하는 관리 되는 가용성의 일부입니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Windows 이벤트 로그</p>
<p>Windows Management Instrumentation</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 서비스 호스트</p></td>
<td><p>MSExchangeServiceHost</p></td>
<td><p>자신의 서비스를 설치 하지 않은 Exchange 구성 요소에 대 한 서비스 호스트를 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>필수</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft Exchange 전송</p></td>
<td><p>MSExchangeTransport</p></td>
<td><p>SMTP 서버와 전송 스택을 제공합니다.</p></td>
<td><p>자동</p></td>
<td><p>네트워크 서비스</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>필수</p></td>
</tr>
<tr class="even">
<td><p>Microsoft Exchange 전송 로그 검색</p></td>
<td><p>MSExchangeTransportLogSearch</p></td>
<td><p>전송 로그 파일 (예: 추적 메시지)에 대 한 원격 검색 기능을 제공 합니다.</p></td>
<td><p>자동</p></td>
<td><p>로컬 시스템</p></td>
<td><p>Microsoft Exchange ADAM</p></td>
<td><p>옵션</p></td>
</tr>
</tbody>
</table>

