---
title: 'Exchange 서버 운영 체제의 바이러스 백신 소프트웨어: Exchange 2013 Help'
TOCTitle: Exchange 서버 운영 체제의 바이러스 백신 소프트웨어
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 50483520
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 서버 운영 체제의 바이러스 백신 소프트웨어

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-07-22_

이 항목에서는 Microsoft Exchange Server 2013을 실행하는 컴퓨터에서 파일 수준 바이러스 백신 프로그램을 사용하는 경우의 효과에 대해 설명합니다. 이 항목에서 설명하는 권장 사항을 구현하면 Exchange 조직의 보안 및 상태를 향상할 수 있습니다.

파일 수준 검색 프로그램은 널리 사용되고 있지만 잘못 구성하는 경우 Exchange 2013에서 문제가 발생할 수 있습니다. 파일 수준 검색 프로그램에는 다음 두 가지 유형이 있습니다.

  - *메모리 상주 파일 수준 검색*은 메모리에 항상 로드되어 있는 파일 수준 바이러스 백신 소프트웨어의 일부분을 가리키며 하드 디스크와 컴퓨터 메모리에서 사용되는 모든 파일을 검사합니다.

  - *주문형 파일 수준 검색*은 하드 디스크에서 수동으로 또는 일정에 따라 파일을 검색하도록 구성할 수 있는 파일 수준 바이러스 백신 소프트웨어 부분을 가리킵니다. 일부 바이러스 백신 소프트웨어 버전은 바이러스 서명이 업데이트되면 자동으로 주문형 검색을 시작하여 모든 파일이 최신 서명으로 검색되도록 합니다.

Exchange 2013에서 파일 수준 검색 프로그램을 사용하면 다음과 같은 문제가 발생할 수 있습니다.

  - 파일 수준 검색 프로그램이 사용 중인 파일을 검색하거나 예약된 간격으로 검색을 수행하는 경우가 있습니다. 이로 인해 Exchange 2013에서 데이터베이스 또는 Exchange 로그 파일을 사용하려 할 때 검색 프로그램이 해당 파일을 잠그거나 격리할 수도 있습니다. 이 작업은 Exchange 2013에서 심각한 오류와 -1018 이벤트 로그 오류를 발생시킬 수 있습니다.

  - 파일 수준 검색 프로그램에서는 스톰 웜(Storm Worm) 바이러스 같은 전자 메일 바이러스에 대한 보호 기능은 제공하지 않습니다. 스톰 웜(Storm Worm)은 전자 메일 메시지를 통해 자체적으로 전파되는 백도어 트로이 목마 프로그램으로, 주기적인 버스트로 스팸을 보내는 데 사용되는 봇넷(botnet)에 감염된 컴퓨터를 연결합니다.

## Exchange 2013에서 파일 수준 검색 프로그램을 사용하기 위한 권장 사항

Exchange 2013 서버에 파일 수준 검색 프로그램을 배포하는 경우에는 디렉터리 제외, 프로세스 제외, 확장명 제외 등, 적절한 제외를 메모리 상주 및 파일 수준 검색 프로그램 모두에 적용해야 합니다. 이 섹션에서는 권장되는 디렉터리 제외, 프로세스 제외 및 확장명 제외에 대해 설명합니다

**목차**

Directory exclusions

Process exclusions

File name extension exclusions

## 디렉터리 제외

