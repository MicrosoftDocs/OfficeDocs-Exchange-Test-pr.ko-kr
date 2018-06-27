---
title: '클라이언트에 대한 네트워크 포트 및 Exchange 2013의 메일 흐름: Exchange 2013 Help'
TOCTitle: 클라이언트에 대한 네트워크 포트 및 Exchange 2013의 메일 흐름
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64126834
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 클라이언트에 대한 네트워크 포트 및 Exchange 2013의 메일 흐름

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

이 항목에서는 전자 메일 클라이언트, 인터넷 메일 서버 및 로컬 Exchange 조직 외부의 기타 서비스를 사용하는 통신을 위해 MicrosoftExchange Server 2013에서 사용하는 네트워크 포트에 대해 설명합니다. 사용하려면 먼저 다음 기본 규칙을 살펴보세요.

  - 모든 유형의 토폴로지에서 내부 Exchange 서버 간, 내부 Exchange 서버 맟 내부 Lync 또는 비즈니스용 Skype 서버 간, 내부 Exchange 서버 및 내부 Active Directory 도메인 컨트롤러 간의 네트워크 트래픽의 제한 및 변경이 지원되지 않습니다. 잠재적으로 제한하거나 이러한 종류의 네트워크 트래픽을 변경할 수 있는 방화벽이나 네트워크 장치가 있는 경우 이러한 서버 간의 통신을 무료 및 무제한 허용하는 규칙을 구성해야 합니다(임의의 RPC 포트를 비롯한 모든 포트에서 들어오고 나가는 네트워크 트래픽 및 네트워크에 대해 변경하지 않는 모든 프로토콜을 허용하는 규칙).

  - Edge 전송 서버는 거의 항상 주변 네트워크에 있으므로 Edge 전송 서버와 인터넷 간의 네트워크 트래픽 및 Edge 전송 서버 및 내부 Exchange 조직 간의 네트워크 트래픽을 제한할 수 있습니다. 이러한 네트워크 포트가 이 항목에 설명되어 있습니다.

  - 외부 클라이언트 및 서비스와 내부 Exchange 조직 간의 네트워크 트래픽을 제한하려고 합니다. 내부 클라이언트와 내부 Exchange 서버 간의 네트워크 트래픽을 제한하려는 경우도 괜찮습니다. 이러한 네트워크 포트가 이 항목에 설명되어 있습니다.

**콘텐츠**

클라이언트와 서비스에 필요한 네트워크 포트

Edge 전송 서버가 없는 메일 흐름에 필요한 네트워크 포트

Edge 전송 서버를 사용하는 메일 흐름에 필요한 네트워크 포트

하이브리드 배포에 필요한 네트워크 포트

통합 메시징에 필요한 네트워크 포트

## 클라이언트와 서비스에 필요한 네트워크 포트

Exchange 조직의 다른 서비스 및 사서함에 액세스하기 위해 전자 메일 클라이언트에 필요한 네트워크 포트는 메뉴에서 다음 다이어그램과 표에 설명되어 있습니다.

**참고:**

  - 이러한 클라이언트와 서비스에 대한 대상은 클라이언트 액세스 서버입니다. 독립 실행형 클라이언트 액세스 서버 또는 클라이언트 액세스 서버와 동일한 컴퓨터에 설치 된 사서함 서버일 수 있습니다.

  - 다이어그램에 인터넷의 클라이언트 및 서비스가 보이더라도 내부 클라이언트의 개념은 같습니다(예: 리소스 포리스트의 Exchange 서버에 액세스하는 계정 포리스트의 클라이언트). 마찬가지로, 원본은 Exchange 조직 외부에 있는 모든 위치일 수 있으므로 테이블에는 원본 열이 없습니다(예: 인터넷 또는 계정 포리스트).

  - Edge 전송 서버는 이러한 클라이언트 및 서비스와 관련된 네트워크 트래픽의 개입이 없습니다.

