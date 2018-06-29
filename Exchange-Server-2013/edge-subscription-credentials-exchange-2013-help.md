---
title: 'Edge 구독 자격 증명: Exchange 2013 Help'
TOCTitle: Edge 구독 자격 증명
ms:assetid: 1d291bc1-9c00-4d1b-8da0-cb81f63d8305
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266959(v=EXCHG.150)
ms:contentKeyID: 61183418
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 구독 자격 증명

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

이 항목에서는 Edge 구독 프로세스에서 EdgeSync 동기화 프로세스 보안에 사용되는 자격 증명을 프로비전하는 방법과 EdgeSync에서 해당 자격 증명을 사용하여 Exchange 2013 사서함 서버와 Edge 전송 서버 간에 보안 LDAP 연결을 설정하는 방법에 대해 설명합니다. Edge 구독에 대한 자세한 내용은 [Edge 구독](edge-subscriptions-exchange-2013-help.md)를 참조하세요.

**목차**

Edge Subscription process

EdgeSync replication accounts

Authenticate initial replication

Authenticate scheduled synchronization sessions

Renew EdgeSync replication accounts

## Edge 구독 프로세스

Edge 전송 서버는 Active Directory 사이트에 구독되어 Active Directory 사이트의 사서함 서버와 구독된 Edge 전송 서버 간의 동기화 관계를 설정합니다. Edge 구독 프로세스 중에 프로비전되는 자격 증명은 경계 네트워크에서 Edge 전송 서버와 사서함 서버 간의 LDAP 연결 보안에 사용됩니다.

Edge 전송 서버에서 **New-EdgeSubscription** cmdlet을 실행하면, ESBRA(EdgeSync 부트스트랩 복제 계정) 자격 증명이 로컬 서버의 AD LDS(Active Directory Lightweight Directory Services) 디렉터리에 만들어지고 Edge 구독 파일에 기록됩니다. 이러한 자격 증명은 초기 동기화를 설정하는 데만 사용되며 Edge 구독 파일이 만들어진 후 24시간이 지나면 만료됩니다. Edge 구독 프로세스가 24시간 이내에 완료되지 않으면 **New-EdgeSubscription** cmdlet을 다시 실행하여 새 Edge 구독 파일을 만들어야 합니다. Edge 구독 XML 파일에는 Edge 구독에 대한 구성 데이터가 저장됩니다.

Edge 구독 XML 파일에는 아래 표에 나와 있는 데이터가 포함됩니다.

### Edge 구독 파일 콘텐츠

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>구독 데이터</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>EdgeServerName</strong></p></td>
<td><p>Edge 전송 서버의 NetBIOS 이름으로 Edge 구독의 Active Directory 이름은 이 이름과 일치합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>EdgeServerFQDN</strong></p></td>
<td><p>Edge 전송 서버의 FQDN(정규화된 도메인 이름)입니다. 구독된 Active Directory 사이트의 사서함 서버는 DNS를 사용하여 FQDN을 확인하는 방법으로 Edge 전송 서버를 찾을 수 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EdgeCertificateBlob</strong></p></td>
<td><p>Edge 전송 서버 자체 서명 인증서의 공개 키입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>ESRAUsername</strong></p></td>
<td><p>ESBRA에 할당된 이름입니다. ESBRA 계정의 형식은 ESRA.<em>Edge 전송 서버 이름</em>입니다. ESRA는 EdgeSync 복제 계정입니다. ESBRA(초기 부트스트랩 복제 계정)와 ESRA의 차이점에 주의해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ESRAPassword</strong></p></td>
<td><p>ESBRA에 할당된 암호입니다. 암호는 난수 생성기를 사용하여 생성되며, 암호화되지 않은 텍스트로 Edge 구독 파일에 저장됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>EffectiveDate</strong></p></td>
<td><p>Edge 구독 파일을 만든 날짜입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>기간</strong></p></td>
<td><p>자격 증명이 만료될 때까지 유효한 상태로 유지되는 시간입니다. ESBRA 계정은 24시간 동안만 유효합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>AdamSslPort</strong></p></td>
<td><p>데이터를 Active Directory에서 AD LDS로 동기화할 때 EdgeSync에서 바인딩하는 보안 LDAP 포트입니다. 기본적으로 이 포트는 TCP 포트 50636입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ProductID</strong></p></td>
<td><p>Edge 전송 서버의 라이선스 정보입니다. Edge 구독을 만들기 전에 Edge 전송 서버의 라이선스를 적용해야 합니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>VersionNumber</strong></p></td>
<td><p>Edge 구독 파일의 버전 번호입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SerialNumber</strong></p></td>
<td><p>Edge 전송 서버의 Exchange 버전입니다.</p></td>
</tr>
</tbody>
</table>



