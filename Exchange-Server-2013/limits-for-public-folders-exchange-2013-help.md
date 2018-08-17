---
title: '공용 폴더의 제한: Exchange 2013 Help'
TOCTitle: 공용 폴더의 제한
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61170955
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공용 폴더의 제한

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange Server 2013에서는 공용 폴더가 기존 데이터베이스 아키텍처에서 사서함 아키텍처로 이동되었습니다. 이러한 이동으로 인해 공용 폴더가 DAG(데이터베이스 사용 가능 그룹) 복원 기능 및 장기간에 걸쳐 향상된 기타 사서함 기능을 활용할 수 있게 되었습니다. 그러나 이러한 기능과 관련하여 고려해야 하는 새로운 제한 및 성능 관련 문제가 있습니다. 이 문서에서는 공용 폴더 성능 및 연결에 영향을 줄 수 있는 구성 옵션에 대한 몇 가지 지침을 간략하게 설명합니다.

## 제한

다음 표에 온-프레미스 Exchange Server 2013의 공용 폴더에 대 한 제한 합니다. 제한 권장 하는 대로 명시 구체적으로 경우가 아니면이 표에 나열 된 값은 공용 폴더에 대 한 지원 되는 제한 합니다.


> [!IMPORTANT]
> Office 365에 대 한 Exchange Online 제한 필요 하신가요? <A href="https://go.microsoft.com/fwlink/?linkid=391188">Exchange Online 제한</A>를 참조 하십시오.




<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>제한</th>
<th>참고</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>공용 폴더 사서함의 총 수</p></td>
<td><p>100</p></td>
<td><p>공용 폴더 사서함을 100개보다 많이 만들 수는 있지만 100개를 초과하는 사서함은 지원되지 않습니다. <a href="create-a-public-folder-mailbox-exchange-2013-help.md">공용 폴더 사서함 만들기</a></p></td>
</tr>
<tr class="even">
<td><p>계층 구조의 총 공용 폴더 수</p></td>
<td><p>1,000,000</p></td>
<td><p>개 이상의 1000000 공용 폴더를 만들 수 있지만, 지원 되지 않습니다. 100, 000 또는 더 공용 폴더의 모든 배포의 경우 <a href="considerations-when-deploying-public-folders-exchange-2013-help.md">공용 폴더를 배포할 때의 고려 사항</a>를 읽는 것이 좋습니다.</p></td>
</tr>
<tr class="odd">
<td><p>상위 폴더 아래의 하위 폴더</p></td>
<td><p>10,000</p></td>
<td><p>상위 폴더 아래에 1000 개이 내의 하위 폴더를 만들 수는 있지만 이렇게 하면 좋습니다 메시지가 표시 하지 않습니다.</p>
<p><a href="https://technet.microsoft.com/ko-kr/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet에서 <em>FolderHierarchyChildrenCountReceiveQuota</em> 매개 변수를 사용하여 설정합니다.</p></td>
</tr>
<tr class="even">
<td><p>폴더 수준</p></td>
<td><p>300</p></td>
<td><p>폴더 수준은 공용 폴더 트리의 분기 하나에 포함될 수 있는 중첩된 폴더의 수준 수입니다. <a href="https://technet.microsoft.com/ko-kr/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet에서 <em>FolderHierarchyDepthRecieveQuota</em> 매개 변수를 사용하여 설정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더당 최대 메시지 수</p></td>
<td><p>1백만 개</p></td>
<td><p><a href="https://technet.microsoft.com/ko-kr/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet에서 <em>MailboxMessagesPerFolderCountRecieveQuota</em> 매개 변수를 사용하여 설정합니다.</p></td>
</tr>
<tr class="even">
<td><p>최대 개별 공용 폴더 크기</p></td>
<td><p>10GB</p></td>
<td><p>단일 폴더 아래의 하위 폴더는 이 제한에 포함되지 않습니다.</p>
<p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">사서함에 대 한 저장소 할당량 구성</a></p></td>
</tr>
<tr class="odd">
<td><p>공용 폴더 사서함 크기</p></td>
<td><p>100GB</p></td>
<td><p><a href="configure-storage-quotas-for-a-mailbox-exchange-2013-help.md">사서함에 대 한 저장소 할당량 구성</a></p></td>
</tr>
<tr class="even">
<td><p>공용 폴더 사서함당 사용자 로그온 수</p></td>
<td><p>2,000번의 동시 사용자 로그온</p></td>
<td><p>공용 폴더 사서함당 사용자 수가 2,000명을 넘지 않도록 계층 구조를 구성하는 것이 좋습니다. 예를 들어 사용자가 20,000명이면 공용 폴더 사서함 10개를 사용해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>이동된 항목 보존 기간</p></td>
<td><p>14일(권장)</p></td>
<td><p><strong>Set-OrganizationConfig</strong> cmdlet에서 <em>DefaultPublicFolderMovedItemRetention</em> 매개 변수를 사용하여 설정합니다.</p></td>
</tr>
<tr class="even">
<td><p>보존 기간</p></td>
<td><p>일반 사서함에 사용하는 것과 같은 기본값으로 설정하는 것이 좋습니다.</p></td>
<td><p>이러한 설정은 다음 수준에서 설정할 수 있습니다.</p>
<ul>
<li><p><strong>조직 수준:</strong> <strong>Set-OrganizationConfig</strong> cmdlet에서 <em>DefaultPublicFolderAgeLimit</em> 매개 변수를 사용하여 설정합니다.</p></li>
<li><p><strong>사서함 수준:</strong> <strong>Set-Mailbox</strong> cmdlet에서 <em>AgeLimit</em> 매개 변수를 사용하여 설정합니다.</p></li>
<li><p><strong>폴더 수준:</strong> <strong>Set-PublicFolder</strong> cmdlet에서 <em>AgeLimit</em> 매개 변수를 사용하여 설정합니다.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="odd">
<td><p>삭제된 항목 보존</p></td>
<td><p>일반 사서함에 사용하는 것과 같은 기본값으로 설정하는 것이 좋습니다.</p></td>
<td><p>이러한 설정은 다음 수준에서 설정할 수 있습니다.</p>
<ul>
<li><p><strong>조직 수준:Set-OrganizationConfig cmdlet에서</strong> <em>DefaultPublicFolderMovedItemRetention</em> 매개 변수를 사용하여 설정합니다.</p></li>
<li><p><strong>사서함 수준:</strong> <strong>Set-Mailbox</strong> cmdlet에서 <em>RetainDeletedItemsFor</em>를 사용하여 설정합니다.</p></li>
<li><p><strong>폴더 수준:</strong> <strong>Set-PublicFolder</strong> cmdlet에서 <em>RetainDeleteItemsFor</em> 매개 변수를 사용하여 설정합니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2013으로 마이그레이션할 수 있습니다. 있는 공용 폴더의 최대 수</p></td>
<td><p>500,000</p></td>
<td><p>단일 마이그레이션에 레거시 버전의 Exchange에서 Exchange 2013으로 이동할 수는 공용 폴더의 최대 수입니다. 공용 폴더 마이그레이션에 대 한 자세한 내용은 <a href="use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md">마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션</a> 을 참조 하십시오.</p></td>
</tr>
</tbody>
</table>

