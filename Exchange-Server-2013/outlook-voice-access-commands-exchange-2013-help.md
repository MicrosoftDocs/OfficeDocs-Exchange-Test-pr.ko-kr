---
title: 'Outlook Voice Access 명령: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 명령
ms:assetid: 8fe9247c-695f-47d8-827e-c79d0426854b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn205137(v=EXCHG.150)
ms:contentKeyID: 54651793
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 명령

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2015-03-09_

UM(통합 메시징) 사용 가능 사용자는 Outlook Voice Access를 통해 아날로그, 디지털 또는 휴대 전화를 사용하여 자신의 사서함에 액세스할 수 있습니다. UM 사용 가능 사용자는 Outlook Voice Access에 있는 메뉴 시스템을 사용하여 전자 메일 읽기, 음성 메시지 듣기, Outlook 일정과의 상호 작용, 개인 연락처에 대한 액세스, 개인 옵션 관리(예: Outlook Voice Access PIN 구성 또는 음성 메일 메시지 녹음)를 수행할 수 있습니다. 이 항목에는 Outlook Voice Access 명령 목록 및 사용자가 Outlook Voice Access 번호로 전화를 걸어 자신의 사서함에 액세스할 때 명령을 사용하는 방법 등이 나와 있습니다.

## Outlook Voice Access 사용자 인터페이스

Outlook Voice Access는 전화 키패드를 사용하는 TUI(전화 사용자 인터페이스) 및 사용자 음성 명령을 사용하는 VUI(음성 사용자 인터페이스) 등과 같은 두 개의 사용자 인터페이스로 구성됩니다. 사용자는 Outlook Voice Access를 사용하여 외부 또는 내부 전화로 음성 메일 시스템에 액세스하여 자신의 사서함의 개인 전자 메일, 음성 메시지, 연락처 및 일정 정보에 액세스할 수 있습니다.

## 전자 메일 및 음성 메일 명령 참조

Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 메뉴 옵션이 표시됩니다. 사용자는 이를 통해 자신의 사서함에 액세스해서 전자 메일 및 음성 메일을 관리할 수 있습니다. 다음 표에는 전자 메일 및 음성 메일을 관리하기 위해 사용할 수 있는 명령이 나열됩니다.

