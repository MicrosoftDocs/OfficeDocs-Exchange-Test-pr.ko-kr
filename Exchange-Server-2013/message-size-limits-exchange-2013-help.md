---
title: '메시지 크기 제한: Exchange 2013 Help'
TOCTitle: 메시지 크기 제한
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 50483982
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 메시지 크기 제한

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-08-20_

Microsoft Exchange Server 2013 조직을 통해 이동하는 메시지에 크기 제한을 적용할 수 있습니다. 메시지의 전체 크기나 메시지 헤더, 메시지 첨부 파일, 받는 사람 수 등 개별 메시지 구성 요소의 크기를 제한할 수 있습니다. 제한은 전체 Exchange 조직에 대해 전체적으로 적용할 수도 있고 특정 커넥터 또는 사용자 개체에 대해서만 적용할 수도 있습니다.

Exchange 조직에 대한 메시지 크기 제한을 계획할 때는 다음 질문을 고려하세요.

  - 모든 받는 메시지에 대해 적용해야 하는 크기 제한은?

  - 모든 보내는 메시지에 대해 적용해야 하는 크기 제한은?

  - Exchange 조직의 사서함 할당량은?

  - 선택한 메시지 크기 제한이 사서함 할당량 크기와 어떤 관계가 있는지?

  - Exchange 조직에 지정된 허용 크기보다 큰 메시지를 보내거나 받아야 하는 사용자가 있는지?

  - Exchange 네트워크 토폴로지에 메시지 크기 제한이 다른 기타 메시징 시스템 또는 확연히 구별되는 사업부가 있는지?

이 항목에서는 이러한 질문에 답할 수 있도록 지침을 제공합니다.

**콘텐츠**

메시지 크기 제한 유형

제한 범위

메시지 크기 제한의 우선 순위 순서

크기 제한을 받지 않는 메시지

## 메시지 크기 제한 유형

다음은 개별 메시지에 사용할 수 있는 크기 제한의 기본 범주입니다.

  - **메시지 헤더 크기 제한**   이 제한은 메시지에 있는 모든 메시지 헤더 필드의 전체 크기에 적용됩니다. 메시지 본문이나 첨부 파일의 크기는 고려되지 않습니다. 헤더 필드는 일반 텍스트이므로 헤더의 크기는 각 헤더 필드의 문자 수와 헤더 필드의 전체 수에 의해 결정됩니다. 텍스트의 각 문자는 1바이트를 차지합니다.
    

    > [!NOTE]
    > 일부 타사 방화벽 또는 프록시 서버는 고유의 메시지 헤더 크기 제한을 적용합니다. 이러한 타사 방화벽 또는 프록시 서버는 50자보다 길거나 US-ASCII 문자가 아닌 첨부 파일 이름을 포함하는 메시지를 처리하지 못할 수도 있습니다.



  - **메시지 크기 제한**   이러한 제한은 메시지 헤더, 메시지 본문 및 첨부 파일을 포함하는 메시지의 전체 크기에 적용됩니다. 메시지 크기 제한은 받는 메시지 또는 보내는 메시지에 적용할 수 있습니다. 내부 메시지 흐름의 경우 Exchange에서는 사용자 지정 `X-MS-Exchange-Organization-OriginalSize:` 메시지 헤더를 사용하여 Exchange 조직으로 들어가는 메시지의 원본 메시지 크기를 기록합니다. 해당 메시지를 지정된 메시지 크기 제한과 비교하여 검사할 때는 항상 현재 메시지 크기 또는 원본 메시지 크기 헤더 중 더 작은 값이 사용됩니다. 내용 변환, 인코딩, 에이전트 처리 등으로 인해 메시지의 크기는 변경될 수 있습니다.

  - **첨부 파일 크기 제한**   이 제한은 메시지 내의 단일 첨부 파일에 대해 허용되는 최대 크기에 적용됩니다. 메시지에는 메시지 전체 크기를 크게 늘리는 많은 첨부 파일이 포함될 수 있습니다. 그러나 첨부 파일 크기 제한은 개별 첨부 파일 크기에만 적용됩니다.

  - **받는 사람 제한**   이 제한은 메시지 받는 사람의 총 수에 적용됩니다. 메시지를 처음 작성할 때 받는 사람은 `To:`, `Cc:` 및 `Bcc:` 헤더 필드에 있습니다. 메시지를 배달하기 위해 전송하면 메시지 받는 사람은 메시지 봉투의 `RCPT TO:` 항목으로 변환됩니다. 메일 그룹은 메시지 전송 과정에서 한 명의 받는 사람으로 계산됩니다.

