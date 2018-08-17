---
title: '검사 목록: 보존 정책 배포: Exchange 2013 Help'
TOCTitle: '검사 목록: 보존 정책 배포'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 50483179
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검사 목록: 보존 정책 배포

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

이 검사 목록을 사용하여 Microsoft Exchange Server 2013 조직에서 보존 정책을 배포합니다. 이 검사 목록으로 작업을 시작하기 전에 다음 항목의 개념을 익혀야 합니다.

  - [메시징 레코드 관리](messaging-records-management-exchange-2013-help.md)

  - [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md)

## 보존 정책 배포 검사 목록


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>완료 여부</th>
<th>작업</th>
<th>리소스</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p> </p></td>
<td><p>여러 사용자 집합에 대한 MRM(메시징 레코드 관리) 요구 사항을 평가합니다.</p></td>
<td><p><a href="messaging-records-management-exchange-2013-help.md">메시징 레코드 관리</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>사용 중인 Microsoft Outlook 클라이언트 버전을 확인합니다.</p></td>
<td><p><code>%ExchangeInstallPath%Logging\RPC Client Access</code>에 있는 RPC 클라이언트 액세스 로그 파일을 구문 분석 합니다.</p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>보존 태그를 만듭니다.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">보존 정책 만들기</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>보존 정책을 만듭니다.</p></td>
<td><p><a href="create-a-retention-policy-exchange-2013-help.md">보존 정책 만들기</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>보존 정책에 보존 태그를 추가합니다.</p></td>
<td><p><a href="add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md">보존 태그를 추가 하거나 보존 정책에서 보존 태그를 제거 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>사서함을 보존 상태로 둡니다.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">사서함 보존에 원본 위치 유지</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>테스트를 위해 단일 사서함에 보존 정책을 적용합니다.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">사서함에 보존 정책 적용</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>옵션: 클라이언트 차단을 구현하여 레거시 Outlook 클라이언트를 차단합니다.</p></td>
<td><p><a href="configure-outlook-client-blocking-exchange-2013-help.md">메시징 레코드 관리에 대 한 차단 하는 Outlook 클라이언트를 구성 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>사용자 통신 및 교육 활동을 시작합니다. 보존 정책이 처리되고 항목이 이동 또는 삭제될 마감 날짜를 포함합니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>추가 사서함에 보존 정책을 적용합니다.</p></td>
<td><p><a href="apply-a-retention-policy-to-mailboxes-exchange-2013-help.md">사서함에 보존 정책 적용</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>며칠 전에 사용자에게 마감 날짜를 미리 알립니다.</p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>마감되면 사서함에서 보존 상태를 제거합니다.</p></td>
<td><p><a href="place-a-mailbox-on-retention-hold-exchange-2013-help.md">사서함 보존에 원본 위치 유지</a></p></td>
</tr>
</tbody>
</table>

