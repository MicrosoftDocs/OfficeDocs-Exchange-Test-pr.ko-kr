---
title: '검사 목록: Lync Server와 Exchange 2013 UM 통합: Exchange 2013 Help'
TOCTitle: '검사 목록: Lync Server와 Exchange 2013 UM 통합'
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 52058071
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 검사 목록: Lync Server와 Exchange 2013 UM 통합

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

이 검사 목록을 사용하여 UM(통합 메시징) 및 Microsoft Lync Server 2013을 설치하고 배포할 수 있습니다. 이 항목에서 "Lync Server"는 Lync Server 2010도 지칭합니다. 그러나 Microsoft Office Communications Server 2007 R2도 통합 메시징과 함께 배포할 수 있습니다.


> [!NOTE]
> &nbsp;



이 검사 목록으로 작업을 시작하기 전에 다음 개념을 익히십시오.

  - [Exchange 2013 UM 및 Lync Server 배포 개요](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Office Communications Server 2007 R2 및 Lync Server와 동시 사용](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

Lync Server에 대 한 완료 되어야 하는 작업을 수행 하는 방법에 대 한 자세한 내용은 [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=265752)를 참조 하십시오.

## Microsoft Lync Server 및 통합 메시징 배포를 위한 검사 목록


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
<td><p>Exchange Server 2013 설치 전에 시스템 요구 사항을 검토합니다.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Exchange 2013 시스템 요구 사항</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>설치를 위한 필수 구성 요소가 충족되었는지 확인합니다.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Exchange 2013 필수 구성 요소</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Microsoft Lync Server 2013 및 Microsoft Exchange Server 2013 통합을 위한 필수 구성 요소를 검토합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282082">Exchange Server 2013 Microsoft Lync Server 2013 및 Microsoft 통합을 위한 필수 구성 요소</a></p>

> [!TIP]
> 통합 통신 관리 되는 API (UCMA) 4.0 런타임은 Exchange 2013 및 Lync Server 2010 및 2013 필요 하 고 설치 하는 동안 설치 됩니다. 을 다운로드 하 고 UCMA 4.0에 대 한 정보를 검토 하려면 <A href="https://go.microsoft.com/fwlink/p/?linkid=258269">Unified Communications Managed API 4.0 Runtime</A>


</td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>필수 클라이언트 액세스 서버 및 사서함 서버를 설치합니다.</p></td>
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
<td><p>조직에 필요한 수의 SIP URI 다이얼 플랜을 만듭니다.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">UM 다이얼 플랜 만들기</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>다이얼 플랜 보안 설정을 구성합니다.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">VoIP 보안 설정 구성</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>사서함 서버에 대한 동시 통화 수를 구성합니다.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">사서함 서버에서 들어오는 호출의 수를 구성 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Outlook Voice Access 번호 및 기타 설정을 구성합니다.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">UM 다이얼 플랜 관리</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>각 SIP URI 다이얼 플랜에 모든 클라이언트 액세스 서버 및 사서함 서버를 추가합니다.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>통합 메시징의 아웃바운드 전화 걸기를 구성합니다. SIP URI 다이얼 플랜 및 해당 다이얼 플랜에 연결되는 UM 사서함 정책에 대한 모든 통화를 허용합니다.</p></td>
<td><p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">사용자에 대 한 호출 다이얼 플랜에 대 한 권한 부여</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">사용자 그룹에 대 한 통화 권한 부여</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>필요한 수의 자동 전화 교환을 만듭니다.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">UM 자동 전화 교환 만들기</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>각 UM 자동 전화 교환을 설치 및 구성합니다.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">UM 자동 전화 교환을 설정합니다</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>UM용 새 Exchange 인증서를 만들고 가져오고 사용하도록 설정하거나, 상호 신뢰 타사 인증서를 사용하도록 설정합니다.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">SIP URI 다이얼 플랜에 사서함 및 클라이언트 액세스 서버를 추가 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>각 클라이언트 액세스 서버 및 사서함 서버에 대해 UM 시작 모드를 이중 또는 TLS로 구성합니다.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">사서함 서버에서 시작 모드를 구성 합니다.</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">클라이언트 액세스 서버에서 시작 모드를 구성 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>모든 Exchange 서버에서 Microsoft Exchange 통합 메시징 서비스 및 통합 메시징 통화 라우터 서비스를 다시 시작하여 필요한 인증서를 로드합니다.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 서비스를 중지 합니다.</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 서비스를 시작 합니다.</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 호출 라우터 서비스를 중지 합니다.</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Microsoft Exchange 통합 메시징 호출 라우터 서비스를 시작 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>UM 사서함 정책을 만들거나 기본 UM 사서함 정책을 구성합니다.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">UM 사서함 정책 만들기</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">UM 사서함 정책 관리</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>SIP 주소를 통해 사용자가 통합 메시징을 사용할 수 있도록 설정하고 SIP URI 다이얼 플랜에 사용자를 연결합니다.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">음성 메일에 대 한 사용자를 사용 하도록 설정</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Lync Server 2013 계획 설명서를 검토합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282081">계획</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Lync Server 2013을 설치 및 배포합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282051">Lync Server 2013 배포</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange UM 서버에서 가져온 상호 신뢰 내부 PKI 또는 타사 인증서를 가져옵니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281863">서버에 대 한 인증서 구성</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281865">인증서 구성 메시징 통합 Microsoft Exchange Server를 실행 하는 서버에서</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>필요한 경우 서버에서 Lync 서비스를 시작하여 인증서를 로드합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=282084">서버 제공 서비스를 시작 합니다.</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exchange 관리 셸을 열고 %Program Files%\Microsoft\Exchange Server\V15\Scripts 폴더에 있는 exchucutil.ps1 스크립트를 실행합니다.</p>
<p></p></td>
<td><p><a href="configure-um-to-work-with-lync-server-exchange-2013-help.md">Lync Server와 함께 작동 하는 UM 구성</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Enterprise Voice 요구 사항을 검토합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281876">Enterprise Voice에 대 한 소프트웨어 필수 구성 요소</a></p>
<p><a href="https://go.microsoft.com/fwlink/p/?linkid=281875">보안 및 Enterprise Voice에 대 한 구성 필수 구성 요소</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>미디어 게이트웨이 또는 중재 서버를 배포 및 구성하고 피어를 정의합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281872">중재 서버를 배포 및 피어 정의</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>중재 서버와 하나 이상의 피어 간에 트렁크를 구성하여 공중 전화망(PSTN) 연결을 제공합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281868">트렁크 구성</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Lync 다이얼 플랜을 만들어서 구성하고 정규화 규칙을 만들어서 정의하고 연결합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281867">다이얼 플랜 구성</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>음성 정책을 구성하고 전화 사용 및 아웃바운드 통화 경로를 정의합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281869">구성 음성 정책, PSTN 사용 레코드 및 음성 경로</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Outlook Voice Access 및 자동 전화 교환용 연락처 개체를 만드는 Exchange 통합 유틸리티(ocsumutil.exe)를 실행합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281866">Microsoft Exchange Server 통합 메시징과 함께 작동 하도록 Lync Server 2013 구성</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>필요한 고급 Enterprise Voice 기능을 정의, 배포 및 구성합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281871">Enterprise Voice 기능을 고급 배포</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>사용자가 Enterprise Voice를 사용할 수 있도록 설정합니다. 줄 URI를 입력하고 음성 정책과 Lync 다이얼 플랜을 할당합니다.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=281873">사용자가 Enterprise Voice 사용 하도록 설정</a></p></td>
</tr>
</tbody>
</table>

