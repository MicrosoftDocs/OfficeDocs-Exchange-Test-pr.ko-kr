---
title: '검사 목록: Exchange 2013의 새로운 설치를 수행 합니다.: Exchange 2013 Help'
TOCTitle: '검사 목록: Exchange 2013의 새로운 설치를 수행 합니다.'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 50484527
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검사 목록: Exchange 2013의 새로운 설치를 수행 합니다.

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

다음 검사 목록을 사용하여 Microsoft Exchange Server 2013을 배포합니다. 이 검사 목록으로 작업을 시작하기 전에 다음에서 설명되는 개념을 익혀야 합니다.

  - [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [배포 보안 검사 목록](deployment-security-checklist-exchange-2013-help.md)

이 검사 목록은 기본 시나리오에 대한 지침을 제공하는 일반적인 목록입니다.


> [!NOTE]
> Exchange Server 배포 도우미에는 Exchange Server를 배포하는 방법에 대한 사용자 지정 단계별 지침이 나와 있습니다. 배포 도우미를 사용하면 새로운 Exchange Server 2013 설치 버전을 배포하거나, 이전 버전을 Exchange 2013으로 업그레이드하거나, Exchange 2013과 Exchange Online의 하이브리드 배포를 구성할 수 있습니다. 자세한 내용은 <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Exchange Server 배포 도우미</A>를 참조하세요.



## Exchange 2013 새 설치를 위한 검사 목록


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>설치</p></td>
<td><p>작업</p></td>
<td><p>항목</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. 릴리스 정보 읽기</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Exchange Server 2013 릴리스 정보</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. 시스템 요구 사항 확인</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 시스템 요구 사항</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. 필수 구성 요소 단계가 완료되었는지 확인</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. 연결되지 않은 네임스페이스 구성</p>

> [!NOTE]
> 이 단계는 선택입니다. 조직이 연결되지 않은 네임스페이스를 실행 중인 경우에만 필요합니다.


</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">분리 된 네임 스페이스 시나리오</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. 사서함 서버 역할 설치</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 설치</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. 클라이언트 액세스 서버 역할 설치</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 설치</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Edge 전송 서버 역할을 설치합니다.</p>

> [!NOTE]
> 이 단계는 선택입니다. Edge 전송 서버를 설치하려는 경우에만 이 단계를 수행하면 됩니다. 자세한 내용은 <A href="edge-transport-servers-exchange-2013-help.md">Edge 전송 서버</A>를 참조하세요.


</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 Edge 전송 역할 설치</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. EdgeSync 구독을 만듭니다.</p>
<p>이 단계는 선택입니다. Edge 전송 서버를 설치했으며 Edge 전송 서버와 허브 전송 서버 간에 EdgeSync 구독을 구성하려는 경우에만 이 단계를 수행하면 됩니다. 자세한 내용은 <a href="edge-subscriptions-exchange-2013-help.md">Edge 구독</a>을 참조하세요.</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. 전송 구성</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. 허용 도메인 추가</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. 전자 메일 주소 정책 구성</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. 오프라인 주소록, Exchange 웹 서비스, EAC(Exchange 관리 센터), Outlook Web App 및 Exchange ActiveSync 가상 디렉터리를 비롯한 가상 디렉터리에 대한 설정 구성</p>

> [!NOTE]
> Exchange 웹 서비스, Outlook Anywhere 또는 오프라인 주소록을 사용하려는 경우에 이 단계가 필요합니다. 또한 EAC, Outlook Web App 또는 Exchange ActiveSync의 기본 설정을 변경해야 하는 경우에도 필요할 수 있습니다.


</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. 클라이언트 액세스 서버에 디지털 인증서 추가</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. 통합 메시징 구성</p>

> [!NOTE]
> 이 단계는 선택입니다. 통합 메시징을 조직에서 사용하려는 경우에만 필요합니다.


</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">음성 메일 및 UM 배포</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. 추가 통합 메시징 및 Lync Server 설정 구성</p>

> [!NOTE]
> 이 단계는 선택입니다. 조직에서 구성한 통합 메시징을 Lync Server와 통합하려는 경우에만 이 단계를 수행하면 됩니다.


</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Exchange 2013 UM 및 Lync Server 배포 개요</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. 설치 후 작업</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Exchange 2013 설치 후 작업</a></p></td>
</tr>
</tbody>
</table>