![클라이언트와 서비스에 필요한 네트워크 포트](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png "클라이언트와 서비스에 필요한 네트워크 포트")


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>용도</th>
<th>포트</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>암호화된 웹 연결이 다음 클라이언트와 서비스에서 사용됩니다.</p>
<ul>
<li><p>자동 검색 서비스</p></li>
<li><p>Exchange ActiveSync</p></li>
<li><p>EWS(Exchange 웹 서비스)</p></li>
<li><p>오프라인 주소록 배포</p></li>
<li><p>Outlook 외부에서 사용(HTTP를 통한 RPC)</p></li>
<li><p>Outlook HTTP를 통한 MAPI</p></li>
<li><p>Outlook Web App</p></li>
</ul></td>
<td><p>443/TCP(HTTPS)</p></td>
<td><p>이러한 클라이언트 및 서비스에 대한 자세한 내용은 다음 항목을 참조하세요.</p>
<ul>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Autodiscover 서비스</a></p></li>
<li><p><a href="exchange-activesync-exchange-2013-help.md">Exchange ActiveSync</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/?linkid=529544">Exchange에 대한 EWS 참조</a></p></li>
<li><p><a href="offline-address-books-exchange-2013-help.md">오프라인 주소록</a></p></li>
<li><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook Anywhere</a></p></li>
<li><p><a href="mapi-over-http-exchange-2013-help.md">MAPI over HTTP</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Exchange 2013에서 Outlook Web App의 새 기능</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>암호화되지 않은 웹 연결이 다음 클라이언트와 서비스에서 사용됩니다.</p>
<ul>
<li><p>인터넷 일정 게시</p></li>
<li><p>Outlook Web App(443/TCP로 리디렉션)</p></li>
<li><p>자동 검색(443/TCP를 사용할 수 없는 경우 대체)</p></li>
</ul></td>
<td><p>80/TCP(HTTP)</p></td>
<td><p>가능 하다면 443/TCP에서 암호화된 웹 연결을 사용하여 데이터 및 자격 증명을 보호하는 것이 좋습니다. 그러나 일부 서비스가 클라이언트 액세스 서버로의 80/TCP의 암호화 되지 않은 웹 연결을 사용하도록 구성해야 할 수 있습니다.</p>
<p>이러한 클라이언트 및 서비스에 대한 자세한 내용은 다음 항목을 참조하세요.</p>
<ul>
<li><p><a href="enable-internet-calendar-publishing-exchange-2013-help.md">인터넷 일정 게시를 사용 하도록 설정</a></p></li>
<li><p><a href="what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md">Exchange 2013에서 Outlook Web App의 새 기능</a></p></li>
<li><p><a href="autodiscover-service-for-exchange-2013.md">Autodiscover 서비스</a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>IMAP4 클라이언트</p></td>
<td><p>143/TCP(IMAP), 993/TCP(보안 IMAP)</p></td>
<td><p>IMAP4는 기본적으로 사용할 수 없도록 설정되어 있습니다. 자세한 내용은 <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">Exchange Server 2013의 POP3 및 IMAP4</a>를 참조하세요.</p>
<p>사서함 서버의 IMAP4 백 엔드 서비스에 대한 클라이언트 액세스 서버 프록시 연결의 IMAP4 서비스입니다.</p></td>
</tr>
<tr class="even">
<td><p>POP3 클라이언트</p></td>
<td><p>110/TCP(POP3), 995/TCP(보안 POP3)</p></td>
<td><p>POP3는 기본적으로 사용할 수 없도록 설정되어 있습니다. 자세한 내용은 <a href="pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md">Exchange Server 2013의 POP3 및 IMAP4</a>를 참조하세요.</p>
<p>사서함 서버의 POP3 백 엔드 서비스에 대한 클라이언트 액세스 서버 프록시 연결의 POP3 서비스입니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMTP 클라이언트(인증됨)</p></td>
<td><p>587/TCP(인증된 SMTP)</p></td>
<td><p>&quot;Client Frontend <em>&lt;Server name&gt;</em>&quot;라는 기본 수신 커넥터가 클라이언트 액세스 서버의 포트 587에서 인증된 SMTP 클라이언트 제출을 수신 대기합니다.</p>
<p><strong>참고:</strong></p>
<p>포트 25에만 인증된 SMTP 메일을 제출할 수 있는 메일 클라이언트가 있는 경우 이 수신 커넥터의 네트워크 어댑터 바인딩 값을 포트 25에서 인증된 SMTP 메일 전송을 수신 대기하도록 수정할 수도 있습니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 돌아가기

## 메일 흐름에 필요한 네트워크 포트

Exchange 토폴로지에 따라 Exchange 조직의 메일을 주고 받는 방법 가장 중요한 요소는 경계 네트워크에 배포된 가입 된 Edge 전송 서버가 있는지 여부입니다.

