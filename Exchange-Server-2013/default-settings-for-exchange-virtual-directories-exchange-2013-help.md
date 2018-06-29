---
title: 'Exchange 가상 디렉터리에 대 한 기본 설정: Exchange 2013 Help'
TOCTitle: Exchange 가상 디렉터리에 대 한 기본 설정
ms:assetid: d2d89ce6-4721-4737-a325-fba5ad9422e0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg247612(v=EXCHG.150)
ms:contentKeyID: 52058121
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 가상 디렉터리에 대 한 기본 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-07_

Exchange Server 2013은 설치 중에 여러 IIS(인터넷 정보 서비스) 가상 디렉터리를 자동으로 구성합니다. 이 항목에는 클라이언트 액세스 서버 및 사서함 서버에 대한 기본 IIS 인증 설정 및 기본 SSL(Secure Sockets Layer) 설정에 대한 정보가 포함되어 있습니다.

## 클라이언트 액세스 서버

다음 표에서 독립 실행형 Exchange 2013 클라이언트 액세스 서버에서 기본 설정을 나열합니다.

### 기본 클라이언트 액세스 서버 IIS 인증 및 SSL 설정

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>가상 디렉터리</th>
<th>인증 방법</th>
<th>SSL 설정</th>
<th>관리 방법</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 웹 사이트</p></td>
<td><ul>
<li><p>익명</p></li>
</ul></td>
<td><ul>
<li><p>필수</p></li>
</ul></td>
<td><p>IIS 관리 콘솔</p></td>
</tr>
<tr class="even">
<td><p>aspnet_client</p></td>
<td><ul>
<li><p>익명 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>IIS 관리 콘솔</p></td>
</tr>
<tr class="odd">
<td><p>자동 검색</p></td>
<td><ul>
<li><p>익명 인증</p></li>
<li><p>기본 인증</p></li>
<li><p>Windows 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>Exchange 관리 셸(셸)</p></td>
</tr>
<tr class="even">
<td><p>ecp</p></td>
<td><ul>
<li><p>익명 인증</p></li>
<li><p>기본 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>EAC(Exchange 관리 센터) 또는 셸</p></td>
</tr>
<tr class="odd">
<td><p>EWS</p></td>
<td><ul>
<li><p>익명 인증</p></li>
<li><p>Windows 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>셸</p></td>
</tr>
<tr class="even">
<td><p>Microsoft-Server-ActiveSync</p></td>
<td><ul>
<li><p>기본 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>EAC 또는 셸</p></td>
</tr>
<tr class="odd">
<td><p>OAB</p></td>
<td><ul>
<li><p>Windows 인증</p></li>
</ul></td>
<td><ul>
<li><p>필요 없음</p></li>
</ul></td>
<td><p>EAC 또는 셸</p></td>
</tr>
<tr class="even">
<td><p>owa</p></td>
<td><ul>
<li><p>기본 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>EAC 또는 셸</p></td>
</tr>
<tr class="odd">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>익명 인증</p></li>
</ul></td>
<td><ul>
<li><p>필요 없음</p></li>
</ul></td>
<td><p>셸</p></td>
</tr>
<tr class="even">
<td><p>Rpc</p></td>
<td><ul>
<li><p>기본 인증</p></li>
<li><p>Windows 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>셸</p></td>
</tr>
<tr class="odd">
<td><p>RpcWithCert</p></td>
<td><p>기본적으로 모든 인증 방법이 사용하지 않도록 설정되어 있습니다.</p></td>
<td><ul>
<li><p>필수</p></li>
</ul></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 사서함 서버

다음 표에서 독립 실행형 Exchange 2013 사서함 서버에서 기본 설정을 나열합니다.

### 기본 사서함 서버 IIS 인증 및 SSL 설정

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>가상 디렉터리</th>
<th>인증 방법</th>
<th>SSL 설정</th>
<th>관리 방법</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>기본 웹 사이트</p></td>
<td><ul>
<li><p>익명 인증</p></li>
</ul></td>
<td><ul>
<li><p>SSL 필요</p></li>
<li><p>128비트 암호화 필요</p></li>
</ul></td>
<td><p>이 가상 디렉터리는 사용자가 구성할 수 없습니다.</p></td>
</tr>
<tr class="even">
<td><p>PowerShell</p></td>
<td><ul>
<li><p>익명 인증</p></li>
</ul></td>
<td><ul>
<li><p>필요 없음</p></li>
</ul></td>
<td><p>셸</p></td>
</tr>
</tbody>
</table>

