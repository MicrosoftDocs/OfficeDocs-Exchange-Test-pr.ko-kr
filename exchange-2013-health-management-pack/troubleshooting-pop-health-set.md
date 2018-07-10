---
title: POP 상태 설정 문제해결
TOCTitle: POP 상태 설정 문제해결
ms:assetid: 6114e9fe-d037-4cb9-a643-933eb5fabc45
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.pop(v=EXCHG.150)
ms:contentKeyID: 53275586
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# POP 상태 설정 문제해결

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

POP 상태 설정은 Microsoft Exchange POP3 서비스의 전체적인 상태와 가용성 및 POP3 클라이언트 연결을 모니터링합니다. POP 상태 설정은 다음 상태 설정과 밀접하게 관련됩니다.

  - [POP 문제를 해결 합니다. 프로토콜 상태 설정](troubleshooting-pop-protocol-health-set.md)

  - [POP 문제를 해결 합니다. 프록시 상태 설정](troubleshooting-pop-proxy-health-set.md)

POP 서비스가 비정상임을 지정하는 경고가 수신된 경우 이는 사용자가 Exchange 환경에서 POP3을 사용하여 자신의 사서함에 액세스할 수 없는 문제를 나타냅니다.

## 설명

POP 서비스는 다음 프로브와 모니터를 사용하여 모니터링됩니다.


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
<td><p>PopCTPProbe</p></td>
<td><p>POP</p></td>
<td><p>Active Directory</p>
<p>인증</p>
<p>사서함 서버 인증</p>
<p>정보 저장소</p>
<p>고가용성</p>
<p>네트워크</p></td>
<td><p>PopCTPMonitor(POP 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>PopProxyTestProbe</p></td>
<td><p>POP.Proxy</p></td>
<td><p>없음</p></td>
<td><p>PopProxyTestMonitor(POP.Proxy 상태 설정)</p></td>
</tr>
<tr class="odd">
<td><p>PopDeepTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>Active Directory</p>
<p>인증</p>
<p>정보 저장소</p>
<p>고가용성</p></td>
<td><p>PopDeepTestMonitor(POP.Protocol 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>PopSelfTestProbe</p></td>
<td><p>POP.Protocol</p></td>
<td><p>없음</p></td>
<td><p>PopSelfTestMonitor(POP.Protocol 상태 설정)</p>
<p>AverageCommandProcessingTimeGt60sMonitor(POP 상태 설정)</p></td>
</tr>
</tbody>
</table>


## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예를 들어 server1.contoso.com에 대한 POP 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "POP"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예를 들어 실패한 모니터가 **PopCTPMonitor**라고 가정합니다. 해당 모니터와 연결된 프로브는 **PopCTPProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe POP\PopCTPProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## PopTestDeepMonitor 및 PopSelfTestMonitor 복구 작업

이 모니터 경고는 일반적으로 사서함 서버에서 발생합니다.

1.  POP3 백 엔드 서비스를 다시 시작합니다. 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/aa997475\(v=exchg.150\))를 참조하십시오.

2.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  프로브가 계속 실패하면 다음 명령을 사용하여 사서함 서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  모든 데이터베이스가 사서함 서버에서 제거되고 나면 데이터베이스가 이동되었는지 확인해야 합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status

5.  서버가 데이터베이스의 어떠한 활성 복사본도 호스트하지 않는지 확인합니다. 그런 다음 서버를 다시 시작합니다.

6.  서버를 다시 시작한 후 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

7.  프로브가 정상적으로 실행되면 다음 명령을 실행하여 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

8.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## POPCTPMonitor 복구 작업

이 모니터 경고는 일반적으로 CAS(CA 서버)에서 발생합니다.

1.  CAS 역할을 실행하는 서버에서 POP3 서비스를 다시 시작합니다. 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/aa997475\(v=exchg.150\))를 참조하십시오.

2.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  문제가 여전히 존재하면 Windows PowerShell에서 다음 명령을 실행합니다.
    
    1.  ``` 
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $true
        ```
    
    2.  CAS 역할을 실행하는 서버에서 POP3 서비스를 다시 시작합니다.
    
    3.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.
    
    4.  다음 명령을 실행한 후 로그 파일의 위치를 찾습니다.
        
            Get-PopSettings -server <CAS server name>
    
    5.  다음 명령을 실행하여 타임스탬프와 프로브를 비교하여 명령을 처리하는 사서함 서버를 확인합니다.
        
            Get-ServerHealth <mailbox server name> | ?{ $_.HealthSetName -like "POP*"}
    
    6.  이러한 서버 중 어느 서버라도 비정상으로 보고되면 PopTestDeepMonitor and PopSelfTestMonitor Recovery Actions 섹션에 나열된 단계를 수행합니다.

4.  사서함 서버가 정상 상태로 보고되면 CAS를 다시 시작합니다.

5.  서버를 다시 시작한 후 Verifying the issue still exists 섹션의 2c단계에 설명된 대로 관련 프로브를 다시 실행합니다.

6.  다음 명령을 실행하여 프로토콜 로깅을 해제합니다.
    
        Set-PopSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  CAS 역할을 실행하는 서버에서 POP3 서비스를 다시 시작합니다. 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/aa997475\(v=exchg.150\))를 참조하십시오.

8.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## PopProxyTestMonitor 복구 작업

1.  CAS 역할을 실행하는 서버에서 POP3 서비스를 다시 시작합니다. 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/aa997475\(v=exchg.150\))를 참조하십시오.

2.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  프로브가 계속 실패하는 경우 CAS를 다시 시작합니다.

4.  서버를 다시 시작한 후 Verifying the issue still exists 섹션의 2c단계에 설명된 대로 관련 프로브를 다시 실행합니다.

5.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## AverageCommandProcessingTimeGt60sMonitor 복구 작업

이 모니터 경고는 일반적으로 CA 또는 사서함 서버에서 발생합니다.

1.  CA 또는 Mailbox 서버에서 POP3 서비스를 다시 시작합니다. 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/aa997475\(v=exchg.150\))를 참조하십시오.

2.  10분 동안 기다리면서 모니터가 계속 정상 상태인지 확인합니다. 10분이 경과되면 다음 명령을 실행합니다(예에서는 server1.contoso.com이 사용됨).
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "POP*"}

3.  그래도 문제가 여전히 존재하면 서버를 다시 시작해야 합니다. 서버가 CAS인 경우 다시 시작하면 되고, 반면 서버가 사서함 서버인 경우에는 데이터베이스에 대해 장애 조치(failover)를 수행한 후 결과를 확인해야 합니다. 이렇게 하려면 다음 단계를 수행합니다.
    
    1.  다음 명령을 사용하여 서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다.
        
            Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **참고**   이 코드 예제 및 이후 모든 예에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.
    
    2.  모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
        
            Get-MailboxDatabaseCopyStatus -Server <ServerName> | group status
        
        명령 출력에 서버의 활성 복사본이 표시되지 않으면 서버를 다시 시작합니다.

4.  서버가 다시 시작되고 나면 10분 동안 기다렸다가 2단계에 나와 있는 명령을 다시 실행하여 모니터가 계속 정상 상태인지 확인합니다.

5.  모니터가 정상으로 표시되고 이 서버가 사서함 서버인 경우 다음 명령을 실행하여 사서함 서버에 대해 데이터베이스에 대한 장애 조치(failover)를 다시 수행합니다.
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $false

6.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[시작 및 POP3 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/aa997475\(v=exchg.150\))

[Test-PopConnectivity](https://technet.microsoft.com/ko-kr/library/bb738143\(v=exchg.150\))

