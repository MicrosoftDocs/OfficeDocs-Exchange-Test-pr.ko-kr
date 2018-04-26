---
title: ECP 문제를 해결 합니다. 프록시 상태 설정
TOCTitle: ECP 문제를 해결 합니다. 프록시 상태 설정
ms:assetid: f2289f81-56cb-40b5-9108-8782976cccc8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.ecp.proxy(v=EXCHG.150)
ms:contentKeyID: 53275590
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ECP 문제를 해결 합니다. 프록시 상태 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

ECP 합니다. 클라이언트 액세스 서버 (CA)에서 Exchange 관리 센터 (EAC) 프록시 인프라의 가용성을 모니터링 하는 프록시 상태 설정 합니다. ECP 합니다. 프록시 상태 집합은 밀접 하 게 다음 상태 설정 합니다.

[ClientAccess.Proxy 상태 설정 \[좀비\] 문제해결](troubleshooting-clientaccess-proxy-health-set.md)

알림이 표시 되도록 지정 하는 ECP 하는 경우. 프록시 정상 임을 EAC를 사용 하 여 하지 못할 수 있는 문제가 아닙니다.

## 설명

EAC 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


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
<td><p>ECPProxyTestProbe</p></td>
<td><p>ECP.Proxy</p></td>
<td><p>Active Directory</p></td>
<td><p>ECPProxyTestMonitor</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 일반적인 문제

다음과 같은 일반적인 이유로 인해 이 프로브에 오류가 발생할 수 있습니다.

  - 모니터링된 CAS에서 호스트되는 응용 프로그램 풀이 제대로 작동하지 않습니다.

  - 모니터링 계정 자격 증명이 잘못되었습니다.

  - 도메인 컨트롤러가 응답하지 않습니다.

## 사용자 작업

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예: ECP를 검색할 수 있습니다. 프록시 상태 server1. contoso.com, 다음 명령을 실행 하는 방법에 대 한 세부 정보를 설정 합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "ECP.Proxy"}
    
    2.  명령 출력을 검토 하 고 오류를 보고 하는 모니터를 결정 합니다. 경고를 모니터에 대 한 **AlertValue** 값 `Unhealthy`됩니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예, 오류가 발생 한 모니터 **ECPProxyTestMonitor** 인지 것으로 가정 합니다. 모니터에 연결 된 프로브 **ECPProxyTestProbe** 됩니다. Server1. contoso.com에 해당 프로브를 실행 하려면 다음 명령을 실행 합니다.
        
            Invoke-MonitoringProbe ECP.Proxy\ECPProxyTestProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## ECPProxyTestMonitor 복구 작업

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

  - 경고를 보낸 CAS의 이름

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)
    
    전체 예외 추적의 정보를 사용하여 문제를 해결할 수 있습니다.

  - 문제가 발생한 날짜와 시간

이 문제를 해결하려면 다음 단계를 수행합니다.

1.  CA 서버에서 프로토콜 로그를 검토합니다. 프로토콜 로그는 CAS에서 *\<Exchange 서버 설치 디렉터리\>*\\Logging\\HttpProxy*\\\<프로토콜\>* 폴더에 있습니다.

2.  테스트 사용자 계정을 만들고 테스트 사용자 계정 이름을 사용 하 여 CAS에 로그온 합니다. 예를 사용 하 여 로그온: https:// *\<servername\>*/owa 합니다.

3.  IIS 관리자를 시작 하 고 문제를 보고 하는 서버에 연결 합니다. MSExchangeServicesAppPool CA에서 실행 되 고 있는지 확인 합니다.

4.  **응용 프로그램 풀** 을 클릭 하 고 후 Exchange 관리 셸 에서 다음 명령을 실행 하 여 **MSExchangeECPAppPool** 응용 프로그램 풀을 재순환 합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeECPAppPool

5.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

6.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하여 IIS 서비스를 재순환합니다.

7.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

8.  그래도 문제가 계속 발생하면 서버를 다시 시작하십시오.

9.  서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

10. 그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

