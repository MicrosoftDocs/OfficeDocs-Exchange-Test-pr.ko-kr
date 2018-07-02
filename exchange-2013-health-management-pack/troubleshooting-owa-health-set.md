---
title: OWA 상태 설정 문제해결
TOCTitle: OWA 상태 설정 문제해결
ms:assetid: eae9dbd7-2ce6-43ce-b9a1-b114fd0c3ab4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.owa(v=EXCHG.150)
ms:contentKeyID: 53275585
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# OWA 상태 설정 문제해결

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Outlook Web App 서비스의 전반적인 상태를 모니터링 하는 Outlook Web App (OWA) 상태 설정 합니다.

알림이 표시 되도록 지정 하는 경우에 Outlook Web App 임을 문제가 있는 사용자가 Outlook Web App 를 사용 하 여 자신의 사서함에 액세스 하지 못하게 할 수 있는 상태가 양호 하지 않습니다.

## 설명

Outlook Web App 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>프로브</th>
<th>상태 설정</th>
<th>종속성</th>
<th>연결된 모니터</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OwaCtpProbe</p></td>
<td><p>Outlook Web App</p></td>
<td><p>Active Directory</p>
<p>정보 저장소</p></td>
<td><p>OwaCtpMonitor</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 일반적인 문제

다음과 같은 몇가지 이유로이 프로브 실패할 수 있습니다. 다음은 일반적인 이유 중입니다.

  - 모니터링 되는 클라이언트 액세스 서버 (CA)에서 호스트 되는 Outlook Web App 응용 프로그램 풀이 응답 하지 않습니다, 또는 사서함 서버에서 호스팅하는 응용 프로그램 풀이 응답 하지 않습니다.

  - CAS가 네트워킹 문제가 발생 하 고 사서함 서버나 도메인 컨트롤러에 연결할 수 없습니다.

  - 모니터링 계정 자격 증명이 잘못되었습니다.

  - 사용자의 데이터베이스가 탑재 되지 되었거나 정보 저장소 해당 사서함에 액세스할 수 없습니다.

  - 정보 저장소 응답 하지 않습니다.

  - 도메인 컨트롤러가 응답하지 않습니다.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸 을 열고 경고를 생성 하는 상태 집합의 세부 정보를 검색 하려면 다음 명령을 실행 합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        Outlook Web App 상태 server1. contoso.com, 다음 명령을 실행 하는 방법에 대 한 세부 정보를 설정 합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "OWA"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예, 모니터링 프로브 *server1.contoso.com*에서 Exchange ActiveSync 를 만들려면 다음 명령을 실행 합니다.
        
            Invoke-MonitoringProbe -Identity ActiveSync.Protocol\ActiveSyncSelfTestProbe -Server server1.contoso.com
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## OwaCtpMonitor 복구 작업

