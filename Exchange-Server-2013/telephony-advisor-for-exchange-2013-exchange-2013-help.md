---
title: 'Exchange 2013에 대 한 전화 통신 관리자: Exchange 2013 Help'
TOCTitle: Exchange 2013에 대 한 전화 통신 관리자
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50556108
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013에 대 한 전화 통신 관리자

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2017-07-25_

통합된 메시징 (UM) 조직에 대 한 기존 전화 통신 시스템과 Microsoft Exchange를 통합 해야 합니다. 성공적인 배포를 사용 해야 기존 전화 통신 인프라의 신중 하 게 분석을 확인 하 고 통합 메시징을 배포 하려면 올바른 계획 단계를 수행 합니다.

계획 단계에는 전화 통신 네트워크와 거의 없거나 전혀 없는 경험을가지고 있는 Exchange 관리자에 게 중요 한 과제로 대 두 될 수 있습니다. 이 문제를 해결 하기 위해이 항목 뒷부분에 나오는 Your UM 배포에 대 한 지원에는 리소스 를 참조 합니다.

통합 메시징에 대 한 지원 되는 VoIP 게이트웨이 보려면, PBX가 지원 되는 특정 VoIP 게이트웨이 모델 또는 제조업체를 사용 하 여 IP PBX와의 직접 SIP 연결을 사용 하 여 사용할 수 있는지 여부 또는 지원 세션 테두리 컨트롤러 (볼 수 있는지 확인 Sbc) Exchange 온라인 UM을 위한 다음 링크 중 하나를 클릭 합니다.

  - 지원 되는 VoIP 게이트웨이

  - 지원 되는 Pbx AudioCodes VoIP 게이트웨이 사용 하는 경우

  - Dialogic VoIP 게이트웨이 사용 하는 경우 Pbx 지원
    
      - Pbx DMG1000 시리즈 미디어 게이트웨이 사용 하는 경우 지원
    
      - Pbx DMG 2000 시리즈 미디어 게이트웨이 사용 하는 경우 지원
    
      - Pbx DMG3000 시리즈 미디어 게이트웨이 사용 하는 경우 지원

  - 지원 되는 IP Pbx

  - SIP 미디어 게이트웨이 사용 하는 경우 IP Pbx를 지원

  - Exchange 통합 메시징, Office Communications Server 2007 R2 및 Microsoft Lync Server

## UM 배포를 위해 리소스