맨 위로 돌아가기

## 제한 범위

다음은 개별 메시지에 사용할 수 있는 제한 범위의 기본 범주입니다.

  - **조직 제한**   이 제한은 조직에 있는 모든 Exchange 2013 사서함 서버와 Exchange 2010 및 Exchange 2007 허브 전송 서버에 적용됩니다. 경계 네트워크에 Edge 전송 서버를 설치했으면 지정된 제한은 특정 서버에 적용됩니다.

  - **커넥터 제한**    이 제한은 메시지 배달을 위해 지정된 송신 커넥터, 수신 커넥터, 배달 에이전트 커넥터 또는 외부 커넥터를 사용하는 모든 메시지에 적용됩니다. 송신 커넥터는 Edge 전송 서버 및 사서함 서버의 전송 서비스에 정의되고, 수신 커넥터는 사서함 서버의 전송 서비스, 클라이언트 액세스 서버의 프런트 엔드 전송 서비스, Edge 전송 서버에 정의됩니다.

  - **Active Directory 사이트 링크**   사서함 서버의 전송 서비스는 Active Directory 사이트 및 Active Directory IP 사이트 링크에 할당된 비용을 하나의 요소로 사용하여 조직의 사서함 서버 간에 최저 비용 라우팅을 결정합니다. 조직의 Active Directory 사이트 링크에 특정 메시지 크기 제한을 할당할 수 있습니다.

  - **서버 제한**   이 제한은 특정 사서함 서버 또는 Edge 전송 서버에 적용됩니다. 각 사서함 서버 또는 Edge 전송 서버에 대해 지정된 메시지 제한을 개별적으로 설정할 수 있습니다.
    
    Outlook Web App에서 클라이언트 액세스 서버에 대한 최대 HTTP 요청 크기 제한 설정은 Outlook Web App 사용자가 보낼 수 있는 메시지 크기도 제어합니다.

  - **사용자 제한**   이 제한은 사서함, 연락처, 메일 그룹 또는 공용 폴더 같은 특정 사용자 개체에 적용됩니다.

다음 표에는 Exchange 관리 셸 또는 EAC(Exchange 관리 센터)에서 제한을 구성하는 방법에 대한 정보를 포함한 메시지 제한이 나와 있습니다.

### 조직 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>크기 제한</th>
<th>기본값</th>
<th>셸 구성</th>
<th>EAC 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>받는 메시지의 최대 크기</p></td>
<td><p>10MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>매개 변수: <em>MaxReceiveSize</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>수신 커넥터</strong> &gt; <strong>추가 옵션</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="기타 옵션 아이콘" alt="기타 옵션 아이콘" /> &gt; <strong>조직 전송 설정</strong> &gt; <strong>제한</strong> 탭 &gt; <strong>최대 수신 메시지 크기</strong></p></td>
</tr>
<tr class="even">
<td><p>보내는 메시지의 최대 크기</p></td>
<td><p>10MB</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>매개 변수: <em>MaxSendSize</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>수신 커넥터</strong> &gt; <strong>추가 옵션</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="기타 옵션 아이콘" alt="기타 옵션 아이콘" /> &gt; <strong>조직 전송 설정</strong> &gt; <strong>제한</strong> 탭 &gt; <strong>최대 보내는 메시지 크기</strong></p></td>
</tr>
<tr class="odd">
<td><p>메시지당 최대 받는 사람 수</p>

> [!Tip]  
> <p></p>

