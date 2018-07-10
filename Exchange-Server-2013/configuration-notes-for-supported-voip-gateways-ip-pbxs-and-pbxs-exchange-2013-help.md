---
title: '지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항: Exchange 2013 Help'
TOCTitle: 지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50555945
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

이 페이지에서는 만들고 Microsoft 또는 VoIP 게이트웨이 파트너에 의해 테스트 구성 참고 사항에 대 한 링크를 제공 합니다. Microsoft 또는 파트너 새 VoIP 게이트웨이와 PBX 또는 IP PBX 구성 사용 하 여 통합 메시징을 배포, 필수 구성 요소 및 구성 설정을 문서화 됩니다. 이 정보는 구성 메모를 작성 하는데 사용 됩니다.

각 PBX 구성 메모는 특정 전화 통신 구성을 사용 하 여 통합 메시징을 배포 하는 방법에 대 한 정보를 포함 하 고 제조업체, 모델 및 VoIP 게이트웨이, IP Pbx 또는 Pbx에 대 한 펌웨어 버전을 포함 합니다. 또한 각 PBX 구성 참고는와 같은 기타 정보를 포함 합니다.

  - 참가자 (영문)에서 구성 메모를 작성 합니다.

  - 자세한 필수 구성 요소를 다음을 포함 합니다.
    
      - 사용 하도록 설정 되거나 PBX를 사용 하지 않도록 설정 될 수 있는 기능입니다.
    
      - 특수 하드웨어를 설치 해야입니다.
    
      - VoIP 게이트웨이 필요한 지 여부.
    
      - 필요한 경우 VoIP 게이트웨이에 포함 되어 있어야 하는 기능입니다.
    
      - IP 게이트웨이 및 PBX 간의 특정 케이블 연결 요구 사항입니다.
    
      - 지정 된 전화 통신 구성으로 사용 하지 못할 수 있는 통합 메시징 기능 목록입니다.

통합 커뮤니케이션의 개방형 상호 운용성 프로그램 찾기 (영문) 정규화 된 SIP PSTN 게이트웨이 및 IP Pbx 및 프로세스 전화 통신 인프라 공급 업체에 참가 하 고 프로그램에 참가 하는데 사용할 수를 포함 하 여 엔터프라이즈 전화 통신 인프라에 대 한 Microsoft 하는 방법에 대 한 자세한 내용을 보려면 [Microsoft 통합 커뮤니케이션의 개방형 상호 운용성 프로그램](https://go.microsoft.com/fwlink/p/?linkid=132071)를 참조 합니다.

## VoIP 게이트웨이, IP PBX 및 PBX 구성 참고 사항

VoIP 게이트웨이 파트너와, AudioCodes 및 Dialogic를 테스트 하는 Pbx의 목록에 추가할 Microsoft 작동 합니다. 현재 많은 조합의 전화 통신 구성 요소를 테스트 하는 때문에이 항목 자주 업데이트 됩니다. 배포에 대 한 적절 한 구성 참고를 찾을 수 없는 경우 다시 확인 하십시오.

다음 구성 참고 사용할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>Tel 사이</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>Nortel</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>Toshiba</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110 (이전의 Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (명시적 BC13)</p></td>
<td><p>아날로그-직렬 MD110</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110 (이전의 Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (명시적 BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Aastra MX-원</p></td>
<td><p>4.0</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>오 라</p></td>
<td><p>통신 관리자 5.2.1 SP 5</p>
<p>세션 관리자 5.2입니다.</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>디지털 집합 에뮬레이션 (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 CAS – 인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>사이버 Magix</p></td>
<td><p>1.5 v.6.0 릴리스</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>G3xV11 통신 관리자 1.3</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 CAS – 인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>통신 관리자 (R013x00.1.346.0) 3.0</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>통신 관리자 (R013x00.1.346.0) 3.0</p></td>
<td><p>T1 CAS – 인밴드 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>통신 관리자 (R013x00.1.346.0) 3.0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco 통화 관리자 4.x</p></td>
<td><p>4.x</p></td>
<td><p>IP-IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco 통화 관리자 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco 통합 커뮤니케이션 관리자 6.0 및 6.1</p></td>
<td><p>6.x</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco 통합 커뮤니케이션 관리자 7.0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco 통합 커뮤니케이션 관리자 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>직접 SIP 연결</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Tel 사이


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>5, 000 개 사이-Tel v2.1</p></td>
<td><p>T1 CAS – 인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess V9.0</p></td>
<td><p>T1 CAS – 인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 CAS-SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>디지털 집합 에뮬레이션 (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Electra 정예 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>7400 버전</p></td>
<td><p>T1 CAS-직렬 MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX (영문) IPX</p></td>
<td><p>7400 버전</p></td>
<td><p>디지털 집합 에뮬레이션 (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>버전 R18.06.24.000</p></td>
<td><p>T1 CAS – 직렬 MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>버전 R18.06.24.000</p></td>
<td><p>아날로그-직렬 MCI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q.SIG – 직렬 MCI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>S</p></td>
<td><p>RMS1 버전 R1.3 E1TA</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Nortel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 (영문) 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>자오선 81 C</p></td>
<td><p>4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>자오선 81 C</p></td>
<td><p>4.5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>릴리스 25</p></td>
<td><p>디지털 집합 에뮬레이션 (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>릴리스 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>릴리스 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>CS-1000 M (연속 해 서)</p></td>
<td><p>릴리스 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX TDA200</p></td>
<td><p>001-001</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>KX TDA200</p></td>
<td><p>3</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>KX TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>디지털 집합 에뮬레이션 (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IP 전화 통신 시스템</p></td>
<td><p>6.1</p></td>
<td><p>아날로그-SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>IP 전화 통신 시스템</p></td>
<td><p>7.5</p></td>
<td><p>아날로그-SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>실제 2.2</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>디지털 집합 에뮬레이션 (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>HiCom 300</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 CAS-인밴드 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>실제 3</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>버전 3.0 SMR5 SMP4</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>버전 3.0 SMR5 SMP4</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>버전 2.0 SMR9 SMP0</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>버전 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Sonus


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
<th>VoIP 게이트웨이 모델</th>
<th>VoIP 게이트웨이 소프트웨어 릴리스</th>
<th>지원 되는 프로토콜</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 이상</p></td>
<td><ul>
<li><p>TDM (ISDN) 신호: at&amp;t 4ESS/5ESS, Nortel DMS 100, 유로 ISDN (ETSI 300 102), QSIG, NTT InsNet (일본), ANSI 국가 ISDN-2 (-니-2)</p></li>
<li><p>TDM 신호 (CA): T1 CAS (E &amp; M, 루프 시작)입니다. E1 CAS (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>산호색 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>산호색 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>산호색 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>산호색 Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>산호색 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>산호색 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="odd">
<td><p>산호색 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS – 인밴드 DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>산호색 IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">다운로드</a></p></td>
</tr>
</tbody>
</table>


## Toshiba


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 모델</th>
<th>PBX 소프트웨어 릴리스</th>
<th>프로토콜</th>
<th>게이트웨이 공급 업체</th>
<th>게이트웨이 모델</th>
<th>만든이 구성</th>
<th>구성 파일 다운로드</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>아날로그-SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>아날로그-인밴드 DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">다운로드</a></p></td>
</tr>
</tbody>
</table>

