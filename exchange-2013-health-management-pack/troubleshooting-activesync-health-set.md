---
title: ActiveSync 상태 문제를 해결 설정
TOCTitle: ActiveSync 상태 문제를 해결 설정
ms:assetid: 8a0b8b26-b4ef-41b8-8f71-8271c1735a69
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.activesync(v=EXCHG.150)
ms:contentKeyID: 53275576
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ActiveSync 상태 문제를 해결 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Exchange ActiveSync 상태 설정은 조직의 모바일 클라이언트에 대한 ActiveSync 서비스의 전체 상태를 모니터링합니다. ActiveSync 상태 설정은 다음 상태 설정과 밀접하게 관련됩니다.

[ActiveSync.Protocol 상태 설정 문제해결](troubleshooting-activesync-protocol-health-set.md)

[ActiveSync.Proxy 상태 설정 문제 해결](troubleshooting-activesync-proxy-health-set.md)

ActiveSync 상태 설정의 상태가 비정상임을 나타내는 경고가 표시되면 사용자의 ActiveSync를 사용한 사서함에 액세스를 막을 수 있는 문제가 있는 것입니다.

## 설명

ActiveSync 서비스는 다음 프로브 및 모니터를 사용하여 모니터링됩니다.


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
<td><p>ActiveSyncCTPProbe</p></td>
<td><p>ActiveSync</p></td>
<td><p>Active Directory</p>
<p>인증</p>
<p>사서함 서버 인증</p>
<p>정보 저장소</p>
<p>고가용성</p>
<p>네트워크</p></td>
<td><p>ActiveSyncCTPMonitor(ActiveSync 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncProxyTestProbe</p></td>
<td><p>ActiveSync.Proxy</p></td>
<td><p>-</p></td>
<td><p>ActiveSyncProxyTestMonitor(ActiveSync.Proxy 상태 설정)</p></td>
</tr>
<tr class="odd">
<td><p>ActiveSyncDeepTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>인증</p>
<p>정보 저장소</p>
<p>고가용성</p></td>
<td><p>ActiveSyncDeepTestMonitor(ActiveSync 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>ActiveSyncSelfTestProbe</p></td>
<td><p>ActiveSync.Protocol</p></td>
<td><p>Active Directory</p>
<p>인증</p></td>
<td><p>ActiveSyncSelfTestMonitor(ActiveSync.Protocol 상태 설정)</p>
<p>RequestsQueuedGt500Monitor(ActiveSync 상태 설정)</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 ActiveSync 상태 설정이 비정상임을 지정하는 경고가 수신되었으면 먼저 해당 문제가 여전히 존재하는지 확인합니다. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제 확인

1.  경고에서 지정된 상태 설정 이름 및 서버 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우 메시지 세부 정보는 근본 원인을 파악할 수 있는, 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보내 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예를 들어 server1.contoso.com에 대한 ActiveSync 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ActiveSync"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고가 발생한 모니터의 **AlertValue** 값은 **비정상**입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예를 들어 실패한 모니터가 **ActiveSyncCTPMonitor**라고 가정합니다. 해당 모니터와 연결된 프로브는 **ActiveSyncCTPProbe**입니다. server1.contoso.com에서 해당 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe ActiveSync\ActiveSyncCTPProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 "Result" 섹션을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## ActiveSyncDeepTestMonitor 및 ActiveSyncSelfTestMonitor 복구 작업

이 모니터 경고는 일반적으로 사서함 서버에서 발생합니다. 복구 작업을 수행하려면 다음 단계를 수행합니다.

1.  IIS 관리자를 시작하고 문제를 보고하는 서버에 연결합니다. **응용 프로그램 풀**을 클릭하고 이름이 **MSExchangeSyncAppPool**인 ActiveSync 응용 프로그램 풀을 재순환합니다.

2.  Verifying the issue 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하여 전체 IIS 서비스를 재순환합니다.

4.  Verifying the issue 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

5.  그래도 문제가 계속 발생하면 서버를 다시 시작하십시오. 이렇게 하려면 먼저 다음 명령을 사용하여 서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    이 코드 예제 및 이후 모든 코드 예에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.

6.  다음으로, 모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status

7.  6단계의 명령 출력에, 서버에 활성 복사본이 없다고 표시되면 서버를 다시 시작합니다. 출력에 활성 복사본이 표시되면 5단계와 6단계를 다시 실행합니다.

8.  서버가 다시 시작되면 Verifying the issue 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

9.  프로브가 정상적으로 실행되면 다음 명령을 실행하여 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

10. 그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## ActiveSyncCTPMonitor 복구 작업

이 모니터 경고는 일반적으로 CAS(CA 서버)에서 발생합니다.

1.  IIS 관리자를 시작하고 문제를 보고하는 서버에 연결합니다. **응용 프로그램 풀**을 클릭하고 이름이 **MSExchangeSyncAppPool**인 ActiveSync 응용 프로그램 풀을 재순환합니다.

2.  Verifying the issue 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하여 전체 IIS 서비스를 재순환합니다.

4.  Verifying the issue 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

5.  문제가 계속되면 해당 사서함 서버에서 상태를 확인해야 합니다. 사서함 서버의 이름은 오류 메시지에서 지정된 `_Mbx:` 값입니다.
    
    1.  해당 사서함 서버에 대해 다음 명령을 실행합니다. 예를 들어 이름이 mailbox1.contoso.com인 사서함 서버에 대해 다음 명령을 실행합니다.
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealtSetName -like "ActiveSync*"}
    
    2.  명령 출력에 나열된 모니터 중 비정상으로 보고된 모니터가 있는 경우 먼저 이러한 모니터를 해결해야 합니다. 이렇게 하려면 ActiveSyncDeepTestMonitor and ActiveSyncSelfTestMonitor Recovery Actions 섹션에 설명된 문제 해결 단계를 수행합니다.

6.  사서함 서버의 모든 모니터가 정상으로 표시되면 CAS를 다시 시작합니다.

7.  서버가 다시 시작되면 Verifying the issue 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

8.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## RequestsQueuedGt500Monitor 복구 작업

이 모니터 경고는 일반적으로 CA 서버에서 발생합니다.

1.  IIS 관리자를 시작하고 문제를 보고하는 서버에 연결합니다. **응용 프로그램 풀**을 클릭하고 이름이 **MSExchangeSyncAppPool**인 ActiveSync 응용 프로그램 풀을 재순환합니다.

2.  10분 동안 기다리면서 모니터가 계속 정상 상태인지 확인합니다. 10분이 경과하면 해당 서버에 대해 다음 명령을 실행합니다. 예를 들어 server1.contoso.com에 대해 다음 명령을 실행합니다.
    
        Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -like "ActiveSync*"}

