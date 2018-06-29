---
title: 'Exchange 2013에서 사라진 기능: Exchange 2013 Help'
TOCTitle: Exchange 2013에서 사라진 기능
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 50482475
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013에서 사라진 기능

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 Microsoft Exchange Server 2013에서 제거되거나, 더 이상 지원되지 않거나, 바뀐 구성 요소, 특징 또는 기능에 대해 설명합니다.


> [!NOTE]
> 다음 항목도 유용할 수 있습니다. 
> <UL>
> <LI>
> <P><A href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 새로운 기능</A>&nbsp;&nbsp;&nbsp;Exchange Server 2013의 새로운 기능에 대한 정보입니다.</P>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=267479">Exchange 2013에 대 한 개발자 로드맵</A>&nbsp;&nbsp;&nbsp;&nbsp;"개발 기술 Exchange에서 제거를 참조 하십시오? Exchange 2013 에서 지원이 중단 된 API 및 개발 기능에 대 한 정보에 대 한 섹션입니다.</P></LI></UL>



## Exchange 2010에서 Exchange 2013으로 업그레이드되면서 지원되지 않는 기능

이 섹션에는 Exchange 2013에서 더 이상 사용할 수 없는 Exchange Server 2010 기능이 나열되어 있습니다.

## 아키텍처


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>허브 전송 서버 역할</p></td>
<td><p>허브 전송 서버 역할은 사서함 및 클라이언트 액세스 서버 역할에 대해 실행되는 전송 서비스로 바뀌었습니다. 사서함 서버 역할에는 Microsoft Exchange 전송, Microsoft Exchange 사서함 전송 배달 및 Microsoft Exchange 사서함 전송 제출 서비스가 포함됩니다. 클라이언트 액세스 서버 역할에는 Microsoft Exchange 프런트 엔드 전송 서비스가 포함됩니다. 자세한 내용은 <a href="mail-flow-exchange-2013-help.md">메일 흐름</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>통합 메시징 서버 역할</p></td>
<td><p>통합 메시징 서버 역할은 사서함 및 클라이언트 액세스 서버 역할에 대해 실행되는 통합 메시징 서비스로 바뀌었습니다. 사서함 서버 역할에는 Microsoft Exchange 통합 메시징 서비스가 포함되고 클라이언트 액세스 서버 역할에는 Microsoft Exchange 통합 메시징 호출 라우터 서비스가 포함됩니다. 자세한 내용은 <a href="voice-architecture-changes-exchange-2013-help.md">아키텍처 변경 사항</a>을 참조하십시오.</p></td>
</tr>
</tbody>
</table>


## 관리 인터페이스


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 관리 콘솔 및 Exchange 제어판</p></td>
<td><p>Exchange 관리 콘솔 및 Exchange 제어판이 EAC(Exchange 관리 센터)로 대체되었습니다. EAC는 Exchange 제어판과 동일한 가상 디렉터리(/ecp)를 사용합니다. 자세한 내용은 <a href="exchange-admin-center-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 Exchange 관리 센터</a>를 참조하십시오.</p></td>
</tr>
</tbody>
</table>


## 클라이언트 액세스


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2003은 지원되지 않음</p></td>
<td><p>Microsoft Outlook을 Exchange 2013에 연결하려면 자동 검색 서비스를 사용해야 합니다. 그러나 Microsoft Outlook 2003은 자동 검색 서비스의 사용을 지원하지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 클라이언트에 대한 RPC/TCP 액세스</p></td>
<td><p>Exchange 2013에서 Microsoft Outlook 클라이언트는 Outlook Anywhere(RPC/HTTP) 또는 Exchange 2013 서비스 팩 1 및 Outlook 2013 서비스 팩 1 이상의 MAPI over HTTP를 사용하여 연결할 수 있습니다. 조직에 Outlook 클라이언트가 있는 경우 Outlook Anywhere 및/또는 MAPI over HTTP를 사용해야 합니다. 자세한 내용은 <a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a> 및 <a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a>를 참조하세요.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 및 Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>맞춤법 검사</p></td>
<td><p>Outlook Web App에서 더 이상 맞춤법 검사 서비스가 기본 제공되지 않습니다. 대신 웹 브라우저의 맞춤법 검사 기능을 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>사용자 지정 가능한 필터</p></td>
<td><p>Outlook Web App에는 더 이상 사용자 지정 가능한 필터링된 보기가 없으며 이제는 필터링된 보기를 즐겨찾기에 저장할 수 없습니다. 사용자 지정 가능한 필터는 모든 메시지, 읽지 않은 메시지, 사용자에게 전송된 메시지 또는 플래그가 지정된 메시지를 보는 데 사용할 수 있는 고정 필터로 대체되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p>메시지 플래그</p></td>
<td><p>Outlook Web App에서는 메시지 플래그에 사용자 지정 날짜를 설정하는 기능을 사용할 수 없으며 Outlook을 통해 사용자 지정 날짜를 설정할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>채팅 연락처 목록</p>
<p></p></td>
<td><p>Outlook Web App for Exchange 2010의 폴더 목록에 표시된 채팅 연락처 목록을 더 이상 사용할 수 없습니다.</p></td>
</tr>
<tr class="odd">
<td><p>검색 폴더</p></td>
<td><p>사용자가 검색 폴더를 사용하는 기능은 현재 Outlook Web App에서 제공되지 않습니다.</p></td>
</tr>
</tbody>
</table>


