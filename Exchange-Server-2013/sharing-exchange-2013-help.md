---
title: '공유: Exchange 2013 Help'
TOCTitle: 공유
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 50482442
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공유

 

_**적용 대상:** Exchange Server 2013, Outlook 2013_

_**마지막으로 수정된 항목:** 2015-02-27_

프로젝트에서 공동 작업을 하거나 사교 모임을 계획하기 위해 다른 조직의 사용자 또는 친구 및 가족과 일정을 조정해야 할 수 있습니다. Exchange 2013을 사용하는 경우 관리자가 다양한 일정 액세스 수준을 설정하여 여러 업체가 서로 공동 작업을 하고 사용자들이 일정을 서로 공유하도록 할 수 있습니다. 기업 간 일정 공유는 *조직 관계*를 만들어 설정합니다. 사용자 간 일정 공유는 *공유 정책*을 적용하여 설정합니다.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



**목차**

Sharing Scenarios in Exchange 2013

Limitations of free/busy sharing

Firewall considerations for federated sharing

Coexistence with Exchange 2010

Coexistence with Exchange 2007

Sharing Documentation

## Exchange 2013의 공유 시나리오

Exchange 2013에서는 다음과 같은 공유 시나리오가 지원됩니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>공유 목표</th>
<th>사용할 설정</th>
<th>요구 사항</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Office 365 조직과 일정 공유</p></td>
<td><p>조직 관계</p></td>
<td><p>Office 365 조직이 구성할 수 있는 상태여야 합니다. 온-프레미스 Exchange 관리자가 클라우드와의 인증 관계(&quot;페더레이션&quot;이라고도 함)를 설정해야 하며 최소 소프트웨어 요구 사항을 충족해야 합니다. 페더레이션을 설정하는 방법에 대한 자세한 내용은 <a href="federation-exchange-2013-help.md">페더레이션</a>을 참조하세요.</p></td>
</tr>
<tr class="even">
<td><p>다른 온-프레미스 Exchange 조직과 일정 공유</p></td>
<td><p>조직 관계</p></td>
<td><p>두 온-프레미스 Exchange 조직이 모두 페더레이션을 설정해야 하며 최소 소프트웨어 요구 사항을 충족해야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>인터넷 사용자와 Exchange 사용자의 일정 공유</p></td>
<td><p>공유 정책</p></td>
<td><p>없음(구성 가능)</p></td>
</tr>
<tr class="even">
<td><p>다른 Exchange 온-프레미스 사용자와 Exchange 사용자의 일정 공유</p></td>
<td><p>공유 정책</p></td>
<td><p>두 온-프레미스 Exchange 조직이 모두 페더레이션을 설정해야 하며 최소 소프트웨어 요구 사항을 충족해야 합니다.</p></td>
</tr>
</tbody>
</table>


다음 표에서는 조직 관계와 공유 정책의 차이를 보여 줍니다.

### 조직 관계와 공유 정책 비교

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>기능</th>
<th>조직 관계</th>
<th>공유 정책</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>조직에 페더레이션 트러스트 필요</p></td>
<td><p>예</p></td>
<td><p>예(다른 페더레이션 도메인 조직과 공유하는 경우). 인터넷 공유 정책에 필요하지 않음</p></td>
</tr>
<tr class="even">
<td><p>외부 도메인 페더레이션 권장</p></td>
<td><p>예</p></td>
<td><p>예(다른 페더레이션 도메인 조직과 공유하는 경우). 인터넷 공유 정책에 필요하지 않음</p></td>
</tr>
<tr class="odd">
<td><p>여러 사용자가 있는 집합에 외부 조직과의 약속 있음/없음 정보(제목 및 위치 포함) 공유 허용</p></td>
<td><p>예</p></td>
<td><p>아니요</p></td>
</tr>
<tr class="even">
<td><p>약속 있음/없음 정보와 일정 폴더 공유 허용</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>약속 있음/없음 정보(제목 및 본문 포함)와 일정 폴더 공유 허용</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>사용자가 외부 받는 사람에게 공유 초대를 보내야 함</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>액세스 방법 제공</p></td>
<td><p>요청이 있으면 클라이언트 액세스 서버가 외부 조직의 클라이언트 액세스 서버에 액세스하여 외부 사용자의 약속 있음/없음 정보를 검색합니다.</p></td>
<td><p>클라이언트 액세스 서버가 외부 조직의 클라이언트 액세스 서버에 액세스하여 외부 사용자의 일정 폴더를 구독합니다. 인터넷 공유 정책의 경우 외부 사용자가 클라이언트 액세스 서버의 제한된 URL 또는 공용 URL을 액세스합니다.</p></td>
</tr>
<tr class="even">
<td><p>모든 외부 도메인에 적용할 수 있음</p></td>
<td><p>아니요(두 Exchange 2013 조직 사이의 일대일 관계)</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>사용자에게 외부 받는 사람과 다른 공유 경험 제공</p></td>
<td><p>아니요</p></td>
<td><p>예, 적용된 공유 정책에 따라</p></td>
</tr>
<tr class="even">
<td><p>일부 사용자에 대해 공유를 사용하지 않도록 설정</p></td>
<td><p>예, 조직 관계에 보안 메일 그룹 지정</p></td>
<td><p>예, 적용된 공유 정책을 사용하지 않도록 설정</p></td>
</tr>
<tr class="odd">
<td><p>사서함이 Exchange 2013 사서함 서버에 있어야 함</p></td>
<td><p>아니요</p></td>
<td><p>예</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 약속 있음/없음 공유의 제한 사항

