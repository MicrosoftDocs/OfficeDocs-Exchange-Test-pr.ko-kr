---
title: 'Exchange 2010에서 Exchange 2013으로 업그레이드: Exchange 2013 Help'
TOCTitle: Exchange 2010에서 Exchange 2013으로 업그레이드
ms:assetid: c0558850-d583-4c4e-a9a0-0d3593f84fcc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ898583(v=EXCHG.150)
ms:contentKeyID: 51407743
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2010에서 Exchange 2013으로 업그레이드

 

_**적용 대상:**Exchange Online, Exchange Server, Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

Microsoft Exchange Server 2010 및 Exchange Server 2007에는 여러 서버 역할이 있습니다. 클라이언트 액세스, 사서함, 허브 전송, 통합 메시징 및 Edge 전송과 같은 여러 서버 역할이 있습니다. Exchange Server 2013에서는 서버 역할의 수가 5개에서 클라이언트 액세스, 사서함 및 Edge 전송의 3개로 줄었습니다. 통합 메시징은 이제 Exchange 2013에서 제공되는 음성 관련 기능의 구성 요소나 하위 기능으로 간주됩니다. 변경에 대한 자세한 내용은 [Exchange 2013의 새로운 기능](what-s-new-in-exchange-2013-exchange-2013-help.md)의 "Exchange 2013 아키텍처"를 참조하세요.

기존 Exchange 2010 조직을 Exchange 2013으로 업그레이드하는 경우 Exchange 2010 및 Exchange 2013 서버가 조직 내에서 동시 사용되는 특정 기간이 있습니다. 이 모드를 무기한 유지하거나, 모든 리소스를 Exchange 2013에서 Exchange 2010으로 이동한 다음 Exchange 2013 서버를 해제하여 Exchange 2010으로의 업그레이드를 즉시 완료할 수 있습니다. 다음 조건에 해당되는 경우 동시 사용 시나리오를 사용할 수 있습니다.

  - Exchange 2013이 기존 Exchange 조직에 배포되어 있습니다.

  - 두 개 이상의 Microsoft Exchange 버전이 조직에 메시징 서비스를 제공합니다.

기존 Exchange 2003 조직을 직접 Exchange 2013으로 업그레이드할 수는 없습니다. 먼저 Exchange 2003 조직을 Exchange 2007 또는 Exchange 2010 조직으로 업그레이드해야 하며, 그런 다음 Exchange 2007 또는 Exchange 2010 조직을 Exchange 2013으로 업그레이드할 수 있습니다. 조직을 Exchange 2003에서 Exchange 2010으로 업그레이드한 다음 Exchange 2010에서 Exchange 2013으로 업그레이드하는 것이 좋습니다.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>먼저 Exchange 2003의 모든 인스턴스를 조직에서 제거해야 Exchange 2013으로 업그레이드할 수 있습니다.</td>
</tr>
</tbody>
</table>


