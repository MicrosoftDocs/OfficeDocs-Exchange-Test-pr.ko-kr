---
title: '사서함 복원 요청 관리: Exchange 2013 Help'
TOCTitle: 사서함 복원 요청 관리
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50556035
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 복원 요청 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

사서함 복원 요청은 연결이 끊긴 사서함을 복원할 때 사용됩니다. 연결이 끊긴 사서함은 Active Directory 사용자 계정과 연결되지 않은 Exchange 사서함 데이터베이스의 사서함입니다. 사서함을 사용하지 않도록 설정하거나 삭제하거나 다른 데이터베이스로 이동하면 사서함의 연결이 끊깁니다. 자세한 내용은 [연결이 끊어진 사서함](disconnected-mailboxes-exchange-2013-help.md)을 참조하십시오.

연결이 끊긴 사서함은 사서함 데이터베이스의 삭제된 사서함 보존 설정에 지정된 기간 동안 사서함 데이터베이스에 남아 있습니다. 기본적으로 연결이 끊긴 사서함은 30일간 보존됩니다. 이 보존 기간 동안에는 삭제된 사서함의 내용을 기존 사서함으로 복원(복사)할 수 있습니다. 이 항목에서는 셸을 사용하여 사서함 복원 요청을 관리하는 방법을 설명합니다.

연결이 끊어진 사서함과 관련된 추가 관리 작업에 대한 자세한 내용은 다음 항목을 참조하십시오.

[사용 하지 않거나 사서함 삭제](disable-or-delete-a-mailbox-exchange-2013-help.md)

[비활성화 된 사서함에 연결](connect-a-disabled-mailbox-exchange-2013-help.md)

