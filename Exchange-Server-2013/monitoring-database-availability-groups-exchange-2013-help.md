---
title: '데이터베이스 사용 가능 그룹 모니터링: Exchange 2013 Help'
TOCTitle: 데이터베이스 사용 가능 그룹 모니터링
ms:assetid: f5bdfd6e-e93c-4d96-8bc2-548750d51930
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351258(v=EXCHG.150)
ms:contentKeyID: 50484553
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 데이터베이스 사용 가능 그룹 모니터링

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

진단 정보를 수집 하 고는 디스크 공간 부족 임계값 모니터링 구성에 대 한 데이터베이스 가용성 그룹 (Dag)에 대 한 사서함 데이터베이스 복사본의 상태를 모니터링 하는 것에 대 한이 항목의 세부 정보를 사용할 수 있습니다.

## Get-MailboxDatabaseCopyStatus cmdlet

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\)) cmdlet을 사용하여 사서함 데이터베이스 복사본에 대한 상태 정보를 볼 수 있습니다. 이 cmdlet을 사용하면 특정 데이터베이스의 모든 복사본에 대한 정보, 특정 서버에 있는 데이터베이스의 특정 복사본에 대한 정보 또는 서버의 모든 데이터베이스 복사본에 대한 정보를 볼 수 있습니다. 다음 표에는 사서함 데이터베이스 복사본의 복사본 상태에 대해 가능한 값이 나와 있습니다.