</td>
<td><p>5000</p></td>
<td><p>Cmdlet: <strong>Set-TransportConfig</strong></p>
<p>매개 변수: <em>MaxRecipientEnvelopeLimit</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>수신 커넥터</strong> &gt; <strong>추가 옵션</strong><img src="images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif" title="기타 옵션 아이콘" alt="기타 옵션 아이콘" /> &gt; <strong>조직 전송 설정</strong> &gt; <strong>제한</strong> 탭 &gt; <strong>최대 받는 사람 수</strong></p></td>
</tr>
<tr class="even">
<td><p>조직의 모든 사서함 서버에 적용되는 전송 규칙의 최대 첨부 파일 크기</p></td>
<td><p>구성되지 않음</p></td>
<td><p>Cmdlet: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>매개 변수: <em>AttachmentSizeOver</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>규칙</strong> &gt; <strong>추가</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="아이콘 추가" alt="아이콘 추가" /> 또는 <strong>편집</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /></p>
<p><strong>다음 경우에 이 규칙 적용</strong> &gt; <strong>모든 첨부 파일</strong> &gt; <strong>다음보다 크거나 같음</strong> 조건자를 사용합니다.</p>
<p><strong>다음 경우에 이 규칙 적용</strong> &gt; <strong>메시지</strong> &gt; <strong>크기가 다음보다 크거나 같음</strong> 조건자를 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p>조직의 모든 사서함 서버에 적용되는 전송 규칙의 최대 메시지 크기</p></td>
<td><p></p></td>
<td><p>Cmdlet: <strong>New-TransportRule</strong>, <strong>Set-TransportRule</strong></p>
<p>매개 변수: <em>MessageSizeOver</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>규칙</strong> &gt; <strong>추가</strong><img src="images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif" title="아이콘 추가" alt="아이콘 추가" /> 또는 <strong>편집</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /></p>
<p><strong>다음 경우에 이 규칙 적용</strong> &gt; <strong>메시지</strong> &gt; <strong>크기가 다음보다 크거나 같음</strong> 조건자를 사용합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 돌아가기

### 커넥터 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>크기 제한</th>
<th>기본값</th>
<th>셸 구성</th>
<th>EAC 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>수신 커넥터를 통한 최대 헤더 크기</p></td>
<td><p>128KB</p></td>
<td><p>Cmdlet: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>매개 변수: <em>MaxHeaderSize</em></p></td>
<td><p>해당 없음</p>
<p></p></td>
</tr>
<tr class="even">
<td><p>수신 커넥터를 통한 최대 메시지 크기</p>

> [!NOTE]
> 메시지 인코딩 및 내용 변환으로 인해 실제 메시지 크기는 더 작을 수 있습니다.


</td>
<td><p><strong>사서함 서버의 전송 서비스</strong></p>
<p>기본 및 클라이언트 프록시 수신 커넥터의 경우 35MB</p>
<p><strong>클라이언트 액세스 서버의 프런트 엔드 전송 서비스</strong></p>
<p>기본 프런트 엔드 및 아웃바운드 프록시 프런트 엔드 수신 커넥터의 경우 36MB</p>
<p>클라이언트 프런트 엔드 수신 커넥터의 경우 35MB</p></td>
<td><p>Cmdlet: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>매개 변수: <em>MaxMessageSize</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>수신 커넥터</strong> &gt; <strong>편집</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /> &gt; <strong>일반</strong> 탭 &gt; <strong>최대 수신 메시지 크기</strong></p></td>
</tr>
<tr class="odd">
<td><p>수신 커넥터를 통한 메시지당 최대 받는 사람 수</p></td>
<td><p><strong>사서함 서버의 전송 서비스</strong></p>
<p>기본 수신 커넥터의 경우 5,000</p>
<p>클라이언트 프록시 수신 커넥터의 경우 200</p>
<p><strong>클라이언트 액세스 서버의 프런트 엔드 전송 서비스</strong></p>
<p>기본 프런트 엔드, 클라이언트 프런트 엔드, 클라이언트 프록시 프런트 엔드 수신 커넥터의 경우 200</p>

> [!NOTE]
> 익명 보낸 사람에 대해 받는 사람 수가 초과되면 해당 메시지는 처음 200명의 받는 사람에 대해 수락됩니다. 대부분의 SMTP 메시징 서버에서는 받는 사람 제한이 적용됩니다. SMTP 메시징 서버는 메시지가 모든 받는 사람에게 배달될 때까지 200명의 받는 사람 그룹으로 메시지를 계속해서 다시 보냅니다.


