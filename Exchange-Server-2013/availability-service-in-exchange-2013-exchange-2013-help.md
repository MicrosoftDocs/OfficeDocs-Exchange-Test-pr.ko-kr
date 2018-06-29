---
title: 'Exchange 2013의 가용성 서비스: Exchange 2013 Help'
TOCTitle: Exchange 2013의 가용성 서비스
ms:assetid: 9722dea2-2bf8-437c-85c0-3ab65b8a07b9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232134(v=EXCHG.150)
ms:contentKeyID: 52058118
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013의 가용성 서비스

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Exchange 2013 가용성 서비스는 Microsoft Outlook 및 Outlook Web App 클라이언트에서 약속 있음/없음 정보를 사용할 수 있게 해줍니다. 가용성 서비스는 안전하고 일관된 최신 약속 있음/없음 정보를 제공하여 정보 근로자의 일정 및 모임 예약 환경을 향상시킵니다.

Outlook 및 Outlook Web App은 가용성 서비스를 사용하여 다음 작업을 수행합니다.

  - Exchange 2013 사서함에 대한 현재 약속 있음/없음 정보 검색

  - 다른 Exchange 2013 조직에서 현재 약속 있음/없음 정보 검색

  - 이전 버전의 Exchange가 설치된 서버의 사서함에 대해 공용 폴더에서 게시된 약속 있음/없음 정보 검색

  - 참석자 작업 시간 보기

  - 모임 시간 제안 표시

**목차**

Overview of the Availability service

Information about away status

Availability service API

Availability service Network Load Balancing

Methods used to retrieve free/busy information

## 가용성 서비스의 개요

가용성 서비스 Exchange 2013, Exchange 2010 또는 Exchange 2007 에 있는 사용자에 대 한 대상 사서함에서 직접 약속 있음/없음 정보를 검색 하 고 Exchange 의 이전 버전에서 사용자에 대 한 약속 있음/없음 정보를 검색 하도록 구성할 수 있습니다. Outlook 2007 를 실행 하는 모든 클라이언트 또는 가용성 서비스 약속 있음/없음 정보를 검색 하는데 사용 되는 이상을 Exchange 2007, Exchange 2010 또는 Exchange 2013 사서함이 있는 토폴로지입니다.

Outlook은 Exchange 자동 검색 서비스를 사용하여 가용성 서비스의 URL을 가져옵니다. 자동 검색 서비스에 대한 자세한 내용은 [Autodiscover 서비스](autodiscover-service-for-exchange-2013.md)를 참조하십시오.

Exchange 관리 셸을 사용하여 가용성 서비스를 구성할 수 있습니다. EAC(Exchange 관리 센터)를 사용하여 가용성 서비스를 구성할 수는 없습니다.

## 부재 중 상태에 대한 정보

가용성 서비스는 또한 사용자가 휴가로 부재 중이거나 장기간 출근하지 않는 경우 보내는 자동 회신 메시지에 대한 액세스를 제공합니다.

정보 근로자는 전자 메일 메시지에 응답할 수 없는 경우 Outlook 및 Outlook Web App의 자동 회신 기능(이전의 부재 중 기능)을 사용하여 이를 다른 사람에게 알립니다. 이 기능은 정보 근로자와 관리자가 자동 회신 메시지를 설정하고 관리하는 작업을 한결 손쉽게 수행할 수 있게 해줍니다.

## 가용성 서비스 API

가용성 서비스는 Exchange 2013 프로그래밍 인터페이스의 일부입니다. 가용성 서비스는 개발자가 통합을 목적으로 타사 도구를 기록할 수 있도록 웹 서비스로 사용할 수 있습니다.

## 가용성 서비스 네트워크 부하 분산

가용성 서비스를 실행하는 클라이언트 액세스 서버에서 NLB(네트워크 부하 분산)를 사용하면 약속 있음/없음 정보를 많이 사용하는 사용자에 대한 성능과 안정성이 향상됩니다. Outlook에서는 자동 검색 서비스를 사용하여 가용성 서비스 URL을 찾습니다. 가용성 서비스에 NLB을 사용하려면 구성을 변경해야 합니다.

인트라넷에서는 내부 URL이 사용되고 인터넷에서는 외부 URL이 사용됩니다. 내부 및 외부 트래픽 모두에 대해 동일한 URL을 사용하려면 DNS가 내부 트래픽을 내부 URL로 직접 라우팅하도록 올바르게 구성되어 있는지 확인합니다. 또한 URL을 내부와 외부에서 액세스할 수 있는지도 확인해야 합니다. 자동 검색 및 가용성 서비스가 작동하려면 mail.\<*도메인 이름*\>.com 및 autodiscover.mail.\<*도메인 이름*\>.com이 부하 분산 솔루션의 VIP(가상 IP)를 가리키도록 DNS를 구성해야 합니다. 여기서 \<*도메인 이름*\>은 사용자 도메인의 이름입니다.


> [!NOTE]
> 자세한 내용은 <A href="https://go.microsoft.com/fwlink/p/?linkid=45959">네트워크 부하 분산 기술 참조 (영문)</A> 및 <A href="https://go.microsoft.com/fwlink/p/?linkid=49315">네트워크 부하 분산 클러스터</A>를 참조 하십시오. 타사 부하 분산 소프트웨어 웹사이트에 대 한 검색할 수 있습니다.



## 약속 있음/없음 정보를 검색하는 데 사용되는 방법

다음 표에서는 다양한 단일 포리스트 토폴로지에서 약속 있음/없음 정보를 검색하는 데 사용하는 여러 가지 방법을 보여줍니다.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>클라이언트</th>
<th>약속 있음/없음 정보를 검색하는 사서함에서 실행되는 버전</th>
<th>대상 사서함에서 실행되는 버전</th>
<th>약속 있음/없음 정보 검색 방법</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013</p></td>
<td><p>Exchange 2013, Exchange 2010 또는 Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 또는 Exchange 2007</p></td>
<td><p>가용성 서비스가 대상 사서함에서 약속 있음/없음 정보를 읽습니다.</p></td>
</tr>
<tr class="even">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 또는 Exchange 2007</p></td>
<td><p>Exchange 2010 또는 Exchange 2007</p></td>
<td><p>가용성 서비스가 대상 사서함에서 약속 있음/없음 정보를 읽습니다.</p></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Exchange 2010 또는 Exchange 2007</p></td>
<td><p>Exchange 2003</p></td>
<td><p>가용성 서비스가 Exchange 2003 사서함의 /public 가상 디렉터리에 대해 HTTP 연결을 수행합니다.</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013, Exchange 2010 또는 Exchange 2007</p></td>
<td><p>Exchange 2013, Exchange 2010 또는 Exchange 2007</p></td>
<td><p>Outlook Web App Exchange 2010 에서 또는 Exchange 2007 에서 Outlook Web Access 가용성 서비스 API를 호출 하면 대상 사서함에서 약속 있음/없음 정보를 읽습니다.</p></td>
</tr>
</tbody>
</table>