### 데이터베이스 복사본 상태

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>데이터베이스 복사본 상태</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Failed</p></td>
<td><p>사서함 데이터베이스 복사본이 일시 중단되지 않았고 로그 파일을 복사하거나 재생할 수 없기 때문에 Failed 상태입니다. Failed 상태이고 일시 중단되지 않은 경우 시스템은 복사본 상태를 Failed로 변경하게 한 문제가 해결되었는지 여부를 정기적으로 확인하게 됩니다. 시스템에서 문제가 해결되었고 다른 문제가 없음을 확인하고 나면 복사본 상태가 정상 상태로 자동 변경됩니다.</p></td>
</tr>
<tr class="even">
<td><p>Seeding</p></td>
<td><p>사서함 데이터베이스 복사본을 시드 중이거나, 사서함 데이터베이스 복사본의 콘텐츠 인덱스를 시드 중이거나 둘 다 시드 중입니다. 시드가 성공적으로 완료되면 복사본 상태가 Initializing으로 변경됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>SeedingSource</p></td>
<td><p>사서함 데이터베이스 복사본은 데이터베이스 복사본 시드 작업을 위한 원본으로 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p>Suspended</p></td>
<td><p>관리자가 <strong>Suspend-MailboxDatabaseCopy</strong> cmdlet을 실행하여 데이터베이스 복사본을 수동으로 일시 중단하였기 때문에 사서함 데이터베이스 복사본이 Suspended 상태입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Healthy</p></td>
<td><p>사서함 데이터베이스 복사본이 로그 파일을 올바르게 복사 및 재생하고 있거나 모든 사용 가능한 로그 파일을 성공적으로 복사하고 재생했습니다.</p></td>
</tr>
<tr class="even">
<td><p>ServiceDown</p></td>
<td><p>Microsoft Exchange 복제 서비스를 사용할 수 없거나 사서함 데이터베이스 복사본을 호스팅하는 서버에서 복제 서비스가 실행 중입니다.</p></td>
</tr>
<tr class="odd">
<td><p>Initializing</p></td>
<td><p>데이터베이스 복사본이 만들어졌을 때, Microsoft Exchange 복제 서비스가 시작 중이거나 시작되었을 때, Suspended, ServiceDown, Failed, Seeding 또는 SinglePageRestore에서 다른 상태로 전환될 때 사서함 데이터베이스 복사본은 Initializing 상태입니다. 이 상태일 때 시스템은 데이터베이스 및 로그 스트림이 일관성 있는 상태인지 확인하는 중입니다. 대부분의 경우 복사의 Initializing 상태는 약 15초 동안 유지되지만 모든 경우에 일반적으로 이 상태는 30초 이상을 초과하지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>Resynchronizing</p></td>
<td><p>두 복사본 간의 차이를 확인하기 위해 사서함 데이터베이스 복사본 및 로그 파일이 현재 데이터베이스의 활성 복사본과 비교되고 있습니다. 확산이 탐지되고 해결될 때까지 복사본 상태가 이대로 유지됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>Mounted</p></td>
<td><p>활성 복사본이 온라인 상태이고 클라이언트 연결을 허용하고 있습니다. 사서함 데이터베이스 복사본의 활성 복사본 상태만 Mounted가 될 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>Dismounted</p></td>
<td><p>활성 복사본이 오프라인 상태이고 클라이언트 연결을 허용하고 있지 않습니다. 사서함 데이터베이스 복사본의 활성 복사본 상태만 Dismounted가 될 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>Mounting</p></td>
<td><p>활성 복사본이 온라인 상태로 전환 중이고 아직 클라이언트 연결을 허용하고 있지 않습니다. 사서함 데이터베이스 복사본의 활성 복사본 상태만 Mounting이 될 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>Dismounting</p></td>
<td><p>활성 복사본이 오프라인 상태로 전환 중이고 클라이언트 연결을 종료하는 중입니다. 사서함 데이터베이스 복사본의 활성 복사본 상태만 Dismounting이 될 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>DisconnectedAndHealthy</p></td>
<td><p>사서함 데이터베이스 복사본이 더 이상 활성 데이터베이스 복사본에 연결되어 있지 않고 연결이 끊길 때 Healthy 상태였습니다. 이 상태는 원본 데이터베이스 복사본에 연결된 관련 데이터베이스 복사본을 나타냅니다. 이 상태는 원본 복사본과 대상 데이터베이스 복사본 간 DAG 네트워크 장애 발생 시 보고될 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>DisconnectedAndResynchronizing</p></td>
<td><p>사서함 데이터베이스 복사본이 더 이상 활성 데이터베이스 복사본에 연결되어 있지 않고 연결이 끊길 때 Resynchronizing 상태였습니다. 이 상태는 원본 데이터베이스 복사본에 연결된 관련 데이터베이스 복사본을 나타냅니다. 이 상태는 원본 복사본과 대상 데이터베이스 복사본 간 DAG 네트워크 장애 발생 시 보고될 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>FailedAndSuspended</p></td>
<td><p>오류가 탐지되었고 오류를 해결하는 데 명시적으로 관리자의 개입이 필요하기 때문에 시스템에서 Failed 및 Suspended 상태를 동시에 설정했습니다. 예를 들어 시스템이 활성 사서함 데이터베이스와 데이터베이스 복사본 간에 복구할 수 없는 차이를 탐지한 경우가 있습니다. Failed 상태와 달리 시스템에서는 문제가 해결되었는지를 정기적으로 확인하여 자동으로 복구하지 않습니다. 대신에 데이터베이스 복사본이 정상적인 상태로 전환될 수 있도록 관리자가 개입하여 오류의 근본적인 원인을 해결해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p>SinglePageRestore</p></td>
<td><p>이 상태는 사서함 데이터베이스 복사본에서 단일 페이지 복원 작업이 실행 중임을 나타냅니다.</p></td>
</tr>
</tbody>
</table>


또한 **Get-MailboxDatabaseCopyStatus** cmdlet은 사용 중인 복제 네트워크의 세부 정보를 반환합니다(수동 데이터베이스 복사본에 대해 반환되는 *IncomingLogCopyingNetwork*, 복사본이 둘 이상 포함되어 있는 활성 데이터베이스에 대해 반환되는 *OutgoingConnections* 및 데이터베이스 시드 작업에 대한 원본으로 사용되는 모든 데이터베이스 복사본 포함). 나가는 연결 정보는 파일 모드 복제 상태의 데이터베이스 복사본에 제공됩니다. 나가는 연결 정보는 차단 모드 복제 상태의 데이터베이스 복사본에 제공되지 않습니다.

## Get-MailboxDatabaseCopyStatus 예

다음 예에서는 **Get-MailboxDatabaseCopyStatus** cmdlet을 사용합니다. 각 예에서는 **Format-List** cmdlet에 대한 결과를 파이프하여 출력을 목록 형식으로 표시합니다.

이 예에서는 DB2 데이터베이스의 모든 복사본에 대한 상태 정보를 반환합니다.

```powershell
Get-MailboxDatabaseCopyStatus -Identity DB2 | Format-List
```

이 예에서는 EXMBX2 사서함 서버의 모든 데이터베이스 복사본에 대한 상태를 반환합니다.

