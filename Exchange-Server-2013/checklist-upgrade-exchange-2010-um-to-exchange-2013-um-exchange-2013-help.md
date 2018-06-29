﻿---
title: '검사 목록: Exchange 2010 UM을 Exchange 2013 UM으로 업그레이드: Exchange 2013 Help'
TOCTitle: '검사 목록: Exchange 2010 UM을 Exchange 2013 UM으로 업그레이드'
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54651825
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검사 목록: Exchange 2010 UM을 Exchange 2013 UM으로 업그레이드

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

이 검사 목록은 Exchange 2010 UM(통합 메시징)을 Exchange 2013 UM으로 업그레이드하는 데 도움이 됩니다. Exchange 2010 조직 및 UM 배포를 Exchange 2013으로 업그레이드할 때 이 정보를 참조하십시오. Exchange 2013 UM으로 업그레이드하는 단계별 지침은 [Exchange 2010 UM을 Exchange 2013 UM으로 업그레이드](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)를 참조하십시오.

이 검사 목록으로 작업을 시작하기 전에 다음 개념을 익히십시오.

  - [통합 메시징에 대 한 계획](planning-for-unified-messaging-exchange-2013-help.md)

  - [Um 전화 시스템 통합](telephone-system-integration-with-um-exchange-2013-help.md)

  - [음성 메일 시스템 전화 네트워크에 연결](connect-your-voice-mail-system-to-your-telephone-network-exchange-2013-help.md)

Exchange 2007 UM에서 Exchange 2013 UM으로 업그레이드하는 방법에 대한 단계별 지침은 [Exchange 2007 UM을 Exchange 2013 UM으로 업그레이드](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md)를 참조하세요.

## Exchange 2010 UM에서 Exchange 2013 UM으로의 업그레이드를 위한 검사 목록


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>완료 여부</th>
<th>작업</th>
<th>항목</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>전화 통신 구성 요소를 배포 및 구성합니다.</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">UM 전화 시스템에 연결</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013을 설치하기 전 시스템 요구 사항을 검토합니다.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 시스템 요구 사항</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>설치를 위한 필수 구성 요소가 충족되었는지 확인합니다.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>필수 클라이언트 액세스 서버 및 사서함 서버를 설치합니다.</p>
<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Exchange 2013 클라이언트 액세스 서버로 UM SIP 및 RTP 트래픽을 보내도록 VoIP 게이트웨이 또는 IP PBX를 구성하기 전에 조직에 Exchange 2013 사서함 서버를 하나 이상 배포해야 합니다.</td>
</tr>
</tbody>
</table>

</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 설치</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>설치를 확인하고 서버 설치 로그를 검토합니다.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 설치를 확인 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>필요한 경우 필수 UM 언어 팩을 설치합니다.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">UM 언어 팩 설치</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>UM 사용자 지정 음성 안내에 사용되는 Exchange 2010 시스템 사서함을 Exchange 2013으로 이동합니다.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 사서함 이동</a></p>

> [!NOTE]
> 시스템 사서함을 이미 이동했더라도 <A href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">가져오기 및 사용자 지정 인사말, 알림, 메뉴 및 음성 안내 내보내기</A>를 통해 Exchange 2010에서 사용자 지정 음성 안내를 수동으로 가져오고 내보낼 수 있습니다.


</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>인증서를 내보내고 가져옵니다.</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">UM에 대 한 인증서를 배포합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>모든 Exchange 2013 클라이언트 액세스 서버에서 UM 시작 모드를 구성합니다.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">클라이언트 액세스 서버에서 시작 모드를 구성 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>모든 Exchange 2013 사서함 서버에 대해 UM 시작 모드를 구성합니다.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">사서함 서버에서 시작 모드를 구성 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>기존 UM 다이얼 플랜을 만들거나 구성합니다.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">UM 다이얼 플랜 만들기</a></p>
<p><a href="manage-a-um-dial-plan-exchange-2013-help.md">UM 다이얼 플랜 관리</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>기존 UM IP 게이트웨이를 만들거나 구성합니다.</p></td>
<td><p><a href="create-a-um-ip-gateway-exchange-2013-help.md">UM IP 게이트웨이 만들기</a></p>
<p><a href="manage-a-um-ip-gateway-exchange-2013-help.md">UM IP 게이트웨이 관리</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>UM 헌트 그룹을 만듭니다.</p></td>
<td><p><a href="create-a-um-hunt-group-exchange-2013-help.md">UM 헌트 그룹 만들기</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>UM 자동 전화 교환을 만들거나 구성합니다.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">UM 자동 전화 교환 만들기</a></p>
<p><a href="manage-a-um-auto-attendant-exchange-2013-help.md">UM 자동 전화 교환 관리</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>UM 사서함 정책을 만들거나 구성합니다.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">UM 사서함 정책 만들기</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">UM 사서함 정책 관리</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>기존 UM 사용 가능 사서함을 Exchange 2013으로 이동합니다.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 사서함 이동</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>새 사용자가 UM을 사용하도록 설정하거나 기존 UM 사용 가능 사용자의 설정을 구성합니다.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">음성 메일에 대 한 사용자를 사용 하도록 설정</a></p>
<p><a href="manage-voice-mail-settings-for-a-user-exchange-2013-help.md">사용자에 대 한 음성 메일 설정 관리</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 2013 클라이언트 액세스 서버로 들어오는 모든 수신 전화를 전송하도록 VoIP 게이트웨이, IP PBX 및 SIP 사용 가능 PBX를 구성합니다.</p></td>
<td><p><a href="configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md">지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">Um VoIP 게이트웨이, IP PBX 또는 세션 테두리 컨트롤러에 연결</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Exchange 2010 UM 서버에서 전화 응답을 사용하지 않도록 설정합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">Exchange 2010에서 통합 메시징을 사용 하지 않도록 설정</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>다이얼 플랜에서 Exchange 2010 UM 서버를 제거합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">다이얼 플랜에서 UM 서버 제거</a></p></td>
</tr>
</tbody>
</table>

