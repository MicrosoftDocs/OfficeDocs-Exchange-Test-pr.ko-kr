---
title: '수신 커넥터 사용 권한: Exchange 2013 Help'
TOCTitle: 수신 커넥터 사용 권한
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 50482783
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수신 커넥터 사용 권한

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

다음 표에는 각 항목에 대한 사용 권한 유형과 설명이 나와 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>수신 커넥터 사용 권한</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ms-Exch-SMTP-Submit</p></td>
<td><p>세션에 이 사용 권한이 부여되지 않으면 이 수신 커넥터로 메시지를 전송할 수 없습니다. 세션에 이 사용 권한이 없으면 MAIL FROM 및 AUTH 명령이 실패합니다.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Any-Recipient</p></td>
<td><p>이 사용 권한은 세션에서 해당 커넥터를 통해 메시지를 릴레이할 수 있도록 허용합니다. 이 사용 권한이 부여되지 않으면 허용 도메인의 받는 사람으로 주소가 지정된 메시지만 이 커넥터에 의해 수락됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Any-Sender</p></td>
<td><p>이 사용 권한은 세션에서 보낸 사람 주소 스푸핑 검사를 건너뛸 수 있도록 허용합니다.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-SMTP-Accept-Authoritative-Domain-Sender</p></td>
<td><p>이 사용 권한은 신뢰할 수 있는 도메인에 전자 메일 주소가 있는 보낸 사람이 이 수신 커넥터에 대해 세션을 설정할 수 있도록 허용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-SMTP-Accept-Authentication-Flag</p></td>
<td><p>이 사용 권한은 Exchange 2003 서버를 내부 보낸에서 사람의 메시지를 전송할 수 있습니다. Exchange 2010 내부 것으로 해당 메시지를 인식 합니다. 보낸 사람이 신뢰할 수 있는으로 메시지를 선언할 수 있습니다. 익명 전송을 통해 Exchange 시스템을 입력 하는 메시지는 신뢰할 수 없는 상태에서이 플래그를 사용 하 여 Exchange 조직의 통해 릴레이 됩니다.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Routing</p></td>
<td><p>이 사용 권한은 세션에서 모든 수신 헤더가 변경되지 않은 상태인 메시지를 전송할 수 있도록 허용합니다. 이 사용 권한이 부여되지 않으면 서버에서 수신한 헤더를 모두 제거합니다.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Headers-Organization</p></td>
<td><p>이 사용 권한은 세션에서 모든 조직 헤더가 변경되지 않은 상태인 메시지를 전송할 수 있도록 허용합니다. 조직 헤더는 모두 <strong>X-MS-Exchange-Organization-</strong>으로 시작합니다. 이 사용 권한이 부여되지 않으면 받는 서버에서 모든 조직 헤더를 제거합니다.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Accept-Headers-Forest</p></td>
<td><p>이 사용 권한은 세션에서 모든 포리스트 헤더가 변경되지 않은 상태인 메시지를 전송할 수 있도록 허용합니다. 포리스트 헤더는 모두 <strong>X-MS-Exchange-Forest-</strong>로 시작합니다. 이 사용 권한이 부여되지 않으면 받는 서버에서 모든 포리스트 헤더를 제거합니다.</p></td>
</tr>
<tr class="odd">
<td><p>ms-Exch-Accept-Exch50</p></td>
<td><p>이 사용 권한은 세션에서 XEXCH50 명령이 포함된 메시지를 전송할 수 있도록 허용합니다. 이 명령은 Exchange 2003과의 상호 운용성을 위해 필요합니다. XEXCH50 명령은 메시지에 대한 SCL(스팸 지수) 등의 데이터를 제공합니다.</p></td>
</tr>
<tr class="even">
<td><p>ms-Exch-Bypass-Message-Size-Limit</p></td>
<td><p>이 사용 권한은 세션에서 커넥터에 대해 구성된 메시지 크기 제한을 초과하는 메시지를 전송할 수 있도록 허용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Ms-Exch-Bypass-Anti-Spam</p></td>
<td><p>이 사용 권한은 세션에서 스팸 방지 필터링을 무시할 수 있도록 허용합니다.</p></td>
</tr>
</tbody>
</table>