```powershell
Get-MailboxDatabaseCopyStatus -Server MBX2 | Format-List
```

이 예에서는 로컬 사서함 서버의 모든 데이터베이스 복사본에 대한 상태를 반환합니다.

```powershell
Get-MailboxDatabaseCopyStatus -Local | Format-List
```

**Get-MailboxDatabaseCopyStatus** cmdlet 사용에 대한 자세한 내용은 [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/ko-kr/library/dd298044\(v=exchg.150\))를 참조하십시오.

## Test-ReplicationHealth Cmdlet

[Test-ReplicationHealth](https://technet.microsoft.com/ko-kr/library/bb691314\(v=exchg.150\)) cmdlet을 사용하여 사서함 데이터베이스 복사본에 대한 연속 복제 상태 정보를 볼 수 있습니다. 이 cmdlet을 사용하여 복제 및 재생 상태의 모든 측면을 확인하여 DAG에 있는 특정 사서함 서버의 전체 개요를 제공할 수 있습니다.

**Test-ReplicationHealth** cmdlet은 연속 복제 및 연속 복제 파이프라인, Active Manager의 가용성, 기본 클러스터 서비스, 쿼럼 및 네트워크 구성 요소의 상태를 사전에 모니터링하는 데 사용됩니다. Test-ReplicationHealth는 DAG의 모든 사서함 서버에 대해 로컬 또는 원격으로 실행할 수 있습니다. **Test-ReplicationHealth** cmdlet은 다음 표에 나열된 테스트를 수행합니다.

### Test-ReplicationHealth cmdlet 테스트

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>테스트 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ClusterService</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 클러스터 서비스가 실행 중이고 연결 가능한지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>ReplayService</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) Microsoft Exchange 복제 서비스가 실행 중이고 연결 가능한지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>ActiveManager</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 실행 중인 Active Manager의 인스턴스가 유효한 역할(기본, 보조 또는 독립 실행형)인지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>TasksRpcListener</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) Tasks RPC(원격 프로시저 호출) 서버가 실행 중이고 연결 가능한지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>TcpListener</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) TCP 로그 복사 수신기가 실행 중이고 연결 가능한지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>ServerLocatorService</p></td>
<td><p>Active Manager 클라이언트/서버가 Active Directory 및 Active Manager에서 조회를 수행하는 클라이언트 액세스 서버 및 DAG 구성원에서 처리되어 사용자의 사서함 데이터베이스가 활성 상태인 위치를 확인하는지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>DagMembersUp</p></td>
<td><p>모든 DAG 구성원이 사용 가능하고, 실행 중이고, 연결 가능한지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>ClusterNetwork</p></td>
<td><p>지정된 DAG 구성원의 모든 클러스터 관리 네트워크(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버)를 사용할 수 있는지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>QuorumGroup</p></td>
<td><p>기본 클러스터 그룹(쿼럼 그룹)이 정상적이고 온라인 상태인지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>FileShareQuorum</p></td>
<td><p>DAG에 대해 구성된 미러링 모니터 서버, 감시 디렉터리 및 공유가 연결 가능한지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>DatabaseRedundancy</p></td>
<td><p>지정된 DAG 구성원에(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에) 데이터베이스의 사용 가능한, 정상 복사본이 하나 이상 있는지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>DatabaseAvailability</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 데이터베이스의 가용성이 충분한지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>DBCopySuspended</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 사서함 데이터베이스 복사본이 Suspended 상태인지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>DBCopyFailed</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 사서함 데이터베이스 복사본이 Failed 상태인지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>DBInitializing</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 사서함 데이터베이스 복사본이 Initializing 상태인지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>DBDisconnected</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 사서함 데이터베이스 복사본이 Disconnected 상태인지 확인합니다.</p></td>
</tr>
<tr class="odd">
<td><p>DBLogCopyKeepingUp</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 데이터베이스의 수동 복사본에 의한 로그 복사 및 검사가 활성 복사본의 로그 생성 작업을 따라갈 수 있는지 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>DBLogReplayKeepingUp</p></td>
<td><p>지정된 DAG 구성원에서(또는 DAG 구성원이 지정되지 않은 경우 로컬 서버에서) 데이터베이스의 수동 복사본에 대한 재생 작업이 로그 복사 및 검사 작업을 따라갈 수 있는지 확인합니다.</p></td>
</tr>
</tbody>
</table>