</td>
<td><p>Cmdlet: <strong>New-ReceiveConnector</strong>, <strong>Set-ReceiveConnector</strong></p>
<p>매개 변수: <em>MaxRecipientsPerMessage</em></p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>송신 커넥터를 통한 최대 메시지 크기</p></td>
<td><p>10MB</p></td>
<td><p>Cmdlet: <strong>New-SendConnector</strong>, <strong>Set-SendConnector</strong></p>
<p>매개 변수: <em>MaxMessageSize</em></p></td>
<td><p><strong>메일 흐름</strong> &gt; <strong>송신 커넥터</strong> &gt; <strong>편집</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /> &gt; <strong>일반</strong> 탭 &gt; <strong>최대 보내는 메시지 크기</strong></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Active Directory 사이트 링크를 통한 최대 메시지 크기</p></td>
<td><p>제한 없음</p></td>
<td><p>Cmdlet: <strong>Set-AdSiteLink</strong></p>
<p>매개 변수: <em>MaxMessageSize</em></p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>배달 에이전트 커넥터를 통한 최대 메시지 크기</p></td>
<td><p>제한 없음</p></td>
<td><p>Cmdlet: <strong>New-DeliveryAgentConnector</strong>, <strong>Set-DeliveryAgentConnector</strong></p>
<p>매개 변수: <em>MaxMessageSize</em></p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>외부 커넥터를 통한 최대 메시지 크기</p></td>
<td><p>제한 없음</p></td>
<td><p><strong>Cmdlet: Set-ForeignConnector</strong> 매개 변수: <em>MaxMessageSize</em></p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


맨 위로 돌아가기

### 서버 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>크기 제한</th>
<th>기본값</th>
<th>셸 구성</th>
<th>EAC 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Pickup 디렉터리의 메시지에 대한 최대 헤더 크기</p></td>
<td><p>64KB</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>매개 변수: <em>PickupDirectoryMaxHeaderSize</em></p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="even">
<td><p>Pickup 디렉터리의 메시지에 대한 메시지당 최대 받는 사람 수</p></td>
<td><p>100</p></td>
<td><p>Cmdlet: <strong>Set-TransportService</strong></p>
<p>매개 변수: <em>PickupDirectoryMaxRecipientsPerMessage</em></p></td>
<td><p>해당 없음</p></td>
</tr>
<tr class="odd">
<td><p>클라이언트별 최대 메시지 크기 제한에 대한 Outlook Web App, Exchange ActiveSync 및 Exchange 웹 서비스 클라이언트</p></td>
<td><p>Outlook Web App   35MB</p>
<p>Exchange ActiveSync   10MB</p>
<p>Exchange 웹 서비스   64MB</p>

> [!NOTE]
> 이러한 값은 Base64 인코딩과 관련된 오버헤드로 인해 실제 사용 가능한 최대 메시지 크기보다 약 33% 더 큽니다.


</td>
<td><p>클라이언트 액세스 서버의 해당 web.config XML 응용 프로그램 구성 파일에서 이러한 값을 구성합니다. 자세한 내용은 <a href="configure-client-specific-message-size-limits-exchange-2013-help.md">클라이언트별 메시지 크기 제한 구성</a>를 참조하세요.</p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


맨 위로 돌아가기

### 사용자 제한

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>크기 제한</th>
<th>기본값</th>
<th>셸 구성</th>
<th>EAC 구성</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>이 받는 사람이 보낼 수 있는 최대 메시지 크기</p></td>
<td><p>제한 없음</p></td>
<td><p>Cmdlet:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-RemoteMailbox</strong></p>
<p>매개 변수: <em>MaxSendSize</em></p></td>
<td><p>사서함의 경우:</p>
<p><strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>편집</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /> &gt; <strong>사서함 기능</strong> &gt; <strong>메일 흐름</strong> &gt; <strong>메시지 크기 제한</strong> &gt; <strong>자세한 내용을 보려면</strong> &gt; <strong>보낸 메시지</strong></p>

> [!NOTE]
> 다른 받는 사람 유형에 대해서는 EAC를 사용하여 이 설정을 구성할 수 없습니다.


