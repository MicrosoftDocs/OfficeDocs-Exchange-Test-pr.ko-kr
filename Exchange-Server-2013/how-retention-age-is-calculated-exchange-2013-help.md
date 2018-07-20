---
title: '보존 기간 계산 방법: Exchange 2013 Help'
TOCTitle: 보존 기간 계산 방법
ms:assetid: a7daf7aa-0411-4b26-a422-eefd1b113f9f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb430780(v=EXCHG.150)
ms:contentKeyID: 50483828
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보존 기간 계산 방법

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-07-27_

MFA(관리되는 폴더 도우미)는 사서함 서버에서 실행되는 많은 *사서함 도우미* 프로세스 중 하나입니다. 해당 작업은 보존 정책이 적용된 사서함을 처리하고 정책에 포함된 보존 태그를 사서함에 추가하고, 사서함의 항목을 처리하는 것입니다. 항목 보존 태그가 있으면 도우미는 해당 항목의 보존 기간을 테스트합니다. 항목이 해당 *보존 기간*을 초과하면 지정된 *보존 작업*을 수행합니다. 보존 작업에는 사용자의 보관 저장소로 항목을 이동하거나, 항목을 삭제하거나, 복구를 허용하거나 항목을 영구적으로 삭제하는 것이 포함됩니다.

자세한 내용은 [보존 태그 및 보존 정책](retention-tags-and-retention-policies-exchange-2013-help.md)을 참조하세요.

## 서로 다른 항목 유형에 대한 보존 기간 결정

배달 또는 배달 되지 않지만 항목이 만들어진 날짜는 사용자가 생성 하는 임시 보관 함 등과 같은 항목의 경우 날짜에서 사서함 항목의 보존 기간 계산 됩니다. 관리 되는 폴더 도우미가 사서함의 항목을 처리 하는 경우 시작 날짜와 함께 **삭제 및 복구 허용** 또는 **영구 삭제** 보존 작업 보존 태그에 포함 된 모든 항목에 대 한 만료 날짜 스탬프 처리 합니다. 보관 태그가 있는 항목에는 또한 이동 날짜 스탬프로 추가.

지운 편지함 폴더의 항목 및 시작 및 종료 날짜가 있을 수 있는 항목(모임 및 약속과 같은 일정 항목, 작업)은 다음 표와 같이 다르게 처리됩니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>항목 형식</th>
<th>항목 위치</th>
<th>보존 기간 계산 기준</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>전자 메일 메시지</p></li>
<li><p>문서</p></li>
<li><p>팩스</p></li>
<li><p>저널 항목</p></li>
<li><p>모임 요청, 응답 또는 취소</p></li>
<li><p>부재 중 전화</p></li>
</ul></td>
<td><p>지운 편지함 폴더에 없음</p></td>
<td><p>배달 날짜 또는 만든 날짜</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>전자 메일 메시지</p></li>
<li><p>문서</p></li>
<li><p>팩스</p></li>
<li><p>저널 항목</p></li>
<li><p>모임 요청, 응답 또는 취소</p></li>
<li><p>부재 중 전화</p></li>
</ul></td>
<td><p>지운 편지함 폴더</p></td>
<td><ul>
<li><p>항목이 상속되었거나 암시적인 보존 태그가 없는 폴더에서 삭제되지 않은 경우 배달 날짜 또는 만든 날짜</p></li>
<li><p>상속 또는 암시적 보존 태그가 적용되지 않은 폴더에 있는 항목은 MFA에 의해 처리되지 않으므로 시작 날짜가 스탬프 처리되지 않습니다. 사용자가 이러한 항목을 삭제하고 MFA가 지운 편지함 폴더에서 이 항목을 처음으로 처리할 때 현재 날짜가 시작 날짜로 스탬프 처리됩니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>일정</p></td>
<td><p>지운 편지함 폴더에 없음</p></td>
<td><ul>
<li><p>되풀이하지 않는 일정 항목은 해당 종료 날짜에 따라 만료됩니다.</p></li>
<li><p>되풀이 일정 항목은 마지막 항목의 종료 날짜에 따라 만료됩니다. 종료 날짜가 없는 되풀이 일정 항목은 만료되지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>일정</p></td>
<td><p>지운 편지함 폴더</p></td>
<td><ol>
<li><p>일정 항목(있는 경우)은 해당 <code>message-received date</code>에 따라 만료됩니다.</p></li>
<li><p>일정 항목에 <code>message-received date</code>가 없으면 해당 항목은 <code>message-creation date</code>에 따라 만료됩니다.</p></li>
<li><p>일정 항목에 <code>message-received date</code>와 <code>message-creation date</code>가 모두 없으면 항목이 만료되지 않습니다.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>작업</p></td>
<td><p>지운 편지함 폴더에 없음</p></td>
<td><ul>
<li><p>되풀이하지 않는 작업</p>
<ol>
<li><p>되풀이하지 않는 작업(있는 경우)은 해당 <code>message-received date</code>에 따라 만료됩니다.</p></li>
<li><p>되풀이하지 않는 작업에 <code>message-received date</code>가 없으면 해당 작업은 <code>message-creation date</code>에 따라 만료됩니다.</p></li>
<li><p>되풀이하지 않는 작업에 <code>message-received date</code>와 <code></code><code>message-creation date</code>가 모두 없으면 작업이 만료되지 않습니다.</p></li>
</ol></li>
<li><p>되풀이 작업은 마지막 항목의 <code>end date</code>에 따라 만료됩니다. 되풀이 작업에 <code>end date</code>가 없으면 작업이 만료되지 않습니다.</p></li>
<li><p>다시 생성하는 작업(작업의 이전 인스턴스가 완료된 후 지정한 시간을 다시 생성하는 되풀이 작업)은 만료되지 않습니다.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>작업</p></td>
<td><p>지운 편지함 폴더</p></td>
<td><ol>
<li><p>작업(있는 경우)은 해당 <code>message-received date</code>에 따라 만료됩니다.</p></li>
<li><p>작업에 <code>message-received date</code>가 없으면 해당 작업은 <code>message-creation date</code>에 따라 만료됩니다.</p></li>
<li><p>작업에 <code>message-received date</code>와 <code>message-creation date</code>가 모두 없으면 작업이 만료되지 않습니다.</p></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>Contact</p></td>
<td><p>모든 폴더에</p></td>
<td><p>연락처 되지 스탬프로 시작 날짜 또는 만료 날짜를 하므로 이러한는 관리 되는 폴더 도우미가 건너뛰며 만료 되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>손상</p></td>
<td><p>모든 폴더에서</p></td>
<td><p>손상된 항목은 관리되는 폴더 도우미가 건너뛰며 만료되지 않습니다.</p></td>
</tr>
</tbody>
</table>