## Test-ReplicationHealth 예

이 예에서는 **Test-ReplicationHealth** cmdlet을 사용하여 MBX1 사서함 서버의 복제 상태를 테스트합니다.

```powershell
Test-ReplicationHealth -Identity MBX1
```

## 크림슨 채널 이벤트 로깅

Windows에는 Windows 로그 및 응용 프로그램 및 서비스 로그 등 두 가지 범주의 이벤트 로그가 포함됩니다. Windows 로그 범주에는 이전 버전의 Windows에서 사용할 수 있는 이벤트 로그 응용 프로그램, 보안 및 시스템 이벤트 로그가 포함됩니다. 또한 두 개의 새 로그 설치 로그 및 ForwardedEvents 로그도 포함됩니다. Windows 로그는 레거시 응용 프로그램의 이벤트 및 전체 시스템에 적용되는 이벤트를 저장하는 데 사용됩니다.

응용 프로그램 및 서비스 로그는 새로운 범주의 이벤트 로그입니다. 이러한 로그는 시스템 전체에 영향을 미칠 수 있는 이벤트가 아닌 단일 응용 프로그램 또는 구성 요소의 이벤트를 저장합니다. 이러한 새로운 범주의 이벤트 로그를 응용 프로그램의 크림슨 채널이라고 합니다.

응용 프로그램 및 서비스 로그 범주에는 네 개의 하위 유형인 관리, 운영, 분석 및 디버그 로그가 포함됩니다. 관리 로그의 이벤트는 이벤트 로그 레코드를 사용하여 문제를 해결하는 경우에 특히 유용합니다. 관리 로그의 이벤트는 이벤트에 응답하는 방법에 대한 지침을 제공합니다. 운영 로그의 이벤트도 유용하지만 관리자 개입이 더 많이 필요할 수 있습니다. 관리 및 디버그 로그는 사용자에게 친숙하지 않습니다. 분석 로그(기본적으로 숨겨져 있고 사용할 수 없도록 설정됨)는 문제를 추적하는 이벤트를 저장하고 많은 양의 이벤트가 기록되는 경우가 많습니다. 디버그 로그는 개발자가 응용 프로그램을 디버깅할 때 사용됩니다.

Exchange 2013은 응용 프로그램 및 서비스 로그 영역의 크림슨 채널에 이벤트를 기록합니다. 다음 단계를 수행하여 이러한 채널을 볼 수 있습니다.

1.  이벤트 뷰어를 엽니다.

2.  콘솔 트리에서 **응용 프로그램 및 서비스 로그** \> **Microsoft** \> **Exchange**로 이동합니다.

3.  **Exchange** 이벤트를 보려면 DAG와 데이터베이스 복사본 관련 이벤트, 또는 **ActiveMontoring** 또는 **ManagedAvailability** 을 참조 하려면 **HighAvailability** 또는 **MailboxDatabaseFailureItems** 등의 크림슨 채널을 선택 관리 되는 가용성 관련이 있습니다.

HighAvailability 채널에는 Microsoft Exchange 복제 서비스의 시작 및 종료와 관련된 이벤트 및 Microsoft Exchange 복제 서비스 내에서 실행되는 다양한 구성 요소(예: Active Manager, 타사 동시 복제 API, Tasks RPC 서버, TCP 수신기 및 VSS(볼륨 섀도 복사본 서비스) 기록기)가 포함됩니다. HighAvailability 채널은 또한 Active Manager에서 Active Manager 역할 모니터링과 관련된 이벤트 및 데이터베이스 작업 이벤트(예: 데이터베이스 탑재 작업 및 로그 자르기)를 로깅하고 DAG의 기본 클러스터와 관련된 이벤트를 기록하는 데도 사용됩니다.

MailboxDatabaseFailureItems 채널은 복제된 사서함 데이터베이스에 영향을 주는 모든 오류와 연관된 이벤트를 기록하는 데 사용됩니다.

ActiveMonitoring 채널 관리 되는 가용성 프로브, 모니터 및 응답자에 대 한 이벤트를 정의 하 고 결과 포함합니다.

ManagedAvailability 채널 복구 작업 로그 및 결과 관련 된 이벤트를 포함 합니다.

## 부족 한 디스크 공간 모니터

