---
title: 'Exchange 하이브리드 배포에서의 공유 약속 있음/없음: Exchange 2013 Help'
TOCTitle: Exchange 하이브리드 배포에서의 공유 약속 있음/없음
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 50484636
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange 하이브리드 배포에서의 공유 약속 있음/없음

 

_**적용 대상:**Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-04-29_

온-프레미스 및 Exchange Online 조직에 있는 사용자 간의 약속 있음/없음(일정 약속 있음/없음) 정보 공유는 하이브리드 배포의 주요 이점 중 하나입니다. 두 조직의 사용자가 실제로 동일한 조직에 있는 것처럼 서로의 일정을 볼 수 있습니다. 이 기능 덕분에 효율적으로 쉽게 모임 및 리소스를 예약할 수 있습니다.

온-프레미스 Exchange 조직과 Exchange Online 사이에서 공유 약속 있음/없음 기능을 사용하도록 설정하려면 하이브리드 배포의 여러 가지 구성 요소가 필요합니다.

  - **페더레이션 트러스트**   온-프레미스 및 Office 365 서비스 조직 모두 Azure AD 인증 시스템과의 페더레이션 트러스트를 설정해야 합니다. 페더레이션 트러스트는 Exchange 조직에 대한 매개 변수를 정의하는 Azure AD 인증 시스템과 일대일 관계입니다. 시스템은 온-프레미스 및 Office 365 서비스 조직 사이에서 트러스트 브로커 역할을 할 때 이러한 매개 변수를 사용하여 온-프레미스 및 Exchange Online 조직 사용자 간에 약속 있음/없음 정보를 교환합니다.
    
    시스템과의 페더레이션 트러스트는 계정을 만들 때 Office 365 서비스 조직에 대해 자동으로 구성됩니다. 하이브리드 구성 마법사는 온-프레미스 조직에 대해 Azure AD 인증 시스템과의 기존 페더레이션 트러스트가 있는지 자동으로 확인합니다. 이러한 것이 있을 경우 하이브리드 배포를 지원하는 데 기존 페더레이션 트러스트가 사용됩니다. 해당 트러스트가 없으면 마법사에서는 온-프레미스 조직에 대해 Azure AD 인증 시스템과의 페더레이션 트러스트를 만듭니다. 또한 이 마법사는 하이브리드 구성 마법사 내에서 선택한 모든 도메인을 온-프레미스 조직 페더레이션 트러스트에 추가합니다.
    
    자세한 내용은 [공유](https://technet.microsoft.com/ko-kr/library/dd638083\(v=exchg.150\))를 참조하십시오.

  - **조직 관계**   조직 관계는 온-프레미스 조직과 Exchange Online 조직 모두에 필요하며 하이브리드 구성 마법사에서 자동으로 구성됩니다. 조직 관계는 조직에서 공유되는 약속 있음/없음 정보 수준을 정의합니다.
    
    기본적으로 약속 있음/없음 데이터 액세스 공유 수준은 온-프레미스 조직 및 Exchange Online 조직 관계 모두에 대해 **약속 있음/없음 시간, 제목 및 위치**입니다. 온-프레미스 조직과 Exchange Online 조직 사용자 사이의 약속 있음/없음 공유 액세스를 수정하려면 하이브리드 구성 마법사가 완료된 후 조직 관계 액세스 수준을 수동으로 구성합니다.
    
    자세한 내용은 [공유](https://technet.microsoft.com/ko-kr/library/dd638083\(v=exchg.150\))를 참조하십시오.

조직에 하이브리드 배포를 구성할 경우 모든 시나리오에 공유 약속 있음/없음 일정 액세스가 하이브리드 구성 마법사에서 자동으로 구성됩니다. Azure AD 인증 시스템과의 페더레이션 트러스트 만들기 및 온-프레미스 조직과 Exchange Online 조직에 대한 조직 관계 구성은 하이브리드 배포 요구 사항입니다. 하이브리드 배포에서 온-프레미스 조직과 Exchange Online 조직 사용자 사이에서 약속 있음/없음 공유를 허용하지 않으려는 경우 하이브리드 구성 마법사가 완료된 후 Exchange 관리 셸 및 [Set-HybridConfiguration](https://technet.microsoft.com/ko-kr/library/hh529932\(v=exchg.150\)) cmdlet을 사용하여 약속 있음/없음 공유를 수동으로 사용하지 않도록 설정할 수 있습니다.

다음 표에 나오는 하이브리드 배포 기능에는 페더레이션 트러스트와 조직 관계에 대한 종속성이 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메시징 영역</th>
<th>기능</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>전자 메일 클라이언트</p></td>
<td><ul>
<li><p>메시지 추적</p></li>
<li><p>메일 설명</p></li>
<li><p>여러 사서함 검색</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>규정 준수</p></td>
<td><ul>
<li><p>Exchange Online Archiving</p></li>
<li><p>Exchange 원본 위치 eDiscovery</p></li>
</ul></td>
</tr>
</tbody>
</table>

