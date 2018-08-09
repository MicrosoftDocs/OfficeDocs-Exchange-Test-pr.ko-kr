---
title: 'Exchange 2000 또는 Exchange 2003 서버를 포함하는 포리스트에 Exchange 2013을 설치할 수 없음'
TOCTitle: Exchange 2000 또는 Exchange 2003 서버를 포함 하는 포리스트에 Exchange 2013을 설치할 수 없습니다.
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 50483776
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2000 또는 Exchange 2003 서버를 포함 하는 포리스트에 Exchange 2013을 설치할 수 없습니다.

 

_**적용 대상:** Exchange Server_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange 2000 Server 또는 Exchange Server 2003을 실행하는 하나 이상의 컴퓨터가 Active Directory 포리스트에 있으므로 Microsoft Exchange Server 2013 설치를 계속할 수 없습니다. Exchange 2013을 설치하려면 모든 Exchange 2000 및 Exchange 2003 서버를 포리스트에서 제거해야 합니다. 사서함, 공용 폴더 및 기타 모든 Exchange 개체 또는 구성 요소는 Exchange Server 2007 또는 Exchange Server 2010으로 업그레이드해야 합니다. Exchange 2000 또는 Exchange 2003에서 Exchange 2013으로 직접 업그레이드할 수는 없습니다.

조직에서 Exchange 2013을 설치하기 위해 따라야 하는 경로는 현재 포리스트에 설치되어 있는 Exchange 버전에 따라 다릅니다. 자세한 내용은 아래 표를 참조하십시오.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>조직에 설치되어 있는 Exchange 버전</th>
<th>Exchange 2013으로 업그레이드하기 위해 따라야 하는 경로</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2000</p></td>
<td><ol>
<li><p>Exchange 2000 조직에 Exchange 2007을 설치합니다.</p></li>
<li><p>Exchange 2007과 Exchange 2000 동시 사용을 구성합니다.</p></li>
<li><p>Exchange 2000 사서함, 공용 폴더 및 기타 구성 요소를 Exchange 2007로 마이그레이션합니다.</p></li>
<li><p>모든 Exchange 2000 서버를 해제 및 제거합니다.</p></li>
<li><p>Exchange 2007 조직에 Exchange 2013을 설치합니다.</p></li>
<li><p>Exchange 2013과 Exchange 2007 동시 사용을 구성합니다.</p></li>
<li><p>Exchange 2007 사서함, 공용 폴더 및 기타 구성 요소를 Exchange 2013으로 마이그레이션합니다.</p></li>
<li><p>모든 Exchange 2007 서버를 해제 및 제거합니다.</p></li>
</ol>
<p>자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=103281">Exchange 2007로 업그레이드</a> 및 <a href="upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md">Exchange 2007에서 Exchange 2013으로 업그레이드</a>를 참조 하십시오.</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2003</p></td>
<td><ol>
<li><p>Exchange 2003 조직에 Exchange 2010을 설치합니다.</p></li>
<li><p>Exchange 2010과 Exchange 2003 동시 사용을 구성합니다.</p></li>
<li><p>Exchange 2003 사서함, 공용 폴더 및 기타 구성 요소를 Exchange 2010으로 마이그레이션합니다.</p></li>
<li><p>모든 Exchange 2003 서버를 해제 및 제거합니다.</p></li>
<li><p>Exchange 2010 조직에 Exchange 2013을 설치합니다.</p></li>
<li><p>Exchange 2013과 Exchange 2010 동시 사용을 구성합니다.</p></li>
<li><p>Exchange 2010 사서함, 공용 폴더 및 기타 구성 요소를 Exchange 2013으로 마이그레이션합니다.</p></li>
<li><p>모든 Exchange 2010 서버를 해제 및 제거합니다.</p></li>
</ol>
<p>자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=268414">Exchange 2003-업그레이드 및 동시 사용 계획 로드맵</a> 및 <a href="upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md">Exchange 2010에서 Exchange 2013으로 업그레이드</a>를 참조 하십시오.</p></td>
</tr>
</tbody>
</table>


Exchange 2010 또는 Exchange 2013으로 업그레이드할 때는 Exchange 배포 도우미를 사용하면 배포를 쉽게 완료할 수 있습니다. 자세한 내용은 다음 링크를 참조하십시오.

  - [Exchange 2010 배포 어시스턴트](https://go.microsoft.com/fwlink/p/?linkid=171086)

  - [Exchange 2013 배포 도우미](https://go.microsoft.com/fwlink/p/?linkid=277105)

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

원하는 정보를 찾으셨나요? 찾으려는 정보에 대해 [피드백을 보내 주세요](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback).

