---
title: 'Exchange Online 및 Exchange 서버에서 기본 보존 정책: Exchange 2013 Help'
TOCTitle: 기본 보존 정책
ms:assetid: bcf31b2d-463b-4623-b488-c8ac40f14f62
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn775046(v=EXCHG.150)
ms:contentKeyID: 62625497
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange Online 및 Exchange 서버에서 기본 보존 정책

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Exchange 보존 정책을 기본 MRM 정책에 프로그램 Exchange Online 만들고 온-프레미스 Exchange 조직입니다. 정책을은 Exchange Online 에서 새 사용자에 게 자동으로 적용 됩니다. 온-프레미스 조직에서 사서함에 대 한 아카이브를 만들 때 정책이 적용 됩니다. 언제 든 지 사용자에 게 적용 되는 보존 정책을 변경할 수 있습니다.

보존 작업 확인 하는 보존 기간을 변경 하 여 기본 MRM 정책에 포함 하는 태그를 수정 하, 태그를 사용 하지 않도록 설정 하거나 추가 (영문) 또는에서 태그를 제거 하 여 정책을 수정할 수 있습니다. 업데이트 된 정책 관리 되는 폴더 도우미에 의해 처리 중인은 다음에 사서함에 적용 됩니다.

## 기본 MRM 정책에 연결된 보존 태그

다음 표에서는 기본 MRM 정책에 연결된 기본 보존 태그를 보여 줍니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>이름</th>
<th>종류</th>
<th>보존 기간(일)</th>
<th>보존 작업</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 2년 후 보관함으로 이동</p></td>
<td><p>기본 정책 태그 (DPT)</p></td>
<td><p>730</p></td>
<td><p>보관함으로 이동</p></td>
</tr>
<tr class="even">
<td><p>복구 가능한 항목 14일 후 보관함으로 이동</p></td>
<td><p>복구 가능한 항목 폴더</p></td>
<td><p>14</p></td>
<td><p>보관함으로 이동</p></td>
</tr>
<tr class="odd">
<td><p>개인 1년 후 보관함으로 이동</p></td>
<td><p>개인 태그</p></td>
<td><p>365</p></td>
<td><p>보관함으로 이동</p></td>
</tr>
<tr class="even">
<td><p>개인 5년 후 보관함으로 이동</p></td>
<td><p>개인 태그</p></td>
<td><p>1,825</p></td>
<td><p>보관함으로 이동</p></td>
</tr>
<tr class="odd">
<td><p>개인 보관함으로 이동 안 함</p></td>
<td><p>개인 태그</p></td>
<td><p>해당 없음</p></td>
<td><p>보관함으로 이동</p></td>
</tr>
<tr class="even">
<td><p>1주일 후 삭제</p></td>
<td><p>개인 태그</p></td>
<td><p>7</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
<tr class="odd">
<td><p>1개월 후 삭제</p></td>
<td><p>개인 태그</p></td>
<td><p>30</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
<tr class="even">
<td><p>6개월 후 삭제</p></td>
<td><p>개인 태그</p></td>
<td><p>180</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
<tr class="odd">
<td><p>1년 후 삭제</p></td>
<td><p>개인 태그</p></td>
<td><p>365</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
<tr class="even">
<td><p>5년 후 삭제</p></td>
<td><p>개인 태그</p></td>
<td><p>1,825</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
<tr class="odd">
<td><p>삭제 안 함</p></td>
<td><p>개인 태그</p></td>
<td><p>해당 없음</p></td>
<td><p>삭제 및 복구 허용</p></td>
</tr>
</tbody>
</table>


## 기본 MRM 정책 수행할 수 있는 작업


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>다음을 수행할 수 있습니다.</th>
<th>Exchange Online...</th>
<th>Exchange Server에서...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>새 사용자에 게 기본 MRM 정책을 자동으로 적용</p></td>
<td><p>예, 기본적으로 적용 됩니다. 조치가 필요 하지 않습니다.</p></td>
<td><p>예, 적용 기본적으로 새 사용자에 대 한 보관을 만들 수도 있습니다.</p>
<p>나중에 사용자가 보관을 만드는 경우 사용자는 기존 보존 정책이 없는 경우에 정책은 자동으로 적용 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>보존 기간 또는 정책에 연결 된 보존 태그의 보존 작업 수정</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>정책에 연결 된 보존 태그를 사용 하지 않도록 설정</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>정책에 보존 태그 추가</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>정책에서 보존 태그를 제거 합니다.</p></td>
<td><p>예</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>새 사용자에 게 자동으로 적용 하려면 기본 보존 정책으로 다른 정책 설정</p></td>
<td><p>아니요</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>


## 추가 정보

  - 둘 이상의 보존 정책에 보존 태그를 연결할 수 있습니다. [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md)를 관리 하는 방법에 대 한 자세한 내용은, [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)을 참조 하십시오.

  - 기본 MRM 정책에 자동으로 항목을 삭제 하려면 DPT 포함 되지 않습니다 (하지만 사용자가 사서함 항목에 적용할 수 있는 다른는 삭제 보존 작업을 개인 태그 포함지 않습니다). 지정된 된 기간 후 항목을 자동으로 삭제 하려는 경우 필요한 delete 매크로 함수와 함께 DPT를 만들 수 있으며 정책 추가. 자세한 내용은 [보존 정책 만들기](create-a-retention-policy-exchange-2013-help.md) 및 [보존 태그를 추가 하거나 보존 정책에서 보존 태그를 제거 합니다.](add-retention-tags-to-or-remove-retention-tags-from-a-retention-policy-exchange-2013-help.md)를 참조 하십시오.

  - 보존 정책은 사서함 사용자에게 적용됩니다. 같은 정책이 사용자의 사서함 및 보관 사서함에 적용됩니다.