## 예


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>사용자 작업</th>
<th>폴더의 보존 태그</th>
<th>관리되는 폴더 도우미</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ol>
<li><p>2013년 1월 26일에 받은 편지함에 메시지가 수신됩니다.</p></li>
<li><p>2013년 2월 27일에 메시지를 삭제합니다.</p></li>
</ol>
<p></p></td>
<td><ul>
<li><p>받은 편지함: 365일 후에 삭제</p></li>
<li><p>지운 편지함: 30일 후에 삭제</p></li>
</ul>
<p></p></td>
<td><ol>
<li><p>2013년 1월 26일에 받은 편지함의 메시지를 처리하고 <em>시작 날짜</em> 2013년 1월 26일과 <em>만료 날짜</em> 2014년 1월 26일을 스탬프 처리합니다.</p></li>
<li><p>2013년 2월 27일에 지운 편지함 폴더에서 해당 메시지를 다시 처리합니다. 동일한 시작 날짜(2013년 1월 26일)에 따라 만료 날짜를 다시 계산합니다.</p></li>
<li><p>항목이 30일보다 오래되었으므로 즉시 만료됩니다.</p></li>
</ol></td>
</tr>
<tr class="even">
<td><ol>
<li><p>2013년 1월 26일에 받은 편지함에 메시지가 수신됩니다.</p></li>
<li><p>2013년 2월 27일에 메시지를 삭제합니다.</p></li>
</ol></td>
<td><ul>
<li><p>받은 편지함: 없음(상속 또는 암시적)</p></li>
<li><p>지운 편지함: 30일 후에 삭제</p></li>
</ul></td>
<td><ol>
<li><p>2013년 2월 27일에 지운 편지함 폴더에서 해당 메시지를 처리하고 항목에 시작 날짜가 없음을 확인합니다. 항목은 현재 날짜를 시작 날짜로, 2013년 3월 27일이 만료 날짜로 스탬프 처리됩니다.</p></li>
<li><p>지운 편지함 폴더에서 삭제 또는 제거된 지 30일 후인 2013년 3월 27일에 항목이 만료됩니다.</p></li>
</ol></td>
</tr>
</tbody>
</table>


## 추가 정보

  - Exchange Online 관리 되는 폴더 도우미가 처리 사서함 7 일간의 한번 합니다. 이 항목에 대해 만료 날짜 스탬프가 지정 된 후에 일 7 개까지 만료 되는 항목 될 수 있습니다.

  - 보존 상태인 사서함 항목은 보존 상태가 제거 될때까지 관리 되는 폴더 도우미에 의해 처리 되지 않습니다.

  - 사서함이 원본 위치 유지 또는 소송 보존으로 지정될 경우 만료 항목은 받은 편지함에서 제거되지만 사서함이 [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md)에서 제거될 때까지 복구 가능한 항목 폴더에 보존됩니다.

  - 하이브리드 배포에서는 온-프레미스 조직 및 Exchange Online 조직 둘 다에서 항목이 일관되게 이동 및 만료되도록 두 조직에 동일한 보존 태그 및 보존 정책이 존재해야 합니다. 자세한 내용은 [보존 태그 내보내기 및 가져오기](export-and-import-retention-tags-exchange-2013-help.md)를 참조하세요.