3.  문제가 계속되면 IISReset 유틸리티를 사용하여 전체 IIS 서비스를 재순환합니다.

4.  10분 정도 기다린 후 2단계에 표시된 명령을 다시 실행하여 모니터가 계속해서 정상으로 표시되는지 확인합니다.

5.  문제가 계속되면 서버를 다시 시작합니다. 서버가 CAS인 경우 다시 시작하면 되고, 사서함 서버인 경우에는 다음을 수행합니다.
    
    1.  서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다. 이렇게 하려면 다음 명령을 실행합니다.
        
            Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
        
        **참고**   이 코드 예제 및 이후 모든 예에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.
    
    2.  모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
        
            Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
        
        명령 출력에 서버의 활성 복사본이 표시되지 않으면 서버를 다시 시작합니다.

6.  서버가 다시 시작되고 나면 10분 동안 기다렸다가 2단계에 나와 있는 명령을 다시 실행하여 모니터가 계속 정상 상태인지 확인합니다.

7.  모니터가 계속해서 정상으로 표시되고 이 서버가 사서함 서버인 경우 다음 명령을 실행하여 데이터베이스에 대해 장애 조치(failover)를 수행합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

8.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange ActiveSync](https://technet.microsoft.com/ko-kr/library/aa998357\(v=exchg.150\))

[모바일 장치](https://technet.microsoft.com/ko-kr/library/bb232129\(v=exchg.150\))

[Exchange ActiveSync 가상 디렉터리 관리 작업](https://technet.microsoft.com/ko-kr/library/bb125170\(v=exchg.150\))

