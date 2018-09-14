---
title: 'SharePoint 및 Lync와의 통합: Exchange 2013 Help'
TOCTitle: SharePoint 및 Lync와의 통합
ms:assetid: 056b29f6-e0e9-4974-b763-002518857a93
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150480(v=EXCHG.150)
ms:contentKeyID: 50482417
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SharePoint 및 Lync와의 통합

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013에는 Microsoft SharePoint 2013 및 Microsoft Lync 2013과 통합되는 많은 기능이 포함되어 있습니다. 이러한 제품은 사이트 사서함을 사용하는 엔터프라이즈 eDiscovery 및 공동 작업과 같은 시나리오가 가능해지도록 하는 여러 기능들을 제공합니다.

## 보관, 유지 및 eDiscovery

전자 메일과 문서를 보관하고 규정 준수 및 비즈니스 요구 사항을 충족하는 데 필요한 기간 동안 보존하며 eDiscovery 요청을 수행하기 위해 빠르게 검색하는 기능은 대부분의 조직에서 매우 중요합니다. Exchange 2013, SharePoint 2013과 Lync Server 2013이 함께 제공하는 통합 보관, 유지 및 eDiscovery 기능을 통해 Exchange 사서함, SharePoint 문서 및 웹 사이트, 보관된 Lync 콘텐츠의 중요한 데이터를 원본 위치에 보존할 수 있습니다. SharePoint 2013의 eDiscovery Center를 사용하면 권한 있는 검색 관리자가 이러한 저장소의 콘텐츠에 대한 eDiscovery 검색을 수행하고 검색 결과를 미리 보며 법률 검토를 위해 데이터를 내보낼 수 있습니다.

## Exchange 2013에 Lync Server 2013 콘텐츠 보관

