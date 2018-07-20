---
title: UM 상태 설정 문제해결
TOCTitle: UM 상태 설정 문제해결
ms:assetid: db947791-63ce-45dd-8634-1dfa5f55e2c2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.um(v=EXCHG.150)
ms:contentKeyID: 53275582
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 상태 설정 문제해결

 

_**적용 대상:** Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

조직에서 UM 서비스의 전반적인 상태를 모니터링 하는 UM (통합 메시징) 상태 설정 합니다.

UM의 상태가 비정상임을 지정하는 경고가 표시되면 조직에서 사용자의 UM 서비스 사용을 막을 수 있는 문제가 있는 것입니다. UM 상태 설정은 다음 상태 설정과 밀접하게 연관되어 있습니다.

[UM 문제를 해결 합니다. CallRouter 상태 설정](troubleshooting-um-callrouter-health-set.md)

[UM 문제를 해결 합니다. 프로토콜 상태 설정](troubleshooting-um-protocol-health-set.md)

## 설명

UM 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


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
<td><p>UMSelfTestProbe</p></td>
<td><p>UM.Protocol</p></td>
<td><p>AD DS(Active Directory 도메인 서비스)</p></td>
<td><p>UMSelfTestMonitor</p></td>
</tr>
<tr class="even">
<td><p>UMCallRouterTestProbe</p></td>
<td><p>UM.CallRouter</p></td>
<td><p>AD DS(Active Directory 도메인 서비스)</p></td>
<td><p>UMCallRouterTestMonitor</p></td>
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
        
        예를 들어 server1.contoso.com에 대한 UM.Protocol 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "UM.Protocol"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예를 들어 오류 발생 모니터가 **UMSelfTestMonitor**라고 가정하면 해당 모니터와 연결된 프로브는 **UMSelfTestProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe UM.Protocol\UMSelfTestMonitor -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## 문제 해결 단계

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

  - 경고를 보낸 서버의 이름

  - 경고가 발생한 날짜와 시간

  - 사용된 인증 메커니즘 및 자격 증명 정보

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)
    
    **참고 사항**  이 문제를 해결 하기 위해 전체 예외 추적에 정보를 사용할 수 있습니다. 프로브에서 생성 된 예외는 프로브 실패 이유를 설명 하는 실패 이유를 포함 합니다.

**UM 서비스에 대 한 sip 옵션 실패**

UM 서비스 비활성화 되는지 여부를 결정 합니다. UM 서비스 시작 하지 않거나 사용 하지 않도록 설정, UM 서비스를 다시 시작 합니다.

**UM 서비스를 통해의 마지막 시간에 의해 거부 된 인바운드 호출의 {0} % 이상**

CAS(클라이언트 액세스 서버)의 이벤트 로그를 검토하여 **umipgateway**, **umhuntgroup** 등의 UM 개체가 올바르게 구성되어 있는지 확인합니다.

이벤트 로그에 정보가 부족하면 고급 수준에서 UM 이벤트 로그를 사용하도록 설정하여 UM 추적 로그 파일을 검토해야 할 수 있습니다.

**UM 작업자 프로세스를 통해의 마지막 시간에 의해 거부 된 인바운드 호출의 {0} % 이상**

**Umipgateway** 및 **umhuntgroup** 개체와 같은 UM 개체를 올바르게 구성 되었는지 여부를 확인 하려면 CA에서 이벤트 로그를 검토 합니다.

이벤트 로그에 정보가 부족하면 고급 수준에서 UM 이벤트 로그를 사용하도록 설정하여 UM 추적 로그 파일을 검토해야 할 수 있습니다.

**성공적으로 처리를 통해는 마지막 시간을 된 메시지의 {0} % 미만**

**Umipgateway** 및 **umhuntgroup** 개체와 같은 UM 개체를 올바르게 구성 되었는지 여부를 확인 하려면 CA에서 이벤트 로그를 검토 합니다.

