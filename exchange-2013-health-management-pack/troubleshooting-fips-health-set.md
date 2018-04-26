---
title: FIPS 상태 설정 문제해결
TOCTitle: FIPS 상태 설정 문제해결
ms:assetid: 96e1b096-9cb5-426f-a84e-50d5599e4bbb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.fips(v=EXCHG.150)
ms:contentKeyID: 54651883
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# FIPS 상태 설정 문제해결

 

_**적용 대상:**Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Exchange 서버에서 처리 표준 FIPS (Federal Information) 설정의 전반적인 상태를 모니터링 하는 **FIPS** 상태 설정 합니다. FIPS 140 하는 방법에 대 한 자세한 내용은 [FIPS 140 유효성 검사](https://go.microsoft.com/fwlink/p/?linkid=521913)을 참조 하십시오.

**FIPS** 상태 설정 상태가 정상 인지 여부를 나타내는 알림이 표시 하는 경우이 Exchange 서버 FIPS 140 규격 구성 요소 및 프로세스를 사용 하 여 하지 못하게 할 수 있는 문제를 나타냅니다.

## 설명

**FIPS** 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>프로브</th>
<th>상태 설정</th>
<th>연결된 모니터</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>CrashEvent.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceFailureMonitor.FIPS</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>MaintenanceTimeoutMonitor.FIPS</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>PrivateWorkingSetError.scanningprocess</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeWarning.scanningprocess</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>FIPS</p></td>
<td><p>ProcessProcessorTimeError.scanningprocess</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 사용자 작업

경고를 발급 한 후 서비스 복구는 불가능 합니다. 따라서 **FIPS** 상태 설정 상태가 정상 인지를 지정 하는 알림을 받으면 먼저 문제가 여전히 있는지 확인 합니다. 이 문제는 존재 하는 경우 다음 섹션에 설명 된 적절 한 복구 작업을 수행 합니다.

## 문제 확인

1.  경고에서 지정된 상태 설정 이름 및 서버 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우 메시지 세부 정보는 근본 원인을 파악할 수 있는, 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보내 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예 상태 **FIPS** 를 검색 하려면 server1. contoso.com, 다음 명령을 실행 하는 방법에 대 한 세부 정보를 설정 합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "FIPS"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고가 발생한 모니터의 **AlertValue** 값은 **비정상**입니다.