Exchange 2013 사서함 서버 역할에서 사용 하는 볼륨에 사용 가능한 디스크 공간의 크기를 포함 하 여 분 마다 가용성 모니터 수백 개의 시스템 메트릭 및 구성 요소를 관리 합니다. Exchange 2013 서비스 팩 1 (SP1) 하기 전에 Exchange 볼륨 모든 데이터베이스를 포함 하지 않거나 로그 파일을 포함 하는 모든 로컬 볼륨에 사용 가능한 공간을 모니터링 합니다. S p 1에서 이동 하 고 나중에 Exchange 데이터베이스를 포함 하 고 로그 파일 볼륨 모니터링 됩니다. S p 1에서 낮은 볼륨 공간 모니터에 대 한 기본 임계값은 200GB입니다. Exchange 2013 6 이상과 누적 업데이트에에서는 기본 임계값은 180 g B입니다. S p 1에서 이동 하 고 나중에 사용자 지정 하려는 각 사서함 서버에는 임계값 (MB)에서 다음 DWORD 레지스트리 값을 추가 하 여 구성할 수 있습니다.

경로: **HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\ExchangeServer\\v15\\Replay\\Parameters**

값: *SpaceMonitorLowSpaceThresholdInMB*

100GB로 임계값을 구성 하는 예에 대 한 다음 레지스트리 값을 구성할 것 있습니다.

**REG\_DWORD 186a0 (100000)**

을 구성 하거나 위의 레지스트리 값을 수정 후 변경 내용을 적용 하려면 Microsoft Exchange DAG 관리 서비스를 다시 시작 해야 합니다.

## CollectOverMetrics.ps1 스크립트

Exchange 2013에는 CollectOverMetrics.ps1이라는 스크립트가 있고 이는 Scripts 폴더에서 찾아볼 수 있습니다. CollectOverMetrics.ps1은 DAG 구성원 이벤트 로그를 읽어 특정 기간의 데이터베이스 작업에 대한 정보(데이터베이스 탑재, 이동 및 장애 조치 등)를 수집합니다. 각 작업에 대해 스크립트는 다음 정보를 기록합니다.

  - 데이터베이스의 ID

  - 작업이 시작되고 종료된 시간

  - 작업 시작 및 종료 시에 데이터베이스가 탑재된 서버

  - 작업 이유

  - 작업이 성공한 경우, 실패한 작업이 있는 경우, 오류 세부 정보

스크립트는 행당 하나의 작업씩 정보를 .csv 파일에 작성합니다. 각 DAG에 대해 별도의 .csv 파일을 작성합니다.

이 스크립트는 스크립트의 동작 및 출력을 사용자 지정할 수 있는 매개 변수를 지원합니다. 예를 들어, *Database* 또는 *ReportFilter* 매개 변수를 사용하여 지정된 하위 집합으로 결과를 제한할 수 있습니다. 이러한 필터와 일치하는 작업만이 요약 HTML 보고서에 포함됩니다. 사용 가능한 매개 변수는 다음 표에 나열되어 있습니다.