조직에 Lync Server 2013과 Exchange 2013을 함께 배포한 경우 사용자의 Exchange 2013 사서함에 있는 공유 프레젠테이션 또는 문서 같은 인스턴트 메시징 및 온라인 모임 콘텐츠를 보관하도록 Lync를 구성할 수 있습니다. Exchange 2013에 Lync 데이터를 보관하면 해당 데이터에 보존 정책을 적용할 수 있습니다. 보관된 Lync 콘텐츠는 eDiscovery 검색에서도 표시됩니다. Lync 보관 및 배포 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [보관에 대 한 계획](https://go.microsoft.com/fwlink/p/?linkid=265005)

  - [보관 배포](https://go.microsoft.com/fwlink/p/?linkid=265006)

## SharePoint 2013 eDiscovery Center를 사용하여 Exchange, SharePoint 및 Lync 데이터 검색

Exchange 2013에서는 SharePoint 2013을 통해 페더레이션 검색 API를 사용하여 Exchange 사서함 콘텐츠를 검색할 수 있습니다. SharePoint 2013이 제공하는 eDiscovery Center를 사용하면 권한 있는 담당자가 eDiscovery를 수행할 수 있습니다. Microsoft Search Foundation이 Exchange 2013과 SharePoint 2013 모두에 제공하는 공통 인덱싱 및 검색 인프라를 통해 두 응용 프로그램 모두에서 동일한 쿼리 구문을 사용할 수 있습니다. 따라서 Exchange 2013의 원본 위치 eDiscovery를 사용하여 수행된 검색의 결과와 동일한 Exchange 2013 콘텐츠가 SharePoint 2013에서 수행된 eDiscovery 검색의 결과로 반환됩니다. 또한 SharePoint 2013 eDiscovery Center를 사용하면 Exchange 2013 콘텐츠를 PST 파일로 내보내기를 포함하여 eDiscovery 검색의 결과로 반환된 콘텐츠를 내보낼 수 있습니다.

자세한 내용은 다음 항목을 참조하십시오.

  - [원본 위치 eDiscovery](in-place-ediscovery-exchange-2013-help.md)

  - [원본 위치 유지 및 소송 보존](https://docs.microsoft.com/ko-kr/exchange/security-and-compliance/in-place-and-litigation-holds)

  - [SharePoint 2013에서 Configure eDiscovery](https://go.microsoft.com/fwlink/p/?linkid=257727)

  - [SharePoint Server 2013에서 eDiscovery의 새로운 란](https://go.microsoft.com/fwlink/?linkid=275091)

  - [SharePoint eDiscovery 센터에 대한 Exchange 구성](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)

## 사이트 사서함

많은 조직에서 정보는 서로 다른 인터페이스를 통해 액세스되는 두 가지 저장소에 상주합니다. 즉, 전자 메일은 Microsoft Exchange에 상주하고 문서는 SharePoint에 상주합니다. 따라서 사용자 환경이 연결되지 않고 공동 작업의 효율이 저하됩니다. 사이트 사서함을 사용하면 사용자가 Exchange 전자 메일과 SharePoint 문서를 함께 불러와서 공동 작업을 효과적으로 수행할 수 있습니다. 사용자의 경우 사이트 사서함은 중앙 서류 보관함 역할을 하면서 사이트 구성원만 액세스하여 편집할 수 있는 프로젝트 전자 메일 및 문서 보관 위치를 제공합니다. 사이트 사서함은 Outlook 2013에 표시되므로, 사용자는 관심이 있는 프로젝트에 대한 전자 메일과 문서에 쉽게 액세스할 수 있습니다. 또한 SharePoint 사이트 자체에서도 동일한 콘텐츠에 액세스할 수 있습니다.

사이트 사서함 범위에 포함되는 콘텐츠는 원래 속한 위치에 보관됩니다. Exchange는 전자 메일을 저장하여, 사용자에게 자신의 사서함에 대해 매일 사용하는 것과 동일한 전자 메일 대화용 메시지 보기를 제공합니다. SharePoint에서는 문서를 저장하고 문서 공동 작성과 버전 관리를 테이블로 불러와 수행할 수 있습니다. Exchange는 SharePoint에서 필요한 만큼의 메타데이터를 동기화하여 Outlook에 문서 보기를 만듭니다(예: 문서 제목, 마지막으로 수정한 날짜, 마지막으로 수정한 작성자, 크기).

사이트 사서함은 SharePoint 2013에서 프로비전되고 관리됩니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [사이트 사서함](site-mailboxes-exchange-2013-help.md)

  - [SharePoint Server 2013에서 사이트 사서함 구성](https://go.microsoft.com/fwlink/p/?linkid=258264)

## 통합 연락처 저장소

UCS(통합 연락처 저장소)는 Microsoft Office 제품에 일관성 있는 연락처 환경을 제공하는 기능입니다. 이 기능을 사용하면 Lync, Exchange, Outlook 및 Outlook Web App에서 전반적으로 동일한 연락처 정보를 사용할 수 있도록 사용자의 Exchange 2013 사서함에 모든 연락처 정보를 저장할 수 있습니다.

Lync Server 2013 Exchange 2013 사용 하는 환경에 설치 되어 두 서버-서버 인증을 구성한 후 사용자가 Lync Server 2013 에서 Exchange 2013 으로 기존 연락처의 마이그레이션을 시작할 수 있습니다. 자세한 내용은 [계획 및 배포 통합 연락처 저장소](https://go.microsoft.com/fwlink/p/?linkid=275092)를 참조 합니다.

## 사용자 사진

사용자 사진 기능은 고해상도 사용자 사진 Outlook, Outlook Web App, SharePoint 2013, Lync 2013 및 모바일 전자 메일 클라이언트를 포함 하는 클라이언트 응용 프로그램에서 액세스할 수 있는 Exchange 2013 에 저장할 수 있습니다. 저해상도 사진 Active Directory 에 저장 됩니다. 통합 연락처 저장소와 함께 하 사용자 사진 사용자 사진 및 여러가지 방법으로 추가 하 고 관리 하는 자체 포함 하도록 각 응용 프로그램을 요구 하지 않고 클라이언트 응용 프로그램에서 사용할 수 있는 일관 된 사용자 프로필 사진 유지 하기 위해 조직의 허용 합니다. 사용자가 자신의 사진을 Outlook Web App, SharePoint 2013 또는 Lync 2013 를 사용 하 여 관리할 수 있습니다. Outlook Web App에서 사진을 관리 하는 방법에 대 한 세부 정보를 [내 계정](https://go.microsoft.com/fwlink/p/?linkid=269646)을 참조 하십시오.

## Outlook Web App에서 Lync 현재 상태 확인

Lync Server 2013을 설치한 Exchange 2013 환경에서는 사용자가 Outlook Web App에서 현재 상태 정보를 확인할 수 있게 구성할 수 있습니다. 사용자는 Outlook Web App의 탐색 창에서 자신의 인스턴트 메시징 연락처와 그룹을 확인하고 Outlook Web App에서 인스턴트 메시징 세션을 시작하거나 인스턴트 메시징 세션에 응답하며 자신의 인스턴트 메시징 연락처와 그룹을 관리할 수 있습니다.

## OAuth 인증

Exchange 2013, SharePoint 2013 및 Lync Server 2013은 서버 간 인증에 OAuth 인증 프로토콜을 사용하여 앞서 설명된 풍부한 제품 간 기능을 제공합니다. 동일한 인증 프로토콜을 사용하면 이러한 응용 프로그램 간에 매끄럽고 안전하게 인증을 수행할 수 있습니다. 인증 메커니즘은 액세스 요청이 사용자 컨텍스트에서 이루어지는 연결된 계정 및 사용자 가장의 컨텍스트를 사용하는 응용 프로그램으로 인증을 지원합니다.

OAuth은 대부분의 웹사이트 및 웹 서비스에서 사용 되는 표준 인증 프로토콜입니다. 클라이언트 사용자 이름 및 암호를 제공 하지 않고도 리소스 서버에서 제공 하는 리소스에 액세스할 수 있도록 합니다. 인증은 액세스 토큰으로 클라이언트를 제공 하는 리소스 소유자가 신뢰할 수 있는 권한 부여 서버에 의해 수행 됩니다. 토큰에 지정된 된 기간에 대 한 자원의 특정 집합에 대 한 액세스 권한을 부여합니다. OAuth의 Exchange 2013 의 구현에 대 한 자세한 내용은 참조 하십시오. [\[MS-XOAUTH\]: OAuth 2.0 인증 프로토콜 확장](https://go.microsoft.com/fwlink/p/?linkid=275093)합니다.

**온-프레미스 배포의 OAuth**

온-프레미스 배포에서 Exchange 2013, SharePoint 2013 및 Lync Server 2013은 인증 서버 없이도 토큰을 발급할 수 있습니다. 이러한 응용 프로그램 각각은 다른 응용 프로그램에서 제공하는 리소스에 액세스하기 위해 자체 서명된 토큰을 발급합니다. 리소스에 액세스할 수 있는 권한을 제공하는 응용 프로그램(예: Exchange 2013)은 호출하는 응용 프로그램에서 제공하는 자체 서명된 토큰을 신뢰할 수 있어야 합니다. 트러스트는 호출하는 응용 프로그램에 대한 *파트너 응용 프로그램* 구성을 만들어 설정되는데, 여기에는 호출하는 응용 프로그램의 ApplicationID, 인증서 및 AuthMetadataUrl이 포함됩니다. Exchange 2013, SharePoint 2013 및 Lync Server 2013은 잘 알려진 URL에 해당 인증 메타데이터 문서를 게시합니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>서버</strong></p></td>
<td><p><strong>AuthMetadataUrl</strong></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/autodiscover/metadata/json/1</code></p></td>
</tr>
<tr class="odd">
<td><p>Lync Server 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/metadata/json/1</code></p></td>
</tr>
<tr class="even">
<td><p>SharePoint 2013</p></td>
<td><p><code>https://&lt;serverfqdn&gt;/_layouts/15/metadata/json/1</code></p></td>
</tr>
</tbody>
</table>


**Exchange 2013 서버 인증 인증서**

Exchange 2013 설치 시 Microsoft Exchange 서버 인증 인증서라는 이름의 자체 서명된 인증서가 만들어집니다. 이 인증서는 Exchange 2013 조직의 모든 프런트 엔드 서버에 복제됩니다. 인증서의 지문은 Exchange 2013의 권한 부여 구성에서 해당 서비스 이름, 즉 온-프레미스 Exchange 2013을 나타내는 잘 알려진 GUID와 함께 지정됩니다. Exchange는 권한 부여 구성을 사용하여 인증 메타데이터 문서를 게시합니다.


> [!IMPORTANT]
> Exchange 2013이 만드는 기본 서버 인증 인증서의 유효 기간은 5년입니다. 권한 부여 구성에 현재 인증서가 포함되는지 확인해야 합니다.



EWS(Exchange 웹 서비스)를 통해 파트너 응용 프로그램의 액세스 요청을 받은 경우 Exchange 2013은 호출하는 서버가 해당 개인 키를 사용하여 서명한 액세스 토큰이 포함된 https 요청의 `www-authenticate` 헤더 구문을 분석합니다. 인증 모듈은 파트너 응용 프로그램 구성을 사용하여 액세스 토큰의 유효성을 검사합니다. 그런 다음 응용 프로그램에 부여된 RBAC 권한을 기반으로 리소스에 액세스할 수 있는 권한을 부여합니다. 액세스 토큰이 사용자를 대신하는 경우에는 사용자에게 부여된 RBAC 권한이 확인됩니다. 예를 들어 사용자가 SharePoint 2013에서 eDiscovery Center를 사용하여 eDiscovery 검색을 수행하는 경우 Exchange는 사용자가 검색 관리 역할 그룹의 구성원인지 또는 사용자에게 사서함 검색 역할이 할당되어 있고 검색 중인 사서함이 RBAC 역할 할당 범위 내에 있는지 여부를 확인합니다. 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md) 항목을 참조하십시오.

## OAuth 인증 관리

Exchange 2013에는 파트너 응용 프로그램과의 OAuth 인증을 위해 관리해야 하는 구성 개체가 두 개 있습니다.

  - **AuthConfig**   AuthConfig Exchange 2013 설치 프로그램에서 생성 되 고 인증 메타 데이터를 게시 하는 데 사용 됩니다. 인증 구성의 기존 인증서 만료에 근접 한 경우 구축 새 인증서를 제외 하 고 관리할 필요가 없습니다. 이 경우 기존 인증서를 갱신 하 수 유효 날짜와 함께 AuthConfig에서 다음 인증서로 새 인증서를 구성 합니다. 새 인증서는 조직에서 다른 Exchange 2013 를 자동으로 복제 하 고 새 인증서의 세부 정보가 들어 있는 인증 메타 데이터 문서를 새로 고칠는 AuthConfig 유효 날짜에 새 인증서에 롤오버 합니다.

  - **파트너 응용 프로그램**   Exchange 2013 에서 액세스 토큰을 요청 하려면 파트너 응용 프로그램을 사용 하도록 설정 하는 파트너 응용 프로그램 구성을 만들어야 합니다. Exchange 2013 수 있도록 신속 하 게 하 고 쉽게 파트너 응용 프로그램 구성을 만들고 있는 구성 오류를 최소화 `Configure-EnterprisePartnerApplication.ps1` 스크립트를 제공 합니다. 자세한 내용은 [SharePoint 2013 및 Lync 2013 OAuth 인증 구성](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)를 참조 합니다.