## 메일 흐름


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>연결된 커넥터</p></td>
<td><p>송신 커넥터를 수신 커넥터에 연결하는 기능이 제거되었습니다. 특히 <em>LinkedReceiveConnector</em> 매개 변수가 <a href="https://technet.microsoft.com/ko-kr/library/aa998936(v=exchg.150)">New-SendConnector</a>와 <a href="https://technet.microsoft.com/ko-kr/library/aa998294(v=exchg.150)">Set-SendConnector</a>에서 제거되었습니다.</p></td>
</tr>
</tbody>
</table>


## 스팸 방지 및 맬웨어 방지


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EMC의 스팸 방지 에이전트 관리</p></td>
<td><p>Exchange 2010에서는 허브 전송 서버에서 스팸 방지 에이전트를 사용하도록 설정한 경우 EMC(Exchange 관리 콘솔)에서 스팸 방지 에이전트를 관리할 수 있었습니다. Exchange 2013에서 사서함 서버의 스팸 방지 에이전트를 사용하도록 설정해도 EAC를 사용하여 에이전트를 관리할 수 없습니다. 셸만 사용할 수 있습니다. 사서함 서버에서 스팸 방지 에이전트를 사용하도록 설정하는 방법에 대한 자세한 내용은 <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">사서함 서버에서 스팸 방지 기능을 사용 하도록 설정</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>허브 전송 서버의 연결 필터링 에이전트</p></td>
<td><p>Exchange 2010에서는 허브 전송 서버에서 스팸 방지 에이전트를 사용하도록 설정한 경우 사용할 수 없는 스팸 방지 에이전트가 첨부 파일 필터 에이전트뿐이었습니다. Exchange 2013에서 사서함 서버의 스팸 방지 에이전트를 사용하도록 설정하는 경우 첨부 파일 필터 에이전트와 연결 필터링 에이전트를 사용할 수 없습니다. 연결 필터링 에이전트는 IP 허용 목록 및 IP 차단 목록 기능을 제공합니다. 사서함 서버에서 스팸 방지 에이전트를 사용하도록 설정하는 방법에 대한 자세한 내용은 <a href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">사서함 서버에서 스팸 방지 기능을 사용 하도록 설정</a>을 참조하십시오.</p>

> [!NOTE]
> Exchange 2013 클라이언트 액세스 서버에서는 스팸 방지 에이전트를 사용하도록 설정할 수 없습니다. 따라서 연결 필터링 에이전트를 사용할 수 있는 유일한 방법은 경계 네트워크에 Edge 전송 서버를 설치하는 것입니다. 자세한 내용은 <A href="edge-transport-servers-exchange-2013-help.md">Edge 전송 서버</A>를 참조하세요.


</td>
</tr>
</tbody>
</table>


## 메시징 정책 및 규정 준수


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>관리되는 폴더</p></td>
<td><p>Exchange 2010 메시징 보존 관리 (MRM)에 대 한 관리 되는 폴더를 사용 합니다. Exchange 2013 관리 되는 폴더 지원 되지 않습니다. MRM에 대 한 보존 정책을 사용 해야 합니다.</p>

> [!NOTE]
> 관리 되는 폴더와 관련된 Cmdlet을 계속 사용할 수 있습니다. 관리되는 폴더, 관리되는 콘텐츠 설정 및 관리되는 폴더 사서함 정책을 만들 수 있으며 관리되는 폴더 사서함 정책을 사용자에게 적용할 수 있습니다. 그러나 MRM 도우미는 관리되는 폴더 사서함 정책이 적용된 사서함을 처리하지 않고 건너뜁니다.