### 전자 메일 및 음성 메일 명령

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>음성 명령</th>
<th>터치톤 명령</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;재생&quot;</p></td>
<td><p></p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 재생합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;다음&quot;</p></td>
<td><p>#</p></td>
<td><p>다음 전자 메일 또는 음성 메일 메시지를 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;읽지 않은 다음 항목&quot;</p></td>
<td><p>00을 누른 다음 ## 누르기</p></td>
<td><p>다음 읽지 않은 전자 메일 메시지를 읽습니다. 전자 메일에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;삭제&quot;</p></td>
<td><p>7</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 삭제합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;회신&quot;</p></td>
<td><p>8</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 보낸 사용자에게 회신합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;전체 회신&quot;</p></td>
<td><p>00을 누른 다음 88 누르기</p></td>
<td><p>현재 전자 메일 메세지의 모든 사용자에게 회신합니다. 음성 메일 메시지에는 사용할 수 없는 옵션입니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;읽지 않은 상태로 표시&quot;</p></td>
<td><p>9</p></td>
<td><p>전자 메일 메시지를 읽지 않은 상태로 표시합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;종료&quot;</p></td>
<td><p>33</p></td>
<td><p>읽기를 중지하고 현재 전자 메일 또는 음성 메일 메시지의 끝으로 이동합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;기타 옵션&quot;</p></td>
<td><p>00</p></td>
<td><p>기타 옵션 메뉴를 엽니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;이전&quot;</p></td>
<td><p>00을 누른 다음 11 누르기</p></td>
<td><p>이전 전자 메일 또는 음성 메일 메시지를 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;헤더 읽기&quot;</p></td>
<td><p></p></td>
<td><p>전자 메일 또는 음성 메일 메시지의 헤더를 읽습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;보낸 사람에게 전화 걸기&quot;</p></td>
<td><p>00을 누른 다음 2 누르기</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 보낸 사용자에게 전화를 겁니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;전달&quot;</p></td>
<td><p>00을 누른 다음 6 누르기</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 다른 전자 메일 받는 사람 또는 그룹에 전달합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;추가 작업 플래그 지정&quot;</p></td>
<td><p>00을 누른 다음 44 누르기</p></td>
<td><p>추가 작업을 위해 현재 전자 메일 또는 음성 메일 메시지를 표시하거나 플래그를 지정합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;이름으로 찾기&quot;</p></td>
<td><p></p></td>
<td><p>사용자 사서함에서 전자 메일 또는 음성 메일 메시지를 찾으려면 사용자 이름을 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;대화 삭제&quot;</p></td>
<td><p>00을 누른 다음 77 누르기</p></td>
<td><p>전자 메일 대화와 연관된 모든 전자 메일 메시지를 삭제합니다. 전자 메일에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;대화 숨기기&quot;</p></td>
<td><p>00을 누른 다음 99 누르기</p></td>
<td><p>동일한 전자 메일 대화 내에 포함된 추가 전자 메일 메시지를 숨깁니다. 전자 메일에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;봉투 정보&quot;</p></td>
<td><p>00을 누른 다음 5 누르기</p></td>
<td><p>전자 메일 또는 음성 메일 메시지의 봉투 정보를 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;언어 선택&quot;</p></td>
<td><p>00을 누른 다음 55 누르기</p></td>
<td><p>읽으려는 전자 메일 또는 음성 메일 메시지의 언어를 선택할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;되감기&quot; 또는 &quot;반복&quot;</p></td>
<td><p>1</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 되감거나 반복합니다. 메시지를 재생하는 동안에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;일시 중지&quot;</p></td>
<td><p>2</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 일시 중지합니다. 메시지를 재생하는 동안에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;빨리 감기&quot;</p></td>
<td><p>3</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 빨리 감습니다. 메시지를 재생하는 동안에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;천천히&quot;</p></td>
<td><p>4</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 더 느리게 재생하거나 읽습니다. 메시지를 재생하는 동안에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;빠르게&quot;</p></td>
<td><p>6</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 더 빠르게 재생하거나 읽습니다. 메시지를 재생하는 동안에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;이전&quot;</p></td>
<td><p>11</p></td>
<td><p>이전 전자 메일 메시지를 처음부터 읽습니다. 전자 메일에만 사용할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;재생&quot;</p></td>
<td><p>00을 누른 다음 1 누르기</p></td>
<td><p>현재 전자 메일 또는 음성 메일 메시지를 재생합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;반복&quot;</p></td>
<td><p>0</p></td>
<td><p>현재 메뉴 옵션을 반복합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;주 메뉴&quot;</p></td>
<td><p>*</p></td>
<td><p>주 메뉴로 종료합니다.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> Outlook Voice Access를 사용하여 전자 메일 메시지를 삭제한 후 해당 메시지에 액세스해야 하는 경우에는 Outlook Web App&nbsp;또는 Outlook을 사용하여 전자 메일 메시지를 지운 편지함 폴더에서 해당 폴더로 다시 이동할 수 있습니다. Outlook Voice Access는 지운 편지함 폴더에 액세스하는 데 사용할 수 없습니다.



## 일정 옵션 명령 참조

Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 메뉴 옵션이 표시됩니다. 사용자는 이를 통해 자신의 사서함에 액세스해서 자신의 일정을 관리할 수 있습니다. 다음 표에는 일정 관리에 사용할 수 있는 명령이 나열됩니다.