> [!IMPORTANT]
> ESBRA 자격 증명은 암호화되지 않은 텍스트로 Edge 구독 파일에 기록됩니다. 구독 프로세스 전체 과정에서 이 파일을 안전하게 보호해야 합니다. Edge 구독 파일을 Exchange 조직으로 가져온 후에는 Edge 전송 서버, 파일을 Exchange 조직으로 가져오기 위해 사용한 네트워크 공유 및 모든 이동식 미디어에서 Edge 구독 파일을 즉시 삭제해야 합니다.



맨 위로 이동

## EdgeSync 복제 계정

ESRA(EdgeSync 복제 계정)는 EdgeSync 보안의 중요한 부분입니다. ESRA의 인증 및 권한은 Edge 전송 서버와 사서함 서버 간의 연결 보안에 사용되는 메커니즘입니다.

Edge 구독 파일에 포함된 ESBRA는 초기 동기화 중에 보안 LDAP 연결을 설정하는 데 사용됩니다. Edge 구독 파일을 Edge 전송 서버가 구독되는 Active Directory 사이트의 사서함 서버로 가져오면 각 Edge 전송 서버와 사서함 서버 쌍에 대해 Active Directory에 ESRA 계정이 추가로 만들어집니다. 초기 동기화하는 동안 새로 만들어진 ESRA 자격 증명은 AD LDS로 복제됩니다. 이러한 ESRA 자격 증명은 이후의 동기화 세션 보안에 사용됩니다.

각 EdgeSync 복제 계정에는 다음 표에 나와 있는 속성이 할당됩니다.

### Ms-Exch-EdgeSyncCredential 속성

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>속성 이름</th>
<th>종류</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>TargetServerFQDN</strong></p></td>
<td><p>String</p></td>
<td><p>이러한 자격 증명을 수락하는 Edge 전송 서버입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceServerFQDN</strong></p></td>
<td><p>String</p></td>
<td><p>이러한 자격 증명을 제시하는 사서함 서버입니다. 부트스트랩 자격 증명의 경우에는 이 값이 비어 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EffectiveTime</strong></p></td>
<td><p>DateTime(UTC)</p></td>
<td><p>해당 자격 증명을 사용하기 시작하는 시간입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>ExpirationTime</strong></p></td>
<td><p>DateTime(UTC)</p></td>
<td><p>해당 자격 증명이 만료되는 시간입니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>UserName</strong></p></td>
<td><p>String</p></td>
<td><p>인증하는 데 사용하는 사용자 이름입니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Password</strong></p></td>
<td><p>Byte</p></td>
<td><p>인증하는 데 사용하는 암호입니다. 이 암호는 <strong>ms-Exch-EdgeSync-Certificate</strong>를 사용하여 암호화됩니다.</p></td>
</tr>
</tbody>
</table>


다음 섹션에서는 EdgeSync 동기화 프로세스 동안 ESRA 자격 증명을 프로비전하고 사용하는 방법에 대해 설명합니다.

## EdgeSync 부트스트랩 복제 계정 프로비전