Exchange 조직 간 약속 있음/없음 정보 공유 시 다음 제한 사항이 적용됩니다.

1.  **Outlook Web Access 2003**   Exchange 2003 조직의 사용자가 Outlook Web Access를 사용하여 원격 Exchange 2013 조직의 사용자에 대한 약속 있음/없음에 액세스하면 요청이 실패합니다. Exchange 2003의 Outlook Web Access 연결은 약속 있음/없음 시스템 폴더에 대한 WebDAV(Web-based Distributed Authoring and Versioning) 연결을 만들어 원격 사용자에 대한 약속 있음/없음 정보를 검색할 수 없습니다. Exchange 2013이 WebDAV 연결을 지원하지 않으므로 Exchange 2003 서버는 Outlook Web Access 요청을 처리하기 위해 Exchange 2013 CAS 서버의 External (FYDIBOHF25SPDLT)에 연결할 수 없습니다. Outlook 클라이언트의 경우 External (FYDIBOHF25SPDLT)에 연결할 때 WebDAV 대신 MAPI를 사용하므로 이 제한 사항이 적용되지 않습니다.

2.  **WAN(광역 네트워크) 대기 시간**   Exchange 2003 조직에서는 모든 약속 있음/없음 폴더의 복제본이 Exchange 2010 SP2 이상의 사서함 서버에 있어야 합니다. Exchange 2003 공용 폴더 데이터베이스가 여러 실제 사이트에 있는 환경에서는 내부 약속 있음/없음 쿼리가 동일한 실제 사이트에 없는 Exchange 2010 공용 폴더 데이터베이스에 액세스하기 위해 WAN 링크를 트래버스해야 하는 경우 과도한 대기 시간 및 성능 문제가 발생할 수 있습니다.

3.  **약속 있음/없음 정보 기간**   요청된 약속 있음/없음 정보 기간의 불일치로 인해 Exchange 2013 조직에서 Exchange 2007 조직으로의 약속 있음/없음 정보 요청이 실패할 수 있습니다. 기본적으로 Exchange 2007은 42일간의 약속 있음/없음 정보에 대한 가용성 요청을 수락하고 Exchange 2013은 62일간의 약속 있음/없음 정보를 요청할 수 있습니다. 요청이 Exchange 2007에서 적용한 기본 제한인 42일을 초과하면 요청이 실패합니다.
    
    아래의 단계를 수행하여 Exchange 2007 CAS 서버가 보다 긴 약속 있음/없음 정보 요청 기간을 수락하도록 구성합니다.
    
    1.  모든 Exchange 2007 CAS 서버에서 메모장과 같은 텍스트 편집기로 다음 파일을 엽니다. \<Exchange Installation Path\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config
        

        > [!WARNING]
        > Web.config 파일을 변경하기 전에 파일의 복사본을 만들어 안전한 위치에 저장해 둡니다.

    
    2.  web.config 파일에서 **appSettings** 섹션을 찾습니다.
    
    3.  새 키 \&quot;\<add key="maximumQueryIntervalDays" value="62" /\>\&quot;를 추가하고 web.config 파일을 저장합니다.
        

        > [!NOTE]
        > maximumQueryIntervalDays 값은 기본적으로 표시되지 않습니다. 이 값이 표시되지 않으면 Exchange 2007이 기본 간격인 42일을 사용하는 것입니다.

    
    4.  모든 Exchange 2007 CAS 서버에서 Microsoft IIS(인터넷 정보 서비스)를 중지했다가 다시 시작합니다.

4.  **온-프레미스 사용자와 클라우드 사용자가 모두 있는 Exchange 조직**   Microsoft Office 365가 있는 하이브리드 배포에 구성된 다른 Exchange 조직과의 일정 공유를 설정하면 클라우드로 이동된 Office 365 기반 사용자 또는 원격 사용자에 대한 약속 있음/없음 가용성 조회가 실패합니다. Exchange 조직의 조직 관계는 Office 365 기반 Exchange Online 조직이 아닌 원격 온-프레미스 Exchange 조직과의 관계이므로 약속 있음/없음 요청은 Office 365 기반 사용자를 쿼리할 수 없습니다. Exchange 2013은 온-프레미스 조직을 통해 Office 365 서비스로 이러한 가용성 요청을 프록시하는 기능을 지원하지 않습니다.