</td>
</tr>
<tr class="even">
<td><p>관리되는 폴더 포트 마법사</p></td>
<td><p>Exchange 2010에서는 관리되는 폴더 포트 마법사를 사용하여 관리되는 폴더 및 관리되는 콘텐츠 설정에 기반한 보존 태그를 만듭니다. Exchange 2013에서 Exchange 관리 센터에는 이 기능이 포함되어 있지 않습니다. <em>ManagedFolderToUpgrade</em> 매개 변수와 함께 <strong>New-RetentionPolicyTag</strong> cmdlet을 사용하여 관리되는 폴더에 기반한 보존 태그를 만들 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 통합 메시징 및 음성 메일


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ASR(자동 음성 인식)을 사용한 디렉터리 조회</p></td>
<td><p>Exchange 2010에서 Outlook Voice Access 사용자는 ASR(자동 음성 인식)을 통해 음성 입력을 사용하여 디렉터리에 나열된 사용자를 검색할 수 있습니다. 또한 음성 입력을 사용하여 Outlook Voice Access에서 메뉴, 메시지 및 기타 옵션을 탐색할 수도 있습니다. 그러나 Outlook Voice Access 사용자가 음성 입력을 사용할 수 있다고 하더라도 PIN을 입력하고 개인 옵션을 탐색할 때는 전화 키패드를 사용해야 합니다.</p>
<p>Exchange 2013에서 인증된 Outlook Voice Access 사용자와 인증되지 않은 Outlook Voice Access 사용자는 모든 언어로 음성 입력 또는 ASR을 사용하여 디렉터리에서 사용자를 검색할 수 없습니다. 그러나 자동 전화 교환을 호출하는 발신자는 여러 언어로 음성 입력을 사용하여 자동 전화 교환 메뉴를 탐색하고 디렉터리에서 사용자를 검색할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


## 도구


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 모범 사례 분석기</p></td>
<td><p>Exchange 2010 Exchange 모범 사례 분석기 Exchange 배포를 검사 하 고 Microsoft에 대 한 유용한 정보 나란히 표시 구성 되었는지 여부를 결정 합니다. Exchange 2013 Exchange 모범 사례 분석기 <a href="https://go.microsoft.com/fwlink/p/?linkid=391077">Exchange Server 2013에 대 한 Office 365 모범 사례 분석기</a>으로 대체 되었습니다.</p></td>
</tr>
<tr class="even">
<td><p>메일 흐름 문제 해결사</p></td>
<td><p>Exchange 2010에서는 메일 흐름 문제 해결사의 도움을 받아서 일반 메일 흐름 문제를 해결할 수 있었습니다. Exchange 2013에서는 메일 흐름 문제 해결사가 제거되었습니다. 이제 Exchange 2013의 EAC에 있는 메시징 추적 기능을 사용할 수 있습니다. 자세한 내용은 <a href="track-messages-with-delivery-reports-exchange-2013-help.md">배달 보고서로 메시지 추적</a>을 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>성능 모니터</p></td>
<td><p>Exchange 2010에서는 성능 모니터가 Exchange 도구 상자에 포함되어 메시징 시스템 성능에 대한 정보를 수집할 수 있었습니다. 성능 모니터는 성능 문제를 해결하는 동안 주요 매개 변수를 보는 데 일반적으로 사용됩니다. Exchange 2013에서는 성능 모니터가 도구 상자에서 제거되었습니다. 그래도 Windows Server 2008의 <strong>관리 도구</strong>에서 성능 모니터를 찾을 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>성능 문제 해결사</p></td>
<td><p>Exchange 2013에서는 성능 문제 해결사가 제거되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p>라우팅 로그 뷰어</p></td>
<td><p>Exchange 2013에서는 라우팅 로그 뷰어가 제거되었습니다.</p></td>
</tr>
</tbody>
</table>


## 사서함 데이터베이스 복사본


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Update-MailboxDatabaseCopy</p></li>
<li><p>사서함 데이터베이스 복사본 마법사 업데이트</p></li>
</ul></td>
<td><p>콘텐츠 인덱스 카탈로그 시드이 더이상 사용할 수 있는 네트워크를 통해 복제 합니다. 또한 MAPI 네트워크를 통해 수행할 수만 있습니다. Update-mailboxdatabasecopy cmdlet에서 <code>-Network</code> 매개 변수를 사용 하는 경우에 마찬가지입니다.</p></td>
</tr>
</tbody>
</table>


## Exchange 2007에서 Exchange 2013으로 업그레이드되면서 지원되지 않는 기능

이 섹션에는 Exchange 2013에서 더 이상 사용할 수 없는 Exchange Server 2007 기능이 나열되어 있습니다.