이벤트 로그에 정보가 부족하면 고급 수준에서 UM 이벤트 로그를 사용하도록 설정하여 UM 추적 로그 파일을 검토해야 할 수 있습니다.

**Microsoft Exchange 통합 메시징 서비스 UM 파이프라인이 전체 때문에 대 한 호출을 거부**

**Umipgateway** 및 **umhuntgroup** 개체와 같은 UM 개체를 올바르게 구성 되었는지 여부를 확인 하려면 CA에서 이벤트 로그를 검토 합니다.

이벤트 로그에 정보가 부족하면 고급 수준에서 UM 이벤트 로그를 사용하도록 설정하여 UM 추적 로그 파일을 검토해야 할 수 있습니다.

**A / V에 지 서비스 잘못 구성 된 또는 실행 되지 않음**

1.  Lync server에서 호출이 실패 이유를 확인 하려고 하는 사서함 서버의 이벤트 로그를 검토 합니다. 그런 다음, 다음을 수행 합니다.
    
      - UM 서비스에 의해 선택 된 Lync 풀 작동 중인지 확인 합니다.
    
      - 특정 Lync server를 사용 하려면 다음 명령을 실행 합니다.
        
            Set-UMServer ExchangeUMServer -SIPAccessService <ServerName>

**UM 서버를 Communications Server A에 성공적으로 자격 증명을 취득 하지 못했습니다. / V에 지 서비스**

Lync 풀을 선택 하면 조사 하 고 선택한 Lync 풀 작동 하는지 확인 이벤트 로그를 검토 합니다.

**Communications Server 오디오/비디오에 지 포트를 열거나 세션을 설정 하는 동안 리소스를 할당 하지 못했습니다.**

Lync 풀을 선택 하면 조사 하 고 선택한 Lync 풀 작동 하는지 확인 이벤트 로그를 검토 합니다.

**Microsoft Exchange 통합 메시징 서비스 인증서가 만료 날짜가 가까워 지**

사서함 서버의 UM 서비스 인증서를 갱신 합니다.

**추가 문제 해결 단계:** 

1.  IIS 관리자를 시작 하 고 **MSExchangeServicesAppPool** 응용 프로그램 풀이 실행 되 고 있는지 여부를 확인 하려면 문제를 보고 하는 서버에 연결 합니다.

2.  IIS 관리자에서 **응용 프로그램 풀** 을 클릭 한 후 **MSExchangeServicesAppPool** 응용 프로그램 풀을 재순환 합니다. 이 작업을 수행 하려면 Exchange 관리 셸 에서 다음 명령을 실행 합니다.
    
        %SystemRoot%\System32\inetsrv\Appcmd recycle MSExchangeServicesAppPool

3.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

4.  문제가 여전히 존재하는 경우 IISReset 유틸리티를 사용하거나 다음 명령을 실행하여 IIS 서비스를 재순환합니다.
    
        Iisreset /noforce

5.  Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

6.  그래도 문제가 계속 발생하면 서버를 다시 시작하십시오.

7.  서버가 다시 시작되면 Verifying the issue still exists 섹션의 2c단계에 나와 있는 대로 관련 프로브를 다시 실행합니다.

8.  그래도 프로브에서 계속 오류가 발생하면 이 문제를 해결하기 위해 지원을 받아야 할 수 있습니다. 이 문제를 해결하려면 Microsoft 기술 지원 전문가에게 문의하세요. Microsoft 기술 지원 전문가에게 문의하려면 [Exchange Server 솔루션 센터](https://go.microsoft.com/fwlink/p/?linkid=180809)를 참조하세요. 탐색 창에서 **지원 옵션 및 리소스**를 클릭하고 **기술 지원 서비스 받기** 아래에 나열된 옵션 중 하나를 사용하여 Microsoft 기술 지원 전문가에게 문의하세요. 조직에 Microsoft 제품 지원 서비스에 직접 문의하는 특정 절차가 있을 수도 있으므로 먼저 조직의 지침을 검토해야 합니다.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