상태 집합에서 전자 메일 알림을 다음 정보가 표시 됩니다.

  - 경고를 보낸 서버의 이름

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)  
    
    **참고 사항**   이 문제를 해결 하기 위해 전체 예외 추적에 정보를 사용할 수 있습니다. 프로브에서 생성 된 예외는 프로브 실패 이유를 설명 하는 실패 이유를 포함 합니다. 예, 예외는 다음 포함 됩니다.
    
      - **MissingKeyword**   서버 응답에서 예상 되는 키워드를 찾지 못했습니다. 이 경우 예외가 예상 되는 키워드를 포함합니다.
    
      - **NameResolution**   지정 된 서버 이름을 확인 하기 위해 DNS 확인 실패 합니다.
    
      - **NetworkConnection**   프로브 카페에서 OWA 응용 프로그램 풀에 연결 하려고 하면 네트워크 연결 오류를 수신 합니다.
    
      - **UnexpectedHttpResponseCode**   응답 한 예기치 않은 HTTP 코드를 했습니다. 등 서버는 HTTP **503** 코드를 반환 합니다.
    
      - **RequestTimeout**   서버 시간 초과로 클라이언트 요청에 응답 합니다.
    
      - **ScenarioTimeout**   프로브 성공적으로 마쳤으나 걸린 1 분 이상이 작업을 수행 합니다. 이것은 보통 오버 로드 되는 시스템을 나타냅니다.
    
      - **OwaErrorPage** Outlook Web App 오류 페이지를 반환 합니다. 오류를 발생 시킨 오류의 이름은 예외 메시지에서 일반적으로 사용할 수 있습니다.   
    
      - **OwaMailboxErrorPage** Outlook Web App 사서함 저장소와 관련 된 오류를 포함 하는 오류 페이지를 반환 합니다. 이 문제는 일반적으로 사서함 저장소 다운 되었거나 사서함을 분리 되는 나타냅니다.   
    
    예외 추적 **FailingComponent** 라는 하는 중요 한 필드를 포함 합니다. 프로브 다음 예제에서와 같이 사용 하 여 오류를 확인 하려고 시도 합니다.
    
      - **사서함**   프로브 Outlook Web App 도달할 수 있지만 사서함 저장소에 연결할 수 없습니다. 이 경우에 프로브 실패 또는 사서함 액세스 대기 시간에 실패 하 고 **ScenarioTimeout** 오류를 생성 하는 프로브를 발생 시킨 합니다. 이러한 종류의 오류가 발생 했을 때에 사서함 서버의 상태를 확인 해야 합니다.
    
      - **Active Directory**    프로브 Outlook Web App 도달할 수 있지만 Active Directory 에 연결할 수 없습니다. 이 경우에 프로브 실패 했거나 발생할 프로브 제한 시간 Active Directory 통화 대기 시간에 있습니다. 이러한 유형의 오류는 발생 하는 경우 도메인 컨트롤러의 상태를 확인 하 고도 CA 및 사서함 서버 및 도메인 컨트롤러 간의 네트워크 연결을 확인 해야 합니다.
    
      - **Owa**   이 일반적으로 Outlook Web App 레이어 내부 오류가 발생 했음을 의미 합니다. 이러한 종류의 오류가 발생 했을 때 CA 및 사서함 서버에서 Outlook Web App 프로세스의 상태를 확인 하 고도 네트워크 연결을 확인 해야 합니다.
    
    예외에는 가장 최근의 HTTP 요청을 받고 응답 정보를 프로브 실패 하기 전에 받은 들어 있습니다. 에스컬레이션 본문 로그 검색에 대 한 경로 포함 합니다. 전체 HTTP 웹 요청 및 프로브 실패 했을 때 전송 된 응답을 확인 하려면이 정보를 사용할 수 있습니다. 이 파일만 로그온 시도 실패 기록 하기 때문에 실패 한 프로브에 대해서만 데이터를 포함 합니다. 이 정보를 가져올 테스트에 실패 한 이유의 완벽 하 게 보기를 사용할 수 있습니다.

  - 어떻게 낮은 가용성 메트릭 (%) x 장식 합니다.

  - 프로브에 대 한 전체 HTTP 요청 추적을 포함 하는 폴더에 대 한 전체 경로입니다. 기본적으로이 정보는 *\<ExchangeServer\>*\\Logging\\Monitoring\\OWA\\ClientAccessProbe 폴더에 있습니다.

  - 경고가 발생 한 날짜와 시간입니다.

이 문제를 해결하려면 다음 단계를 수행합니다.

1.  테스트 사용자 계정을 만들고 테스트 사용자 계정을 사용 하 여 CAS에 로그온 합니다. 예, https:// *\<servername\>*/owa를 사용 하 여 로그온 합니다.
    
    이 오류가 발생 하는 경우에 사서함 서버 아니라 특정 CAS에 문제가 발생 되었는지 확인 하려면 다른 CA 서버를 사용 하 여 테스트 합니다.

2.  CA 및 사서함 서버 간의 네트워크 연결을 확인 합니다. Ping.exe를 사용 하 여 각 서버가 응답 하는지 확인 합니다.

