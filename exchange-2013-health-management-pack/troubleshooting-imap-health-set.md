---
title: IMAP 상태 설정 문제해결
TOCTitle: IMAP 상태 설정 문제해결
ms:assetid: 2a06e671-4cc2-4ce5-bf53-6243ea140f20
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.imap(v=EXCHG.150)
ms:contentKeyID: 53275572
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IMAP 상태 설정 문제해결

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

IMAP 상태 설정은 CAS(클라이언트 액세스 서버)에 있는 IMAP4 프록시 인프라의 사용 가능 여부를 모니터링합니다. IMAP 상태 설정은 다음 상태 설정과 밀접하게 연관되어 있습니다.

[IMAP 문제를 해결 합니다. 프로토콜 상태 설정](troubleshooting-imap-protocol-health-set.md)

[IMAP 문제를 해결 합니다. 프록시 상태 설정](troubleshooting-imap-proxy-health-set.md)

IMAP의 상태가 비정상임을 지정하는 경고가 표시되면 사용자의 IMAP를 사용한 사서함 액세스를 막을 수 있는 문제가 있는 것입니다.

## 설명

IMAP4 서비스는 다음 프로브 및 모니터를 사용하여 모니터링됩니다.


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
<td><p>ImapCTPProbe</p></td>
<td><p>IMAP</p></td>
<td><p>Active Directory</p>
<p>인증</p>
<p>사서함 서버 인증</p>
<p>고가용성</p>
<p>네트워킹</p></td>
<td><p>ImapCTPMonitor(IMAP 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>ImapProxyTestProbe</p></td>
<td><p>IMAP.Proxy</p></td>
<td><p>Active Directory</p>
<p>인증</p></td>
<td><p>ImapProxyTestMonitor(IMAP.Proxy 상태 설정)</p></td>
</tr>
<tr class="odd">
<td><p>ImapDeepTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>인증</p>
<p>정보 저장소</p>
<p>고가용성</p></td>
<td><p>IMAP.Protocol(IMAP.Protocol 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>ImapSelfTestProbe</p></td>
<td><p>IMAP.Protocol</p></td>
<td><p>Active Directory</p>
<p>인증</p></td>
<td><p>IMAP.Protocol(IMAP.Protocol 상태 설정)</p>
<p>AverageCommandProcessingTimeGt60sMonitor(IMAP 상태 설정)</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예를 들어 server1.contoso.com에 대한 IMAP 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예를 들어 오류 발생 모니터가 **ImapCTPMonitor**라고 가정하면 해당 모니터와 연결된 프로브는 **ImapCTPProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe IMAP\ImapCTPProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## ImapTestDeepMonitor and ImapSelfTestMonitor 복구 작업

1.  백 엔드 서버에서 Exchange IMAP4 서비스를 다시 시작합니다. IMAP4 서비스를 중지 및 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/bb124022\(v=exchg.150\))를 참조하십시오.

2.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  문제가 계속 발생하면 다음 명령을 사용하여 사서함 서버에서 호스트되는 데이터베이스를 장애 조치(failover)해야 합니다.
    
        Set-MailboxServer -Identity <ServerName> -DatabaseCopyActivationDisabledAndMoveNow $true

4.  모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    명령 출력에 서버의 활성 복사본이 표시되지 않으면 서버를 다시 시작합니다.

5.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

6.  프로브가 정상적으로 실행되면 다음 명령을 실행하여 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## ImapCTPMonitor 복구 작업

이 모니터 경고는 대개 CAS 서버에서 생성됩니다.

1.  백 엔드 서버에서 Exchange IMAP4 서비스를 다시 시작합니다. IMAP4 서비스를 중지 및 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/bb124022\(v=exchg.150\))를 참조하십시오.

