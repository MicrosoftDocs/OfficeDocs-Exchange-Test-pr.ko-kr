---
title: '페더레이션 트러스트에 대한 신뢰할 수 있는 루트 인증 기관: Exchange 2013 Help'
TOCTitle: 페더레이션 트러스트에 대한 신뢰할 수 있는 루트 인증 기관
ms:assetid: d4224bf5-69b3-484c-8a70-4f230d3dbdd9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee332350(v=EXCHG.150)
ms:contentKeyID: 50484222
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션 트러스트에 대한 신뢰할 수 있는 루트 인증 기관

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-07-26_

Microsoft Exchange Server 2013 조직과 [Azure Active Directory 인증 시스템](https://go.microsoft.com/fwlink/p/?linkid=135986)간에 페더레이션 트러스트를 설정 하기 위해 사용 하는 트러스트를 만들려면 Exchange 서버에 설치 된 디지털 인증서가 필요 합니다. 자체 서명 된 인증서를 사용 하는 것이 좋습니다. 자체 서명 된 인증서를 만들고 Exchange 관리 센터 (EAC) **페더레이션 트러스트 사용** 마법사를 사용 하는 경우 자동으로 설치 됩니다.

권장 되는 자체 서명 된 인증서를 사용 하 여 않으려면에 요청 하 고 Microsoft가 신뢰할 수 있는 인증 기관 (CA)에서 X.509 Secure Sockets Layer (SSL) 인증서를 설치 해야 합니다. Azure AD 인증 시스템과 페더레이션 트러스트를 설정 하려면 다른 Ca에서 발급 한 인증서를 사용할 수도 있습니다, 하지만 날짜를 Microsoft에서 인증 되지 않은 있습니다.

다음 표에는 현재 Microsoft에서 신뢰하는 CA의 목록이 나와 있습니다. Exchange 2013에서 사용할 수 있도록 이러한 CA는 테스트되었습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>CA 이름</th>
<th>발급자</th>
<th>용도</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>Autoridade Certificadora Raiz Brasileira</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>Comodo</p></td>
<td><p>Comodo 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>CyberTrust</p></td>
<td><p>볼티모어 CyberTrust 루트 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>Digicert</p></td>
<td><p>Digicert 전역 루트 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>Digicert High Assurance EV</p></td>
<td><p>Digicert 전역 루트 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>Entrust</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>Entrust(2048)</p></td>
<td><p>Entrust.net Secure Server Certification Authority</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>Equifax</p></td>
<td><p>Equifax Secure Certification Authority</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>GlobalSign</p></td>
<td><p>GlobalSign 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>Go Daddy</p></td>
<td><p>Go Daddy Class 2 Certification Authority</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>Network Solutions</p></td>
<td><p>네트워크 솔루션 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>PositiveSSL</p></td>
<td><p>Comodo 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>SECOM</p></td>
<td><p>SECOM Trust Systems 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>UTN-UserFirst-Hardware</p></td>
<td><p>Comodo 인증 기관</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="odd">
<td><p>VeriSign</p></td>
<td><p>Class 3 Public Primary Certification Authority</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
<tr class="even">
<td><p>VeriSign</p></td>
<td><p>VeriSign Trust Network</p></td>
<td><p>서버 인증, 클라이언트 인증</p></td>
</tr>
</tbody>
</table>


페더레이션용 인증서 요구 사항에 대한 자세한 내용은 [페더레이션](federation-exchange-2013-help.md)를 참조하십시오.

