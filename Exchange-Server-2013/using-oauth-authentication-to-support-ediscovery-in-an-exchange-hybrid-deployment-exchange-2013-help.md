---
title: 'OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원: Exchange 2013 Help'
TOCTitle: OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원
ms:assetid: b069f8db-fbe1-4047-ad97-d00172ee6a12
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn497703(v=EXCHG.150)
ms:contentKeyID: 61301917
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

Exchange 2013 하이브리드 조직에서 프레미스 간 eDiscovery 검색을 정상적으로 수행하려면 원본 위치 eDiscovery를 사용하여 온-프레미스 및 클라우드 기반 사서함을 검색할 수 있도록 Exchange 온-프레미스 및 Exchange Online 조직 간에 OAuth(Open Authorization) 인증을 구성해야 합니다. OAuth 인증에서는 Exchange 하이브리드 배포에서 다음 eDiscovery 시나리오가 지원됩니다.

  - 클라우드 기반 보관 사서함에 대해 Exchange Online Archiving을 사용하는 온-프레미스 사서함 검색

  - 같은 eDiscovery 검색에서 온-프레미스 사서함 및 클라우드 기반 사서함 검색

eDiscovery를 지원하도록 OAuth 인증을 구성하는 단계별 지침은 [Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)을 참조하세요.

## OAuth 인증이란?

OAuth 인증은 응용 프로그램이 서로 인증할 수 있도록 하는 서버 간 인증 프로토콜입니다. OAuth 인증을 사용할 경우 사용자 자격 증명 및 암호가 한 컴퓨터에서 다른 컴퓨터로 전달되지 않습니다. 대신 인증 및 권한 부여는 보안 토큰이 교환되면서 수행됩니다. 이러한 토큰은 일정 시간 동안 특정 리소스 집합에 대한 액세스 권한을 부여합니다.

OAuth 인증에는 보통 세 가지 요소, 즉 권한 부여 서버 하나와 서로 통신해야 하는 두 개의 영역이 사용됩니다. 보안 토큰은 보안 토큰 서버라고도 하는 권한 부여 서버에서 서로 통신해야 하는 두 영역에 발급됩니다. 이러한 토큰은 특정 영역에서 시작되는 통신을 다른 영역에서 신뢰해야 하는지를 확인합니다. 온-프레미스 Exchange 조직 및 Exchange Online 간에 OAuth 인증을 사용하면 Office 365 조직의 Microsoft Azure Active Directory ACS(액세스 제어 서비스)에서 권한 부여 서버의 기능이 제공됩니다. 예를 들어 크로스-프레미스 eDiscovery 검색 중에 Azure ACS는 Exchange 온-프레미스 조직의 관리자 또는 규정 준수 담당자가 Exchange Online 조직의 사서함에 액세스할 수 있는지 확인하거나 그 반대의 경우를 확인하는 토큰을 발급합니다.

## 하이브리드 배포의 eDiscovery 시나리오

다음 표에서는 Exchange 하이브리드 배포에서 OAuth 인증을 요구하는 eDiscovery 시나리오를 식별합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>eDiscovery 시나리오</th>
<th>OAuth 인증이 필요합니까?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 온-프레미스 조직에서 시작된 동일한 eDiscovery 검색에서 Exchange 온-프레미스 사서함 및 Exchange Online 사서함을 검색합니다. 예를 들어 단일 eDiscovery 검색에서 조직의 모든 사서함을 검색할 수 있습니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>클라우드 기반 보관 사서함에 대해 Exchange Online Archiving을 사용하는 Exchange 온-프레미스 사서함을 검색합니다. 원본 위치 eDiscovery를 사용할 경우 기본 사서함 및 보관 사서함이 모두 검색됩니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="odd">
<td><p>관리자 또는 규정 준수 담당자가 Exchange 온-프레미스 조직에서 시작된 eDiscovery 검색으로부터 Exchange Online 사서함을 검색합니다.</p></td>
<td><p>예</p></td>
</tr>
<tr class="even">
<td><p>관리자 또는 규정 준수 담당자가 Exchange 온-프레미스 조직에서 시작된 eDiscovery 검색을 사용하여 온-프레미스 사서함을 검색합니다.</p></td>
<td><p>아니요</p>

> [!NOTE]
> 앞서 설명한 것처럼 온-프레미스 사서함이 클라우드 기반 보관 사서함으로 구성된 경우 OAuth 인증이 필요합니다.


</td>
</tr>
<tr class="odd">
<td><p>Office 365 사용자 계정으로 로그인한 Office 365 테넌트 관리자 또는 규정 준수 관리자가 Exchange Online 또는 SharePoint Online의 eDiscovery 센터에서 시작된 eDiscovery 검색으로부터 Exchange Online 사서함을 검색합니다.</p></td>
<td><p>아니요</p></td>
</tr>
</tbody>
</table>


## eDiscovery를 지원하도록 OAuth 인증 구성

앞서 설명한 것처럼 Exchange 하이브리드 배포에서 eDiscovery를 지원하도록 OAuth 인증을 구성하기 위한 지침을 보려면 [Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)을 참조하세요.

Exchange 하이브리드 배포에 대해 OAuth가 구성되지 않은 경우 동일한 eDiscovery 검색에서 eDiscovery를 사용하여 Exchange 온-프레미스 및 Exchange Online 사서함을 둘 다 검색할 수는 없습니다. 온-프레미스 조직에서 시작된 eDiscovery 검색으로부터 온-프레미스 사서함을 검색해야 합니다. 마찬가지로 Exchange Online 조직에서 시작된 eDiscovery 검색으로부터 또는 SharePoint Online의 eDiscovery 센터를 사용하여 Exchange Online 사서함을 검색하는 것만 가능합니다. 또한 해당 보관 사서함이 Exchange Online 또는 Exchange Online Archiving 조직에 있는 경우 기본 온-프레미스 사서함을 검색할 수 없습니다.

## 추가 정보

  - OAuth을 사용하여 SharePoint 2013 및 Lync Server 2013과 같은 기타 응용 프로그램이 Exchange 2013에서 인증되도록 할 수도 있습니다. 자세한 내용은 [SharePoint 2013 및 Lync 2013 OAuth 인증 구성](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)을 참조하세요.

  - 관리자 및 규정 준수 담당자가 SharePoint 2013의 eDiscovery 센터를 사용하여 Exchange 2013 사서함을 검색할 수 있도록 Exchange 2013 및 SharePoint 2013 사이에 서버 간 인증을 구성할 수 있습니다. 자세한 내용은 [SharePoint eDiscovery 센터에 대한 Exchange 구성](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)을 참조하세요.

  - Exchange 2013 에서 하이브리드 구성 마법사를 사용 하 여 Exchange 하이브리드 배포를 구성할 수 있습니다. 사용자 지정, 단계별 하이브리드 배포 구성 검사 목록에 대 한 [Exchange Server 배포 도우미](https://go.microsoft.com/fwlink/p/?linkid=277105)를 참조 하십시오.

