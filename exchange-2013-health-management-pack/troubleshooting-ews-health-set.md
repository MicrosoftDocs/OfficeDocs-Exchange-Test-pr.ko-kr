---
title: EWS 상태 설정 문제 해결
TOCTitle: EWS 상태 설정 문제 해결
ms:assetid: f5aaacdd-7f4a-4d63-8440-1c564e644dfc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.ews(v=EXCHG.150)
ms:contentKeyID: 53275592
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# EWS 상태 설정 문제 해결

 

_**적용 대상:**Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

EWS(Exchange 웹 서비스) 상태 설정은 EWS 서비스의 전체 상태를 모니터링합니다. EWS 상태 설정은 다음 상태 설정과 밀접하게 연관되어 있습니다.

[EWS 문제를 해결 합니다. 프로토콜 상태 설정](troubleshooting-ews-protocol-health-set.md)

[EWS 문제를 해결 합니다. 프록시 상태 설정](troubleshooting-ews-proxy-health-set.md)

EWS의 상태가 비정상임을 지정하는 경고가 표시되면 사용자와 Exchange 서버의 통신을 막을 수 있는 문제가 있는 것입니다.

## 설명

EWS는 다음 프로브 및 모니터를 사용하여 모니터링됩니다.


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
<td><p>EwsCtpProbe</p></td>
<td><p>EWS</p></td>
<td><p>정보 저장소</p>
<p>AD DS(Active Directory 도메인 서비스)</p></td>
<td><p>EwsCtpMonitor(EWS 상태 설정)</p></td>
</tr>
<tr class="even">
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>AD DS(Active Directory 도메인 서비스)</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="odd">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>정보 저장소</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


이 프로브는 모니터링 계정을 사용하여 CAS(클라이언트 액세스 서버)에서 사서함 서버로의 전체 EWS 로그온을 수행하며, EWS에서 **GetFolder** 메서드를 호출합니다. 프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 일반적인 문제

다음과 같은 일반적인 이유로 인해 이 프로브에 오류가 발생할 수 있습니다.

  - 프로브에서 사용하는 인증 메커니즘과 CAS 가상 디렉터리에 사용되는 인증 메커니즘이 일치하지 않습니다.

  - 모니터링 중인 CAS의 EWS 응용 프로그램 풀이 응답하지 않습니다.

  - CAS가 사서함 서버에 연결할 때 네트워크 문제가 발생합니다.

  - CAS가 도메인 컨트롤러에 연결할 때 통신 문제가 발생합니다.

  - 도메인 컨트롤러가 응답하지 않습니다.

  - 하나 이상의 사서함 서버에 있는 EWS 응용 프로그램 풀이 응답하지 않습니다.

  - 사용자의 데이터베이스가 탑재되지 않았거나 특정 사서함의 정보 저장소를 사용할 수 없습니다.

  - 하나 이상의 사서함 서버에서 정보 저장소 서비스에 문제가 발생합니다.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.
    
    상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.
    
    1.  경고가 발생한 CAS의 이름
    
    2.  프로브가 대상 리소스로 모니터링 중이었던 사서함 서버의 이름
    
    3.  마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)
    
    4.  인시던트 발생 시간
    
    5.  사용된 인증 메커니즘 및 자격 증명 정보
    
    예외 추적 정보를 통해 프로브에 오류가 발생하는 원인에 대한 보다 중요한 정보를 파악할 수 있습니다. 에스컬레이션 메시지에는 다음 HTTP 헤더도 포함됩니다.
    
    1.  **X-FEServer**   프로브가 실행된 CAS를 나타냅니다.
    
    2.  **X-TargetBEServer**   요청이 라우팅된 MBX 서버를 나타냅니다.
    
    3.  **X-DiagInfo**   요청을 받은 MBX 서버를 나타냅니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예를 들어 server1.contoso.com에 대한 EWS 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        EWS 상태 설정에 대해 오류 발생 모니터가 **EWSCtpMonitor**라고 가정하면 해당 모니터와 연결된 프로브는 **EWSCtpProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe EWS\EWSCtpProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## EwsCtpMonitor 복구 작업

1.  IIS 관리자를 시작한 후 문제를 보고하는 서버에 연결하여 **MSExchangeServicesAppPool** 응용 프로그램 풀이 CA 서버와 사서함 서버에서 모두 실행 중인지 확인합니다.

2.  오류가 발생한 프로브의 MailboxDatabase를 찾습니다. 그런 다음 사서함 서버에 대해 사서함 데이터베이스가 활성 상태이며 정보 저장소가 정상 상태인지 확인합니다.

3.  **응용 프로그램 풀**을 클릭한 후 셸에서 다음 명령을 실행하여 **MSExchangeServicesAppPool** 응용 프로그램 풀을 재순환합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

5.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하여 전체 IIS 서비스를 재순환합니다.

6.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

7.  그래도 문제가 계속 발생하면 CA 서버 및 사서함 서버의 프로토콜 로그 파일을 검토합니다. CAS의 프로토콜 로그는 *\<Exchange Server 설치 디렉터리\>\\Logging\\HttpProxy\\Ews* 폴더에 있습니다. 사서함 서버에서 로그는 *\<Exchange Server 설치 디렉터리\>\\Logging\\Ews* 폴더에 있습니다.

8.  테스트 사용자 계정을 만든 다음 지정된 CAS에 대해 이 테스트 사용자 계정을 실행하여 로그온합니다. 예를 들어 https://\<서버 이름\>/ews/exchange.asmx를 사용하여 로그온합니다. 그래도 문제가 계속 발생하면 다른 CAS에 로그온하여 사서함 서버가 아닌 해당 CAS에서 문제가 발생하는지를 확인합니다. 테스트 사용자 이름이 테스트를 통과하면 모니터링 사서함이 있는 특정 사서함 데이터베이스 또는 사서함 서버에 영향을 주는 문제일 수 있습니다. 사서함 데이터베이스에 있는 테스트 계정을 사용하여 이 단계를 반복해 봅니다.

9.  CA 서버와 사서함 서버 간의 네트워크 연결을 확인합니다.

10. EWS.Proxy 상태 설정에서 특정 CAS에 영향을 주는 문제를 나타낼 수 있는 경고를 확인합니다.

11. EWS.Protocol 상태 설정에서 특정 사서함 서버에 영향을 주는 문제를 나타낼 수 있는 경고를 확인합니다.

12. 그래도 문제가 계속 발생하면 서버를 다시 시작하십시오. 서버를 다시 시작하려면 먼저 서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    **참고**   이 코드 예제 및 이후 모든 예에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.

13. 모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    명령 출력에 서버의 활성 복사본이 표시되지 않으면 서버를 다시 시작합니다.

14. 서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

15. 프로브가 정상적으로 실행되면 다음 명령을 실행하여 데이터베이스를 사서함 서버로 다시 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

16. 그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

