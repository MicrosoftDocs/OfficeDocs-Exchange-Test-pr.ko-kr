---
title: '배포 보안 검사 목록: Exchange 2013 Help'
TOCTitle: 배포 보안 검사 목록
ms:assetid: 0cbfad59-f503-48a0-8184-6ca999d89e61
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996026(v=EXCHG.150)
ms:contentKeyID: 50482484
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 배포 보안 검사 목록

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Microsoft Exchange Server 2013 기능은 메시징 환경의 보안을 개선할 수 있도록 설계되었습니다. 일반적으로 Exchange 2013에서는 다음 내용이 적용됩니다.

  - Exchange 2013에 사용되는 계정이 지정된 작업 모음을 수행하는 데 필요한 최소 권한만 갖습니다.

  - 기본적으로 서비스가 필요할 때만 시작됩니다.

  - Exchange 개체에 대한 ACL(액세스 제어 목록) 권한이 최소화되어 있습니다.

  - 지정된 수정 작업에 필요한 개체의 변경 범위에 따라 관리 권한이 설정됩니다.

  - 기본적으로 모든 내부 기본 메시지 경로가 암호화되어 있습니다.

이 항목에서는 Microsoft Exchange를 설치하기 전에 메시징 환경을 강화하기 위해 수행해야 할 단계를 제공합니다. 새 Exchange 서버 역할을 설치할 때마다 이 검사 목록을 확인하는 것이 좋습니다.

Exchange 2013을 설치하기 전에 다음 절차를 수행하십시오.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>절차</th>
<th>완료 여부</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=54836">Microsoft Update</a>를 실행 합니다.</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Microsoft Windows 악성 소프트웨어 제거 도구를 실행합니다. 악성 소프트웨어 제거 도구는 Microsoft Update에 포함되어 있습니다. 이 도구에 대한 자세한 내용은 <a href="http://go.microsoft.com/fwlink/p/?linkid=73452">악성 소프트웨어 제거 도구</a>를 참조하십시오.</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=16526">Microsoft 기본 보안 분석기</a>를 실행 합니다.</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