## Edge 전송 서버가 없는 메일 흐름에 필요한 네트워크 포트

클라이언트 액세스 서버와 사서함 서버만 있는 Exchange 조직의 메일 흐름에 필요한 네트워크 포트가 다음 다이어그램과 테이블에 나와 있습니다. 다이어그렘에 별도 사서함 및 클라이언트 액세스 서버가 있지만 개념은 클라이언트 액세스 서버 및 사서함 서버가 같은 컴퓨터 또는 별도 컴퓨터에 설치 되어 있는지 여부와 상관없이 같습니다.

![Edge 전송 서버가 없는 메일 흐름에 필요한 네트워크 포트](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "Edge 전송 서버가 없는 메일 흐름에 필요한 네트워크 포트")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>용도</th>
<th>포트</th>
<th>원본</th>
<th>Destination</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인바운드 메일</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>모든 인터넷</p></td>
<td><p>클라이언트 액세스 서버</p></td>
<td><p>클라이언트 액세스 서버에서 이름이 &quot;기본 프런트 엔드 <em>&lt;Client Access server name&gt;</em>&quot;인 기본 수신 커넥터가 포트 25에서 익명 인바운드 SMTP 메일을 수신 대기합니다.</p>
<p>같은 조직에 있는 Exchange 서버 간의 메일을 자동으로 라우팅하는 표시되지 않는 암시적 조직 간 송신 커넥터를 사용하여 메일이 클라이언트 액세스 서버에서 사서함 서버로 릴레이됩니다.</p></td>
</tr>
<tr class="even">
<td><p>아웃바운드 메일</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>사서함 서버</p></td>
<td><p>모든 인터넷</p></td>
<td><p>기본적으로 Exchange는 인터넷으로 메일을 보낼 수 있는 모든 송신 커넥터를 만들지 않습니다. 송신 커넥터는 수동으로 만들어야 합니다. 자세한 내용은 를 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p>아웃바운드 메일(클라이언트 액세스 서버를 통해 라우팅하는 경우)</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>클라이언트 액세스 서버</p></td>
<td><p>모든 인터넷</p></td>
<td><p>Exchange 관리 센터에서 또는 Exchange 관리 셸의 <code>-FrontEndProxyEnabled $true</code>에서 <strong>클라이언트 액세스 서버를 통한 프록시</strong>를 사용하여 송신 커넥터를 구성하는 경우 클라이언트 액세스 서버를 통해서만 아웃 바운드 메일을 라우팅합니다.</p>
<p>이 경우 클라이언트 액세스 서버에서 이름이 &quot;아웃바운드 프록시 프런트 엔드 <em>&lt;Client Access server name&gt;</em>&quot;인 기본 수신 커넥터가 사서함 서버에서 아웃바운드 메일을 수신 대기합니다. 자세한 내용은 <a href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기</a>를 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>다음 메일 홉의 이름 확인에 대한 DNS(그림 포함 안 됨)</p></td>
<td><p>53/UDP, 53/TCP(DNS)</p></td>
<td><p>인터넷 연결 Exchange 서버(클라이언트 액세스 서버 또는 사서함 서버)</p></td>
<td><p>DNS 서버</p></td>
<td><p>이름 확인 섹션을 참조하세요.</p></td>
</tr>
</tbody>
</table>


맨 위로 돌아가기

## Edge 전송 서버를 사용하는 메일 흐름에 필요한 네트워크 포트

경계 네트워크에 설치되어 있는 가입된 Edge 전송 서버는 기본적으로 클라이언트 액세스 서버를 통해 SMTP 메일 흐름을 제거합니다. 특히 다음 사항에 유의합니다.

  - Exchange 조직의 아웃바운드 메일은 클라이언트 액세스 서버를 통과하지 않습니다. 메일은 항상 가입된 Active Directory 사이트의 사서함 서버에서 Edge 전송 서버로 전송됩니다(Edge 전송 서버의 Exchange 버전과 관계없음).

  - 인바운드 메일은 독립 실행형 클라이언트 액세스 서버를 통해 전송되지 않습니다. 메일은 Edge 전송 서버에서 가입된 Active Directory 사이트의 사서함 서버로 전송됩니다. 우편 사서함 서버와 클라이언트 액세스 서버가 같은 컴퓨터에 설치된 경우 전송 서비스(사서함 서버 역할)를 전송하기 전에 Exchange 2013 Edge 전송 서버의 메일이 프런트 엔드 전송 서비스(클라이언트 액세스 서버 역할)에 가장 먼저 도착합니다. 사서함 서버와 클라이언트 액세스 서버가 같은 컴퓨터에 설치된 경우에도 Exchange 2007 또는 Exchange 2010 Edge 전송 서버가 항상 메일을 전송 서비스에 전달합니다.

