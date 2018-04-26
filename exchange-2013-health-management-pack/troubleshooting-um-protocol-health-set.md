---
title: UM 문제를 해결 합니다. 프로토콜 상태 설정
TOCTitle: UM 문제를 해결 합니다. 프로토콜 상태 설정
ms:assetid: 8dd9a16f-77a1-4a8d-aea4-5e96ab922dd4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.um.protocol(v=EXCHG.150)
ms:contentKeyID: 53275591
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 문제를 해결 합니다. 프로토콜 상태 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

UM.Protocol 상태 설정은 사서함 서버에서 UM(통합 메시징) 프로토콜을 모니터링합니다.

UM.Protocol이 비정상임을 지정하는 경고가 수신된 경우 이는 사용자가 조직의 UM 서비스를 사용할 수 없는 문제를 나타냅니다. UM.Protocol 상태 설정은 다음 상태 설정과 밀접하게 관련됩니다.

[UM 상태 설정 문제해결](troubleshooting-um-health-set.md)

[UM 문제를 해결 합니다. CallRouter 상태 설정](troubleshooting-um-callrouter-health-set.md)

## 설명

UM.Protocol 서비스는 다음 프로브와 모니터를 사용하여 모니터링됩니다.


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
    
    **참고**   전체 예외 추적의 정보를 사용하여 문제를 해결할 수 있습니다. 프로브에서 생성하는 예외에는 프로브가 실패한 원인을 설명하는 실패 이유가 포함되어 있습니다.

UM 경고 메시지 문제 해결에 대한 자세한 내용은 [UM 상태 설정 문제해결](troubleshooting-um-health-set.md)을 참조하십시오.

## 자세한 내용

[Exchange 2013의 새로운 기능](https://technet.microsoft.com/ko-kr/library/jj150540\(v=exchg.150\))

[Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))