[삭제 된 사서함을 복원 또는 연결](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[일시 삭제 된 사서함 복원](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[사서함을 영구적으로 삭제](permanently-delete-a-mailbox-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 복원 요청" 항목

  - 이 항목의 프로시저만 셸에서 수행할 수 있습니다. 사서함 복원 요청을 관리하는 데 EAC를 사용할 수 없습니다.

  - 모든 사서함 복원 요청의 *Identity* 속성 값을 표시하려면 다음 명령을 실행합니다.
    
        Get-MailboxRestoreRequest | Format-Table Identity
    
    이 항목의 절차를 수행할 때 이 ID 값을 사용하면 특정 사서함 복원 요청을 지정할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 복원 요청 속성 보기

사서함 복원 요청의 상태에 대한 기본 정보를 제공하는 사서함 복원 요청 속성을 볼 수 있습니다.

모든 사서함 복원 요청의 *Identity* 속성 및 해당 값 목록을 표시하려면 다음 명령을 실행합니다.

    Get-MailboxRestoreRequest | Format-Table Identity

이 ID를 사용하여 특정 사서함 복원 요청에 대한 정보를 가져올 수 있습니다.

이 예에서는 *Identity* 매개 변수를 사용하여 복원 요청 "Pilar Pinilla \\MailboxRestore"의 상태를 반환합니다.

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"

이 예에서는 Pilar Pinilla 대상 사서함에 대한 두 번째 복원 요청과 관련된 모든 정보를 반환합니다.

    Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List

이 예에서는 원본 데이터베이스 MBD01에서 복원 중인 복원 요청 상태를 반환합니다.

    Get-MailboxRestoreRequest -SourceDatabase MBD01

이 예에서는 현재 진행 중인 모든 복원 요청을 반환합니다.

    Get-MailboxRestoreRequest -Status InProgress

그 밖의 유용한 상태로는 `Queued`, `Completed`, `Suspended` 및 `Failed`가 있습니다.

이 예에서는 일시 중단된 모든 복원 요청을 반환합니다.

    Get-MailboxRestoreRequest -Suspend $true

구문과 매개 변수에 대한 자세한 내용은 [Get-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829907\(v=exchg.150\))를 참조하십시오.

## Get-MailboxRestoreRequest 출력

기본적으로 **Get-MailboxRestoreRequest** cmdlet은 요청 이름, 데이터가 복원되는 대상 사서함 및 요청 상태를 반환합니다. 다음 표에서는 이 cmdlet을 **Format-List** cmdlet에 파이프할 경우 반환되는 유용한 정보를 보여줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>복원하려는, 연결이 끊긴 사서함이 포함된 데이터베이스를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>데이터를 복원할 사서함을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>요청의 이름을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Microsoft Exchange MRS(사서함 복제 서비스)가 요청의 자세한 상태를 저장하는 데이터베이스를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>요청의 상태를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>요청의 일시 중단 여부를 지정합니다. <strong>New-MailboxRestoreRequest</strong> cmdlet에 <em>Suspend</em> 매개 변수를 사용하여 사서함 복원을 요청한 경우 사서함 복원을 일시 중단할 수 있습니다. 사서함 복원 작업이 실패한 경우 또는 관리자가 <strong>Suspend-MailboxRestoreRequest</strong> cmdlet을 사용할 경우에도 사서함 복원이 일시 중단될 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>요청의 ID를 지정합니다. 이 ID는 대상 사서함 이름 및 요청 이름의 조합입니다.</p></td>
</tr>
</tbody>
</table>


## 작동 여부는 어떻게 확인합니까?

**Get-MailboxRestoreRequest** cmdlet을 실행하여 사서함 복원 요청의 속성을 볼 수 있는지 확인합니다. 오류가 반환되면 올바른 구문 및 ID를 사용하고 있는지 확인하십시오. cmdlet이 제대로 실행되었지만 결과가 반환되지 않는 경우도 있습니다. 예를 들어 사서함 복원 요청을 전송하고 `Get-MailboxRestoreRequest -Status InProgress` 명령을 실행했는데 결과가 반환되지 않으면 현재 실행 중인 복원 요청이 없는 것입니다.

## 셸을 사용하여 복원 요청 통계 보기

문제 해결 목적으로 사용할 수 있는 자세한 정보를 제공하는 사서함 복원 요청 통계를 볼 수 있습니다.

이 예에서는 복원 요청 danp\\MailboxRestore1에 대한 기본 통계를 반환합니다. 반환되는 정보에는 기본적으로 이름, 사서함, 상태 및 완료율이 포함됩니다.

    Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1

이 예에서는 Dan Park의 사서함에 대한 통계를 반환하고 보고서를 .csv 파일로 내보냅니다.

    Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv

이 예에서는 *IncludeReport* 매개 변수를 사용하고 결과를 **Format-List** cmdlet으로 파이프하여 Pilar Pinilla의 사서함에 대한 복원 요청과 관련된 추가 정보를 반환합니다.

    Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 

이 예에서는 *IncludeReport* 매개 변수를 사용하여 `Failed` 상태인 모든 복원 요청에 대한 추가 정보를 반환한 다음 해당 정보를 명령이 실행 중인 위치에 있는 AllRestoreReports.txt 파일에 저장합니다.

    Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt

구문과 매개 변수에 대한 자세한 내용은 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ko-kr/library/ff829912\(v=exchg.150\)) 및 [Get-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829907\(v=exchg.150\))을 참조하십시오.

## Get-MailboxRestoreRequestStatistics 출력

기본적으로 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ko-kr/library/ff829912\(v=exchg.150\)) cmdlet은 요청의 이름, 요청의 상태, 대상 사서함의 별칭 및 완료 백분율을 반환합니다. 다음 표에서는 이 cmdlet을 **Format-List** cmdlet에 파이프라이닝할 경우 반환되는 유용한 정보를 보여줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>값</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>요청의 이름을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>요청의 상태를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>요청 상태에 대한 세부 정보를 지정합니다. 예를 들어 <code>Status</code> 값이 <code>InProgress</code>를 반환하는 경우 <code>StatusDetail</code> 값은 <code>InProgress</code> 상태에 대한 특정 단계(예: <code>CreatingFolderHierarchy</code> 및 <code>CopyingMessages</code>)를 반환합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>복원 프로세스를 통해 요청이 진행되는 범위를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>복원 요청의 일시 중단 여부를 지정합니다. 다음 시나리오에서는 이 값이 <code>true</code>입니다.</p>
<ul>
<li><p>MRS가 중지되었거나 실패로 인해 요청을 중지하고 있습니다.</p></li>
<li><p>관리자가 요청을 일시 중단했습니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>데이터를 복원할 원본 사서함의 GUID를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>데이터를 복원할 원본 사서함 계층의 루트 폴더 이름을 지정합니다. 이 값이 비어 있으면 데이터가 최상위 정보 저장소 폴더에서 복원됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>원본 사서함이 있는 데이터베이스의 이름을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>복원할 사서함이 <code>Disabled</code>인지, <code>Soft-Deleted</code>인지 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>대상 사서함의 별칭을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>사서함이 아카이브로 복원되는지 여부를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>대상 사서함의 GUID를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>데이터를 복원할 대상 사서함 계층의 루트 폴더 이름을 지정합니다. 이 값이 비어 있으면 데이터가 최상위 정보 저장소 폴더로 복원됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>대상 사서함이 있는 데이터베이스의 이름을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>대상 사서함의 ID를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>복원하는 동안 포함할 폴더의 목록을 지정합니다. 이 값이 비어 있고 요청 시 폴더를 지정하지 않았으면 모든 폴더가 사서함으로 복원됩니다(<em>ExcludeFolders</em> 매개 변수를 사용하여 특정 폴더를 제외하지 않은 경우).</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>복원하는 동안 제외할 폴더의 목록을 지정합니다. 이 값이 비어 있고 요청 시 폴더를 지정하지 않았으면 모든 폴더가 사서함으로 복원됩니다(<em>IncludeFolders</em> 매개 변수를 사용하여 특정 폴더를 포함하지 않은 경우).</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>요청을 만들 때 복구할 수 있는 항목 폴더가 제외되었는지 여부를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>대상 및 소스 폴더에 일치하는 메시지가 있을 경우 MRS에 대한 동작을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>요청이 처리될 때 연결된 메시지를 복사할 것인지 여부를 지정합니다. 연결된 메시지는 규칙, 보기 및 양식에 대한 정보가 있는 숨겨진 데이터가 포함된 특별한 메시지입니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>요청이 손상된 메시지를 발견하는 경우 MRS에서 건너뛸 잘못된 항목 수를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>명령에 의해 발견되는 손상된 메시지 수를 지정합니다. <em>BadItemsEncountered</em> 값이 <em>BadItemLimit</em> 값보다 크면 요청이 실패합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>MRS로 요청이 시작된 날짜 및 시간을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>복원 요청이 MRS에 의해 처리되기 시작한 날짜 및 시간을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>요청이 마지막으로 변경된 날짜 및 시간을 지정합니다. 관리자 또는 MRS에 의해 변경되었을 수도 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>요청이 일시 중단된 날짜 및 시간을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>요청을 완료하는 데 걸린 시간을 지정합니다. 요청이 <code>Failed</code> 상태인 경우 이 값은 요청을 시작한 후 요청이 실패할 때까지 걸린 시간을 지정합니다. 요청이 완료되지 않은 경우 이 값은 시작 중인 요청과 실행 중인 <strong>Get-MailboxRestoreRequestStatistics</strong> cmdlet 사이의 시간을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>요청이 <code>Suspended</code> 상태에 있었던 시간을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>요청이 <code>Failed</code> 상태에 있었던 시간을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>요청이 <code>Queued</code> 상태에 있었던 시간을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>요청이 <code>In Progress</code> 상태에 있었던 시간을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>고가용성 때문에 요청이 중단되었던 시간을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>요청을 처리한 클라이언트 액세스 서버의 이름을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>복원된 총 파일 크기나, 요청이 <code>In Progress</code> 상태일 경우 MRS에서 복원할 것으로 예상되는 파일 크기를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>복원된 항목 수 또는 요청이 <code>In Progress</code> 상태인 경우 MRS에서 복원할 것으로 예상되는 항목 수를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>분당 전송된 평균 바이트 수를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>전송된 항목 수를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>완료된 요청의 백분율을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>완료된 복원 요청이 삭제되기 전까지 보존되는 기간을 지정합니다. 기본값은 30일입니다.</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>요청이 시작되지 않은 경우 이 값은 큐에서 요청의 위치를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>오류가 발생한 경우 이 값은 오류 코드를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>오류가 발생한 경우 이 값은 오류 유형을 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>오류가 발생한 경우 이 값은 오류가 대상 사서함에서 발생했는지, 원본 사서함에서 발생했는지를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>오류가 발생한 경우 이 값은 오류 메시지를 지정합니다. 이 값으로 일시 중단 설명을 지정할 수도 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>요청이 실패한 경우 이 값은 요청이 실패한 날짜 및 시간을 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>요청이 실패한 경우 이 값은 실패 시 수행 중이던 작업에 대한 정보를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>요청이 유효하지 않은 경우 이 값은 이유를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>MRS가 요청의 자세한 상태를 저장하는 데이터베이스를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>요청의 ID를 지정합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p><em>IncludeReport</em> 매개 변수를 사용한 경우 이 값은 요청 문제 해결에 사용할 수 있는 정보를 지정합니다.</p></td>
</tr>
</tbody>
</table>


## 작동 여부는 어떻게 확인합니까?

**Get-MailboxRestoreRequestStatistics** cmdlet을 실행하여 사서함 복원 요청의 통계를 볼 수 있는지 확인합니다. 오류가 반환되면 복원 요청에 올바른 ID를 사용하고 있는지 확인하십시오.

## 셸을 사용하여 복원 요청 속성 변경

사서함 복원 요청이 실패할 경우 **Set-MailboxRestoreRequest** cmdlet을 사용하여 요청의 속성을 변경해 문제를 해결할 수 있습니다.

이 예에서는 Debra Garcia의 사서함에 대한 복원 요청 MailboxRestore1이 10개의 손상된 사서함 항목을 건너뛰도록 지정합니다.

    Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10

이 예에서는 Florence Flipo의 사서함에 대한 복원 요청 MailboxRestore1이 100개의 손상된 사서함 항목을 건너뛰도록 지정합니다. *BadItemLimit* 값이 50보다 크기 때문에 *AcceptLargeDataLoss* 매개 변수가 지정되어야 합니다.

    Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss

구문과 매개 변수에 대한 자세한 내용은 [Set-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829909\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

복원 요청의 속성이 변경되었는지 확인하려면 **Get-MailboxRestoreRequestStatistics** cmdlet을 실행하여 복원 요청의 수정된 속성을 표시합니다. 복원 요청에 성공한 경우 *Status* 속성의 값은 `Queued`, `InProgress` 또는 `Completed`입니다. 복원 요청이 완료되면 일시 삭제된 사서함의 내용이 대상 사서함에 표시됩니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/ko-kr/library/ff829912\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 복원 요청 일시 중단

요청이 만들어진 후 `Completed` 상태에 이르기 전까지는 언제든지 복원 요청을 일시 중단할 수 있습니다. [Resume-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829908\(v=exchg.150\)) cmdlet을 사용하여 복원 요청을 다시 시작하는 명령 구문은 이 항목 뒷부분의 Use the Shell to resume a restore request을 참조하십시오.

이 예에서는 Pilar Pinilla의 사서함에 대한 복원 요청 MailboxRestore1을 일시 중단합니다.

    Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

이 예에서는 `InProgress` 상태인 모든 요청을 검색한 후 "Resume after FY13Q2 Maintenance"라는 일시 중단 설명과 함께 출력을 **Suspend-MailboxRestoreRequest** cmdlet으로 파이프하여, 진행 중인 복원 요청을 모두 일시 중단합니다.

    Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"

구문과 매개 변수에 대한 자세한 내용은 [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829906\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함 복원 요청이 일시 중단되었는지 확인하려면 다음 명령을 실행합니다.

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

*Suspend* 속성의 값이 `True`이면 복원 요청이 일시 중단된 것입니다. *Status* 속성의 값이 `Suspended`인 경우에도 복원 요청이 일시 중단되었음을 나타냅니다.

## 셸을 사용하여 복원 요청 다시 시작

**Resume-MailboxRestoreRequest** cmdlet을 사용하여 실패하거나 일시 중단된 복원 요청을 다시 시작할 수 있습니다.

이 예에서는 복원 요청 Pilar Pinilla\\MailboxRestore1을 다시 시작합니다.

    Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

이 예에서는 실패 상태인 모든 복원 요청을 다시 시작합니다.

    Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest

구문과 매개 변수에 대한 자세한 내용은 [Resume-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829908\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

복원 요청이 다시 시작되었는지 확인하려면 다음 명령을 실행합니다.

    Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status

*Suspend* 속성의 값이 `False`이면 복원 요청이 다시 시작된 것입니다. *Status* 속성의 값이 `InProgress`인 경우에도 복원 요청이 다시 시작되었음을 나타냅니다.

## 셸을 사용하여 복원 요청 제거

**Remove-MailboxRestoreRequest** cmdlet을 사용하여 사서함 복원 요청을 제거할 수 있습니다. 사서함 데이터를 대상 사서함으로 복사하기 시작한 후에 복원 요청을 제거할 경우 복사된 사서함 데이터는 대상 사서함에 남아 있습니다.


> [!NOTE]
> 앞에서 언급했듯이 완료된 복원 요청은 기본적으로 30일 동안 보존된 후 자동으로 삭제됩니다.



이 예에서는 복원 요청 Pilar Pinilla\\MailboxRestore1을 제거합니다.

    Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"

이 예에서는 완료 상태의 모든 복원 요청이 제거됩니다.

    Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest

이 예에서는 MBXDB01에 저장된 요청에 대해 *RequestGuid* 매개 변수를 사용하여 복원 요청을 취소합니다. *RequestGuid* 및 *RequestQueue* 매개 변수를 필요로 하는 매개 변수 집합을 Microsoft Replication Service 디버깅 목적으로만 사용됩니다. Microsoft 고객 지원 서비스에서 안내하는 경우에만 이 매개 변수 집합을 사용해야 합니다.

    Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f

구문과 매개 변수에 대한 자세한 내용은 [Remove-MailboxRestoreRequest](https://technet.microsoft.com/ko-kr/library/ff829910\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함 복원 요청이 제거되었는지 확인하려면 다음 명령을 실행합니다.

    Get-MailboxRestoreRequest -Identity <identity of removed restore request>

복원 요청이 없다는 내용의 오류가 반환됩니다.

**Get-MailboxRestoreRequest** cmdlet을 실행할 수도 있습니다. 복원 요청이 제거되었으면 결과에 해당 복원 요청이 포함되지 않습니다.