**New-EdgeSubscription** cmdlet가 Edge 전송 서버에서 실행되면 ESBRA가 다음과 같이 제공됩니다.

  - 자체 서명 인증서(Edge-Cert)가 Edge 전송 서버에 만들어집니다. 개인 키는 로컬 컴퓨터 저장소에 저장되고 공개 키는 Edge 구독 파일에 기록됩니다.

  - ESBRA 계정이 AD LDS에 만들어지고 해당 자격 증명이 Edge 구독 파일에 기록됩니다.

  - Edge 구독 파일을 이동식 미디어에 복사하는 방법으로 내보냅니다. Edge 서버는 Active Directory에 포함되어 있지 않으므로 공유 폴더를 사용하여 파일을 내보낼 수는 없습니다. 이렇게 내보낸 파일은 사서함 서버로 가져올 수 있습니다.

## Active Directory에서 EdgeSync 복제 계정 프로비전

사서함 서버에서 Edge 구독 파일을 가져오면 다음 단계가 수행되어 Active Directory에서 Edge 구독 레코드가 설정되고 추가 ESRA 자격 증명이 프로비전됩니다.

1.  Edge 전송 서버 구성 개체가 Active Directory에 만들어집니다. Edge-Cert 인증서가 이 개체에 특성으로 기록됩니다.

2.  구독된 Active Directory 사이트의 모든 사서함 서버는 새 Edge 구독이 등록되었다는 Active Directory 알림을 받습니다. 알림을 수신하는 즉시 각 사서함 서버는 ESRA.edge 계정을 검색하고, Edge-Cert 공개 키를 사용하여 해당 계정이 암호화됩니다. 암호화된 ESRA.edge 계정은 Edge 전송 서버 구성 개체에 기록됩니다.

3.  각 사서함 서버에서 자체 서명 인증서(TransportService-Cert)를 만듭니다. 개인 키는 로컬 컴퓨터 저장소에 저장되고 공개 키는 Active Directory의 사서함 서버 구성 개체에 저장됩니다.

4.  각 사서함 서버에서는 자체 TransportService 인증서의 공개 키를 사용하여 ESRA.edge 계정이 암호화된 다음 자체 구성 개체에 저장됩니다.

