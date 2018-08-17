---
title: 'EdgeSync 복제 데이터: Exchange 2013 Help'
TOCTitle: EdgeSync 복제 데이터
ms:assetid: c7dd137d-7ed4-4f16-9895-f354c449cf9b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232177(v=EXCHG.150)
ms:contentKeyID: 61183428
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# EdgeSync 복제 데이터

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_

Edge 전송 서버를 배포할 때 해당 서버에는 Active Directory 액세스 권한이 없습니다. 받는 사람 조회 및 수신 허용 목록 집계 작업을 수행하고 MTLS(상호 전송 계층 보안) 인증을 사용하여 도메인 보안을 구현하려면 Edge 전송 서버에는 Active Directory의 데이터가 필요합니다. 이 데이터는 EdgeSync를 사용하여 Edge 전송 서버로 복제됩니다. Edge 전송 서버는 복제된 모든 정보를 AD LDS(Active Directory Lightweight Directory Services)에 저장합니다.

이 항목에서는 Active Directory에서 Active Directory 사이트에 구독된 Edge 전송 서버의 AD LDS로 복제되는 데이터에 대해 중점적으로 설명합니다. EdgeSync 및 Edge 구독에 대해 자세히 알아보려면 [Edge 구독](edge-subscriptions-exchange-2013-help.md)을 참조하세요.

AD LDS로 복제되며 Edge 전송 서버에서 사용하는 데이터에는 다음 네 가지 형식이 있습니다.

Edge Subscription information

Configuration information

Recipient information

Topology information

## Edge 구독 정보

Exchange 2013은 Active Directory 및 AD LDS 스키마를 확장하여 EdgeSync 동기화를 제어하는 데 필요한 데이터를 표시하는 특성을 **ms-Exch-ExchangeServer** 개체에 제공합니다. 이러한 특성은 EdgeSync에 다음 세 가지 기능을 제공합니다.

  - 사서함 서버와 구독된 Edge 전송 서버 간의 LDAP 연결을 보호하는 데 사용되는 자격 증명의 자동 프로비전 및 유지 관리

  - 한 번에 하나의 서버만 개별 Edge 전송 서버에 대해 동기화를 시도할 수 있도록 동기화 잠금 및 임대 프로세스 중재 잠금 및 임대 프로세스에 대한 자세한 내용은 [Edge 구독](edge-subscriptions-exchange-2013-help.md)를 참조하세요.

  - 현재 동기화 상태 레코드를 유지 관리하기 위해 EdgeSync 동기화 최적화 동기화 상태를 쉽게 확인할 수 있으면 수동 동기화를 과도하게 수행하지 않아도 됩니다.

아래 표에는 Edge 구독과 관련된 스키마 확장이 나와 있습니다. 이러한 특성에 할당되는 값은 Edge 구독 및 EdgeSync에서 유지 관리하므로 수동으로 편집할 필요는 없습니다.

### Edge 구독 스키마 확장

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>특성 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ms-Exch-Server-EKPK-Public-Key</strong></p></td>
<td><p>서버에서 사용 중인 인증서의 현재 공개 키를 나타냅니다. 이 값은 Edge 전송 서버와 사서함 서버에 모두 저장됩니다. 공개 키는 LDAP 및 SMTP 통신 중에 서버를 인증하는 데 사용되는 자격 증명을 암호화하는 데 사용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-EdgeSync-Credential</strong></p></td>
<td><p>EdgeSync에서 AD LDS와의 인증된 LDAP 세션을 설정하는 데 사용하는 자격 증명 목록입니다. 사서함 서버의 경우 이 특성에는 사서함 서버가 구독된 Edge 전송 서버를 인증하는 데 사용하는 자격 증명만이 포함됩니다. 반면 Edge 전송 서버의 경우 이 특성에는 EdgeSync 동기화에 참가하는 구독된 Active Directory 사이트에 있는 각 사서함 서버의 자격 증명이 포함됩니다. 이 특성은 EdgeSync 동기화를 실행하는 사서함 서버와 구독된 Edge 전송 서버에만 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ms-Exch-Edge-Sync-Lease</strong></p></td>
<td><p>여러 사서함 서버에서 같은 Edge 전송 서버를 복제하려고 할 때 사서함 서버 간의 작업을 중재합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>ms-Exch-Edge-Sync-Status</strong></p></td>
<td><p>Edge 전송 서버 개체의 AD LDS에만 있습니다. 이 특성은 AD LDS 인스턴스에 대한 복제 상태를 추적하며 복제에 대한 정보를 포함합니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 구성 정보

