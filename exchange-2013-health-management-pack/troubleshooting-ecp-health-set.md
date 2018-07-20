---
title: ECP 상태 설정 문제해결
TOCTitle: ECP 상태 설정 문제해결
ms:assetid: 0a1cfcd5-585c-4a0a-9d3c-28dc49e16a6c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.ecp(v=EXCHG.150)
ms:contentKeyID: 53275568
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# ECP 상태 설정 문제해결

 

_**적용 대상:** Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

ECP(Exchange 제어판) 상태 설정은 EAC(Exchange 관리 센터) 및 OWA(Outlook Web App) 사용자 설정 서비스의 전체 상태를 모니터링합니다. ECP 상태 설정은 다음 상태 설정과 밀접하게 연관되어 있습니다.

[ECP 문제를 해결 합니다. 프록시 상태 설정](troubleshooting-ecp-proxy-health-set.md)

알림이 표시 되도록 지정 하는 경우에 ECP 상태 설정 임을 문제가 있는 사용자가 EAC에 액세스 하지 못하게 할 수 있는 상태가 양호 하지 않습니다.

## 설명

EAC 서비스는 다음 프로브 및 모니터를 사용하여 모니터링됩니다.


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
<td><p>EacSelfTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>EacDeepTestProbe</p></td>
<td><p>ECP</p></td>
<td><p>Active Directory</p></td>
<td><p>EacDeepTestMonitor</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 사용자 작업

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

  - 경고를 보낸 서버의 이름

  - 경고가 발생한 날짜와 시간

  - 인증 및 자격 증명 정보

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)
    
    **참고**   전체 예외 추적의 정보를 사용하여 문제를 해결할 수 있습니다.

서비스가 경고를 보낸 후 복구되었을 수도 있습니다. 따라서 상태 설정이 비정상임을 지정하는 경고가 표시되면 해당 문제가 여전히 존재하는지를 먼저 확인하십시오. 문제가 있는 경우 다음 섹션에 설명된 적절한 복구 작업을 수행합니다.

## 문제가 여전히 존재하는지 확인

1.  경고의 서버 이름 및 상태 설정 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우에는 메시지 세부 정보에서 근본 원인을 파악하는 데 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음 단계를 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보낸 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth -Identity <ServerName> -HealthSet <HealthSetName>
        
        예, 상태 ECP를 검색 하려면 server1. contoso.com, 다음 명령을 실행 하는 방법에 대 한 세부 정보를 설정 합니다.
        
            Get-ServerHealth -Identity server1.contoso.com -HealthSetName ECP
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <HealthSetName>\<ProbeName> -Server <ServerName> | Format-List
        
        예를 들어 오류 발생 모니터가 **EacSelfTestMonitor**라고 가정하면 해당 모니터와 연결된 프로브는 **EacSelfTestProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe ECP\EacSelfTestProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## EacSelfTestMonitor 및 EacDeepTestMonitor 복구 작업

1.  IIS 관리자를 시작 하 고 문제를 보고 하는 서버에 연결 합니다. **응용 프로그램 풀** 을 클릭 한 후 **MSExchangeECPAppPool** 라는 ECP 응용 프로그램 풀을 재순환 합니다.

2.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

3.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하여 전체 IIS 서비스를 재순환합니다.

4.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

5.  프로브에 오류가 발생하면 서버를 다시 시작합니다.

6.  서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

7.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

[Exchange 2013의 Exchange 관리 센터](https://technet.microsoft.com/ko-kr/library/jj150562\(v=exchg.150\))