5.  각 사서함 서버에서는 Active Directory에서 개별 기존 Edge 전송 서버 구성 개체에 대해 ESRA를 생성됩니다(ESRA.edge.*사서함 이름.\#*).
    
    예: ESRA.edge.Example.0
    
    ESRA.edge의 암호는 난수 생성기를 통해 생성되며 TransportService-Cert 인증서의 공개 키를 사용하여 암호화됩니다. 암호는 Windows Server에 허용되는 최대 길이로 생성됩니다.

6.  각 ESRA.edge.*사서함 이름.\#* 계정은 Edge-Cert 인증서의 공개 키를 사용하여 암호화되며 Active Directory의 Edge 전송 서버 구성 개체에 저장됩니다.

다음 섹션에서는 EdgeSync 동기화 중에 이러한 계정을 사용하는 방법에 대해 설명합니다.

맨 위로 이동

## 초기 복제 인증

초기 ESBRA 계정은 초기 동기화를 설정할 때만 사용됩니다. 첫 번째 EdgeSync 동기화 중에 추가 ESRA 계정인 ESRA.edge.*사서함 이름.\#*이 AD LDS로 복제됩니다. 이러한 계정은 이후의 EdgeSync 동기화 세션을 인증하는 데 사용됩니다.

초기 복제를 수행하는 사서함 서버는 임의로 결정됩니다. 토폴로지 검색을 수행하고 새 Edge 구독을 검색하는 Active Directory 사이트의 첫 번째 사서함 서버에서 초기 복제가 수행됩니다. 이 검색 작업은 토폴로지 검색 시간을 기반으로 수행하므로 사이트에 있는 모든 사서함 서버에서 초기 복제를 수행할 수 있습니다.

EdgeSync는 사서함 서버에서 Edge 전송 서버로의 보안 LDAP 세션을 시작합니다. Edge 전송 서버에서 자체 서명 인증서를 제공하면 사서함 서버에서 해당 인증서가 Active Directory의 Edge 전송 서버 구성 개체에 저장되어 있는 인증서와 일치하는지 확인합니다. Edge 전송 서버의 ID가 확인되면 사서함 서버에서 ESRA.edge.*사서함 이름.\#* 계정의 자격 증명이 Edge 전송 서버에 제공됩니다. 그러면 Edge 전송 서버에서 해당 자격 증명을 AD LDS에 저장되어 있는 계정과 비교하여 확인합니다.

그런 다음 사서함 서버의 EdgeSync 서비스가 Active Directory의 토폴로지, 구성 및 받는 사람 데이터가 AD LDS로 전달됩니다. Active Directory의 Edge 전송 서버 구성 개체에 대한 변경 내용이 AD LDS로 복제됩니다. AD LDS가 새로 추가된 ESRA.edge.*사서함 이름.\#* 항목을 받고 Microsoft Exchange 자격 증명 서비스가 해당 AD LDS 계정을 만듭니다. 그러면 이후에 예약된 EdgeSync 동기화 세션을 인증하는 데 이러한 계정을 사용할 수 있습니다.

## Microsoft Exchange Credential Service

Microsoft Exchange 자격 증명 서비스는 Edge 구독 프로세스의 일부입니다. 자격 증명 서비스는 Edge 전송 서버에서만 실행됩니다. 이 서비스는 사서함 서버가 Edge 전송 서버에 인증해 EdgeSync 동기화를 수행할 수 있도록 AD LDS에 역 ESRA 계정을 만듭니다. EdgeSync는 Microsoft Exchange 자격 증명 서비스와 직접 통신하지 않습니다. Microsoft Exchange 자격 증명 서비스는 AD LDS와 통신하며 사서함 서버에서 ESRA 자격 증명을 업데이트할 때마다 해당 자격 증명을 설치합니다.

맨 위로 이동

## 예약된 동기화 세션 인증

초기 EdgeSync 동기화가 완료되면 EdgeSync 동기화 일정이 설정되고 변경된 Active Directory 데이터가 AD LDS에서 정기적으로 업데이트됩니다. 사서함 서버에서는 Edge 전송 서버에 있는 AD LDS 인스턴스를 사용하여 보안 LDAP 세션이 시작됩니다. AD LDS에서는 자체 서명 인증서가 제공되어 사서함 서버에 ID를 증명합니다. 그러면 사서함 서버의 해당 ESRA.edge 자격 증명이 AD LDS에 제공됩니다. ESRA.edge 암호는 사서함 서버의 자체 서명 인증서 공개 키를 사용하여 암호화됩니다. 즉, 해당 사서함 서버만이 이러한 자격 증명을 사용하여 AD LDS를 인증할 수 있습니다.

맨 위로 이동

## EdgeSync 복제 계정 갱신

ESRA 계정의 암호는 로컬 서버의 암호 정책을 따라야 합니다. 암호 갱신 프로세스로 인해 일시적으로 인증이 실패하는 현상이 발생하지 않도록 첫 번째 ESRA.edge 계정이 만료되기 7일 전(첫 번째 ESRA 만료 시간 3일 전)에 두 번째 ESRA.edge 계정이 만들어집니다. 두 번째 ESRA.edge 계정이 적용되는 즉시 EdgeSync에서 첫 번째 계정 사용을 중지하고 두 번째 계정이 사용됩니다. 첫 번째 계정이 만료되면 해당 ESRA 자격 증명은 삭제됩니다. Edge 구독을 제거할 때까지 이 갱신 프로세스는 계속됩니다.

맨 위로 이동

