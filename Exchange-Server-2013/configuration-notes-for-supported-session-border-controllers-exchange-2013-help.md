---
title: '지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항: Exchange 2013 Help'
TOCTitle: 지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항
ms:assetid: d161f94a-a243-4294-93b3-2bf1dc17b59f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673565(v=EXCHG.150)
ms:contentKeyID: 50556092
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 지원 되는 세션 테두리 컨트롤러에 대 한 구성 참고 사항

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2017-07-25_

SBC(Session border controllers)를 사용하면 공용 WAN 연결을 통해 온-프레미스 전화 통신 네트워크를 Microsoft 데이터센터에 연결할 수 있습니다. SBC는 온-프레미스 IP 네트워크 에지에 위치하며 Microsoft 데이터센터의 보조 SBC에 연결합니다.

SBC에서 온-프레미스 조직과 Microsoft 데이터 센터 간의 모든 트래픽을 암호화하기 위해서는 디지털 인증서를 사용해야 합니다. SBC(Session Border Controller)와 같이 Exchange 하이브리드 및 온라인 배포와 통신하는 데 사용 중인 네트워크 테두리 요소의 디지털 인증서를 확보해야 합니다. 디지털 인증서는 온-프레미스 조직과 Microsoft 데이터 센터 간에 트러스트를 구축하여 상호 전송 계층 보안(상호 TLS)을 사용하도록 합니다. 이 트러스트가 구축되면 사용자의 온-프레미스 조직에 있는 네트워크 테두리 요소와 Microsoft 데이터 센터의 네트워크 테두리 요소가 세션 키를 교환하고 데이터 트래픽을 이 키로 암호화합니다.

하이브리드 또는 온라인 배포에서 UM IP 게이트웨이는 SBC를 나타냅니다. 인증서의 주체 일반 이름은 만든 UM IP 게이트웨이 주소 상자의 FQDN(정규화된 도메인 이름) 값과 일치해야 합니다. 예를 들어 UM IP 게이트웨이에서 FQDN 주소 sbcexternal.contoso.com을 지정하는 경우, 인증서의 주체 이름과 주체 대체 이름에 sbcexternal.contoso.com이 동일하게 들어가야 합니다. 사용하는 이름은 대/소문자를 구분하므로 인증서와 UM IP 게이트웨이의 대/소문자가 서로 일치해야 합니다. Acme Packet SBC를 사용하는 경우 일반 이름이 UM IP 게이트웨이의 FQDN과 일치하지 않으면 403 오류와 함께 호출이 거부됩니다.


> [!NOTE]
> Sbc을는 네트워크에 지에 배치 하기 위한 때문에 방화벽으로도 작동 합니다. 조직 방화벽 뒤에 SBC를 설정 하는 경우 구성 문제를 일으킬 수 하 고 Office 365에 연결 하는 것에 대 한 지원 되지 않습니다.



## 지원되는 Session Border Controller

다음 SBC는 Exchange 하이브리드 및 온라인 배포와의 상호 운용성이 성공적으로 테스트되었습니다. SBC의 기능과 호환성이 다를 수 있으며 SBC를 설정하는 방법이 네트워크의 장비에 따라 다를 수 있습니다. 하이브리드 또는 온라인 배포의 통합 메시징에 대한 특정 구성 참고 사항이 있는지 SBC 제조업체에 문의하십시오.


> [!NOTE]
> 7 월 2018에서 작동 하는 고객 Sbc에서 직접 연결을 통해 타사 PBX 시스템에 대 한 Exchange Online UM 지원 종료 됩니다. 자세한 내용은 Exchange 팀 블로그 <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">한 Exchange Online에서 세션 테두리 컨트롤러에 대 한 지원 중단 통합 메시징</A> 를 참조 하십시오.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>공급업체</strong></p></td>
<td><p><strong>모델</strong></p></td>
<td><p><strong>구성 참고 사항</strong></p></td>
<td><p><strong>Comments</strong></p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.acmepacket.com">Acme Packet</a></p></td>
<td><p>Net-Net 3820 또는 4500</p></td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>전용 SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>전용 SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.audiocodes.com">AudioCodes</a></p></td>
<td><p>Mediant 1000B MSBG</p></td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>SBC 및 IP 게이트웨이</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://www.cisco.com/c/dam/en/us/solutions/collateral/enterprise-networks/unified-access/cube-asr-release-10-0.pdf">Cisco</a></p></td>
<td><p>ASR 1000</p>

> [!NOTE]
> 이상이 설치 되어 또는 IOS 15.4 (3) s 3에 있어야 합니다.


</td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>전용 SBC</p></td>
</tr>
<tr class="even">
<td><p><a href="https://www.ingate.com/">Ingate</a></p></td>
<td><p>SIParator</p></td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>전용 SBC</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.net.com">NET</a></p></td>
<td><p>VX1200 및 VX1800</p></td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>VoIP 게이트웨이 제품에 대한 SBC 옵션</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.sonus.net/">Sonus</a></p></td>
<td><p>SBC 1000/2000 2.2.1 이상</p></td>
<td><p><strong>가 장치를 설정 하는 방법에 대 한 최신 하드웨어 공급 업체에 문의 하십시오.</strong></p></td>
<td><p>전용 SBC</p></td>
</tr>
</tbody>
</table>

