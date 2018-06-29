---
title: '검사 목록: Exchange 2010에서 업그레이드: Exchange 2013 Help'
TOCTitle: '검사 목록: Exchange 2010에서 업그레이드'
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51407662
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검사 목록: Exchange 2010에서 업그레이드

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

이 검사 목록을 사용 하 여 Microsoft Exchange 2010 에서 Exchange 2013 으로 업그레이드 합니다. 이 검사 목록으로 작업을 시작 하기 전에 맞는지 확인에 설명 된 개념을 파악 합니다.

  - [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Exchange 2013의 새로운 기능](what-s-new-in-exchange-2013-exchange-2013-help.md)

이 검사 목록은 기본 업그레이드 시나리오에 대한 지침을 제공하는 일반적인 목록입니다.


> [!NOTE]
> Exchange Server 배포 도우미에는 Exchange Server를 배포하는 방법에 대한 사용자 지정 단계별 지침이 나와 있습니다. 배포 도우미를 사용하면 새로운 Exchange Server 2013 설치 버전을 배포하거나, 이전 버전을 Exchange 2013으로 업그레이드하거나, Exchange 2013과 Exchange Online의 하이브리드 배포를 구성할 수 있습니다. 자세한 내용은 <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 배포 도우미</A>를 참조하세요.



## Exchange 2010을 Exchange 2013으로 업그레이드하기 위한 검사 목록


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>완료 여부</p></td>
<td><p>작업</p></td>
<td><p>항목</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. 릴리스 정보 읽기</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange Server 2013 릴리스 정보</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. 시스템 요구 사항 확인</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 시스템 요구 사항</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. 필수 구성 요소 단계 완료 확인</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">배포 보안 검사 목록</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. 연결되지 않은 네임스페이스 구성</p>

> [!NOTE]
> 이 단계는 선택입니다. 조직이 연결되지 않은 네임스페이스를 실행 중인 경우에만 필요합니다.


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">분리 된 네임 스페이스에 대 한 DNS 접미사 검색 목록을 구성 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. 모든 Exchange 2010 사서함 데이터베이스용 오프라인 주소록 선택</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> in <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 사서함 데이터베이스를 관리 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Exchange 2013 설치</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 설치</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 Edge 전송 역할 설치</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 설치를 확인 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Exchange 2013 사서함 만들기</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">사용자 사서함 만들기</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Exchange 관련 가상 디렉터리 구성</p>

> [!NOTE]
> Exchange 웹 서비스, 외부에서 Outlook 사용 또는 오프라인 주소록을 사용하려는 경우에 이 단계가 필요합니다. Exchange 제어판, Microsoft Office&nbsp;Outlook Web App 또는 Exchange ActiveSync에 대한 기본 설정을 변경해야 하는 경우에도 필요할 수 있습니다.<BR>


</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 클라이언트 액세스 서버 구성</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. 클라이언트 액세스 서버에 디지털 인증서 추가</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">디지털 인증서 및 SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 중재 사서함 이동</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">Exchange 2010 시스템 사서함을 Exchange 2013으로 이동</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 통합 메시징 구성</p>

> [!NOTE]
> 이 단계는 선택입니다. 통합 메시징을 조직에서 사용하려는 경우에만 필요합니다.


</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">Exchange 2010 UM을 Exchange 2013 UM으로 업그레이드</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Edge 전송 서버 구성</p>

> [!NOTE]
> 이 단계는 선택입니다. 조직에서 Edge 전송 서버를 사용하는 경우에만 필요합니다.


</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. 외부에서 Outlook 사용 구성 및 사용</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. 서비스 연결 지점 구성</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 클라이언트 액세스 서버 구성</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. DNS 레코드 구성</p></td>
<td><p><a href="https://technet.microsoft.com/ko-kr/library/dn307232(v=exchg.150)">Exchange 2010 다중 서버 설치에 대한 DNS 레코드 구성</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16.에서으로 사서함 이동 Exchange 2010Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 사서함 이동</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Exchange 2013에서 Exchange 2013으로 공용 폴더 데이터 이동</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">공용 폴더</a></p>
<p><a href="https://technet.microsoft.com/ko-kr/library/jj150486(v=exchg.150)">직렬 마이그레이션을 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. 사후 설치 작업</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 설치 후 작업</a></p></td>
</tr>
</tbody>
</table>

