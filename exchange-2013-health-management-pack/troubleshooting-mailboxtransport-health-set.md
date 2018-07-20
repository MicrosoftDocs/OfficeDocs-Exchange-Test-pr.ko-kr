---
title: 설정 MailboxTransport 상태 문제를 해결
TOCTitle: 설정 MailboxTransport 상태 문제를 해결
ms:assetid: 02bfa4cf-6929-437e-bae5-079ea1b92373
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.mailboxtransport(v=EXCHG.150)
ms:contentKeyID: 54651858
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 설정 MailboxTransport 상태 문제를 해결

 

_**적용 대상:** Exchange Server 2013, Project Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

사서함 서버의 사서함 전송 및 사서함 전송 배달 서비스의 전반적인 상태를 모니터링 하는 **MailboxTransport** 상태 설정 합니다. 이러한 서비스는 사서함 데이터베이스에서 메일을 보내는 담당 합니다. 자세한 내용은 [메일 흐름](https://technet.microsoft.com/ko-kr/library/aa996349\(v=exchg.150\))을 참조 하십시오.

**MailboxTransport** 상태 설정 상태가 정상 인지 여부를 나타내는 알림이 표시 하는 경우이 메일 전송 또는 사서함 데이터베이스에서 수신 되지 않도록를 방해할 수 있는 문제를 나타냅니다.

## 설명

**MailboxTransport** 서비스는 다음 프로브 및 모니터를 사용 하 여 모니터링 됩니다.


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
<td><p>MailboxDeliveryAvailability</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxDeliveryAvailabilityAggregationProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryAvailabilityAggregationMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxDeliveryInstanceAvailabilityProbe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxDeliveryInstanceAvailabilityMonitor</p></td>
</tr>
<tr class="even">
<td><p>MailboxTransportDeliveryServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportDeliveryServiceRunningMonitor</p></td>
</tr>
<tr class="odd">
<td><p>MailboxTransportSubmissionServiceRunning</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportSubmissionServiceRunningMonitor</p></td>
</tr>
<tr class="even">
<td><p>Mapi.Submit.Probe</p></td>
<td><p>MailboxTransport</p></td>
<td><p>Mapi.Submit.Monitor</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>CrashEvent.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>DeliveryInterceptorStoreDriverAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MailboxTransportUserQuarantineMonitor</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MBTSubmissionInterceptorSubmissionAgentMonitor</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor50</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor70</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>PrivateWorkingSetWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeError.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangedelivery</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>ProcessProcessorTimeWarning.msexchangesubmission</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionBackpressureSustainedTimeMonitor</p></td>
</tr>
<tr class="even">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>SubmissionInterceptorSubmissionAgentPctPermFailedMonitor</p></td>
</tr>
<tr class="odd">
<td><p>없음 (알림 또는 확인)</p></td>
<td><p>MailboxTransport</p></td>
<td><p>TransportDeliveryFailuresDeliveryStoreDriver560Monitor</p></td>
</tr>
</tbody>
</table>


프로브 및 모니터에 대한 자세한 내용은 [서버 상태 및 성능](https://technet.microsoft.com/ko-kr/library/jj150551\(v=exchg.150\))을 참조하십시오.

## 사용자 작업

경고를 발급 한 후 서비스 복구는 불가능 합니다. 따라서 **MailboxTransport** 상태 설정 상태가 정상 인지를 지정 하는 알림을 받으면 먼저 문제가 여전히 있는지 확인 합니다. 이 문제는 존재 하는 경우 다음 섹션에 설명 된 적절 한 복구 작업을 수행 합니다.

## 문제 확인

1.  경고에서 지정된 상태 설정 이름 및 서버 이름을 확인합니다.

2.  메시지 세부 정보에서 경고의 정확한 원인에 대한 정보를 제공합니다. 대부분의 경우 메시지 세부 정보는 근본 원인을 파악할 수 있는, 충분한 문제 해결 정보를 제공합니다. 메시지 세부 정보가 명확하지 않은 경우 다음을 수행합니다.
    
    1.  Exchange 관리 셸를 열고 다음 명령을 실행하여 경고를 보내 상태 설정의 세부 정보를 검색합니다.
        
            Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
        
        예 **MailboxTransport** 를 검색 하려면 상태는 mailbox1.contoso.com, 다음 명령을 실행 하는 방법에 대 한 세부 정보를 설정 합니다.
        
            Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "MailboxTransport"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고가 발생한 모니터의 **AlertValue** 값은 **비정상**입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 [Explanation](troubleshooting-activesync-health-set.md) 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예, 오류가 발생 한 모니터 **MailboxDeliveryAvailabilityMonitor**인지 것으로 가정 합니다. 모니터에 연결 된 프로브 **MailboxDeliveryAvailability**됩니다. 이 프로브에 mailbox1.contoso.com를 실행 하려면 다음 명령을 실행 합니다.
        
            Invoke-MonitoringProbe MailboxTransport\MailboxDeliveryAvailabilityMonitor -Server mailbox1.contoso.com | Format-List
    
    4.  명령 출력에는 프로브의 "결과" 섹션을 검토 합니다. **성공** 값을 사용 하는 경우이 문제에 일시적인 오류가 이었으며 더이상 존재 합니다.