### CollectOverMetrics.ps1 스크립트 매개 변수

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DatabaseAvailabilityGroup</em></p></td>
<td><p>메트릭을 수집할 DAG의 이름을 지정합니다. 이 매개 변수를 생략하면 로컬 서버가 구성원으로 속한 DAG가 사용됩니다. 여러 DAG의 보고서에서 정보를 수집하고 보고하는 데 와일드카드 문자를 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Database</em></p></td>
<td><p>보고서를 생성해야 할 데이터베이스의 목록을 제공합니다. 와일드카드 문자가 지원됩니다(예: <code>-Database:&quot;DB1&quot;,&quot;DB2&quot;</code> 또는 <code>-Database:&quot;DB*&quot;</code>).</p></td>
</tr>
<tr class="odd">
<td><p><em>StartTime</em></p></td>
<td><p>보고 기간을 지정합니다. 이 기간 동안 스크립트는 로그된 이벤트만을 수집합니다. 즉, 스크립트는 부분 작업 레코드를 캡처할 수 있습니다(예를 들어, 해당 기간이 시작될 때의 작업 끝 또는 그 반대의 경우만). <em>StartTime</em> 또는 <em>EndTime</em>이 지정되지 않은 경우 스크립트의 기본값은 지난 24시간이 됩니다. 하나의 매개 변수만 지정된 경우 기간은 24시간이며 지정된 시간의 시작 또는 끝입니다.</p></td>
</tr>
<tr class="even">
<td><p><em>EndTime</em></p></td>
<td><p>보고 기간을 지정합니다. 이 기간 동안 스크립트는 로그된 이벤트만을 수집합니다. 즉, 스크립트는 부분 작업 레코드를 캡처할 수 있습니다(예를 들어, 해당 기간이 시작될 때의 작업 끝 또는 그 반대의 경우만). <em>StartTime</em> 또는 <em>EndTime</em>이 지정되지 않은 경우, 스크립트의 기본값은 지난 24시간입니다. 하나의 매개 변수만이 지정된 경우 기간은 24시간이며 지정된 시간의 시작 또는 끝입니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>이벤트 처리 결과를 저장하는 데 사용할 폴더를 지정합니다. 이 매개 변수를 생략하면 Scripts 폴더가 사용됩니다. 지정된 경우, 스크립트는 스크립트에서 생성된 .csv 파일의 목록을 가져와 이를 원본 데이터로 사용하여 요약 HTML 보고서를 생성합니다. 보고서는 -GenerateHtmlReport 옵션을 사용하여 생성된 것과 같습니다. 여러 다른 시간 또는 중복된 시간이라도 여러 DAG에 파일이 생성될 수 있으며 스크립트는 모든 데이터를 병합합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>GenerateHtmlReport</em></p></td>
<td><p>스크립트는 기록된 모든 정보를 수집하며 작업 유형별로 데이터를 분류한 다음 각 그룹의 통계를 포함하는 HTML 파일을 생성하도록 지정합니다. 보고서에는 각 그룹에 총 작업 수, 실패한 작업의 수, 각 그룹 내에서 소요된 시간의 통계가 포함됩니다. 또한 보고서에는 작업 실패로 인해 발생한 오류 유형의 검색 결과도 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>ShowHtmlReport</em></p></td>
<td><p>HTML로 생성된 보고서가 생성 후 웹 브라우저에 표시되도록 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>SummariseCsvFiles</em></p></td>
<td><p>스크립트는 스크립트에서 이전에 생성한 기존 .csv 파일에서 데이터를 읽도록 지정합니다. 이 데이터는 <em>GenerateHtmlReport</em> 매개 변수에서 생성된 보고서와 유사한 요약 보고서를 생성하는 데 사용됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>ActionType</em></p></td>
<td><p>스크립트가 수집해야 하는 작업 조치 유형을 지정합니다. 이 매개 변수의 값은 <code>Move</code>, <code>Mount</code>, <code>Dismount</code> 및 <code>Remount</code>입니다. <code>Move</code> 값은 데이터베이스가 활성 서버를 변경하는 시간, 이동이나 장애 조치로 제어되는지 여부를 참조합니다. <code>Mount</code>, <code>Dismount</code> 및 <code>Remount</code> 값은 다른 컴퓨터로 이동하지 않고 데이터베이스가 탑재된 상태를 변경하는 시간을 참조합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>ActionTrigger</em></p></td>
<td><p>스크립트에서 수집되어야 하는 관리 작업을 지정합니다. 이 매개 변수의 값은 <code>Admin</code> 또는 <code>Automatic</code>입니다. 자동 조치는 시스템에서 자동으로 수행됩니다(예를 들어, 서버가 오프라인인 경우의 장애 조치(failover)). 관리 조치는 Exchange 관리 셸 또는 Exchange 관리 센터를 사용하여 관리자가 수행한 조치입니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>RawOutput</em></p></td>
<td><p>스크립트는 write-output과 마찬가지로 .csv 파일에 직접 작성된 결과를 출력 스트림에 작성하도록 지정합니다. 이 정보는 다른 명령으로 파이프될 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>IncludedExtendedEvents</em></p></td>
<td><p>스크립트는 데이터베이스를 탑재하는 데 소요된 시간의 진단 세부 내용을 제공하는 이벤트를 수집하도록 지정합니다. 서버의 응용 프로그램 이벤트 로그가 클 경우 시간이 오래 소요되는 단계일 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>MergeCSVFiles</em></p></td>
<td><p>스크립트는 각 작업에 대한 데이터를 포함한 모든 .csv 파일을 가져와서 단일 .csv 파일에 병합하도록 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>ReportFilter</em></p></td>
<td><p>필터가 .csv 파일에 나타난 대로 필드를 사용하여 작업에 적용되도록 지정합니다. 이 매개 변수는 각 요소가 <code>$_</code>로 설정되며 부울 값을 반환하는 <code>Where</code> 작업과 동일한 형식을 사용합니다. 예를 들면 다음과 같습니다. <code>{$_DatabaseName -notlike &quot;Mailbox Database*&quot;}</code>는 보고서에서 기본 데이터베이스를 제외하는 데 사용될 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## CollectOverMetrics.ps1 예