3.  OWA에 대 한 경고를 확인 합니다. 특정 사서함 서버에 영향을 주는 문제를 나타낼 수 있는 프로토콜 상태 설정 합니다. 자세한 내용은 [OWA 문제를 해결 합니다. 프로토콜 상태 설정](troubleshooting-owa-protocol-health-set.md)을 참조 하십시오.

4.  IIS 관리자를 시작 하 고 MSExchangeOwaAppPool 응용 프로그램 풀이 CA에서 실행 되 고 있는지 확인 하려면 문제를 보고 하는 서버에 연결 합니다.

5.  IIS 관리자에서 기본 웹사이트 실행 되 고 있는지 확인 합니다.

6.  실패 한 프로브에 대 한 사서함 데이터베이스를 찾아 사서함 데이터베이스 사서함 서버에서 활성 상태 이며 사서함 저장소의 상태가 정상 인지 확인 합니다. 실패 한 데이터베이스 GUID 정보를 찾으려면 전체 예외 추적 정보를 엽니다. 각 오류는 다음 예와 유사 하는 항목을 포함 해야 합니다.
    
    대상으로 시작 하 여 Owa 프로브: https://localhost/owa/, 사용자 이름: *HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com*

7.  HealthMailbox GUID를 복사 하 고 셸에서 다음 명령을 실행 합니다.
    
        Get-Mailbox -Monitoring -Identity <username>
    
    예, 다음 명령을 실행 합니다.
    
        Get-Mailbox -Monitoring -Identity HealthMailboxdf8b87828ab0427cb91e985bbdfcec62@yourdomain.com
    
    반환 된 개체는 사용자의 데이터베이스 이름을 찾아 현재 활성 상태인 데이터베이스가 있는 확인할 수 있습니다.

8.  사이트 간에 리디렉션을 구성한 경우 실패 하 고 MissingKeyword 오류를 생성 하는 프로브 표시 될 수 있습니다. 기본적으로 CA 프로브 모든 위치에 대 한 계정에서 실행 하기 때문에 발생 하는이 하 고 있으므로 리디렉션을 사용 하는 경우 다른 사이트에서 CA를 테스트 하는 프로브를 시도 하지 않습니다. 이 문제를 해결 하려면 각 사이트에서 서버 MonitoringGroups에 포함 되는 있는지 확인 합니다. 지정한 모니터링 그룹에서 CA 서버를 같은 그룹에 사서함 서버와 함께 테스트합니다.
    
    서버에 대 한 모니터링 그룹을 확인 하려면 다음 명령을 실행 합니다.
    
        Get-ExchangeServer | ft MonitoringGroup
    
    서버에 모니터링 그룹을 수정 하려면 **Set-ExchangeServer** cmdlet과 함께 *MonitoringGroup* 매개 변수를 사용 합니다. 예, 다음을 사용 합니다.
    
        Set-ExchangeServer -Identity "ServerName" -MonitoringGroup "Primary"

9.  IIS 관리자에서 **응용 프로그램 풀** 을 클릭 한 후 Exchange 관리 셸 에서 다음 명령을 실행 하 여 **MSExchangeOWAAppPool** 응용 프로그램 풀을 재순환 합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeOWAAppPool

10. 문제가 여전히 존재 하는 Verifying 섹션의 2c 단계에 나와있는 대로 관련된 프로브를 다시 실행 합니다.

11. 문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하거나 다음 명령을 실행하여 IIS 서비스를 재순환합니다.
    
        Iisreset /noforce

12. 문제가 여전히 존재 하는 Verifying 섹션의 2c 단계에 나와있는 대로 관련된 프로브를 다시 실행 합니다.

13. 그래도 문제가 계속 발생하면 서버를 다시 시작하십시오.

14. 서버를 다시 시작한 후 문제가 여전히 존재 하는 Verifying 섹션의 2c 단계에 나와있는 대로 관련된 프로브를 다시 실행 합니다.

15. 프로브 계속 실패 하면, 하는 경우에이 문제를 해결 하기 위해 도움이 필요할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