자세한 내용은 [메일 흐름](mail-flow-exchange-2013-help.md)를 참조하세요.

Edge 전송 서버가 있는 Exchange 조직의 메일 흐름에 필요한 네트워크 포트가 다음 다이어그램과 테이블에 나와 있습니다. 다른 설명이 없는 한 개념은 클라이언트 액세스 서버와 사서함 서버가 같은 컴퓨터 또는 별도 컴퓨터에 설치되어 있는지 여부와 상관없이 같습니다.

![Edge 전송 서버를 사용하는 메일 흐름에 필요한 네트워크 포트](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Edge 전송 서버를 사용하는 메일 흐름에 필요한 네트워크 포트")


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>용도</th>
<th>포트</th>
<th>원본</th>
<th>Destination</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>인바운드 메일 - 인터넷에서 Edge 전송 서버로</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>모든 인터넷</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>Edge 전송 서버에서 이름이 &quot;기본 내부 수신 커넥터 <em>&lt;Edge Transport server name&gt;</em>&quot;인 기본 수신 커넥터가 포트 25에서 익명 SMTP 메일을 수신 대기합니다.</p></td>
</tr>
<tr class="even">
<td><p>인바운드 메일-Edge 전송 서버에서 내부 Exchange 조직으로</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>가입된 Active Directory 사이트의 사서함 서버</p></td>
<td><p>이름이 &quot;EdgeSync - <em>&lt;Active Directory site name&gt;</em>로 인바운드&quot;인 기본 송신 커넥터가 가입된 Active Directory 사이트의 모든 사서함 서버로 포트 25의 인바운드 메일을 릴레이합니다. 자세한 내용은 항목에서 &quot;Edge 구독 프로세스 중에만든 전송 커넥터” 섹션 <a href="edge-subscriptions-exchange-2013-help.md">Edge 구독</a>을 참조하세요.</p>
<p>실제로 메일을 수신하는 서비스는 같은 컴퓨터 또는 별도 컴퓨터에 사서함 서버와 클라이언트 액세스 서버가 설치되어 있는지 여부에 따라 다릅니다.</p>
<ul>
<li><p><strong>독립 실행형 사서함 서버</strong>   이름이 &quot;기본 <em>&lt;Mailbox server name&gt;</em>&quot; 인 기본 수신 커넥터가 Edge 전송 서버의 메일을 비롯한 인바운드 메일을 포트 25에서 수신 대기합니다.</p></li>
<li><p><strong>사서함 서버와 동일한 컴퓨터에 설치된 클라이언트 액세스 서버</strong>   프런트 엔드 전송 서비스(클라이언트 액세스 서버 역할)에서 이름이 &quot;기본 프런트 엔드 <em>&lt;Server name&gt;</em>&quot;인 기본 수신 커넥터가 포트 25에서 Exchange 2013 Edge 전송 서버의 메일을 비롯한 인바운드 메일을 수신 대기합니다.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>아웃바운드 메일-내부 Exchange 조직에서 Edge 전송 서버로</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>가입된 Active Directory 사이트의 사서함 서버</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>아웃바운드 메일은 클라이언트 액세스 서버를 항상 우회합니다.</p>
<p>같은 조직에 있는 Exchange 서버 간의 메일을 자동으로 라우팅하는 표시되지 않는 암시적 조직 간 송신 커넥터를 사용하여 메일이 가입된 Active Directory 사이트의 모든 사서함 서버에서 Edge 전송 서버로 릴레이됩니다.</p>
<p>Edge 전송 서버에서 이름이 &quot;기본 내부 수신 커넥터 <em>&lt;Edge Transport server name&gt;</em>&quot;인 기본 수신 커넥터가 가입된 Active Directory 사이트의 모든 사서함 서버의 포트 25에서 SMTP 메일을 수신 대기합니다.</p></td>
</tr>
<tr class="even">
<td><p>아웃바운드 메일 - Edge 전송 서버에서 인터넷으로</p></td>
<td><p>25/TCP(SMTP)</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>모든 인터넷</p></td>
<td><p>이름이 &quot;EdgeSync - <em>&lt;Active Directory site name&gt;</em> 인터넷으로&quot;인 기본 전송 커넥터가 Edge 전송 서버의 포트 25에서 인터넷으로 아웃바운드 메일을 릴레이합니다.</p></td>
</tr>
<tr class="odd">
<td><p>EdgeSync 동기화</p></td>
<td><p>50636/TCP(보안 LDAP)</p></td>
<td><p>EdgeSync 동기화에 참여하는 가입된 Active Directory 사이트의 사서함 서버</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>Active Directory 사이트에 대한 Edge 전송 서버를 구독할 때 사이트에 있는 모든 사서함 서버가 EdgeSync 동기화에 참여합니다. 그러나 나중에 추가하는 모든 사서함 서버는 EdgeSync 동기화에 자동으로 참여되지 않습니다.</p></td>
</tr>
<tr class="even">
<td><p>다음 메일 홉의 이름 확인에 대한 DNS(그림 포함 안 됨)</p></td>
<td><p>53/UDP, 53/TCP(DNS)</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>DNS 서버</p></td>
<td><p>이름 확인 섹션을 참조하세요.</p></td>
</tr>
<tr class="odd">
<td><p>다음 메일 홉의 이름 확인에 대한 DNS(그림 포함 안 됨)</p></td>
<td><p>사용자 정의됨</p></td>
<td><p>Edge 전송 서버</p></td>
<td><p>인터넷</p></td>
<td><p>보낸 사람 신뢰도(프로토콜 분석 에이전트)가 스팸 메일을 줄이기 위해 인바운드 메시지 경로를 분석합니다. 조직에서 인터넷에 대한 액세스 제어 프록시 서버를 사용하는 경우 보낸 사람 신뢰도를 제대로 사용할 수 있도록(특히, 개방형 프록시 검색 및 보낸 사람 차단) 프록시 서버에 대한 세부 정보를 정의해야 합니다. 보낸 사람 신뢰도를 정상적으로 인터넷에 연결할 수 있도록 <strong>Set-SenderReputationConfig</strong> cmdlet의 <em>ProxyServerName</em>, <em>ProxyServerPort</em> 및 <em>ProxyServerType</em> 매개 변수를 사용하여 조직의 프록시 서버를 정의할 수 있습니다. 자세한 내용은 <a href="manage-sender-reputation-exchange-2013-help.md">보낸사람 신뢰도 관리 합니다.</a>를 참조하세요.</p></td>
</tr>
</tbody>
</table>


맨 위로 돌아가기

## 이름 확인

다음 메일 홉의 DNS 확인은 모든 Exchange 조직 내 메일 흐름의 기본적인 부분입니다. 인바운드 메일 수신 또는 아웃바운드 메일 배달을 담당하는 Exchange 서버는 올바른 메일 라우팅에 대한 내부 및 외부 호스트 이름을 모두 확인할 수 있어야 합니다. 모든 내부 Exchange 서버는 올바른 메일 라우팅에 대한 내부 호스트 이름을 확인할 수 있어야 합니다. DNS 인프라를 디자인하는 다양한 방법이 있지만 모든 Exchange 서버에 대해 제대로 작동 중인 다음 홉에 대한 이름 확인을 수행해야 합니다.

## 하이브리드 배포에 필요한 네트워크 포트.

Exchange 2013 및 MicrosoftOffice 365 모두 사용하는 조직에 필요한 네트워크 포트는 [하이브리드 배포 필수 구성 요소](https://technet.microsoft.com/ko-kr/library/hh534377\(v=exchg.150\))의 "하이브리드 배포 프로토콜, 포트 및 끝점" 섹션에서 다룹니다.

## 통합 메시징에 필요한 네트워크 포트

통합 메시징에 필요한 네트워크 포트는 다음 항목에서 다룹니다.

  - [UM 프로토콜, 포트 및 서비스](um-protocols-ports-and-services-exchange-2013-help.md)

  - [Exchange Server 2013 SP1 아키텍처 포스터](https://go.microsoft.com/fwlink/p/?linkid=518646)

맨 위로 돌아가기