일반 Exchange 배포 간에 약속 있음/없음 공유를 구성하는 방법에 대한 자세한 내용은 [Exchange 조직 간의 페더레이션 공유 구성](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md) 항목을 참조하십시오.

## 페더레이션 공유에 대한 방화벽 고려 사항

페더레이션된 공유 기능을 사용 하려면 HTTPS를 사용 하 여 조직에서 클라이언트 액세스 서버 아웃 바운드 인터넷에 액세스할 수 있는 합니다. 조직에서 모든 Exchange 2013 사서함 서버에 아웃 바운드 HTTPS 액세스 (TCP 포트 443)를 허용 해야 합니다.

조직의 약속 있음/없음 정보에 대한 외부 조직 액세스를 허용하려면 인터넷에 클라이언트 액세스 서버를 하나 이상 게시해야 합니다. 그러려면 인터넷에서 클라이언트 액세스 서버로 인바운드 HTTPS 액세스를 해야 합니다. 인터넷에 클라이언트 액세스 서버를 게시하지 않은 Active Directory 사이트의 클라이언트 액세스 서버도 인터넷에서 액세스가 가능한 다른 Active Directory 사이트의 클라이언트 액세스 서버를 사용할 수 있습니다. 인터넷에 게시되지 않은 클라이언트 액세스 서버는 외부 조직에 표시되는 URL로 설정된 웹 서비스 가상 디렉터리의 외부 URL이 있어야 합니다.

맨 위로 이동

## Exchange 2010과 함께 사용

Exchange 2010 서버와 Exchange 2013 서버가 모두 포함된 조직에서는 Exchange 2010 사서함 서버에 사서함이 있는 사용자가 조직 관계를 사용하여 외부 Exchange 2013 페더레이션 도메인 조직의 받는 사람과 약속 있음/없음 정보를 공유할 수 있습니다. Exchange 2010 클라이언트 액세스 및 사서함 서버에서 SP2 이상을 실행하고 있어야 하고 Exchange 2010 조직에 Exchange 2013 클라이언트 액세스 서버가 하나 이상 있어야 합니다.

## Exchange 2007와 함께 사용

Exchange 2013 및 Exchange 2007 서버 모두가 포함된 조직에서 Exchange 2007 사서함 서버에 사서함이 있는 사용자는 조직 관계를 사용하여 외부 페더레이션 도메인 조직의 받는 사람과 약속 있음/없음 정보를 공유할 수 있습니다. 사서함 서버에서 Exchange 2007 SP2 이상을 실행하고 있어야 하며 Exchange 조직에 Exchange 2013 클라이언트 액세스 서버가 하나 이상 있어야 합니다. 조직에 단일 Exchange 2013 클라이언트 액세스 서버를 도입하여 조직 관계를 사용하면 약속 있음/없음 정보를 동기화하며 GAL 동기화를 요구하는 솔루션보다 더 강력한 솔루션을 제공할 수 있습니다.

Outlook 2010 또는 Outlook Web App를 사용하여 Exchange 2007 서버에서 모임 일정을 잡을 경우 Exchange 2007 서버에 사서함이 있는 사용자는 외부 조직에 있는 사용자의 약속 있음/없음 정보를 볼 수 있습니다. Exchange 2007 사서함의 약속 있음/없음 정보는 외부 조직의 받는 사람에게 표시됩니다.

공유 정책은 Exchange 2013 사서함 사용자에게 할당됩니다. 공유 정책을 사용하려면 사서함이 Exchange 2013 사서함 서버에 있어야 합니다. 공유 초대를 생성하거나 공유 초대에 응답하는 일에는 Outlook 2010 및 Outlook Web App 클라이언트만 사용할 수 있습니다.

맨 위로 이동

## 공유 설명서

다음 표는 Exchange 2013의 공유에 대해 알아보고 공유를 관리하는 데 유용한 항목에 대한 링크를 보여 줍니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>항목</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="federation-exchange-2013-help.md">페더레이션</a></p></td>
<td><p>사용자가 외부 받는 사람과 일정 정보를 손쉽게 공유할 수 있는 방법인 공유를 지원하는 기본 트러스트 인프라에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="organization-relationships-exchange-2013-help.md">조직 관계</a></p></td>
<td><p>약속 있음/없음 일정 공유를 사용할 수 있도록 하는 Exchange 조직 간의 일대일 관계에 대해 자세히 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="sharing-policies-exchange-2013-help.md">공유 정책</a></p></td>
<td><p>공유를 사용할 수 있도록 하는 사용자 간 정책에 대해 자세히 알아봅니다.</p>
<p></p></td>
</tr>
</tbody>
</table>