파일 수준 바이러스 백신 검색 프로그램을 실행하는 각 Exchange 서버에 대해 특정 디렉터리를 제외해야 합니다. 이 섹션에서는 파일 수준 검색에서 제외해야 하는 디렉터리에 대해 설명합니다

  - **사서함 서버**
    
      - **사서함 데이터베이스**
        
          - Exchange 데이터베이스, 검사점 파일 및 로그 파일. 기본적으로 %ExchangeInstallPath%Mailbox 폴더의 하위 폴더에 있습니다. 사서함 데이터베이스, 트랜잭션 로그 및 검사점 파일의 위치를 확인하려면 다음 명령을 실행합니다. `Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - 데이터베이스 콘텐츠 인덱스. 기본적으로 데이터베이스 파일과 동일한 폴더에 있습니다.
        
          - 그룹 메트릭 파일. 기본적으로 %ExchangeInstallPath%GroupMetrics 폴더에 있습니다.
        
          - 메시지 추적 로그 파일 및 일정 수정 로그 파일 같은 일반 로그 파일. 기본적으로 %ExchangeInstallPath%TransportRoles\\Logs 폴더 및 %ExchangeInstallPath%Logging 폴더의 하위 폴더에 있습니다. 사용 중인 로그 경로를 확인하려면 Exchange 관리 셸에서 다음 명령을 실행하십시오. `Get-MailboxServer <servername> | Format-List *path*`
        
          - 오프라인 주소록 파일. 기본적으로 %ExchangeInstallPath%ClientAccess\\OAB 폴더의 하위 폴더에 있습니다.
        
          - %SystemRoot%\\System32\\Inetsrv 폴더의 IIS 시스템 파일
        
          - 사서함 데이터베이스 임시 폴더: %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **데이터베이스 가용성 그룹의 구성원**
        
          - **사서함 데이터베이스** 목록에 나열된 모든 항목 및 %Windir%\\Cluster에 있는 클러스터 쿼럼 데이터베이스
        
          - 미러링 모니터 디렉터리 파일. 환경의 다른 서버, 일반적으로 사서함 서버와 동일한 컴퓨터에 설치되어 있지 않은 클라이언트 액세스 서버에 있습니다. 기본적으로 감시 디렉터리 파일은 %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>에 있습니다.
    
      - **전송 서비스**
        
          - 메시지 추적 및 연결 로그 같은 로그 파일. 기본적으로 %ExchangeInstallPath%TransportRoles\\Logs 폴더의 하위 폴더에 있습니다. 사용 중인 로그 경로를 확인하려면 Exchange 관리 셸에서 다음 명령을 실행하십시오. `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - Pickup 및 Replay 디렉터리 폴더 메시지입니다. 기본적으로 이러한 폴더는 % ExchangeInstallPath %TransportRoles 폴더 아래의 있습니다. 사용 중인 경로 확인 하려면 Exchange 관리 셸 다음 명령을 실행: `Get-TransportService <servername>| Format-List *dir*path*`
        
          - 큐 데이터베이스, 검사점 및 로그 파일. 기본적으로 %ExchangeInstallPath%TransportRoles\\Data\\Queue 폴더에 있습니다.
        
          - 보낸 사람 신뢰도 데이터베이스, 검사점 및 로그 파일. 기본적으로 %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation 폴더에 있습니다.
        
          - 변환을 수행하는 데 사용되는 임시 폴더
            
              - 기본적으로 내용 변환은 Exchange 서버의 %TMP% 폴더에서 수행됩니다.
            
              - 기본적으로 서식 있는 텍스트 (rtf) MIME/HTML 변환 하는 %ExchangeInstallPath%\\Working\\OleConverter 폴더에서 수행 됩니다.
        
          - 맬웨어 에이전트 및 DLP(데이터 손실 방지)에서 사용되는 콘텐츠 검색 구성 요소. 기본적으로 %ExchangeInstallPath%FIP-FS 폴더에 있습니다.
    
      - **사서함 전송 서비스**
        
          - 연결 로그 같은 로그 파일. 기본적으로 %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox 폴더의 하위 폴더에 있습니다. 사용 중인 로그 경로를 확인하려면 Exchange 관리 셸에서 다음 명령을 실행하십시오. `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **통합 메시징**
        
          - 다른 로캘(예: en-EN 또는 es-ES)에 대한 문법 파일. 기본적으로 %ExchangeInstallPath%UnifiedMessaging\\grammars 폴더의 하위 폴더에 저장됩니다.
        
          - 음성, 인사말 및 알림 메시지 파일. 기본적으로 %ExchangeInstallPath%UnifiedMessaging\\Prompts 폴더의 하위 폴더에 저장됩니다.
        
          - %ExchangeInstallPath%UnifiedMessaging\\voicemail 폴더에 임시 저장된 음성 메일 파일.
        
          - 통합 메시징에 의해 생성된 임시 파일. 기본적으로 %ExchangeInstallPath%UnifiedMessaging\\temp 폴더에 저장됩니다.
    
      - **설치**
        
          - Exchange Server 설치 프로그램 임시 파일입니다. 이러한 파일은 일반적으로 SystemRoot%\\Temp\\ExchangeSetup %에 배치 됩니다.
    
      - **Exchange 검색 서비스**
        
          - 임시 파일을 샌드박스 환경에서 파일 변환을 수행 하기 위해 Exchange 검색 서비스 및 Microsoft Filter Pack 사용 합니다. 이러한 파일은 %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\입니다.

<!-- end list -->

  - **클라이언트 액세스 서버**
    
      - **웹 구성 요소**
        
          - Microsoft Outlook Web App과 함께 사용되는 IIS(인터넷 정보 서비스) 7.0 압축 폴더를 사용하는 서버인 경우. 기본적으로 IIS 7.0의 압축 폴더는 %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files에 있습니다.
        
          - %SystemRoot%\\System32\\Inetsrv 폴더의 IIS 시스템 파일
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET 파일의 하위 폴더
    
      - **POP3 및 IMAP4 프로토콜 로깅**
        
          - POP3 폴더: %ExchangeInstallPath%Logging\\POP3
        
          - IMAP4 폴더: %ExchangeInstallPath%Logging\\IMAP4
    
      - **프런트 엔드 전송 서비스**
        
          - 연결 로그 및 프로토콜 로그 같은 로그 파일. 기본적으로 %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd 폴더의 하위 폴더에 있습니다. 사용 중인 로그 경로를 확인하려면 Exchange 관리 셸에서 다음 명령을 실행하십시오. `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **설치**
        
          - Exchange Server 설치 프로그램 임시 파일입니다. 이러한 파일은 일반적으로 SystemRoot%\\Temp\\ExchangeSetup %에 배치 됩니다.