### 일정 명령

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>음성 명령</th>
<th>터치톤 명령</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;다음&quot;</p></td>
<td><p>#</p></td>
<td><p>다음 일정 약속을 읽습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;다음 날&quot;</p></td>
<td><p>##</p></td>
<td><p>다음 날의 일정 약속을 열어서 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;반복&quot;</p></td>
<td><p>0</p></td>
<td><p>사용 가능한 메뉴 옵션을 반복합니다. 또는 VUI를 사용하는 경우 시스템에서 일정 약속을 다시 읽습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;기타 옵션&quot;</p></td>
<td><p>00</p></td>
<td><p>추가 일정 옵션 메뉴를 재생합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;반복&quot;</p></td>
<td><p>1</p></td>
<td><p>일정 약속을 다시 읽습니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;이전 모임&quot;</p></td>
<td><p>00을 누른 다음 11 누르기</p></td>
<td><p>예약된 이전 모임을 엽니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;위치로 전화 걸기&quot;</p></td>
<td><p>2</p></td>
<td><p>모임 위치에 대해 나열된 전화 번호로 전화를 겁니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;이끌이에게 전화 걸기&quot;</p></td>
<td><p>00을 누른 다음 22 누르기</p></td>
<td><p>모임 이끌이에 대해 나열된 전화 번호로 전화를 겁니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;늦게 도착&quot;</p></td>
<td><p>3</p></td>
<td><p>모임의 모든 참석자에게 늦을 것 같다는 메시지를 보냅니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;수락&quot; 또는 &quot;미정 수락&quot;</p></td>
<td><p>4</p></td>
<td><p>모임 요청을 수락하거나 미정으로 수락합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;모임 세부 정보&quot;</p></td>
<td><p>5</p></td>
<td><p>현재 읽고 있는 모임 세부 정보를 읽거나 재생합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;참석 세부 정보&quot;</p></td>
<td><p>00을 누른 다음 55 누르기</p></td>
<td><p>예약된 모임 세부 정보를 읽거나 재생합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;전달&quot;</p></td>
<td><p>00을 누른 다음 6 누르기</p></td>
<td><p>모임에 대한 요청을 다른 사용자에게 전달합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;거절&quot; 또는 &quot;취소&quot;</p></td>
<td><p>7</p></td>
<td><p>모임 요청을 거절하거나 취소합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;내 일정 지우기&quot;</p></td>
<td><p>00을 누른 다음 77 누르기</p></td>
<td><p>해당 날짜에 대해 특정 기간 동안의 일정을 지웁니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;회신&quot;</p></td>
<td><p>00을 누른 다음 8 누르기</p></td>
<td><p>모임 이끌이에게 회신합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;전체 회신&quot;</p></td>
<td><p>00을 누른 다음 88 누르기</p></td>
<td><p>모든 모임 참석자에게 회신합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;메뉴 반복&quot;</p></td>
<td><p>5를 누른 다음 0 누르기</p></td>
<td><p>사용 가능한 메뉴 옵션을 반복합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;되감기&quot;</p></td>
<td><p>5를 누른 다음 1 누르기</p></td>
<td><p>모임 세부 정보를 되감습니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5를 누른 다음 11 누르기</p></td>
<td><p>모임 세부 정보의 처음으로 돌아갑니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5를 누른 다음 2 누르기</p></td>
<td><p>모임 세부 정보의 재생을 일시 중지하고 다시 시작합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;빨리 감기&quot;</p></td>
<td><p>5를 누른 다음 3 누르기</p></td>
<td><p>모임 세부 정보 내에서 앞으로 건너뜁니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;종료&quot;</p></td>
<td><p>5를 누른 다음 33 누르기</p></td>
<td><p>모임 세부 정보의 끝으로 건너뜁니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5를 누른 다음 4 누르기</p></td>
<td><p>모임 세부 정보를 천천히 재생하거나 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5를 누른 다음 55 누르기</p></td>
<td><p>모임 세부 정보를 읽는 데 사용할 언어를 선택합니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5를 누른 다음 6 누르기</p></td>
<td><p>모임 세부 정보를 빠르게 재생하거나 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;주 메뉴&quot;</p></td>
<td><p>*</p></td>
<td><p>주 메뉴로 종료합니다.</p></td>
</tr>
</tbody>
</table>


