---
title: MRS 상태 설정 문제해결
TOCTitle: MRS 상태 설정 문제해결
ms:assetid: 21947ed6-1584-4db9-9cd6-f6c1de22e352
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.scom.mrs(v=EXCHG.150)
ms:contentKeyID: 53275581
ms.date: 03/06/2017
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MRS 상태 설정 문제해결

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

MRS(사서함 복제 서비스) 상태 설정은 MRS 서비스의 전체 상태를 모니터링합니다.

## 설명

MRS 서비스는 다음 프로브 및 모니터를 사용하여 모니터링됩니다.


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
<td><p>MRSServiceCrashingProbe</p></td>
<td><p>MRS</p></td>
<td><p>정보 저장소</p></td>
<td><p>MRSServiceCrashingMonitor</p></td>
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
        
        예를 들어 server1.contoso.com에 대한 MRS 상태 설정 세부 정보를 검색하려면 다음 명령을 실행합니다.
        
            Get-ServerHealth server1.contoso.com | ?{$_.HealthSetName -eq "MRS"}
    
    2.  명령 출력을 검토하여 오류를 보고한 모니터를 확인합니다. 경고를 보낸 모니터의 **AlertValue** 값은 `Unhealthy`입니다.
    
    3.  비정상 상태인 모니터에 대해 관련 프로브를 다시 실행합니다. 관련 프로브를 찾으려면 Explanation 섹션의 표를 참조하십시오. 이렇게 하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
        
        예를 들어 오류 발생 모니터가 **MRSServiceCrashingMonitor**라고 가정하면 해당 모니터와 연결된 프로브는 **MRSServiceCrashingProbe**입니다. server1.contoso.com에서 이 프로브를 실행하려면 다음 명령을 실행합니다.
        
            Invoke-MonitoringProbe MRS\MRSServiceCrashingProbe -Server server1.contoso.com | Format-List
    
    4.  명령 출력에서 프로브의 **Result** 값을 검토합니다. 값이 **Succeeded**이면 문제는 일시적인 오류이며 더 이상 존재하지 않는 문제입니다. 그렇지 않은 경우에는 다음 섹션에 설명된 복구 단계를 참조하십시오.

## 일반적인 문제

상태 설정에서 경고가 표시될 때는 다음 정보가 포함된 전자 메일 메시지를 받게 됩니다.

  - 경고를 보낸 서버의 이름

  - 경고가 발생한 날짜와 시간

  - 사용된 인증 메커니즘 및 자격 증명 정보

  - 마지막 오류의 전체 예외 추적(진단 데이터 및 특정 HTTP 헤더 정보 포함)
    
    전체 예외 추적의 정보를 사용하여 문제를 해결할 수 있습니다. 프로브에서 생성하는 예외에는 프로브가 실패한 원인을 설명하는 실패 이유가 포함되어 있습니다.

**사서함 잠김**

사서함이 잠겨 있으면 다음과 같은 경고가 표시될 수 있습니다.

*MailboxIdentity: namprd03.prod.outlook.com/Microsoft Exchange Hosted Organizations/example.com/User6 MailboxGuid: 기본 (00000000-abcd-01234-5678-1234567890ab) RequestFlags: IntraOrg, Pull, 보호된 데이터베이스: exampledb-db089 예외: MapiExceptionADUnavailable: 사용자에 대한 캐시를 미리 채울 수 없음 …*

이 경고는 사서함이 잠겨 있음을 나타냅니다. 사서함 잠금을 해제하려면 다음 명령을 실행합니다.

    New-MailboxRepairRequest -CorruptionType LockedMoveTarget -Identity <mailboxIdentity> [-Archive]

**참고**   이 명령에서 \<*mailboxIdentity*\>는 전자 메일 메시지에서 **MailboxIdentity**로 제공되는 사서함 이름으로 바꾸십시오. 사서함이 보관 사서함이면 **–Archive** 플래그를 포함해야 합니다. 경고의 **MailboxGuid** 필드를 통해 사서함이 기본 사서함인지 보관 사서함인지를 확인할 수 있습니다.

**손상된 마이그레이션 작업**

손상된 마이그레이션 작업이 수행되면 다음과 같은 경고가 표시될 수 있습니다.

*2012/9/7 오후 9:08:32에 MailboxMigration에서 알림이 발생했습니다. 세부 정보: 진단 정보: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

마이그레이션 메타데이터에 문제가 있으면 마이그레이션이 손상됩니다. 마이그레이션이 손상되면 Microsoft는 Watson 보고서를 수신하여 조사합니다. 이 문제를 복구하려면 마이그레이션 일괄 처리를 제거했다가 다시 만들어야 합니다. 이렇게 하려면 다음 단계를 수행합니다.

1.  손상된 일괄 처리를 제거하려면 다음 명령을 실행합니다.
    
        Remove-MigrationBatch -Identity