다음 예에서는 DAG DAG1에서 DB\*(와일드카드 문자 포함)가 일치하는 모든 데이터베이스의 메트릭을 수집합니다. 메트릭이 수집되면 HTML 보고서가 생성되고 표시됩니다.

    CollectOverMetrics.ps1 -DatabaseAvailabilityGroup DAG1 -Database:"DB*" -GenerateHTMLReport -ShowHTMLReport

다음 예에서는 요약 HTML 보고서가 필터링될 수 있는 방법을 나타냅니다. 첫 번째 방법은 데이터베이스 이름의 목록을 가져오는 *Database* 매개 변수를 사용하는 것입니다. 요약 보고서에는 이들 데이터베이스에 대한 데이터만이 포함됩니다. 다음 두 예에서는 *ReportFilter* 옵션을 사용합니다. 마지막 예에서는 모든 기본 데이터베이스를 필터링합니다.

    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -Database MailboxDatabase123,MailboxDatabase456
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { $_.DatabaseName -notlike "Mailbox Database*" }
    CollectOverMetrics.ps1 -SummariseCsvFiles (dir *.csv) -ReportFilter { ($_.ActiveOnStart -like "ServerXYZ*") -and ($_.ActiveOnEnd -notlike "ServerXYZ*") }

## CollectReplicationMetrics.ps1 스크립트

Exchange 2013에 포함된 다른 상태 메트릭 스크립트는 CollectReplicationMetrics.ps1입니다. 이 스크립트는 스크립트가 실행 중일 때 실시간으로 메트릭을 수집하므로 활성 형태의 모니터링을 제공합니다. CollectReplicationMetrics.ps1은 데이터베이스 복제와 관련된 성능 카운터의 데이터를 수집합니다. 스크립트는 여러 사서함 서버의 카운터 데이터를 수집하며, 각 서버의 데이터를 .csv 파일에 작성한 다음 이 데이터 전체에 다양한 통계를 보고합니다(예를 들어, 각 복사본이 실패하거나 일시 중단된 시간, 평균 복사본 또는 재생 큐 길이 또는 복사본이 장애 조치 조건 밖에 있는 시간).

개별적으로 서버를 지정하거나 전체 DAG를 지정할 수 있습니다. 스크립트를 실행하여 첫 번째로 데이터를 수집한 다음 보고서를 생성하거나, 아니면 스크립트를 실행하여 데이터만을 수집하거나 이미 수집된 데이터에 대해 보고할 수 있습니다. 데이터가 샘플링되는 빈도 및 데이터를 수집하는 총 기간을 지정할 수 있습니다.

각 서버에서 수집된 데이터는 파일 이름 **CounterData.\<ServerName\>.\<TimeStamp\>.csv**로 작성됩니다. *DagName* 매개 변수로 스크립트를 실행하지 않은 경우 요약 보고서는 **HaReplPerfReport.\<DAGName\>.\<TimeStamp\>.csv** 또는 **HaReplPerfReport.\<TimeStamp\>.csv**라는 이름의 파일에 작성됩니다.

스크립트는 Windows PowerShell 작업을 시작하여 각 서버에서 데이터를 수집합니다. 데이터가 수집되는 전체 시간 동안 이러한 작업을 실행합니다. 여러 서버를 지정하는 경우 이 프로세스는 상당한 양의 메모리를 사용할 수 있습니다. 데이터가 요약 보고서로 처리되는 프로세스의 마지막 단계에서는 대용량의 데이터를 처리하기 위해 시간이 꽤 소요될 수도 있습니다. 한 대의 컴퓨터에서 수집 단계를 실행한 다음 다른 컴퓨터에서 데이터를 처리하도록 복사할 수 있습니다.