맨 위로 이동

## 프로세스 제외

이제 다수의 파일 수준 검색 프로그램은 프로세스의 검색을 지원하므로, 정상적인 프로세스가 잘못 검색되면 Microsoft Exchange에 부정적인 영향을 줄 수 있습니다. 그러므로 다음 프로세스를 파일 수준 검색 프로그램에서 제외해야 합니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>프로세스</th>
<th>경로</th>
<th>설명</th>
<th>서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>Active Directory Lightweight 디렉터리 서비스 (AD LDS) 가입 된 Edge 전송 서버에 있습니다.</p></td>
<td><p>Edge 전송 서버</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport service 작업자 프로세스</p></td>
<td><p>사서함 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>콘텐츠 검색 구성 요소는 맬웨어 에이전트 및 DLP에 사용 되는 합니다.</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Microsoft Exchange 검색 호스트 컨트롤러 서비스 (HostControllerService)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>IIS(인터넷 정보 서비스)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 스팸 방지 업데이트 서비스 (MSExchangeAntispamUpdate)</p></td>
<td><p>사서함 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>콘텐츠 필터 에이전트</p></td>
<td><p>사서함 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange에 대 한 진단 유틸리티 서비스 (MSExchangeDiagnostics)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Active Directory 토폴로지 서비스 (MSExchangeADTopology)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 자격 증명 서비스 (MSExchangeEdgeCredential)</p></td>
<td><p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange EdgeSync 서비스 (MSExchangeEdgeSync)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 서비스 (MSExchangeImap4)</p></td>
<td><p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange IMAP4 백엔드 서비스 (MSExchangeIMAP4BE)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Microsoft Exchange POP3 서비스 (MSExchangePop3)</p></td>
<td><p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Microsoft Exchange POP3 백엔드 서비스 (MSExchangePOP3BE)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 서비스 호스트 서비스 (MSExchangeServiceHost)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange RPC 클라이언트 액세스 서비스 (MSExchangeRPC)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Search 서비스 (MSExchangeFastSearch)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 서비스 호스트 서비스 (MSExchangeServiceHost)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 정보 저장소 서비스 (MSExchangeIS)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 정보 저장소 서비스 작업자 프로세스</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Microsoft Exchange 통합 메시징 호출 라우터 서비스 (MSExchangeUMCR)</p></td>
<td><p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange DAG 관리 서비스 (MSExchangeDagMgmt)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 사서함 전송 배달 서비스 (MSExchangeDelivery)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 프런트엔드 전송 서비스 (MSExchangeFrontEndTransport)</p></td>
<td><p>클라이언트 액세스 서버</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Health Manager 서비스 (MSExchangeHM)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Health Manager 서비스 작업자 프로세스</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 사서함 도우미 서비스 (MSExchangeMailboxAssistants)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 사서함 복제 서비스 (MSExchangeMailboxReplication)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 마이그레이션 워크플로 서비스 (MSExchangeMigrationWorkflow)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Replication service (MSExchangeRepl)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 사서함 전송 서비스 (MSExchangeSubmission)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange Transport service (MSExchangeTransport)</p></td>
<td><p>사서함 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 전송 로그 검색 서비스 (MSExchangeTransportLogSearch)</p></td>
<td><p>사서함 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 제한 서비스 (MSExchangeThrottling)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Microsoft Exchange Search 서비스 (MSExchangeFastSearch)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>서식 있는 텍스트 (rtf) 메시지를 외부 받는 사람에 대 한 MIME/HTML로 변환합니다.</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Microsoft Exchange Search 서비스 (MSExchangeFastSearch)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Exchange 관리 셸</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p>
<p>Edge 전송 서버</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>콘텐츠 검색 구성 요소는 맬웨어 에이전트 및 DLP에 사용 되는 합니다.</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>콘텐츠 검색 구성 요소는 맬웨어 에이전트 및 DLP에 사용 되는 합니다.</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>WebReady 문서 Outlook Web App의 보기입니다.</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 통합 메시징 서비스 (MSExchangeUM)</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Microsoft Exchange 통합 메시징 서비스 작업자 프로세스</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>콘텐츠 검색 구성 요소는 맬웨어 에이전트 및 DLP에 사용 되는 합니다.</p></td>
<td><p>사서함 서버</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>IIS(인터넷 정보 서비스)</p></td>
<td><p>사서함 서버</p>
<p>클라이언트 액세스 서버</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 확장명 제외

특정 디렉터리와 프로세스를 제외하는 것과 함께, 디렉터리 제외가 실패하거나 파일이 기본 위치에서 이동한 경우 다음 Exchange 특정 파일 이름 확장명도 제외해야 합니다.

  - 응용 프로그램 관련 확장명
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - 데이터베이스 관련 확장명
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - 오프라인 주소록 관련 확장명:
    
      - .lzx

<!-- end list -->

  - 콘텐츠 인덱스 관련 확장명
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - 통합 메시징 관련 확장명
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - 그룹 메트릭 관련 확장명
    
      - .dsc
    
      - .txt

맨 위로 이동