2.  일괄 처리 작업을 다시 만들려면 다음 명령을 실행합니다.
    
        New-MigrationBatch -Local -Name

자세한 내용은 [Exchange 2013 cmdlet](https://technet.microsoft.com/ko-kr/library/bb124413\(v=exchg.150\))을 참조하십시오.

**MailboxMigration 경고: CriticalError**

메일 마이그레이션 중에 오류가 발생하면 다음과 같은 경고가 표시될 수 있습니다.

*2012/9/7 오후 9:08:32에 MailboxMigration에서 알림이 발생했습니다. 세부 정보: 진단 정보: ProcessCacheEntry: First Organization :: /o=ExchangeLabs/ou=Exchange Administrative Group (FYDIBOHF23SPDLT)/cn=Recipients/cn=e80fc128879e452ebc882f6bca7007fa-Migration.8*

이 문제를 해결하려면 마이그레이션을 다시 시도해야 합니다. 이렇게 하려면 다음 명령을 실행하거나 EAC(Exchange 관리 센터)에서 **시작** 단추를 누릅니다.

    Call start-migrationbatch -Identity batchName

이 문제가 발생하면 조사를 위해 Dr. Watson 메시지가 Microsoft로 전송됩니다.

**Migration Exchange Replication Service가 실행되고 있지 않습니다.**

이 오류 이유가 표시되면 다음 명령을 실행하여 서비스 상태를 확인할 수 있습니다.

    Test-MRSHealth <servername> -MonitoringContext:$true

다음 명령을 실행하여 서비스를 시작할 수도 있습니다.

    Start-Service msexchangemailboxreplication

**MSExchangeMailboxReplication RCP Ping 실패**

이 오류 이유가 표시될 때는 다음과 같은 경고가 표시될 수 있습니다.

*2012/6/26 오전 6:08:47에 MRS에서 문제가 검색되었습니다. 세부 정보: 다음 오류로 인해 서버 \<서버 이름\>에 대한 MRS RPC Ping 검사가 실패했습니다. Microsoft Exchange 사서함 복제 서비스의 RPC 끝점이 응답할 수 없습니다.*

이 문제가 발생하면 다음 명령을 실행하여 서비스 상태를 확인할 수 있습니다.

    Test-MRSHealth <servername> -MonitoringContext:$true

다음 명령을 실행하여 서비스를 다시 시작할 수도 있습니다.

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication Service의 작동이 계속 중단됨**

MSExchangeMailboxReplication 서비스의 작동이 중단되거나 서비스가 응답하지 않으면 다음과 같은 경고가 표시될 수 있습니다.

*지난 01:00:00 동안 MRS 프로세스가 3번 이상 중단되었습니다. \<b\>Watson 메시지:\</b\> 다음 프로세스 ID에 대해 Watson 보고서를 보냅니다. 41432, 매개 변수: E12, \<서버 이름\>, 15.00.0516.024, MSExchangeMailboxReplication, M.Exchange.MailboxReplicationService, M.E.M.BaseJob.BeginJob, System.ApplicationException, 7ec9, 15.00.0516.024. ErrorReportingEnabled: True.*

이 문제가 발생하면 다음 명령을 실행하여 서비스 상태를 확인할 수 있습니다.

    Test-MRSHealth <servername> -MonitoringContext:$true

다음 명령을 실행하여 서비스를 다시 시작할 수도 있습니다.

    Restart-Service msexchangemailboxreplication

**MSExchangeMailboxReplication에서 MDB 큐를 검색하지 않음**

MSExchangeMailboxReplication 서비스에서 큐를 검색하지 못하면 다음과 같은 경고가 표시될 수 있습니다.

*2012/6/12 오후 6:20:44에 MRS에서 문제가 검색되었습니다. 세부 정보: 다음 오류로 인해 서버 \<서버 이름\>에 대한 MRS 큐 검색 검사가 실패했습니다. Microsoft Exchange 사서함 복제 서비스가 작업에 대한 사서함 데이터베이스 큐를 검색하지 않습니다. 마지막 검색 시간: 04:38:02.1959439..*

이 문제가 발생하면 다음 명령을 실행하여 서비스 상태를 확인할 수 있습니다.

    Test-MRSHealth <servername> -MonitoringContext:$true

다음 명령을 실행하여 서비스를 다시 시작할 수도 있습니다.

    Restart-Service msexchangemailboxreplication

**추가 문제 해결 단계**

1.  IIS 관리자를 시작한 다음 문제를 보고하는 서버에 연결하여 **MSExchangeServicesAppPool** 응용 프로그램 풀이 실행되고 있는지 확인합니다.

2.  IIS 관리자에서 **응용 프로그램 풀**을 클릭한 후 셸에서 다음 명령을 실행하여 **MSExchangeServicesAppPool** 응용 프로그램 풀을 재순환합니다.
    
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

