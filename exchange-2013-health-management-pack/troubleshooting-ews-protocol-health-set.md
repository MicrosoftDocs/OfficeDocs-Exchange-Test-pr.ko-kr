---
title: EWS 문제를 해결 합니다. 프로토콜 상태 설정
TOCTitle: EWS 문제를 해결 합니다. 프로토콜 상태 설정
ms:assetid: 826b2d5b-adbb-4bf5-94b6-0a8de2e3aac0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.ews.protocol(v=EXCHG.150)
ms:contentKeyID: 53275589
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# EWS 문제를 해결 합니다. 프로토콜 상태 설정

 

_**적용 대상:** Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

EWS.Protocol 상태 설정은 사서함 서버에서 EWS(Exchange Web Services) 통신 프로토콜을 모니터링합니다. EWS.Protocol 상태 설정은 다음 상태 설정과 밀접하게 관련됩니다.

[EWS 상태 설정 문제 해결](troubleshooting-ews-health-set.md)

[EWS 문제를 해결 합니다. 프록시 상태 설정](troubleshooting-ews-proxy-health-set.md)

EWS.Protocol이 비정상임을 지정하는 경고가 수신된 경우 이는 사용자가 Exchange에 액세스할 수 없는 문제를 나타냅니다.

## 설명

EWS.Protocol 상태 설정은 다음 프로브로 구성됩니다.

1.  EwsSelfTestProbe

2.  EwsDeepTestProbe

EwsSelfTestProbe에서는 정보 저장소가 사용되지 않습니다. 그러나 EwsDeepTestProbe 프로브에서는 정보 저장소가 사용됩니다. 이 두 프로브 모두 사서함 서버에서 EWS 작업을 수행하며 CAS(클라이언트 액세스 서버)와 같은 인증 방법을 사용합니다. EwsSeftTestProbe는 **ConvertId** 메서드를 호출하고 EwsDeepTestProbe는 **GetFolder** 메서드를 호출합니다.


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
<td><p>EwsSelfTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>Active Directory</p></td>
<td><p>EWSSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EwsDeepTestProbe</p></td>
<td><p>EWS.Protocol</p></td>
<td><p>정보 저장소</p></td>
<td><p>EWSDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

1.  경고가 발생한 사서함 서버의 이름

2.  마지막 오류에 대한 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)

3.  인시던트 발생 시간

## 일반적인 문제

다음과 같은 일반적인 이유로 인해 이 프로브에 오류가 발생할 수 있습니다.

  - 모니터링된 사서함 서버의 EWS 응용 프로그램 풀이 제대로 작동하지 않습니다.

  - 도메인 컨트롤러가 응답하지 않거나 사서함 서버와 통신할 수 없습니다.

  - 사용자의 데이터베이스가 탑재되지 않았거나 특정 사서함의 정보 저장소를 사용할 수 없습니다.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예를 들어 server1.contoso.com에 대한 EWS.Protocol 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "EWS.Protocol"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예를 들어 실패한 모니터가 **EWSSelfTestMonitor**라고 가정합니다. 해당 모니터와 연결된 프로브는 **EWSSelfTestProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe EWS.Protocol\EWSSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## EWSSelfTestMonitor 및 EWSDeepTestMonitor 복구 작업

이 모니터 경고는 일반적으로 사서함 서버에서 발생합니다.

1.  IIS 관리자를 시작한 후 문제를 보고한 서버에 연결하여 CA 및 사서함 서버 둘 다에서 MSExchangeServicesAppPool이 실행 중인지 확인합니다.

2.  실패한 프로브에 대한 MailboxDatabase를 찾은 후 MailboxServer에 대해 MailboxDatabase가 활성 상태인지, 정보 저장소가 정상인지 확인합니다.

3.  **응용 프로그램 풀**을 클릭한 후 셸에서 다음 명령을 실행하여 **MSExchangeServicesAppPool** 응용 프로그램 풀을 재순환합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

4.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

5.  문제가 여전히 존재하면 IISReset 유틸리티를 사용하여 IIS 서비스를 다시 시작합니다.

6.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

7.  문제가 여전히 존재하면 사서함 서버에서 프로토콜 로그 파일을 확인합니다. 사서함 서버에서 로그는 *\<exchange 서버 설치 디렉터리\>*\\Logging\\Ews 폴더에 있습니다.

8.  테스트 사용자 계정을 만들고 이 테스트 사용자 계정을 사용하여 포트 444에서 지정된 사서함 서버에 로그온합니다(https://*\<서버 이름\>*:444/ews/exchange.asmx). 테스트가 성공한 경우 문제가 모니터링 사서함이 있는 사서함 서버나 특정 사서함 데이터베이스에 영향을 줄 수 있습니다. 해당 데이터베이스에 대해 테스트 계정을 사용하여 이 단계를 반복하십시오.

9.  EWS.Protocol 상태 설정에서 특정 사서함 서버에 영향을 주는 문제를 나타낼 수 있는 경고가 있는지 확인합니다.

10. 그래도 문제가 계속 발생하면 서버를 다시 시작하십시오. 이렇게 하려면 먼저 다음 명령을 사용하여 서버에서 호스트되는 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $true
    
    이 코드 예제 및 이후 모든 코드 예에서 *server1.contoso.com*을 실제 서버 이름으로 바꿉니다.

11. 모든 데이터베이스가 문제를 보고하는 서버에서 다른 곳으로 이동되었는지 확인합니다. 이렇게 하려면 다음 명령을 실행합니다.
    
        Get-MailboxDatabaseCopyStatus -Server server1.contoso.com | Group Status
    
    명령 출력에, 서버에 활성 복사본이 없다고 표시되면 서버를 다시 시작합니다.

12. 서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

13. 프로브가 정상적으로 실행되면 다음 명령을 실행하여 데이터베이스를 장애 조치(failover)합니다.
    
        Set-MailboxServer server1.contoso.com -DatabaseCopyActivationDisabledAndMoveNow $false

14. 그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