</td>
</tr>
<tr class="even">
<td><p>이 받는 사람에게 보낼 수 있는 최대 메시지 크기</p></td>
<td><p>제한 없음</p>
<p>사이트 사서함 프로비전 정책의 경우 36MB</p></td>
<td><p>Cmdlet:</p>
<p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>New-SiteMailboxProvisioningPolicy</strong></p>
<p><strong>Set-SiteMailboxProvisioningPolicy</strong></p>
<p>매개 변수: <em>MaxReceiveSize</em></p></td>
<td><p>사서함의 경우:</p>
<p><strong>받는 사람</strong> &gt; <strong>사서함</strong> &gt; <strong>편집</strong><img src="images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif" title="편집 아이콘" alt="편집 아이콘" /> &gt; <strong>사서함 기능</strong> &gt; <strong>메일 흐름</strong> &gt; <strong>메시지 크기 제한</strong> &gt; <strong>자세한 내용</strong> &gt; <strong>받은 메시지</strong></p>

> [!NOTE]
> 다른 받는 사람 유형에 대해서는 EAC를 사용하여 이 설정을 구성할 수 없습니다.


</td>
</tr>
<tr class="odd">
<td><p>이 받는 사람이 보내는 메시지당 최대 받는 사람 수</p></td>
<td><p>제한 없음</p></td>
<td><p>Cmdlet:</p>
<p><strong>Set-Mailbox</strong>, <strong>Set-MailUser</strong></p>
<p>매개 변수: <em>RecipientLimits</em></p>
<p></p></td>
<td><p>해당 없음</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 메시지 크기 제한의 우선 순위 순서

Exchange 조직에서 각 수준에 대해 다른 메시지 크기 제한을 설정할 수 있습니다. 메시지가 전송 인프라를 통해 라우팅될 때 여러 메시지 크기 제한이 적용될 수 있습니다. 전송 파이프라인의 메시지가 메시지 크기 제한을 위반하는 경우 최대한 빨리 거부되도록 메시지 크기 제한을 계획해야 합니다. 일반적으로 메시지가 인프라에 들어오는 지점에 가장 제한적인 제한을 설정해야 합니다. 예를 들어, 인터넷에서 메시지를 받는 수신 커넥터의 메시지 크기 제한은 내부 Exchange 조직에 대해 구성하는 메시지 크기 제한보다 작거나 같아야 합니다. Exchange 서버가 사서함 서버의 전송 서비스에서 거부될 인터넷 메시지를 수락하고 처리한다면 시스템 리소스만 낭비하게 됩니다. 조직, 서버 및 커넥터 제한이 불필요한 메시지 처리를 최소화하도록 구성되었는지 확인합니다.

이 접근 방법에서 한 가지 예외는 사용자 제한입니다. 사용자 수준 제한은 다른 메시지 크기 제한보다 우선합니다. 따라서 조직에 대한 기본 메시지 크기 제한을 초과하도록 사용자를 구성할 수 있습니다. 예를 들면 사서함에 대해 사용자 지정 송신 및 수신 제한을 구성하여 특정 사용자 사서함 그룹이 나머지 조직보다 큰 메시지를 보낼 수 있도록 할 수 있습니다.

사용자 제한의 예외는 인증된 사용자 간의 메시지 교환에만 적용됩니다. 인터넷에서 받는 사람에게 메시지를 보내거나 받는 사람이 메시지를 받으면 조직 제한이 적용됩니다. 예를 들어 조직의 메시지 크기 제한은 10MB이지만 마케팅 부서의 사용자는 최대 50MB의 메시지를 보내고 받도록 구성했다고 가정합니다. 이러한 사용자는 서로 대용량 메시지를 교환할 수 있지만 인터넷 사용자의 메시지는 인증되지 않은 보낸 사람에게서 오는 메시지이기 때문에 인터넷 사용자로부터는 대용량 메시지를 받을 수 없습니다.

맨 위로 돌아가기

## 크기 제한을 받지 않는 메시지

다음 목록에는 사서함 서버 또는 Edge 전송 서버에서 생성되며 모든 메시지 크기 제한을 받지 않는 메시지 유형이 나와 있습니다.

  - 시스템 메시지

  - 에이전트 생성 메시지

  - DSN(배달 상태 알림) 메시지

  - 저널 보고서 메시지

  - 격리된 메시지

하지만 메시지의 최대 받는 사람 수에 대한 조직 값은 이러한 메시지에 계속 적용됩니다.

맨 위로 돌아가기