## API 및 개발


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange WebDAV</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=167197">Exchange 웹 서비스</a> 나 <a href="https://go.microsoft.com/fwlink/p/?linkid=157179">EWS 관리 API를</a>사용 합니다. 또는 WebDAV를 사용 하는 응용 프로그램에 의해 관리 되는 사서함에 대 한 Exchange 2007 서버를 유지할 수 있습니다. 자세한 내용은 <a href="https://go.microsoft.com/fwlink/p/?linkid=169474">WebDAV에서 마이그레이션</a>를 참조 하십시오.</p></td>
</tr>
</tbody>
</table>


## 아키텍처


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>저장소 그룹</p></td>
<td><p>Exchange 2013에서는 더 이상 저장소 그룹 구조를 사용하지 않고 대신 사서함 데이터베이스를 간단하게 관리할 수 있습니다. 자세한 내용은 <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 사서함 데이터베이스를 관리 합니다.</a>를 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>ESE(Extensible Storage Engine) 스트리밍 백업 API</p></td>
<td><p>Exchange 2013에서는 Exchange 인식 VSS(볼륨 섀도 복사본 서비스) 기반 백업만 지원됩니다. Exchange 2013에는 데이터를 백업 및 복원할 수 있는 Windows 서버 백업용 플러그 인이 포함되어 있습니다. 자세한 내용은 <a href="backup-restore-and-disaster-recovery-exchange-2013-help.md">백업, 복원 및 재해 복구</a>을 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p>UDP(사용자 데이터그램 프로토콜) 알림</p></td>
<td><p>UDP(User Datagram Protocol) 알림에 대한 지원이 Exchange 2013에서 제거되었습니다. 이러한 변경은 Outlook 2003 클라이언트가 Exchange 2013 서버의 사서함에 연결될 때 사용자 환경에 영향을 미칩니다. 자세한 내용은 Microsoft 기술 자료 문서 2009942, <a href="http://go.microsoft.com/fwlink/?linkid=3052%26kbid=2009942">Exchange Server 2010 사용자가 온라인 모드에서 Outlook 2003을 사용할 때 폴더를 업데이트하는 데 시간이 오래 걸림</a>을 참조하십시오.</p></td>
</tr>
</tbody>
</table>


## 고가용성


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CCR(클러스터 연속 복제)</p></td>
<td><p>Exchange 2013에서는 DAG(데이터베이스 사용 가능 그룹) 및 사서함 데이터베이스 복사본을 사용합니다. 자세한 내용은 <a href="high-availability-and-site-resilience-exchange-2013-help.md">고가용성 및 사이트 복구</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>LCR(로컬 연속 복제)</p></td>
<td><p>Exchange 2013에서는 DAG 및 사서함 데이터베이스 복사본을 사용합니다. 자세한 내용은 <a href="high-availability-and-site-resilience-exchange-2013-help.md">고가용성 및 사이트 복구</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>SCR(대기 연속 복제)</p></td>
<td><p>Exchange 2013에서는 DAG 및 사서함 데이터베이스 복사본을 사용합니다. 자세한 내용은 <a href="high-availability-and-site-resilience-exchange-2013-help.md">고가용성 및 사이트 복구</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>SCC(단일 복사본 클러스터)</p></td>
<td><p>Exchange 2013에서는 DAG 및 사서함 데이터베이스 복사본을 사용합니다. 자세한 내용은 <a href="high-availability-and-site-resilience-exchange-2013-help.md">고가용성 및 사이트 복구</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>Setup /recoverCMS</p></td>
<td><p>Exchange 2013에서는 Setup /m:recoverServer를 사용합니다. 자세한 내용은 <a href="recover-an-exchange-server-exchange-2013-help.md">Exchange Server 복구</a>을 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>클러스터된 사서함 서버</p></td>
<td><p>Exchange 2013에서는 DAG 및 사서함 데이터베이스 복사본을 사용합니다. 자세한 내용은 <a href="high-availability-and-site-resilience-exchange-2013-help.md">고가용성 및 사이트 복구</a>를 참조하십시오.</p></td>
</tr>
</tbody>
</table>


## 클라이언트 액세스


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>POP3 및 IMAP4 사용자에 대해 통합 Windows 인증(NTLM)을 사용하여 클라이언트 인증</p></td>
<td><p>NTLM은 Exchange 2013 에서 POP3 또는 IMAP4 클라이언트 연결에 대 한 지원 되지 않습니다. NTLM을 사용 하는 POP3 또는 IMAP4 클라이언트 프로그램에서 연결 실패 합니다. Exchange 2013 의 RTM 버전을 실행 하는 경우 NTLM 대신 하는 것이 좋습니다 SSL과 함께 일반 텍스트 인증을 사용 하는 것입니다.</p>
<p>Exchange 2013을 사용 중인 경우 NTLM을 사용하려면 Exchange 2013 조직에서 Exchange 2007 서버를 보유해야 합니다.</p></td>
</tr>
</tbody>
</table>