조직에 Edge 전송 서버를 구독하려는 경우 조직 내부의 Exchange 조직과 Edge 전송 서버에 공통적으로 적용되는 구성 개체를 관리할 수 있습니다. 그러면 변경 내용이 EdgeSync를 사용하여 Edge 전송 서버에 복제됩니다. 이 프로세스를 수행하면 메시지 처리에 관련된 모든 서버에서 구성을 일관성 있게 유지 관리할 수 있습니다.

Exchange 조직의 구성 데이터 하위 집합도 Edge 전송 서버에서 유지 관리해야 합니다. EdgeSync 동기화 중에 Edge 전송 서버에서 필요로 하는 구성 데이터는 AD LDS의 구성 파티션에 기록됩니다. AD LDS에 기록되는 구성 데이터는 다음과 같습니다.

  - **사서함 서버**   구독된 Active Directory 사이트에 있는 각 사서함 서버의 FQDN(정규화된 도메인 이름)을 Edge 전송 서버의 로컬 AD LDS 저장소에서 사용할 수 있습니다. 이 정보는 인바운드 송신 커넥터의 스마트 호스트 서버 목록을 파생시키는 데 사용됩니다.

  - **허용 도메인**   Exchange 조직에 대해 구성된 모든 신뢰할 수 있는 도메인, 내부 릴레이 도메인 및 외부 릴레이 도메인이 AD LDS에 기록됩니다. Edge 전송 서버가 허용 도메인을 사용할 수 있도록 하면 Exchange에서 도메인 필터링을 수행하고 조직 내로 유입되는 잘못된 SMTP 트래픽을 최대한 빨리 거부할 수 있습니다. 허용 도메인에 대한 자세한 내용은 [허용 도메인](accepted-domains-exchange-2013-help.md)를 참조하세요.

  - **메시지 분류**   Edge 전송 서버에서 메시지 분류를 사용할 수 있는 경우 경계 네트워크에서 메시지 분류 작업을 수행할 때 전송 에이전트와 콘텐츠 변환을 사용할 수 있습니다. 예를 들어 첨부 파일 필터 에이전트에서 첨부 파일을 제거할 때 첨부 파일에 제거됨 분류를 적용하여 Microsoft Outlook 사용자 또는 Outlook Web App 사용자에게 정보 텍스트를 보내 받는 사람에게 수행된 작업을 알릴 수 있습니다. 타사 응용 프로그램에서 사용하도록 개발된 에이전트에서도 유사한 방식으로 메시지 분류를 사용할 수 있습니다.

  - **원격 도메인**   Exchange 조직용으로 구성된 모든 원격 도메인 항목이 AD LDS에 기록됩니다. 원격 도메인 항목은 부재 중 메시지 설정과 원격 도메인의 메시지 형식 설정을 제어합니다. 원격 도메인에 대한 자세한 내용은 [원격 도메인](remote-domains-exchange-2013-help.md)을 참조하세요.

  - **송신 커넥터**   기본적으로 Edge 구독을 만들면 Edge 전송 서버 구독 시 Exchange 조직과 인터넷 간의 종단 간 메일 흐름을 사용하도록 설정하는 데 필요한 송신 커넥터가 자동으로 만들어집니다. 그러면 Edge 전송 서버에 있는 기존 송신 커넥터는 모두 삭제됩니다. 송신 커넥터를 추가로 구성하려는 경우 Exchange 조직 내에 송신 커넥터를 구성하고 Edge 구독을 해당 커넥터의 원본 서버로 선택합니다. 자세한 내용은 [Edge 구독](edge-subscriptions-exchange-2013-help.md)을 참조하세요.

  - **내부 SMTP 서버**   *InternalSMTPServers* 특성의 값은 Exchange 조직과 로컬 Edge 전송 서버에 대해 모두 **TransportConfig** 개체에 저장됩니다. EdgeSync 동기화 중에 Exchange 조직에 대해 이 개체에 저장되는 값이 로컬 Edge 전송 서버 개체에 저장되는 값을 덮어씁니다. 이 특성은 보낸 사람 ID 및 연결 필터링에서 무시할 내부 SMTP 서버 IP 주소 또는 IP 주소 범위의 목록을 지정합니다.

  - **도메인 보안 목록**   *TLSReceiveDomainSecureList* 및 *TLSSendDomainSecureList* 특성은 Exchange 조직과 로컬 Edge 전송 서버에 대해 모두 **TransportConfig** 개체에 저장됩니다. EdgeSync 동기화 중에 Exchange 조직에 대해 이 개체에 저장되는 값이 로컬 Edge 전송 서버 개체에 저장되는 값을 덮어씁니다. 이러한 특성은 상호 TLS 인증용으로 구성되는 원격 도메인 목록을 지정합니다.