모든 Exchange 2003 사서함을 Exchange Online으로 마이그레이션할 수 있습니다. 이 방식에 대한 자세한 내용은 [Office 365로 여러 전자 메일 계정을 마이그레이션하는 방법](https://go.microsoft.com/fwlink/p/?linkid=524030)을 참조하세요.

다음 표에서는 Exchange 2013과 Exchange 이전 버전의 동시 사용이 지원되는 시나리오를 보여 줍니다.

### Exchange 2013과 Exchange Server 이전 버전의 동시 사용

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Exchange 버전</th>
<th>Exchange 조직 동시 사용</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 이하 버전</p></td>
<td><p>지원되지 않음</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>다음 최소 Exchange 버전에서 지원됩니다.</p>
<ul>
<li><p>1Edge 전송 서버를 포함하여 조직의 모든 Exchange 2007 서버에 Exchange 2007 SP3(서비스 팩 3)용 업데이트 롤업 10이 설치된 경우</p></li>
<li><p>조직의 모든 Exchange 2013 서버에 Exchange 2013 CU2(누적 업데이트 2)가 설치된 경우.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>다음 최소 Exchange 버전에서 지원됩니다.</p>
<ul>
<li><p>2Edge 전송 서버를 포함하여 조직의 모든 Exchange 2010 서버에 Exchange 2010 SP3이 설치된 경우</p></li>
<li><p>조직의 모든 Exchange 2013 서버에 Exchange 2013 CU2가 설치된 경우.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Exchange 2010 및 Exchange 2007 혼합 조직</p></td>
<td><p>다음 최소 Exchange 버전에서 지원됩니다.</p>
<ul>
<li><p>1Edge 전송 서버를 포함하여 조직의 모든 Exchange 2007 서버에 Exchange 2007 SP3용 업데이트 롤업 10이 설치된 경우</p></li>
<li><p>2Edge 전송 서버를 포함하여 조직의 모든 Exchange 2010 서버에 Exchange 2010 SP3이 설치된 경우</p></li>
<li><p>조직의 모든 Exchange 2013 서버에 Exchange 2013 CU2가 설치된 경우.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Exchange 2007 허브 전송 서버와 Exchange 2013 SP1 Edge 전송 서버 간에 구독을 만들려면 Exchange 2007 허브 전송 서버에 Exchange 2007 SP3 업데이트 롤업 13 이상을 설치해야 합니다.

2   Exchange 2010 허브 전송 서버와 Exchange 2013 SP1 Edge 전송 서버 간에 구독을 만들려면 Exchange 2010 허브 전송 서버에 Exchange 2010 SP3 업데이트 롤업 5 이상을 설치해야 합니다.

## Exchange 2013 및 Exchange 2007과 Exchange 2010의 혼합 모드 동시 사용

사용자의 Active Directory 사이트에 Exchange 2010 및 Exchange 2007이 모두 설치되어 있는 경우 Exchange 2010 및 Exchange 2007 모두에 대한 업그레이드 지침을 따르고 둘 모두에 필요한 업그레이드 단계를 수행하세요.

## 업그레이드 프로세스 개요

아래 표에는 Exchange 2010을 Exchange 2013으로 업그레이드하는 프로세스에 대한 개요를 파악하는 데 도움이 되는 각 주요 작업과 관련된 리소스가 나와 있습니다. 구체적인 단계별 지침은 [검사 목록: Exchange 2010에서 업그레이드](checklist-upgrade-from-exchange-2010-exchange-2013-help.md)를 참조하십시오.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>작업</th>
<th>항목</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 역할 및 구성 요소에 대해 알아보기</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Exchange 2013의 새로운 기능</a></p>
<p><a href="client-access-server-exchange-2013-help.md">클라이언트 액세스 서버</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">사서함 서버</a></p>
<p><a href="mail-flow-exchange-2013-help.md">메일 흐름</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">통합 메시징</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 설치</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 설치</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">설치 마법사를 사용하여 Exchange 2013 Edge 전송 역할 설치</a>(옵션)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Exchange 2013 설치를 확인 합니다.</a></p></td>
</tr>
<tr class="odd">
<td><p>클라이언트 액세스 서버에 디지털 인증서 추가</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Exchange 2013 클라이언트 액세스 서버 구성</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">디지털 인증서 및 SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">디지털 인증서 요청 만들기</a></p></td>
</tr>
<tr class="even">
<td><p>Exchange 관련 가상 디렉터리 구성</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Exchange 가상 디렉터리에 대 한 기본 설정</a></p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010에서 사서함 이동</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Exchange 2013 사서함 이동</a></p></td>
</tr>
<tr class="even">
<td><p>전송 구성 요소 구성</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">Edge 구독</a>(Edge 전송 서버를 설치한 경우에만 필요)</p>
<p><a href="mail-routing-exchange-2013-help.md">메일 라우팅</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">섀도 중복성</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">관리자에 대 한 배달 보고서</a></p></td>
</tr>
<tr class="odd">
<td><p>UM 구성 및 배포</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">통합 메시징에 대 한 계획</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">음성 메일 및 UM 배포</a></p></td>
</tr>
</tbody>
</table>