## Outlook Web App 및 Outlook


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>문서 액세스</p></td>
<td><p>Outlook Web App를 사용하여 Microsoft SharePoint 문서 라이브러리와 Windows 파일 공유에 액세스할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>메시지 플래그</p></td>
<td><p>Outlook Web App 2013에서는 메시지 플래그에 사용자 지정 날짜를 설정하는 기능을 사용할 수 없으며 Outlook을 사용하여 사용자 지정 날짜를 설정할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>맞춤법 검사</p></td>
<td><p>Outlook Web App에서는 웹 브라우저의 맞춤법 검사 기능을 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p>검색 폴더</p></td>
<td><p>사용자가 검색 폴더를 사용하는 기능은 현재 Outlook Web App에서 제공되지 않습니다.</p></td>
</tr>
<tr class="odd">
<td><p>캐시 된 최대 보기</p></td>
<td><p>Exchange 2007 지원 Outlook 클라이언트에 대 한 데이터베이스 (msExchMaxCachedViews) 매개 변수 당 캐시 된 보기의 최대 수를 수정 합니다. Exchange 2013 더이상이 매개 변수를 사용합니다.</p></td>
</tr>
</tbody>
</table>


## 받는 사람 관련 기능


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Export-Mailbox</strong> 및 <strong>Import-Mailbox</strong> cmdlet</p></td>
<td><p>Exchange 2013에서는 내보내기 요청이나 가져오기 요청을 사용합니다. 자세한 내용은 <a href="mailbox-import-and-export-requests-exchange-2013-help.md">사서함 가져오기 및 내보내기 요청</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p><strong>Move-Mailbox</strong> cmdlet 집합</p></td>
<td><p>Exchange 2013에서는 이동 요청을 사용하여 사서함을 이동합니다. 자세한 내용은 <a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 사서함 이동</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>ISInteg</p></td>
<td><p>Exchange 2013에서는 <a href="https://technet.microsoft.com/ko-kr/library/ff625226(v=exchg.150)">New-MailboxRepairRequest</a>를 사용합니다.</p></td>
</tr>
</tbody>
</table>


## 메시징 정책 및 규정 준수


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>관리되는 폴더</p></td>
<td><p>Exchange 2007에서는 관리되는 폴더가 MRM(메시징 보존 관리)에 사용됩니다. Exchange 2013에서는 관리되는 폴더가 지원되지 않습니다. MRM에 대한 보존 정책을 사용해야 합니다.</p>

> [!NOTE]
> 관리 되는 폴더와 관련된 Cmdlet을 계속 사용할 수 있습니다. 관리되는 폴더, 관리되는 콘텐츠 설정 및 관리되는 폴더 사서함 정책을 만들 수 있으며 관리되는 폴더 사서함 정책을 사용자에게 적용할 수 있습니다. 그러나 MRM 도우미는 관리되는 폴더 사서함 정책이 적용된 사서함을 처리하지 않고 건너뜁니다.


</td>
</tr>
</tbody>
</table>


## 통합 메시징 및 음성 메일


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>설명 및 완화</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook Voice Access에 ASR(자동 음성 인식)을 사용하여 디렉터리 조회</p></td>
<td><p>Exchange 2007에서 Outlook Voice Access 사용자는 ASR(자동 음성 인식)을 통해 영어(미국)(en-US)로 음성 입력을 사용하여 디렉터리에 나열된 사용자를 검색할 수 있습니다. 또한 음성 입력을 사용하여 Outlook Voice Access에서 메뉴, 메시지 및 기타 옵션을 탐색할 수도 있습니다. 그러나 Outlook Voice Access 사용자가 음성 입력을 사용할 수 있다고 하더라도 PIN을 입력하고 개인 옵션을 탐색할 때는 전화 키패드를 사용해야 합니다.</p>
<p>Exchange 2013에서 인증된 Outlook Voice Access 사용자와 인증되지 않은 Outlook Voice Access 사용자는 모든 언어로 음성 입력 또는 ASR을 사용하여 디렉터리에서 사용자를 검색할 수 없습니다. 그러나 자동 전화 교환을 호출하는 발신자는 여러 언어로 음성 입력을 사용하여 자동 전화 교환 메뉴를 탐색하고 디렉터리에서 사용자를 검색할 수 있습니다.</p></td>
</tr>
</tbody>
</table>

