---
title: '메시징 레코드 관리에 대 한 성능 카운터: Exchange 2013 Help'
TOCTitle: 메시징 레코드 관리에 대 한 성능 카운터
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 51407733
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시징 레코드 관리에 대 한 성능 카운터

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

이 항목의 성능 카운터는 Microsoft Exchange Server 2010용 MRM(메시징 레코드 관리)을 구현하면서 관리되는 폴더 도우미를 모니터링합니다. 관리되는 폴더 도우미를 실행하는 데에는 리소스가 많이 사용되기 때문에 서버가 추가 부하를 견딜 수 있는 경우에만 실행해야 합니다. 관리되는 폴더 도우미가 실행 중일 때 서버 성능도 모니터링해야 합니다. 이 항목에 나열된 성능 카운터와 함께 디스크 성능, CPU 사용 등의 항목을 모니터링하는 추가 성능 카운터를 모니터링할 수도 있습니다.

MRM을 실행하는 컴퓨터 모니터링에 대한 자세한 내용은 [모니터링 메시징 레코드 관리](monitoring-messaging-records-management-exchange-2013-help.md)을 참조하십시오.

## MRM에 대한 성능 카운터

다음 표에서는 MRM에 대한 성능 카운터를 설명합니다.

### 성능 카운터, 성능 개체 및 설명

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>성능 카운터</th>
<th>성능 개체</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Average Mailbox Processing Time In Seconds</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>시간 기반 도우미의 평균 사서함 처리 시간을 계산합니다.</p></td>
</tr>
<tr class="even">
<td><p>Mailboxes Processed</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>서비스가 시작된 후에 시간 기반 도우미가 처리한 사서함의 수를 계산합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Mailboxes processed/sec</p></td>
<td><p>MSExchange Assistants</p></td>
<td><p>시간 기반 도우미가 처리한 초당 사서함 비율을 확인합니다.</p></td>
</tr>
<tr class="even">
<td><p>Items Deleted but Recoverable</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>가장 최근의 일정 간격이 시작된 이후로 관리되는 폴더 도우미가 삭제한 항목의 수를 계산합니다. 복구 가능한 항목 폴더를 통해 항목을 복구할 수 있습니다. 이 숫자에는 일정 간격 동안 처리하도록 예약된 사서함의 항목과 사용자가 처리하도록 지정한 사서함의 항목이 모두 포함됩니다. 이 카운터는 각 일정 간격이 시작될 때 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>Items Journaled</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>가장 최근의 일정 간격이 시작된 이후로 관리되는 폴더 도우미가 저널링한 항목의 수를 계산합니다. 이 숫자에는 현재 작업 주기 동안 처리하도록 예약된 사서함의 항목과 사용자가 처리하도록 지정한 사서함의 항목이 모두 포함됩니다. 이 카운터는 각 작업 주기가 시작될 때 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="even">
<td><p>Items Marked as Past Retention Date</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>가장 최근의 일정 간격이 시작된 이후로 관리되는 폴더 도우미가 보존 날짜가 지난 것으로 표시한 항목의 수를 계산합니다. 이 숫자에는 일정 간격 동안 처리하도록 예정된 사서함의 항목과 사용자가 처리하도록 지정한 사서함의 항목이 모두 포함됩니다. 이 카운터는 각 일정 간격이 시작될 때 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>Items Moved</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>가장 최근의 일정 간격이 시작된 이후로 관리되는 폴더 도우미가 이동한 항목의 수를 계산합니다. 이 숫자에는 일정 간격 동안 처리하도록 예정된 사서함의 항목과 사용자가 처리하도록 지정한 사서함의 항목이 모두 포함됩니다. 이 카운터는 각 일정 간격이 시작될 때 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="even">
<td><p>Items Permanently Deleted</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>가장 최근의 일정 간격이 시작된 이후로 관리되는 폴더 도우미가 영구적으로 삭제한 항목의 수를 계산합니다. 이 숫자에는 일정 간격 동안 처리하도록 예정된 사서함의 항목과 사용자가 처리하도록 지정한 사서함의 항목이 모두 포함됩니다. 이 카운터는 각 일정 간격이 시작될 때 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>Items Subject to Retention Policy</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>가장 최근의 일정 간격이 시작된 이후로 관리되는 폴더 도우미가 보존 정책을 적용한 항목의 수를 계산합니다. 이 숫자에는 일정 간격 동안 처리하도록 예정된 사서함의 항목과 사용자가 처리하도록 지정한 사서함의 항목이 모두 포함됩니다. 이 카운터는 각 일정 간격이 시작될 때 0으로 다시 설정됩니다. 이 카운터는 다음 4개의 만료 관련 카운터의 합계입니다.</p>
<ul>
<li><p>Items Journaled</p></li>
<li><p>Items Marked as Past Retention Date</p></li>
<li><p>Items Moved</p></li>
<li><p>Items Permanently Deleted</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsExpired - 보존 정책이 적용되는 항목 크기(바이트)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>관리되는 폴더 도우미에 의해 만료된 항목의 전체 크기를 나타냅니다(SoftDelete, HardDelete, MoveToArchive).</p>
<p>다음과 같은 항목이 포함됩니다.</p>
<ul>
<li><p>관리되는 폴더 사서함 정책에 의해 삭제되거나 관리되는 사용자 지정 폴더로 이동하는 메시지</p></li>
<li><p>사용자의 보존 정책에 따라 삭제되거나 보관함으로 이동하는 메시지</p></li>
<li><p>휴지통 정책에 의해 만료된 메시지</p></li>
<li><p>시스템 정리 태그에 의해 정리된 메시지</p></li>
</ul>
<p>이 카운터는 관리되는 폴더 도우미 작업 주기의 모든 작업 주기 검사점에서 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsSoftDeleted - 삭제되었지만 복구할 수 있는 항목 크기(바이트)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>관리되는 폴더 도우미에 의해 일시 삭제된 항목의 전체 크기를 나타냅니다.</p>
<p>다음과 같은 항목이 포함됩니다.</p>
<ul>
<li><p>관리되는 폴더 사서함 정책에 의해 일시 삭제된 메시지</p></li>
<li><p>보존 정책에 의해 일시 삭제된 메시지</p></li>
</ul>
<p>이 카운터는 관리되는 폴더 도우미 작업 주기의 모든 작업 주기 검사점에서 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="even">
<td><p>TotalSizeItemsPermanentlyDeleted - 영구적으로 삭제된 항목 크기(바이트)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>관리되는 폴더 도우미에 의해 일시 삭제된 항목의 전체 크기를 나타냅니다.</p>
<p>다음과 같은 항목이 포함됩니다.</p>
<ul>
<li><p>관리되는 폴더 사서함 정책에 의해 영구적으로 삭제된 메시지</p></li>
<li><p>보존 정책에 의해 영구적으로 삭제된 메시지</p></li>
<li><p>복구 가능한 항목 정책에 의해 영구적으로 삭제된 메시지</p></li>
</ul>
<p>이 카운터는 관리되는 폴더 도우미 작업 주기의 모든 작업 주기 검사점에서 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>TotalSizeItemsMoved - 보관 정책 태그로 인해 이동한 항목 크기(바이트)</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>관리되는 폴더 도우미에 의해 폴더로 이동하거나 보관함으로 이동한 항목의 전체 크기를 나타냅니다.</p>
<p>다음과 같은 항목이 포함됩니다.</p>
<ul>
<li><p>관리되는 폴더 사서함 정책에 의해 관리되는 사용자 지정 폴더로 이동한 메시지</p></li>
<li><p>보존 정책에 의해 개인 보관함으로 이동한 메시지</p></li>
</ul>
<p>이 카운터는 관리되는 폴더 도우미 작업 주기의 모든 작업 주기 검사점에서 0으로 다시 설정됩니다.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsWithPersonalTag - 개인 태그(만료 또는 보관)에 의해 스탬프 처리된 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>사용자가 항목에 개인 태그를 지정한 횟수를 나타냅니다.</p>
<p>여기에는 삭제 및 보관 태그가 모두 포함됩니다.</p>
<p>예를 들면 다음과 같습니다.</p>
<ul>
<li><p>항목에 개인 태그가 지정된 경우</p></li>
<li><p>개인 태그가 있는 항목에 다른 개인 태그를 다시 지정한 경우</p></li>
</ul>
<p>폴더에 개인 태그가 지정되면 폴더에 있는 전체 항목 수만큼 카운터가 올라갑니다.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsWithDefaultTag - 기본 태그(만료 또는 보관)에 의해 스탬프 처리된 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>사용자가 개인 태그가 지정된 메시지를 선택하고 <strong>폴더 정책 사용</strong>을 선택한 경우 등의 사용자 작업을 기반으로 DPT(기본 정책 태그)가 지정된 항목의 수를 나타냅니다.</p>
<p>새 사용자에게 DPT로 보존 정책을 지정한 경우 보존 정책에 의해 DPT가 지정되는 항목의 수만큼 카운터가 올라갑니다.</p>