CollectReplicationMetrics.ps1 스크립트는 스크립트의 동작 및 출력을 사용자 지정할 수 있는 매개 변수를 지원합니다. 사용 가능한 매개 변수는 다음 표에 나열되어 있습니다.

### CollectReplicationMetrics.ps1 스크립트 매개 변수

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DagName</em></p></td>
<td><p>메트릭을 수집할 DAG의 이름을 지정합니다. 이 매개 변수를 생략하면 로컬 서버가 구성원으로 속한 DAG가 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>DatabaseNames</em></p></td>
<td><p>보고서를 생성해야 할 데이터베이스의 목록을 제공합니다. 와일드카드 문자를 사용할 수 있습니다(예: <code>-DatabaseNames:&quot;DB1&quot;,&quot;DB2&quot;</code> 또는 <code>-DatabaseNames:&quot;DB*&quot;</code>).</p></td>
</tr>
<tr class="odd">
<td><p><em>ReportPath</em></p></td>
<td><p>이벤트 처리 결과를 저장하는 데 사용할 폴더를 지정합니다. 이 매개 변수를 생략하면 Scripts 폴더가 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Duration</em></p></td>
<td><p>수집 프로세스를 실행할 기간을 지정합니다. 일반적인 값은 1시간에서 3시간입니다. 각 샘플 사이의 긴 간격 또는 예약된 작업에서 실행한 일련의 더 짧은 작업으로만 더 긴 기간이 사용되어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>Frequency</em></p></td>
<td><p>데이터 메트릭을 수집할 빈도를 지정합니다. 일반적인 값은 30초, 1분 또는 5분입니다. 일반적으로, 이보다 더 짧은 간격은 각 샘플 사이의 주요 변경 내용을 나타내지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Servers</em></p></td>
<td><p>통계를 수집할 서버의 ID를 지정합니다. 와일드카드 문자 또는 GUID를 포함한 값을 지정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><em>SummariseFiles</em></p></td>
<td><p>.csv 파일의 목록을 지정하여 요약 보고서를 생성합니다. <strong>CounterData.&lt;CounterData&gt;*</strong>라는 파일이 있으며 CollectReplicationMetrics.ps1 스크립트에서 생성됩니다.</p></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>스크립트가 실행되는 처리 단계를 지정합니다. 다음 값을 사용할 수 있습니다.</p>
<ul>
<li><p><code>CollectAndReport</code>   이 값은 기본값입니다. 이 값은 스크립트가 서버에서 데이터를 수집한 다음 요약 보고서를 생성하도록 처리해야 한다는 것을 모두 의미합니다.</p></li>
<li><p><code>CollectOnly</code>   이 값은 스크립트가 데이터만을 수집하고 보고서를 생성하지 않음을 의미합니다.</p></li>
<li><p><code>ProcessOnly</code>   이 값은 스크립트가 .csv 파일에서 데이터를 가져와 요약 보고서를 생성하도록 처리함을 의미합니다. <em>SummariseFiles</em> 매개 변수는 처리할 파일 목록이 있는 스크립트를 제공하는 데 사용됩니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>MoveFilestoArchive</em></p></td>
<td><p>스크립트는 파일을 처리한 후 압축된 폴더로 이동하도록 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><em>LoadExchangeSnapin</em></p></td>
<td><p>스크립트가 셸 명령을 로드하도록 지정합니다. 스크립트를 예약된 작업에서와 같이 셸 밖에서 실행해야 할 때 이 매개 변수가 유용합니다.</p></td>
</tr>
</tbody>
</table>


## CollectReplicationMetrics.ps1 예

다음 예에서는 1시간짜리 데이터를 1분 간격으로 샘플링된 DAG DAG1의 모든 서버에서 수집하여 요약 보고서를 생성합니다. 또한 *ReportPath* 매개 변수가 사용되며 이로 인해 스크립트가 모든 파일을 현재 디렉터리에 배치합니다.

```powershell
CollectReplicationMetrics.ps1 -DagName DAG1 -Duration "01:00:00" -Frequency "00:01:00" -ReportPath
```

다음 예에서는 CounterData\*와 일치하는 모든 파일에서 데이터를 읽은 다음 요약 보고서를 생성합니다.

    CollectReplicationMetrics.ps1 -SummariseFiles (dir CounterData*) -Mode ProcessOnly -ReportPath