## 연락처 명령 찾기 참조

Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 메뉴 옵션이 표시됩니다. 사용자는 이를 통해 자신의 사서함에 액세스하거나 개인 옵션을 변경하거나 연락처로 메시지를 호출하거나 보낼 수 있습니다. 음성을 사용하도록 선택하고(기본적으로 선택됨) 연락처 메뉴 옵션을 선택하면 음성 메일 시스템을 통해 전화 키패드를 사용하여 연락처 옵션 찾기를 탐색할 수 있습니다. 전화 키패드를 사용하여 디렉터리나 연락처에서 사용자를 찾을 수도 있습니다. 다음 표에는 연락처 관리 또는 사용자 검색에 사용할 수 있는 명령이 나열됩니다.

### 연락처 명령

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>음성 명령</th>
<th>터치톤 명령</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&quot;디렉터리&quot;</p></td>
<td><p>00</p></td>
<td><p>사용자의 디렉터리를 검색합니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;자세히 재생&quot;</p></td>
<td><p>1</p></td>
<td><p>개인 연락처에 대해 나열된 전화 번호와 같은 개인 연락처 세부 정보를 재생합니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;메시지 보내기&quot;</p></td>
<td><p>3</p></td>
<td><p>선택한 개인 연락처로 메시지를 보냅니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;다른 연락처 찾기&quot;</p></td>
<td><p>4</p></td>
<td><p>다른 개인 연락처를 찾습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;휴대폰으로 전화 걸기&quot;</p></td>
<td><p>2를 누른 다음 1 누르기</p></td>
<td><p>개인 연락처에 대해 나열된 휴대폰 전화 번호로 전화를 겁니다.</p></td>
</tr>
<tr class="even">
<td><p>&quot;사무실에 전화&quot;</p></td>
<td><p>2를 누른 다음 2 누르기</p></td>
<td><p>개인 연락처에 대해 나열된 근무처 또는 사무실 번호로 전화를 겁니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;집에 전화&quot;</p></td>
<td><p>2를 누른 다음 3 누르기</p></td>
<td><p>개인 연락처에 대해 나열된 집 전화 번호로 전화를 겁니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>##</p></td>
<td><p>디렉터리 검색 기능을 사용하는 경우, 디렉터리에서 전자 메일 별칭 또는 사용자의 이름을 입력할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>&quot;주 메뉴&quot;</p></td>
<td><p>*</p></td>
<td><p>주 메뉴로 종료합니다.</p></td>
</tr>
</tbody>
</table>


## 개인 옵션 명령 참조

Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 메뉴 옵션이 표시됩니다. 사용자는 이를 통해 자신의 사서함에 액세스해서 자신의 개인 옵션을 관리할 수 있습니다. Outlook Voice Access를 사용하여 개인 옵션을 구성할 경우 메뉴를 탐색하려면 전화 키패드만 사용할 수 있습니다. 개인 옵션을 구성하기 위해 음성을 사용하여 메뉴를 탐색하는 작업은 사용할 수 없습니다. 다음 표에는 개인 옵션 관리에 사용할 수 있는 명령이 나열됩니다.

### 개인 옵션 명령

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>음성 명령</th>
<th>터치톤 명령</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>1</p></td>
<td><p>전화의 부재 중 음성 인사말을 켜거나 끕니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>2</p></td>
<td><p>개인 음성 메일 또는 부재 중 음성 메일의 인사말을 녹음합니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>3</p></td>
<td><p>Outlook Voice Access에 사용하는 PIN을 변경합니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>4</p></td>
<td><p>VUI 또는 터치톤 인터페이스 사용을 시작합니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>5</p></td>
<td><p>사용할 현지 표준 시간대를 설정합니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>6</p></td>
<td><p>12시간 또는 24시간 형식을 선택합니다.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>*</p></td>
<td><p>주 메뉴로 돌아갑니다.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>0</p></td>
<td><p>사용 가능한 메뉴 옵션을 반복합니다.</p></td>
</tr>
</tbody>
</table>


## 자세한 내용

[Outlook Voice Access 설정](setting-up-outlook-voice-access-exchange-2013-help.md)

[클라이언트 음성 메일 기능 설정](set-up-client-voice-mail-features-exchange-2013-help.md)