맨 위로 이동

## 받는 사람 정보

AD LDS로 복제되는 받는 사람 정보에는 받는 사람 특성 하위 집합만 포함됩니다. Edge 전송 서버에서 특정 스팸 방지 작업을 수행하는 데 필요한 데이터만 복제됩니다. AD LDS로 복제되는 받는 사람 정보에는 다음이 포함됩니다.

  - **받는 사람**   Exchange 조직의 받는 사람 목록이 AD LDS로 복제됩니다. 각 받는 사람은 할당받은 Active Directory GUID로 식별됩니다. 조직 외부에서 들어오는 메일 수신을 거부하도록 받는 사람의 계정을 구성하는 경우 해당 받는 사람은 AD LDS로 복제되지 않습니다. 받는 사람의 사서함을 사용하지 않도록 설정하거나 삭제하면 해당 사서함은 AD LDS로 더 이상 복제되지 않습니다.

  - **프록시 주소**   각 받는 사람에게 할당되는 모든 프록시 주소가 해시된 데이터로 AD LDS에 복제됩니다. 이 해시는 SHA(보안 해시 알고리즘) 256을 사용하는 단방향 해시입니다. SHA-256은 원본 데이터에 대해 256비트의 메시지 다이제스트를 생성합니다. 프록시 주소를 해시된 데이터로 저장하면 Edge 전송 서버 또는 AD LDS가 손상된 경우 이 정보를 보호할 수 있습니다. Edge 전송 서버는 받는 사람 조회 스팸 방지 작업을 수행할 때 프록시 주소를 참조합니다.

  - **수신 허용 - 보낸 사람 목록, 수신 거부 목록 및 수신 허용 - 받는 사람 목록**   각 받는 사람의 Outlook 인스턴스에 정의되어 있는 수신 허용 - 보낸 사람 목록, 수신 거부 목록 및 수신 허용 - 받는 사람 목록이 집계되어 AD LDS로 복제됩니다. 이러한 설정은 받는 사람의 사서함이 있는 사서함 데이터베이스에 저장됩니다. Outlook 사용자의 수신 허용 목록 모음에는 사용자의 수신 허용 - 보낸 사람 목록, 수신 허용 - 받는 사람 목록, 수신 거부 목록 및 외부 연락처의 데이터가 함께 들어 있습니다. AD LDS에서 수신 허용 목록 모음 데이터를 사용할 수 있도록 하면 Edge 전송 서버가 보낸 사람을 적절하게 차단할 수 있으므로 메일 필터링과 관련된 작업 오버헤드를 줄일 수 있습니다. 이 정보는 해시된 데이터로 발송됩니다.
    

    > [!IMPORTANT]
    > 수신 허용 - 받는 사람 데이터가 Outlook에 저장되고 Edge 전송 서버에서 AD LDS 인스턴스의 수신 허용 목록 컬렉션으로 집계될 수 있지만 콘텐츠 필터링 기능은 수신 허용 - 받는 사람 데이터에서 작동하지 않습니다.



  - **받는 사람당 스팸 방지 설정**   **Set-Mailbox** cmdlet을 사용하면 조직 전체의 스팸 방지 설정과는 다른 스팸 방지 임계값 설정을 각 받는 사람에 대해 할당할 수 있습니다. 받는 사람당 스팸 방지 설정을 구성하면 해당 설정이 조직 전체의 설정을 무시합니다. 이러한 설정을 AD LDS로 복제하면 Exchange 조직으로 메시지를 릴레이하기 전에 받는 사람당 설정을 고려해 볼 수 있습니다. 이 정보는 해시된 데이터로 발송됩니다.

맨 위로 이동

## 토폴로지 정보

토폴로지 정보에는 새로 가입된 Edge 전송 서버 또는 제거된 Edge 구독의 알림이 포함됩니다. 5분마다 이 정보를 새로 고칩니다.

맨 위로 이동