2.  Verifying the issue still exists 섹션의 2.c.단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  그래도 문제가 계속 발생하면 IMAP 프로토콜 로깅을 설정하여 문제를 해결해야 합니다. 이렇게 하려면 다음 단계를 수행합니다.
    
    1.  Windows PowerShell에서 다음 명령을 실행합니다.
        
            Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $true
    
    2.  백 엔드 서버에서 Exchange IMAP4 서비스를 다시 시작합니다. IMAP4 서비스를 중지 및 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/bb124022\(v=exchg.150\))를 참조하십시오.
    
    3.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.
    
    4.  다음 명령을 실행하고 로그 파일의 위치를 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
        
            Get-ImapSettings -server <CAS server name>
    
    5.  이 명령을 실행하는 사서함을 확인합니다. 사서함 서버의 이름은 오류 메시지의 `_Mbx:` 값입니다.
    
    6.  다음 명령을 실행합니다.
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "IMAP*"}
        
        **참고**   이 명령에서 *mailbox1.contoso.com*을 실제 사서함 서버 이름으로 바꿉니다.
    
    7.  명령 출력에 나열된 모니터가 비정상 상태로 보고되는 경우에는 해당 모니터의 문제를 먼저 해결해야 합니다. ImapTestDeepMonitor and ImapSelfTestMonitor Recovery Actions 섹션에 나와 있는 문제 해결 단계를 따르십시오.

4.  사서함 서버가 정상 상태로 보고되면 CAS를 다시 시작합니다.

5.  서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

6.  프로토콜 로깅을 해제합니다. 이렇게 하려면 다음 Windows PowerShell 명령을 실행합니다.
    
        Set-ImapSettings -server <CAS server name> -ProtocolLoggingEnabled $false

7.  IMAP4 서비스를 다시 시작합니다.

8.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## ImapProxyTestMonitor 복구 작업

1.  IMAP4 서비스를 다시 시작합니다.

2.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  프로브에서 문제가 계속 발생하면 CAS를 다시 시작합니다.

4.  서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

5.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## AverageCommandProcessingTimeGt60sMonitor RequestsQueuedGt500Monitor 복구 작업

이 모니터 경고는 대개 CAS 및 사서함 서버에서 생성됩니다.

1.  백 엔드 서버 또는 CAS에서 Exchange IMAP4 서비스를 다시 시작합니다. IMAP4 서비스를 중지 및 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](https://technet.microsoft.com/ko-kr/library/bb124022\(v=exchg.150\))를 참조하십시오.

2.  10분 동안 기다리면서 모니터가 계속 정상 상태인지 확인합니다. 10분 후에 다음 명령을 실행합니다.
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "IMAP*"}
    
    **참고**   이 명령에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.

3.  10분 동안 기다렸다가 2단계에 나와 있는 명령을 다시 실행하여 모니터가 계속 정상 상태인지 확인합니다.

4.  그래도 문제가 계속 발생하면 서버를 다시 시작해야 합니다. 서버가 CAS인 경우 다시 시작하면 되고, 사서함 서버인 경우에는 다음을 수행합니다.
    
    1.  서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다. 이렇게 하려면 다음 명령을 실행합니다.
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **참고**   이 코드 예제 및 이후 모든 예에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.
    
    2.  모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        명령 출력에 서버의 활성 복사본이 표시되지 않으면 서버를 다시 시작합니다.

5.  서버가 다시 시작되고 나면 10분 동안 기다렸다가 2단계에 나와 있는 명령을 다시 실행하여 모니터가 계속 정상 상태인지 확인합니다.

6.  사서함 서버의 경우 모니터가 정상 상태로 유지되면 다음 명령을 실행하여 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

7.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange Server 2013의 POP3 및 IMAP4](https://technet.microsoft.com/ko-kr/library/jj657728\(v=exchg.150\))

[Exchange 2016에서 IMAP4를 사용 하도록 설정](https://technet.microsoft.com/ko-kr/library/bb124489\(v=exchg.150\))

[Test-ImapConnectivity](https://technet.microsoft.com/ko-kr/library/bb738126\(v=exchg.150\))

