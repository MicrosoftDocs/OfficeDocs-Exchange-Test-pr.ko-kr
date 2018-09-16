---
title: '검사 목록: Exchange 2013 UM 배포: Exchange 2013 Help'
TOCTitle: '검사 목록: Exchange 2013 UM 배포'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52058075
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검사 목록: Exchange 2013 UM 배포

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-03-09_

이 검사 목록을 사용하여 조직에 UM(통합 메시징)을 설치 및 배포할 수 있습니다.

이 검사 목록으로 작업을 시작하기 전에 다음 개념을 익히십시오.

  - [통합 메시징](unified-messaging-exchange-2013-help.md)

  - [새 음성 메일 기능](new-voice-mail-features-exchange-2013-help.md)

  - [통합 메시징에 대 한 계획](planning-for-unified-messaging-exchange-2013-help.md)

UM 및 Microsoft Lync Server를 배포하는 방법에 대한 단계별 지침은 [검사 목록: Lync Server와 Exchange 2013 UM 통합](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md)을 참조하십시오.

## 통합 메시징 배포 관련 검사 목록


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
<td><p> </p></td>
<td><p>설치를 위한 필수 구성 요소가 충족되었는지 확인합니다.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>필수 클라이언트 액세스 서버 및 사서함 서버를 설치합니다.</p>

> [!CAUTION]
> Exchange 2013 클라이언트 액세스 서버로 UM SIP 및 RTP 트래픽을 보내도록 VoIP 게이트웨이 또는 IP PBX를 구성하기 전에 조직에 Exchange 2013 사서함 서버를 하나 이상 배포해야 합니다.

</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 설치</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>설치를 확인하고 서버 설치 로그를 검토합니다.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 설치를 확인 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>필요한 경우 필수 UM 언어 팩을 설치합니다.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">UM 언어 팩 설치</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>조직에 필요한 수의 다이얼 플랜을 만듭니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan">UM 다이얼 플랜 만들기</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>다이얼 플랜 보안 설정을 구성합니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/configure-voip-security-setting">VoIP 보안 설정 구성</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>각 클라이언트 액세스 서버 및 사사험 서버에 대해 UM 시작 모드를 구성합니다.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">사서함 서버에서 시작 모드를 구성 합니다.</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">클라이언트 액세스 서버에서 시작 모드를 구성 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>사서함 서버에 대한 동시 통화 수를 구성합니다.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">사서함 서버에서 들어오는 호출의 수를 구성 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Outlook Voice Access 번호 및 기타 설정을 구성합니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-dial-plan">UM 다이얼 플랜 관리</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>통합 메시징의 아웃바운드 전화 걸기를 구성합니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-using-dialing-rules">전화걸기 규칙을 사용 하 여 전화 대 한 권한 부여</a></p>
<p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-users-in-a-dial-plan">사용자에 대 한 호출 다이얼 플랜에 대 한 권한 부여</a></p>
<p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-client-voice-mail-features/authorize-calls-for-a-group-of-users">사용자 그룹에 대 한 통화 권한 부여</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>필요한 수의 자동 전화 교환을 만듭니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant">UM 자동 전화 교환 만들기</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>각 UM 자동 전화 교환을 설치 및 구성합니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/set-up-um-auto-attendant">UM 자동 전화 교환을 설정합니다</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>UM용 새 Exchange 인증서를 만들고 가져오고 사용하도록 설정하거나, 상호 신뢰 타사 인증서를 사용하도록 설정합니다. 또한 모든 VoIP 게이트웨이, IP PBX 및 SBC에 대해 인증서를 가져옵니다.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>모든 Exchange 서버에서 Microsoft Exchange 통합 메시징 서비스 및 통합 메시징 통화 라우터 서비스를 다시 시작하여 필요한 인증서를 로드합니다.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 서비스를 중지 합니다.</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 서비스를 시작 합니다.</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 호출 라우터 서비스를 중지 합니다.</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 호출 라우터 서비스를 시작 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>UM 사서함 정책을 만들거나 기본 UM 사서함 정책을 구성합니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy">UM 사서함 정책 만들기</a></p>
<p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy">UM 사서함 정책 관리</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>내선 번호 및 E.164 번호(필요한 경우)로 사용자가 통합 메시징을 사용하도록 설정합니다.</p></td>
<td><p><a href="https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail">음성 메일에 대 한 사용자를 사용 하도록 설정</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>수신 팩스를 사용하도록 설정합니다(옵션).</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">음성 메일 사용자가 팩스를 받을 수 있도록</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>보호된 음성 메일을 설정합니다(옵션).</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">음성 메일 보호</a></p></td>
</tr>
</tbody>
</table>


맨 위로 이동