전화 통신 네트워크를 배포 하기 위한 지침을 만들려는 하기가 어려울 뿐 아니라 합니다. 서로 다른 구성 설정, 펌웨어, 및 요구 사항을 사용 하 여 VoIP 게이트웨이, IP Pbx 및 Pbx를 포함할 수 있기 때문에 서로에서 매우 다를 수 수 있습니다. 그러나 여러 리소스를 성공적으로 통합 메시징을 배포 하기 위해 사용할 수 있습니다.

  - **통합 메시징 전문가** UM 전문가 Exchange 엔지니어링 팀에 의해 수행 된 Exchange 통합 메시징에 대 한 기술 교육 제공 받은 시스템 통합자입니다. 을 레거시 음성 메일 시스템에서 통합 메시징에 원활 하 게 전환을 보장 하기 위해 Microsoft 모든 고객 참여할 UM 전문가 것이 좋습니다. 연락처 정보를 [Microsoft Exchange Server 2013 통합 메시징 (UM) 전문가](http://go.microsoft.com/fwlink/p/?linkid=262708) 또는 [통합 메시징에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/p/?linkid=261951)를 참고 하십시오.

  - **구성 참고 사항 지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx**   이러한 구성 참고 설정과 네트워크에 있는 경우 통합 메시징 서버와 VoIP 게이트웨이, IP Pbx와 통신 하도록 Pbx를 구성 하는 경우에 매우 유용 하는 기타 정보를 포함 합니다. 자세한 내용은 [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)을 참조 하십시오.

  - **지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항**   이러한 구성 참고 설정과 세션 테두리 컨트롤러 (Sbc) 서버와 통신 하는 통합 메시징 하이브리드 및 Exchange Online UM 배포를 구성 하는 경우 매우 유용 하는 기타 정보를 포함 합니다. 자세한 내용은 [지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)을 참조 하십시오.
    

    > [!NOTE]
    > 7 월 2018에서 작동 하는 고객 Sbc에서 직접 연결을 통해 타사 PBX 시스템에 대 한 Exchange Online UM 지원 종료 됩니다. 자세한 내용은 Exchange 팀 블로그 <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">한 Exchange Online에서 세션 테두리 컨트롤러에 대 한 지원 중단 통합 메시징</A> 를 참조 하십시오.



통합 메시징 전문가, 참여하기 전에 요청할 수 있는 주요 질문에 답할 수 있습니다. 다음 질문에 대답 필요 하 고 UM 전문가 사이의 대화를 생산성을 확인 하는데 도움이 됩니다.

  - 얼마나 많은 조직에 있는 기존 전화 또는 음성 메일 사용자 또는 둘 모두?

  - 얼마나 많은 사용자가 통합 메시징과 제공 하려는?

  - 어떤 PBX 또는 Pbx 통합 메시징과 통합을 사용 하 려 한다고?

  - 조직에는 얼마나 많은 Pbx 해야 합니까? 공급 업체, 형식 (회로 또는 IP 기반), 모델 및 펌웨어 버전을 지정 합니다.

  - Pbx 네트워크 연결, 되며 이러한 중앙 배치 또는 여러 위치에 있는?

  - 어떤 음성 메일 시스템 또는 시스템에서 조직의 현재 사용 합니까? 공급 업체, 형식, 모델 및 펌웨어 버전을 지정 합니다.

  - 사용자의 Pbx에 음성 메일 시스템 통합 방법 (아날로그, T1/E1, PRI, 디지털 설정 에뮬레이션, VoIP, 다른)?

  - 현재 사용 중인 음성 네트워킹

  - 조직에서 팩스 시스템 또는 시스템의 종류를 사용, 및는 팩스 시스템 또는 시스템 지원 Exchange 에 인바운드 팩스 라우팅?

  - 조직에서 자동된 전화 교환 기능을 사용 합니까?

  - 필요한 지원 하나요 전화 전용 사용자에 대 한 즉, 사용자에 게 전자 메일 액세스를 갖지 않도록?

## 지원 되는 VoIP 게이트웨이

Pbx와 통합 메시징 통합를 사용 하 여 하나 이상의 VoIP 게이트웨이 TDM 기반 Pbx 통합 메시징에 사용 되는 IP 기반, 패킷 전환 프로토콜에 사용 되는 회로 전환 프로토콜 변환 해야 합니다. VoIP 게이트웨이 공급 업체에 VoIP와 미디어 게이트웨이의 다양 한 모델 테스트 된 및 통합 메시징에 대 한 지원 됩니다.

VoIP 게이트웨이, IP Pbx 및 Sbc와의 통합 메시징 상호 운용성 테스트가 Microsoft Unified Communications 개방형 상호 운용성 프로그램 통합 되었습니다. 자세한 내용은 [Microsoft 통합 커뮤니케이션의 개방형 상호 운용성 프로그램](http://go.microsoft.com/fwlink/p/?linkid=140722)을 참조 하십시오.

VoIP 게이트웨이, IP Pbx 및 고급 VoIP 게이트웨이 용 [Microsoft 통합 커뮤니케이션의 개방형 상호 운용성 프로그램](http://go.microsoft.com/fwlink/p/?linkid=140722) 검증 프로그램 통해 고객 원활 하 게 설치 및 지원 될 때 발생 하 게는 사용 하 여 정규화 된 전화 통신 VoIP 게이트웨이 및 IP Pbx Microsoft 통합 커뮤니케이션 소프트웨어 사용 합니다. 엄격한 및 광범위 한 테스트 요구 사항을 충족 하 고 사양에 일치 하 고 테스트 계획 하는 제품 정규화를 수신 합니다.

지원 되는 VoIP 게이트웨이, IP Pbx, Pbx 및 Sbc를 구성 하는 방법에 대 한 자세한 내용은, 다음 리소스 중 하나를 참조 합니다.

  - [지원 되는 VoIP 게이트웨이, IP Pbx 및 Pbx에 대 한 구성 참고 사항](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

상호 운용성 다음 VoIP 게이트웨이 공급 업체에 대 한 확인 되었습니다.

  - AudioCodes

  - Dialogic

  - 다음 표에서 VoIP 게이트웨이 공급 업체, VoIP 게이트웨이 모델 및 각 모델에 의해 지원 되는 프로토콜을 보여줍니다.

### 통합 메시징에 대 한 지원 되는 VoIP 게이트웨이

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>공급업체</th>
<th>모델</th>
<th>지원 되는 프로토콜</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>인밴드 DTMF와 아날로그</p></li>
<li><p>SMDI와 아날로그</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>인밴드 DTMF와 아날로그</p></li>
<li><p>SMDI와 아날로그</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>T1/E1 CA</p></li>
<li><p>T1/E1 Q.SIG</p></li>
<li><p>IP-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>디지털 집합 에뮬레이션</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>인밴드 DTMF와 아날로그</p></li>
<li><p>SMDI와 아날로그</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>T1 CA</p></li>
<li><p>T1/E1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 이상</p></td>
<td><ul>
<li><p>TDM (ISDN) 신호: at&amp;t 4ESS/5ESS, Nortel DMS 100, 유로 ISDN (ETSI 300 102), QSIG, NTT InsNet (일본), ANSI 국가 ISDN-2 (-니-2)</p></li>
<li><p>TDM 신호 (CA): T1 CAS (E &amp; M, 루프 시작)입니다. E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>테너 DX 시리즈</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 지원 되는 Pbx AudioCodes VoIP 게이트웨이 사용 하는 경우

다음 표에서 AudioCodes VoIP 게이트웨이, MediaPack 114 FXO, MediaPack 118 FXO Mediant 2000 등을 사용 하 여 지원 되는 Pbx를 보여줍니다.

### Pbx AudioCodes VoIP 게이트웨이 사용한 지원

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 제조업체</th>
<th>PBX 모델/유형</th>
<th>AudioCodes 모델 &quot;x&quot;-4 또는 필요 &quot;y&quot; 당 8로 교체-1, 2, 4, 8 또는 필요 당 16 바꿉니다.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/사이버</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>IP Office</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4.x</p></td>
<td><ul>
<li><p>Mediant1000-IP</p></li>
<li><p>Mediant2000-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Electra 정예</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>S</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>통신 서버-1000 M, 1000 단위, 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>자오선 11 c 51 c, 61 c, 81 c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824, KX TEA308</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30, KX-TDA100 KX-TDA200, KX TDA600</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>IP 전화 통신 시스템</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Tadiran 통신</p></td>
<td><p>산호색 Flexicom, 산호색 IPX</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## 지원 되는 Pbx Dialogic VoIP 게이트웨이 사용 하는 경우

각 Dialogic VoIP 게이트웨이 모델 다른 Pbx를 지원합니다. 다음 표에 표시 PBX 제조업체 및 모델 및 Dialogic VoIP 게이트웨이 사용할 수 있습니다. 각 VoIP 게이트웨이 서로 다른 신호 방법, 하 게 되 면 및 프로토콜을 사용 합니다.

## Pbx DMG1000 시리즈 미디어 게이트웨이 사용 하는 경우 지원

다음 표에서 저밀도 Dialogic 미디어 게이트웨이 (DMG1000)와 지원 되는 Pbx를 보여줍니다. 그러나는 아날로그 DMG1000를 사용한 경우, 보충 신호 (RS232 SMDI, MD110, MCI 프로토콜 또는 전송 되는 인밴드 DTMF 신호)가 필요 합니다.

### Pbx 저밀도 Dialogic DMG1000 시리즈 VoIP 게이트웨이 사용 하는 경우 지원

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 제조업체</th>
<th>PBX 모델/유형</th>
<th>DMG 모델 및 추가 신호</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (이전의 Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>MD110 RS232 프로토콜을 사용 하 여 아날로그 연결</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>전체 조명 PCX 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100, S8300, S8700, 및 S8710 (통신 관리자 s W V2.0 또는 이상 버전)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>인터</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>SMDI 직렬 프로토콜을 사용 하 여 아날로그 연결</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX-200 D, SX 200 연한, SX 2000 연한, SX 2000 S, SX 2000 VS, SX 200 ICP</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>자오선 1-옵션 11, 21, 21A, 51, 61, 71, 및 81</p>
<p>자오선 SL1-일반 X11 릴리스 15 이상 버전</p>
<p>Nortel 통신 서버-1, 000, 000만, 1000 단위, 1000E V3.0 또는 이상 버전</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>SMDI 직렬 프로토콜을 사용 하 여 아날로그 연결</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (유럽)</p></td>
<td><p>DMG1008LSW</p>
<p>전송 되는 인밴드 DTMF 신호를 사용 하 여 아날로그 연결</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (소프트웨어 릴리스 80003 이상 버전)<br />
9000 (모든 버전)</p>
<p>9751 (모든 버전의 소프트웨어는 9005 버전)</p>
<p>9751 (소프트웨어 릴리스 9006.4 이상 버전)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (소프트웨어 버전 AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>다른 사용자에 게</p></td>
<td><p>다양</p></td>
<td><p>DMG1008LSW</p>
<p>전송 되는 인밴드 DTMF 또는 SMDI 중 하나를 사용 하 여 아날로그 연결</p></td>
</tr>
</tbody>
</table>


## Pbx DMG 2000 시리즈 미디어 게이트웨이 사용 하는 경우 지원

다음 표에서 지원 되는 T1/E1 Dialogic 미디어 게이트웨이 (DMG2000)와 Pbx를 보여줍니다. 단일 범위 (DMG2030DTIQ)에 나오는 DMG2000 게이트웨이 이중 (DMG2060DTIQ)에 걸쳐, 또는 4 중 (DMG2120DTIQ) 밀도 걸쳐, 프로토콜을 지원 합니다.

  - T1 CA

  - T1 Q.SIG

  - E1 Q.SIG

  - T1-니-2

  - T1 5ESS

  - T1 DMS100

신호 채널 연결 된 신호 (CA)를 사용 하는 경우 추가 신호 (RS232 SMDI, MD110, MCI 프로토콜 또는 전송 되는 인밴드 DTMF 신호)가 필요 합니다. Q.SIG 신호를 사용 하는 경우 PBX 통화와 연결 된 사용자 정보 및 통화 전송 통합 메시징에 필요한 기능을 호출 하는 추가 서비스를 지원 해야 합니다.

### Pbx DMG2000 미디어 게이트웨이와 지원

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 제조업체</th>
<th>PBX 모델/유형</th>
<th>필수 소프트웨어 버전</th>
<th>프로토콜 및 추가 신호</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>전체 조명 PCX 4400</p></td>
<td><p>버전 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>3 이상 버전</p></td>
<td><p>T1 CA</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>관리자 s W V2.0 또는 이상 버전</p></td>
<td><p>T1 CA</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>MX1 TSW R2A 릴리스 (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>인터</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS (w / SMDI 직렬 프로토콜)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>릴리스 5200 년 12 월 92 1b 또는 이상 버전</p></td>
<td><p>CAS (MCI 직렬 프로토콜)이 포함 된</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 릴리스 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>자오선 1-11 옵션</p></td>
<td><p>릴리스 15 또는 이상 버전 및 19 및 46 옵션은 필요</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>통신 서버 1000</p></td>
<td><p>2121, 4 릴리스 버전</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>9006.4 이상 버전 (참고: 북미 소프트웨어 부하만)</p></td>
<td><p>T1 CA</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 9 SMR SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>SX 2000 S, SX 2000 VS</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>버전 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## Pbx DMG4008BRI 시리즈 미디어 게이트웨이 사용 하는 경우 지원

DMG4000 시리즈 미디어 게이트웨이 여러 TDM 인터페이스 옵션이 제공 됩니다. DMG4008BRI 4 포트/8 채널 밀도 지원할 뿐 이며 프로토콜을 지원 합니다.

  - ISDN BRI Q.SIG

  - ETSI DSS1 (유로 ISDN)

  - NET 3 (벨기에)

  - VN3 (프랑스)

  - 1TR6 (독일)

  - 기능 키를 누른 상태로 64 (일본)

  - 5ESS 사용자 정의 (북미-at\&t)

  - 국가 ISDN (NI1-북미)

다음 표에서 Dialogic 4000 미디어 게이트웨이 시리즈 (DMG4008)를 사용 하 여 지원 되는 Pbx를 보여줍니다.

### Pbx DMG4008BRI 미디어 게이트웨이 사용 하 여 지원

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 제조업체</th>
<th>PBX 모델/유형</th>
<th>필수 소프트웨어 버전</th>
<th>프로토콜 및 추가 신호</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q 합니다. SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q 합니다. SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## 지원 되는 IP Pbx

IP Pbx 통합 메시징에서 지원 됩니다. 다음 표에서 통합 메시징에 대 한 직접 SIP 연결을 사용 하 여 지원 되는 IP Pbx를 보여줍니다.

### 직접 SIP 연결을 사용 하는 경우 지원 되는 IP Pbx

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 제조업체</th>
<th>PBX 모델/유형</th>
<th>필수 소프트웨어 버전</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>MX 하나</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>오 라</p></td>
<td><p>5.2.1와 서비스 팩 5 (s p 5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>통신 서버 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>관리자, 통합된 커뮤니케이션 관리자를 호출 합니다.</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## IP Pbx SIP 미디어 게이트웨이 사용 하는 경우 지원

IP Pbx 게이트웨이 통합 메시징에서 지원 되는 SIP 미디어를 사용 하 여 합니다. 다음 표에서 SIP 미디어 게이트웨이의 IP 기능에 IP를 사용 하 여 통합 메시징 연결을 지원 되는 IP Pbx를 보여줍니다.

### IP Pbx SIP 미디어 게이트웨이 사용 하는 경우 지원

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>PBX 제조업체</th>
<th>PBX 모델/유형</th>
<th>SIP 게이트웨이 모델</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>관리자를 호출 4.x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (IP--IP 사용)</p></td>
</tr>
</tbody>
</table>


## Exchange 통합 메시징, Office Communications Server 2007 R2 및 Microsoft Lync Server

온-프레미스 및 하이브리드 배포의 경우 Exchange 통합 메시징 Microsoft Office Communications Server 2007 R2, Microsoft Lync Server 2010 또는 음성 메시지를 제공 하도록 Lync Server 2013 IM (인스턴트 메시징)과 함께 배포할 수 있습니다 사용자 현재 상태, 오디오-비디오 회의 및 통합 된 전자 메일 및 메시징 환경을 조직에서 사용자를 위한 향상 된합니다. 자세한 내용은 다음을 참조 합니다.

  - [Exchange 2013 UM 및 Lync Server 배포 개요](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

Microsoft 통합 커뮤니케이션 개방형 상호 운용성 프로그램 찾기 (영문) 정규화 된 SIP PSTN 게이트웨이 및 IP Pbx 및 프로세스에 대 한 전화 통신에 참가 하도록 인프라 공급 업체를 포함 하 여 엔터프라이즈 전화 통신 인프라에 대 한 하는 방법에 대 한 자세한 내용을 보려면 및 프로그램에 참여 하 고 [Microsoft 통합 커뮤니케이션의 개방형 상호 운용성 프로그램](https://go.microsoft.com/fwlink/p/?linkid=132071)을 참조 하십시오.

