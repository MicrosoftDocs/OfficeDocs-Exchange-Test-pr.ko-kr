---
title: '수신 커넥터 인증 메커니즘: Exchange 2013 Help'
TOCTitle: 수신 커넥터 인증 메커니즘
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 50483674
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수신 커넥터 인증 메커니즘

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-03-09_


수신 커넥터 인증 메커니즘은 다음과 같습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>인증 메커니즘</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>없음</p></td>
<td><p>인증이 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>TLS</p></td>
<td><p>보급 STARTTLS. TLS를 제공하기 위해 서버 인증서를 사용할 수 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>Integrated</p></td>
<td><p>NTLM 및 Kerberos(Windows 통합 인증)</p></td>
</tr>
<tr class="even">
<td><p>BasicAuth</p></td>
<td><p>기본 인증. 인증된 로그온이 필요합니다.</p></td>
</tr>
<tr class="odd">
<td><p>BasicAuthRequireTLS</p></td>
<td><p>TLS를 통한 기본 인증. 서버 인증서가 필요합니다.</p></td>
</tr>
<tr class="even">
<td><p>ExchangeServer</p></td>
<td><p>Exchange 서버 인증(GSSAPI(Generic Security Services Application Programming Interface) 및 상호 GSSAPI).</p></td>
</tr>
<tr class="odd">
<td><p>ExternalAuthoritative</p></td>
<td><p>연결은 Exchange 외부의 보안 메커니즘을 사용하여 외부에서 보안이 유지되는 것으로 간주됩니다. 연결은 IPsec(인터넷 프로토콜 보안) 연결 또는 VPN(가상 사설망)일 수 있습니다. 또는 서버가 실제로 제어되는 트러스트된 네트워크에 상주할 수 있습니다. <code>ExternalAuthoritative</code> 인증 방법을 사용하려면 <code>ExchangeServers</code> 사용 권한 그룹이 필요합니다. 이러한 인증 방법과 보안 그룹의 조합을 사용하면 이 커넥터를 통해 받은 메시지에 대해 익명 보낸 사람의 전자 메일 주소를 확인할 수 있습니다.</p></td>
</tr>
</tbody>
</table>


수신 커넥터 인증 메커니즘에 대 한 자세한 내용은 [New-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125139\(v=exchg.150\))을 참조 하십시오.