> [!NOTE]
> 사용자가 DPT가 있는 보존 정책을 사용하는 경우 전송을 통해 도착하는 새 메시지는 기본 태그로 지정되지만 이 카운터로 추적되지는 않습니다.


</td>
</tr>
<tr class="even">
<td><p>TotalItemsWithSystemCleanupTag - 시스템 정리 태그로 스탬프 처리된 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>시스템 정리 태그가 지정된 항목의 수를 나타냅니다. 여기에는 사용자에게 표시되지 않는 사서함 메타데이터 항목이 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsExpiredByDefaultExpiryTag - 기본 만료 태그로 인해 만료된 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>보존 정책에서 개인 태그 이외의 태그(기본 또는 시스템)로 인해 관리되는 폴더 도우미에서 만료된(일시 삭제 또는 영구 삭제) 항목의 수를 나타냅니다.</p>
<p>복구 가능한 항목 정리나 시스템 정리로 인해 만료된 항목은 여기에 포함되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsExpiredByPersonalExpiryTag - 개인 만료 태그로 인해 만료된 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>보존 정책의 개인 태그로 인해 관리되는 폴더 도우미에서 만료된(일시 삭제 또는 영구 삭제) 항목의 수를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>TotalItemsMovedByDefaultArchiveTag - 기본 보관 태그로 인해 이동한 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>보존 정책에서 개인 보관 태그 이외의 태그(기본 또는 시스템)로 인해 관리되는 폴더 도우미에서 보관함으로 이동한 항목의 수를 나타냅니다.</p>
<p>복구 가능한 항목 정리로 인해 보관함의 복구 가능한 항목 폴더로 이동한 항목은 여기에 포함되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>TotalItemsMovedByPersonalArchiveTag - 보관 태그로 인해 이동한 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>보존 정책에서 개인 보관 태그로 인해 관리되는 폴더 도우미에서 보관함으로 이동한 항목의 수를 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>TotalMovedDumpsterItems - 사서함 휴지통 이동 항목</p></td>
<td><p>MSExchange Managed Folder Assistant</p></td>
<td><p>복구 가능한 항목 정리를 통해 보관함의 복구 가능한 항목 폴더로 이동한 항목의 수를 나타냅니다.</p></td>
</tr>
</tbody>
</table>

