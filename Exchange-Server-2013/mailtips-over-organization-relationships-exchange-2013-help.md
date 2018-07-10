---
title: '조직 관계를 통해 메일 설명: Exchange 2013 Help'
TOCTitle: 조직 관계를 통해 메일 설명
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 50482563
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 조직 관계를 통해 메일 설명

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Microsoft Exchange Server 2013에서는 Microsoft Exchange Online 또는 다른 Exchange 조직과의 조직 관계를 구성할 수 있습니다. 조직 관계를 설정하면 다른 조직을 처리할 때 사용자 환경을 개선할 수 있습니다. 예를 들어 약속 있음/없음 데이터를 공유하고, 보안 메시지 흐름을 구성하고, 두 조직 모두에서 메시지 추적을 사용하도록 설정할 수 있습니다.

## 메일 설명 액세스 수준 제어

특정 유형의 메일 설명을 제한할 수 있습니다. 모든 메일 설명이 반환되도록 하거나 NDR를 방지하는 제한된 메일 설명만 반환되도록 할 수 있습니다. 이 설정은 **Set-OrganizationRelationship** cmdlet의 *MailTipsAccessLevel* 매개 변수를 사용하여 구성할 수 있습니다. 다음 표는 조직 관계에 대해 반환되는 메일 설명 종류를 나타낸 것입니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>메일 설명</th>
<th>액세스 수준을 모두로 설정하는 경우 메일 설명을 사용할 수 있습니까?</th>
<th>액세스 수준을 제한으로 설정하는 경우 메일 설명을 사용할 수 있습니까?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>큰 대상 그룹</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>자동 회신</p></td>
<td><p>예</p>
<p>받는 사람의 원격 도메인이 내부로 지정된 경우에는 내부 자동 회신이 표시됩니다. 그렇지 않으면 외부 자동 회신이 표시됩니다.</p></td>
<td><p>예</p>
<p>외부 자동 회신이 표시됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>중재된 받는 사람</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>대용량 메시지</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>제한된 받는 사람</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>사서함 꽉 참</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="odd">
<td><p>사용자 지정 메일 설명</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>외부 받는 사람</p></td>
<td><p>예</p>
<p>받는 사람의 원격 도메인이 내부로 지정된 경우에는 이 메일 설명이 생략됩니다. 그렇지 않으면 외부 메일 설명이 반환됩니다.</p></td>
<td><p>예</p>
<p>받는 사람의 원격 도메인이 내부로 지정된 경우에는 이 메일 설명이 생략됩니다. 그렇지 않으면 외부 메일 설명이 반환됩니다.</p></td>
</tr>
</tbody>
</table>


메일 설명 액세스 수준을 구성하는 방법에 대한 자세한 내용은 [조직 관계에 대 한 메일 설명 관리](manage-mailtips-for-organization-relationships-exchange-2013-help.md)을 참조하십시오.

## 메일 설명 액세스 범위 제어

조직 관계에 대한 메일 설명을 사용하도록 설정하고 액세스 수준을 `All`로 설정하면 모든 사용자에 대해 받는 사람별 메일 설명, 사서함 꽉 참, 자동 회신 및 사용자 지정 메일 설명이 반환됩니다. 그러나 특정 사용자 집합에게만 이 메일 설명을 허용할 수도 있습니다. 예를 들어 파트너와의 조직 관계를 설정하는 경우 그 파트너와 작업하는 사용자에게만 이 메일 설명을 허용할 수도 있습니다.

이를 위해서는 먼저 그룹을 만들고 받는 사람별 메일 설명을 공유할 모든 사용자를 그룹에 추가해야 합니다. 그런 다음 조직 관계에서 그룹을 지정할 수 있습니다.

이 제한을 구현하면 클라이언트 액세스 서버는 먼저 메일 설명 쿼리를 수신한 받는 사람이 이 그룹의 일부인지 확인합니다. 받는 사람이 그룹의 구성원이면 클라이언트 액세스 서버는 받는 사람별 메일 설명을 포함한 모든 메일 설명을 다시 프록시 처리합니다. 그렇지 않으면 클라이언트 액세스 서버는 받는 사람별 메일 설명을 응답에 포함시키지 않습니다.

메일 설명 액세스 수준을 구성하는 방법에 대한 자세한 내용은 [조직 관계에 대 한 메일 설명 관리](manage-mailtips-for-organization-relationships-exchange-2013-help.md)을 참조하십시오.

