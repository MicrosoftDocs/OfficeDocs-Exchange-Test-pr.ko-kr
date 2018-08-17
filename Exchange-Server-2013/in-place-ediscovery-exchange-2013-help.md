---
title: '원본 위치 eDiscovery: Exchange 2013 Help'
TOCTitle: 원본 위치 eDiscovery
ms:assetid: 6377cb7a-3416-4e15-8571-c45d2160fc6f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298021(v=EXCHG.150)
ms:contentKeyID: 50483268
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 원본 위치 eDiscovery

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-01-17_


> [!NOTE]
> Exchange Online(Office 365 및 Exchange Online 독립 실행형 계획)에 새 원본 위치 eDiscovery 검색 만들기에 대한 마감 날짜인 2017년 7월 1일을 연기했습니다. 하지만 올해 말 또는 내년 초에는 Exchange Online에 새 검색을 만들 수 없습니다. eDiscovery 검색을 만들려면 Office 365 보안 및 준수 센터의 <A href="https://go.microsoft.com/fwlink/?linkid=847843">콘텐츠 검색</A>을 사용하시기 바랍니다. 새 원본 위치 eDiscovery를 해제한 후에도 기존 원본 위치 eDiscovery 검색을 계속 수정할 수 있으며 Exchange Server 2013 및 Exchange 하이브리드 배포에서 새 원본 위치 eDiscovery 검색을 계속 만들 수 있습니다.



조직 (조직의 정책, 준수, 또는 소송에 관련 된) 법적 개시가 필요한 준수, 하는 경우 사서함 내의 관련 콘텐츠에 대 한 검색 검색을 수행 하 원본 위치 eDiscovery (영문) Microsoft Exchange Server 2013 및 Exchange Online 수 있습니다. Exchange 2013 및 Exchange Online 도 연결 된 검색 기능 및 Microsoft SharePoint 2013 및 Microsoft SharePoint Online 와 통합을 제공합니다. SharePoint에서 eDiscovery 센터를 사용 하 여 검색할 수 있으며 Exchange 사서함 콘텐츠 및 보관 된 Lync 2013 콘텐츠 SharePoint 2013 및 SharePoint Online 웹사이트, 문서, SharePoint (SharePoint 2013 만 해당)을 사용 하 여 인덱싱된 파일 공유를 포함 하는 경우에 관련 된 모든 콘텐츠를 보관할 수도 있습니다. 동일한 검색에서 온-프레미스 및 클라우드 기반 사서함을 검색 하는 Exchange 하이브리드 환경에서 원본 위치 eDiscovery를 사용할 수 있습니다.

**목차**

How In-Place eDiscovery works

Exchange Search

Discovery Management role group and management roles

Custom management scopes for In-Place eDiscovery

Integration with SharePoint Server 2013 and SharePoint Online

eDiscovery in an Exchange hybrid deployment

Discovery mailboxes

Using In-Place eDiscovery

Estimate, preview, and copy search results

Export search results to a PST file

Different search results

Logging for In-Place eDiscovery searches

In-Place eDiscovery and In-Place Hold

Preserving mailboxes for In-Place eDiscovery

In-Place eDiscovery limits and throttling policies

In-Place eDiscovery documentation


> [!IMPORTANT]
> 원본 위치 eDiscovery는 적절한 권한이 있는 사용자가 Exchange 2013 또는 Exchange Online 조직 전체에 저장된 모든 메시징 레코드에 액세스할 수 있도록 허용하는 강력한 기능입니다. 검색 관리 역할 그룹이나 사서함 검색 관리 역할이 있는 구성원 추가, 사서함을 검색할 수 있는 사서함 액세스 권한 할당을 포함한 검색 활동을 제어 및 모니터링해야 합니다.



## 원본 위치 eDiscovery의 작동 방식

원본 위치 eDiscovery에서는 Exchange 검색에서 만든 콘텐츠 인덱스를 사용합니다. RBAC(역할 기반 액세스 제어)는 관련 기술 지식이 없는 사람에게 검색 작업을 위임할 수 있는 [검색 관리](discovery-management-exchange-2013-help.md) 관리 역할 그룹을 제공합니다. 이때 Exchange 구성의 작동 관련 내용을 사용자가 변경할 수 있도록 허용하는 상승된 권한을 제공하지 않아도 됩니다. EAC(Exchange 관리 센터)는 법무 및 준수 관리자, 레코드 관리자 및 HR(인적 리소스) 전문가 등 관련 기술 지식이 없는 사람도 쉽게 사용할 수 있습니다.

권한이 있는 사용자는 사서함을 선택하고 키워드, 시작/종료 날짜, 보낸 사람/받는 사람 주소, 메시지 유형 등의 검색 조건을 지정하여 원본 위치 eDiscovery 검색을 수행할 수 있습니다. 검색이 완료되면 권한이 있는 사용자는 다음 작업 중 하나를 선택할 수 있습니다.

  - **검색 결과 예상**   이 옵션은 지정된 조건에 따라 검색에 의해 반환될 항목의 예상 전체 크기 및 개수가 반환됩니다.

  - **검색 결과 미리 보기**   이 옵션은 결과 미리 보기가 제공됩니다. 검색된 각 사서함에서 반환된 메시지가 표시됩니다.

  - **검색 결과 복사**   이 옵션을 사용하면 메시지를 검색 사서함으로 복사할 수 있습니다.

  - **검색 결과 내보내기**   검색 결과를 검색 사서함으로 복사한 다음 PST 파일로 내보낼 수 있습니다.

![검색 결과 예상, 미리 보기, 복사 및 내보내기](images/Dd298021.6356971a-34ed-4586-8229-030448d4fe2d(EXCHG.150).gif "검색 결과 예상, 미리 보기, 복사 및 내보내기")

## Exchange 검색

원본 위치 eDiscovery는 Exchange 검색에서 만든 콘텐츠 인덱스를 사용합니다. 대폭 향상된 인덱싱 및 쿼리 성능과 검색 기능을 제공하는 강력한 검색 플랫폼인 Microsoft Search Foundation을 사용하도록 Exchange 검색이 변경되었습니다. Microsoft Search Foundation은 SharePoint 2013을 비롯한 다른 Office 제품에서도 사용되므로 상호 운용성이 탁월하며 해당 제품 간 쿼리 구문도 비슷합니다.

단일 콘텐츠 인덱싱 엔진을 사용하는 경우에는 IT 부서에서 eDiscovery 요청을 받은 경우에도 원본 위치 eDiscovery를 위한 사서함 데이터베이스의 크롤링 및 인덱싱용으로 추가 리소스가 사용되지 않습니다.

원본 위치 eDiscovery에서는 Microsoft Outlook과 Outlook Web App의 빠른 검색에 사용되는 AQS(고급 검색 구문)와 비슷한 쿼리 구문인 KQL(Keyword Query Language)을 사용합니다. KQL에 익숙한 사용자는 쉽게 강력한 검색 쿼리를 구성하여 콘텐츠 인덱스를 검색할 수 있습니다.

Exchange 검색을 통해 인덱싱되는 파일 형식에 대한 자세한 내용은 [Exchange 검색에서 인덱싱하는 파일 형식](file-formats-indexed-by-exchange-search-exchange-2013-help.md)을 참조하세요.

## 검색 관리 역할 그룹 및 관리 역할

[검색 관리](discovery-management-exchange-2013-help.md) RBAC 역할 그룹에 추가한 사용자만 원본 위치 eDiscovery 검색을 수행할 수 있습니다. 이 역할 그룹은 사용자가 원본 위치 eDiscovery 검색을 수행할 수 있게 해주는 [사서함 검색 역할](mailbox-search-role-exchange-2013-help.md) 관리 역할과 사용자가 사서함에 원본 위치 유지 또는 소송 보존을 적용할 수 있게 해 주는 [법적 보존 역할](legal-hold-role-exchange-2013-help.md) 관리 역할 등 두 관리 역할로 구성됩니다.

원본 위치 eDiscovery 관련 작업을 수행하는 권한은 기본적으로 어떤 사용자나 Exchange 관리자에게도 할당되지 않습니다. 조직 관리 역할 그룹에 속한 Exchange 관리자는 검색 관리 역할 그룹에 사용자를 추가하고 사용자 지정 역할 그룹을 만들어 검색 관리자 범위를 일부 사용자로 좁힐 수 있습니다. 검색 관리 역할 그룹에 사용자를 추가하는 방법에 대한 자세한 내용은 [Exchange eDiscovery 사용 권한 할당](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> 사용자가 검색 관리 역할 그룹에 추가되지 않았거나 사서함 검색 역할이 할당되지 않은 경우에는 EAC에서 <STRONG>원본 위치 eDiscovery 및 유지</STRONG> 사용자 인터페이스가 표시되지 않고 Exchange 관리 셸에서 원본 위치 eDiscovery cmdlet을 사용할 수도 없습니다.



기본적으로 사용하도록 설정되는 RBAC 역할 변경 감사는 검색 관리 역할 그룹 할당을 추적하기 위해 적정 레코드가 유지되도록 합니다. 관리자 역할 그룹 보고서를 사용하여 관리자 역할 그룹에 대한 변경 내용을 검색할 수 있습니다. 자세한 내용은 [역할 그룹 변경 내용을 검색 또는 관리자 감사 로그](search-the-role-group-changes-or-administrator-audit-logs-exchange-2013-help.md)을 참조하세요.

맨 위로 이동

## 원본 위치 eDiscovery의 사용자 지정 관리 범위

사용자 지정 관리 범위를 사용하여 특정 사람이나 그룹이 원본 위치 eDiscovery를 사용하여 Exchange 2013 또는 Exchange Online 조직에서 사서함 하위 집합을 검색하도록 할 수 있습니다. 예를 들어 검색 관리자가 특정 위치나 부서의 사용자 사서함만 검색하도록 할 수 있습니다. 이 작업을 위해 받는 사람 필터를 사용하여 검색할 수 있는 사서함을 제어하는 사용자 지정 관리 범위를 만들면 됩니다. 받는 사람 필터 범위는 필터를 사용하여 받는 사람 유형 또는 기타 받는 사람 속성에 따라 특정 받는 사람을 대상으로 지정합니다.

원본 위치 eDiscovery의 경우 사용자 지정 범위에 대해 받는 사람 필터를 만드는 데 사용할 수 있는 사용자 사서함에 대한 유일한 속성은 메일 그룹 구성원입니다. *CustomAttributeN*, *Department*, *PostalCode* 등의 다른 속성을 사용하는 경우 사용자 지정 범위에 할당된 역할 그룹의 구성원이 실행하는 검색은 실패합니다. 자세한 내용은 [원본 위치 eDiscovery 검색의 사용자 지정 관리 범위 만들기](create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md)를 참조하세요.

## SharePoint Server 2013 및 SharePoint Online과 통합

SharePoint 2013 및 SharePoint Online과 통합되어 Exchange 2013 및 Exchange Online 검색 관리자는 SharePoint의 eDiscovery Center를 사용하여 다음 작업을 수행할 수 있습니다.

  - **단일 위치에서 콘텐츠 검색 및 보존** 권한이 있는 검색 관리자는 SharePoint와 Exchange 간에 인스턴트 메시징 대화 같은 Lync 콘텐츠 및 Exchange 사서함에 보관된 공유 모임 문서를 비롯한 콘텐츠를 검색하고 보존할 수 있습니다.

  - **사례 관리** eDiscovery Center에서는 eDiscovery에 대해 사례 관리 접근 방식을 사용하므로 사례를 만들고 각 사례에 대한 콘텐츠 리포지토리에서 콘텐츠를 검색 및 보존할 수 있습니다.

  - **검색 결과 내보내기** 검색 관리자는 eDiscovery Center를 사용하여 검색 결과를 내보낼 수 있습니다. 검색 결과에 포함된 사서함 콘텐츠를 PST 파일로 내보냅니다.

SharePoint에서도 콘텐츠 인덱싱 및 쿼리에 Microsoft Search Foundation을 사용합니다. 검색 관리자가 Exchange 콘텐츠 검색에 EAC를 사용하는지 eDiscovery Center를 사용하는지에 관계없이 동일한 사서함 콘텐츠가 반환됩니다.

온-프레미스 배포에서 SharePoint의 eDiscovery Center를 사용하여 Exchange 사서함을 검색하려면 두 응용 프로그램 간에 트러스트를 설정해야 합니다. Exchange 2013 및 SharePoint 2013에서는 이 작업을 수행하는 데 OAuth 인증을 사용합니다. 자세한 내용은 [SharePoint eDiscovery 센터에 대한 Exchange 구성](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)을 참조하십시오. SharePoint에서 수행된 eDiscovery 검색은 Exchange에서 RBAC를 통해 권한이 부여됩니다. SharePoint 사용자가 Exchange 사서함에 대해 eDiscovery 검색을 수행할 수 있으려면 Exchange에 대한 위임된 검색 관리 권한을 할당받아야 합니다. SharePoint eDiscovery Center를 통해 수행된 eDiscovery 검색에서 반환된 사서함 콘텐츠를 미리 보려면 검색 관리자의 사서함이 동일한 Exchange 조직에 있어야 합니다.

단계는 단계별 지침은 Office 365 조직에서 eDiscovery 센터 설정에 대 한, [SharePoint Online에서 eDiscovery 센터 설정](https://go.microsoft.com/fwlink/p/?linkid=331600)를 참조 하십시오.

## Exchange 하이브리드 배포의 eDiscovery

Exchange 2013 하이브리드 조직에서 프레미스 간 eDiscovery 검색을 정상적으로 수행하려면 원본 위치 eDiscovery를 사용하여 온-프레미스 및 클라우드 기반 사서함을 검색할 수 있도록 Exchange 온-프레미스 및 Exchange Online 조직 간에 OAuth(Open Authorization) 인증을 구성해야 합니다. OAuth 인증은 응용 프로그램이 서로 인증할 수 있도록 하는 서버 간 인증 프로토콜입니다.

OAuth 인증은 Exchange 하이브리드 배포에서 다음 eDiscovery 시나리오를 지원합니다.

  - 클라우드 기반 보관 사서함에 대해 Exchange Online Archiving을 사용하는 온-프레미스 사서함 검색

  - 같은 eDiscovery 검색에서 온-프레미스 사서함 및 클라우드 기반 사서함 검색

  - SharePoint Online에서 eDiscovery 센터를 사용하여 온-프레미스 사서함 검색

Exchange 하이브리드 배포에서 OAuth 인증을 구성해야 하는 eDiscovery 시나리오에 대한 자세한 내용은 [OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)을 참조하세요. eDiscovery를 지원하도록 OAuth 인증을 구성하는 단계별 지침은 [Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)을 참조하세요.

## 검색 사서함

원본 위치 eDiscovery 검색을 만든 후 검색 결과를 대상 사서함에 복사할 수 있습니다. EAC를 사용하면 대상 사서함으로 지정할 검색 사서함을 선택할 수 있습니다. 검색 사서함은 다음과 같은 기능을 제공하는 특수한 유형의 사서함입니다.

  - **쉽고 안전한 대상 사서함 선택**   EAC를 사용하여 원본 위치 eDiscovery 검색을 만들 때 검색 결과를 저장할 수 있는 리포지토리로 검색 사서함만 사용할 수 있습니다. 조직에서 사용할 수 있는 긴 사서함 목록을 일일이 살펴볼 필요가 없습니다. 검색 관리자가 실수로 다른 사용자의 사서함이나 보안되지 않은 사서함을 선택하여 중요한 메시지를 저장할 가능성도 없습니다.

  - **큰 사서함 저장소 할당량**   대상 사서함은 원본 위치 eDiscovery 검색에서 반환되는 대량의 메시지 데이터를 저장할 수 있어야 합니다. 기본적으로 검색 사서함의 사서함 저장소 할당량은 50GB(기가바이트)입니다. 이 저장소 할당량은 늘릴 수 없습니다.

  - **기본적으로 더 안전**   모든 사서함 유형과 마찬가지로 검색 사서함에도 연결된 Active Directory 사용자 계정이 있습니다. 하지만 이 계정은 기본적으로 사용하지 않도록 설정됩니다. 검색 사서함에 액세스하도록 명시적으로 권한이 부여된 사용자만 액세스가 가능합니다. 검색 관리 역할 그룹의 구성원에게는 기본 검색 사서함에 대한 모든 권한이 할당됩니다. 추가로 만드는 검색 사서함에 대한 사서함 액세스 권한은 기본적으로 사용자에게 할당되지 않습니다.

  - **전자 메일 배달 사용 안 함**   검색 사서함이 Exchange 주소 목록에 표시되지만 사용자가 검색 사서함에 전자 메일을 보낼 수는 없습니다. 검색 사서함에 대한 전자 메일 배달은 배달 제한을 통해 금지됩니다. 따라서 검색 사서함에 복사되는 검색 결과의 무결성이 유지됩니다.

Exchange 2013에서는 설치 과정 중에 표시 이름이 **사서함 검색**인 검색 사서함이 하나 만들어집니다. 셸을 사용하여 추가 검색 사서함을 만들 수 있습니다. 기본적으로 추가로 만든 검색 사서함에는 사서함 액세스 권한이 할당되지 않습니다. 검색 사서함에 복사된 메시지에 액세스할 수 있도록 검색 관리자에게 "모든 권한" 권한을 할당할 수 있습니다. 자세한 내용은 [검색 사서함 만들기](create-a-discovery-mailbox-exchange-2013-help.md)를 참조하십시오.

또한 원본 위치 eDiscovery에서는 표시 이름이 **SystemMailbox{e0dc1c29-89c3-4034-b678-e6c29d823ed9}**인 시스템 사서함에 원본 위치 eDiscovery 메타데이터를 보관합니다. 시스템 사서함은 EAC 또는 Exchange 주소 목록에 표시되지 않습니다. 온-프레미스 조직에서 원본 위치 eDiscovery 시스템 사서함이 있는 사서함 데이터베이스를 제거하려면 먼저 사서함을 다른 사서함 데이터베이스로 옮겨야 합니다. 사서함이 제거되거나 손상된 경우 사서함을 다시 만들지 않으면 검색 관리자가 eDiscovery 검색을 수행할 수 없습니다. 자세한 내용은 [검색 시스템 사서함을 다시 만들려면](re-create-the-discovery-system-mailbox-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 원본 위치 eDiscovery 사용

원본 위치 eDiscovery 검색은 검색 관리 역할 그룹에 추가된 사용자가 수행할 수 있습니다. EAC에서 웹 기반 인터페이스를 사용하여 검색을 수행할 수 있습니다. 따라서 레코드 관리자, 준수 관리자 또는 법무 및 HR 전문가 등 관련 기술 지식이 없는 사람도 원본 위치 eDiscovery 기능을 쉽게 사용할 수 있습니다. 셸을 사용하여 검색을 수행할 수도 있습니다. 자세한 내용은 [원본 위치 eDiscovery 검색 만들기](create-an-in-place-ediscovery-search-exchange-2013-help.md)를 참조하세요.


> [!NOTE]
> 온-프레미스 조직에서 원본 위치 eDiscovery를 사용하면 Exchange 2013 사서함 서버에 있는 사서함을 검색할 수 있습니다. Exchange 2010 사서함 서버에 있는 사서함을 검색하려면 Exchange 2010 서버에서 여러 사서함 검색을 사용하십시오.<BR>하이브리드 배포(일부 사서함은 온-프레미스 사서함 서버에 있고 일부 사서함은 클라우드 기반 조직에 있는 환경)에서 온-프레미스 조직의 EAC를 사용하여 클라우드 기반 사서함에 대한 원본 위치 eDiscovery 검색을 수행할 수 있습니다. 메시지를 검색 사서함에 복사하려는 경우 온-프레미스 검색 사서함을 선택해야 합니다. 검색 결과에 반환된 클라우드 기반 사서함의 메시지는 지정된 온-프레미스 검색 사서함에 복사됩니다. 하이브리드 배포에 대한 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/jj200581(v=exchg.150)">Exchange Server 하이브리드 배포</A>를 참조하십시오.



EAC의 **원본 위치 eDiscovery 및 유지** 마법사를 사용하면 원본 위치 eDiscovery 검색을 만들 수 있으며 원본 위치 유지를 사용하여 검색 결과를 유지할 수도 있습니다. 원본 위치 eDiscovery 검색을 만들면 원본 위치 eDiscovery 시스템 사서함에 검색 개체가 만들어집니다. 이 개체를 조작하여 검색을 시작, 중지, 수정 및 제거할 수 있습니다. 검색을 만든 후 쿼리 효율성을 확인하는 데 유용한 키워드 통계가 포함된 예상 검색 결과를 가져올 수 있습니다. 또한 검색에 반환된 항목을 실시간으로 미리 볼 수 있으며 이를 통해 메시지 콘텐츠, 각 원본 사서함에서 반환된 메시지 개수 및 총 메시지 개수를 볼 수 있습니다. 필요한 경우 이 정보를 기반으로 쿼리를 더 세밀하게 조정할 수 있습니다.

검색 결과에 만족하면 결과를 검색 사서함에 복사합니다. EAC 또는 Outlook을 사용하여 검색 사서함이나 해당 콘텐츠 중 일부를 PST 파일로 내보낼 수도 있습니다.

원본 위치 eDiscovery 검색을 만들 때 다음 매개 변수를 지정해야 합니다.

  - **이름**   검색을 식별하는 데 사용되는 검색 이름입니다. 검색 결과를 검색 사서함에 복사하면, 검색 사서함에서 검색 결과를 고유하게 식별하는 검색 이름 및 타임스탬프를 사용하여 폴더가 하나 만들어집니다.

  - **사서함**   Exchange 2013 또는 Exchange Online 조직에서 모든 사서함을 검색 하거나 검색할 사서함을 지정 하도록 선택할 수 있습니다. 사용자의 기본 및 보관 사서함의 검색에 포함 됩니다. 항목을 대기 시키려면 동일한 검색을 사용 하려면 사서함을 지정 해야 합니다. 해당 그룹의 구성원 인 사서함 사용자를 포함 하도록 메일 그룹을 지정할 수 있습니다. 그룹의 구성원은 검색을 만들 때 한번 계산 되 고 그룹 구성원 자격의 변경 내용이 검색에 자동으로 반영 되지 않습니다.
    
    Exchange Online 지정할 수도 있습니다 Office 365 그룹 콘텐츠 원본으로 그룹 사서함 검색 (또는 대기 상태에 놓일) 되도록 합니다. 원본 위치 eDiscovery 검색을 Office 365 그룹을 추가할 때만 그룹 사서함이 검색 되지 않습니다. 그룹 구성원의 사서함 검색 되지 않습니다.

  - **검색 쿼리**   지정한 사서함에 있는 모든 사서함 콘텐츠를 포함할 수도 있고 검색 쿼리를 사용하여 사례나 검색과 관련이 더 많은 항목을 반환할 수도 있습니다. 검색 쿼리에 다음 매개 변수를 지정할 수 있습니다.
    
      - **키워드**   검색 메시지 콘텐츠에 키워드 및 구문을 지정할 수 있습니다. **AND**, **OR** 및 **NOT** 논리 연산자를 사용할 수도 있습니다. Exchange 2013에서는 **NEAR** 연산자도 지원하므로 다른 단어나 구와 유사한 단어나 구를 검색할 수 있습니다.
        
        여러 단어로 된 구문이 정확하게 일치하는 부분을 검색하려면 구문을 따옴표로 묶어야 합니다. 예를 들어 "plan and competition" 구문을 검색하면 이 구문과 똑같은 메시지가 반환되고, **plan AND competition**을 검색하면 **plan**과 **competition** 단어를 무작위로 포함하는 메시지가 반환됩니다.
        
        또한 Exchange 2013에서는 원본 위치 eDiscovery 검색에 KQL(Keyword Query Language) 구문을 지원합니다.
        

        > [!NOTE]
        > 원본 위치 eDiscovery는 정규식을 지원하지 않습니다.

        
        **AND** 및 **OR**과 같은 논리 연산자를 키워드 대신 연산자로 처리하도록 하려면 대문자로 표기해야 합니다. 실수나 잘못된 해석을 방지하려면 여러 논리 연산자가 혼합된 쿼리에 대해 명시적 괄호를 사용하는 것이 좋습니다. 예를 들어, WordA or WordB AND 또는 WordC or WordD를 포함하는 메시지를 검색하려면, **(WordA OR WordB) AND (WordC OR WordD)**를 사용해야 합니다.
    
      - **시작 날짜 및 종료 날짜**   기본적으로 원본 위치 eDiscovery는 날짜 범위로 검색을 제한하지 않습니다. 특정 날짜 범위에 보낸 메시지를 검색하려면 시작 날짜와 종료 날짜를 지정하여 검색 범위를 좁힙니다. 종료 날짜를 지정하지 않으면 검색을 다시 시작할 때마다 최신 결과가 반환됩니다.
    
      - **보낸 사람 및 받는 사람**   메시지의 보낸 사람 또는 받는 사람을 지정하여 검색 범위를 좁힐 수 있습니다. 전자 메일 주소, 표시 이름 또는 도메인 이름을 사용하여 도메인에 있는 사람이 보내거나 받은 항목을 검색할 수 있습니다. 예를 들어 Contoso, Ltd.의 누군가로부터 받은 전자 메일을 찾으려면 EAC의 **보낸 사람** 또는 **받는 사람/참조** 필드에서 **@contoso.com**을 지정합니다. 셸에서 *Senders* 또는 *Recipients* 매개 변수에 **@contoso.com**을 지정할 수도 있습니다.
    
      - **메시지 유형**   기본적으로 모든 유형의 메시지가 검색됩니다. 전자 메일, 연락처, 문서, 업무 일지, 모임, 메모 및 Lync 콘텐츠와 같은 특정 메시지 유형을 선택하여 검색을 제한할 수 있습니다.

다음 스크린샷에는 EAC의 검색 쿼리 예가 나와 있습니다.

![eDiscovery 검색 쿼리 구성](images/Dd353189.a3626569-8700-421e-8b4e-7ec520b28272(EXCHG.150).png "eDiscovery 검색 쿼리 구성")

원본 위치 eDiscovery를 사용하는 경우 다음 사항도 고려해야 합니다.

  - **첨부 파일**   원본 위치 eDiscovery는 Exchange 검색에서 지원하는 첨부 파일을 검색합니다. 자세한 내용은 [Exchange 검색에서 인덱싱하는 파일 형식](file-formats-indexed-by-exchange-search-exchange-2013-help.md)를 참조하십시오. 온-프레미스 배포에서, 사서함 서버에서 파일 형식별로 검색 필터(iFilter)를 설치하여 파일 형식을 더 추가할 수도 있습니다.

  - **검색할 수 없는 항목**   검색할 수 없는 항목은 Exchange 검색에서 인덱싱할 수 없는 사서함 항목입니다. 첨부된 파일의 검색 필터가 설치되지 않았거나, 파일 오류가 발생했거나, 메시지가 암호화된 등의 경우에 이러한 항목이 인덱싱될 수 없습니다. eDiscovery 검색이 수행되도록 조직에서 검토를 위해 이러한 항목을 포함해야 할 수도 있습니다. 검색 결과를 검색 사서함에 복사하거나 PST 파일로 내보낼 때는 검색할 수 없는 항목을 포함할 수 있습니다. 자세한 내용은 [Exchange eDiscovery의 검색할 수 없는 항목](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)를 참조하세요.

  - **암호화된 항목**   S/MIME을 사용하여 암호화된 메시지는 Exchange 검색에서 인덱싱되지 않으므로 원본 위치 eDiscovery에서도 검색되지 않습니다. 검색할 수 없는 항목을 검색 결과에 포함하는 옵션을 선택하면 이러한 S/MIME 암호화 메시지가 검색 사서함에 복사됩니다.

  - **IRM 보호 항목**   IRM(정보 권한 관리)을 사용하여 보호된 메시지는 Exchange 검색에서 인덱싱되므로 쿼리 매개 변수와 일치할 경우 검색 결과에 포함됩니다. 메시지는 사서함 서버와 같은 Active Directory 포리스트에 있는 AD RMS(Active Directory Rights Management Services)를 사용하여 보호되어야 합니다. 자세한 내용은 [정보 권한 관리](information-rights-management-exchange-2013-help.md)를 참조하십시오.
    

    > [!IMPORTANT]
    > Exchange 검색에서 암호 해독에 실패하거나 IRM을 사용하지 않도록 설정되어 있어 IRM 보호 메시지를 인덱싱하지 못한 경우에는 보호된 메시지가 실패 항목 목록에 추가되지 않습니다. 검색 결과에 검색할 수 없는 항목을 포함하는 옵션을 선택한 경우 해독하지 못한 보호된 메시지는 결과에 포함되지 않을 수도 있습니다.<BR>IRM 보호 메시지를 검색에 포함하려면 .rpmsg 첨부 파일이 있는 메시지를 포함하는 다른 검색을 만듭니다. 쿼리 문자열 <CODE>attachment:rpmsg</CODE>를 사용하면 인덱싱되었는지 여부에 관계없이 지정한 사서함에 있는 IRM 보호 메시지를 모두 검색할 수 있습니다. 이 경우 인덱싱된 IRM 보호 메시지와 같이 한 검색에서 다른 검색 조건에도 적합한 메시지를 반환하는 시나리오에서 검색 결과가 중복될 가능성이 있습니다. 인덱싱할 수 없는 IRM 보호 메시지는 검색에서 반환되지 않습니다.<BR>모든 IRM 보호 메시지에 대해 두 번째 검색을 수행하면 첫 번째 검색에서 인덱싱 및 반환된 IRM 보호 메시지도 포함됩니다. 두 번째 검색에서 반환되는 IRM 보호 메시지가 첫 번째 검색에 사용된 키워드 등의 검색 조건과 일치하지 않을 수도 있습니다.



  - **중복 제거** 검색 결과를 검색 사서함에 복사할 때 검색 결과에 대해 *중복 제거*를 사용하도록 설정하여 메시지의 공유 복사본 하나만 검색 사서함에 복사할 수 있습니다. 중복 제거를 사용할 경우 이점은 다음과 같습니다.
    
      - 복사된 메시지 수가 줄어들어 저장소 요구 사항 및 검색 사서함 크기가 줄어듭니다.
    
      - 검색 관리자, 법적 자문 위원 또는 검색 결과 검토와 관련된 다른 사람들의 작업량이 줄어듭니다.
    
      - 검색 결과의 중복 항목 수에 따라 eDiscovery 비용이 줄어듭니다.

맨 위로 이동

## 검색 결과 예상, 미리 보기 및 복사

원본 위치 eDiscovery 검색을 완료하면 EAC의 세부 정보 창에서 예상 검색 결과를 볼 수 있습니다. 여기에서 반환된 항목 수와 해당 항목들의 총 크기가 포함됩니다. 검색 쿼리에 사용된 각 키워드에 대해 반환된 항목 수에 대한 세부 정보가 포함된 키워드 통계도 볼 수 있습니다. 이 정보는 쿼리의 효율성을 확인하는 데 유용합니다. 쿼리 범위가 너무 광범위하면 반환되는 데이터 집합이 커져 검토에 필요한 리소스가 늘어나고 결국 eDiscovery 비용이 증가할 수 있습니다. 쿼리 범위가 너무 좁으면 반환되는 레코드 수가 크게 줄어들거나 전혀 반환되지 않을 수 있습니다. 예상 결과 및 키워드 통계를 기반으로 요구 사항에 맞게 쿼리를 세부적으로 조정할 수 있습니다.


> [!NOTE]
> Exchange 2013에서는 키워드 통계에 검색 쿼리에 지정된 보낸 사람/받는 사람, 메시지 유형 및 날짜와 같은 키워드가 아닌 속성에 대한 통계도 포함됩니다.



검색 결과를 미리 보고 반환될 메시지에 검색하려는 콘텐츠가 포함되어 있는지 확인하고 필요한 경우 쿼리 쿼리를 세부적으로 조정할 수도 있습니다. eDiscovery 검색 미리 보기에는 검색된 각 사서함에서 반환된 메시지 개수와 검색에서 반환된 총 메시지 개수가 표시됩니다. 미리 보기가 빠르게 생성되어 메시지를 검색 사서함에 복사할 필요가 없습니다.

검색 결과의 양과 질에 만족하면 그때 검색 사서함에 복사하면 됩니다. 메시지를 복사할 때 다음 옵션을 사용할 수 있습니다.

  - **검색할 수 없는 항목 포함**   검색할 수 없는 것으로 간주되는 항목 유형에 대한 자세한 내용은 이전 섹션에 나와 있는 eDiscovery 검색 고려 사항을 참조하십시오.

  - **중복 제거 사용**   중복 제거는 검색된 사서함 중 하나 이상에 레코드의 인스턴스가 여러 개 있는 경우 단일 인스턴스만 포함하도록 함으로써 데이터 집합의 크기를 줄입니다.

  - **전체 로깅 사용**   기본적으로 항목을 복사할 때는 기본 로깅만 사용됩니다. 전체 로깅을 선택하여 검색에서 반환된 모든 레코드에 대한 정보를 포함할 수 있습니다.

  - **복사가 완료되면 메일 받기**   원본 위치 eDiscovery 검색에서 대량의 레코드를 반환할 가능성이 있습니다. 반환된 메시지를 검색 사서함에 복사하는 데 시간이 오래 걸릴 수 있습니다. 복사가 완료될 때 전자 메일 알림을 받으려면 이 옵션을 사용합니다. Outlook Web App에서 쉽게 액세스할 수 있도록 이 알림에는 검색 사서함 내 메시지가 복사된 위치에 대한 링크가 포함됩니다.

자세한 내용은 [EDiscovery 검색 결과 검색 사서함으로 복사](copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md)를 참조하세요.

맨 위로 이동

## PST 파일로 검색 결과 내보내기

검색 결과를 검색 사서함으로 복사한 다음 PST 파일로 내보낼 수 있습니다.

![PST 파일로 eDiscovery 검색 결과 내보내기](images/Dd298021.4ddca8af-1af5-4cb2-852c-e3a292099a58(EXCHG.150).gif "PST 파일로 eDiscovery 검색 결과 내보내기")

검색 결과를 PST 파일로 내보내면 사용자 또는 다른 사용자가 Outlook에서 열어 검색 결과에 반환된 메시지를 검토하거나 인쇄할 수 있습니다. 자세한 내용은 [PST 파일로 eDiscovery 검색 결과 내보내기](export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md)를 참조하세요.

## 다양한 검색 결과

원본 위치 eDiscovery가 라이브 데이터에서 검색을 수행하므로, 같은 콘텐츠 원본에 대해 두 가지 검색이 가능하고 동일한 검색 쿼리를 사용하여 다른 결과를 반환할 수 있습니다. 예상 검색 결과는 검색 사서함에 복사되는 실제 검색 결과와 다를 수도 있습니다. 이 결과는 짧은 시간 안에 동일한 검색을 다시 실행하는 경우에도 발생할 수 있습니다. 검색 결과의 일관성에 영향을 줄 수 있는 몇 가지 요인은 다음과 같습니다.

  - Exchange 검색이 조직의 사서함 데이터베이스와 전송 파이프라인을 계속해서 크롤링 및 인덱싱하기 때문에 받는 전자 메일이 지속적으로 인덱싱되는 경우

  - 사용자 또는 자동화된 프로세스에 따라 전자 메일이 삭제되는 경우

  - 인덱싱에 시간이 걸리는 대용량 전자 메일을 대량 가져오는 경우

동일한 검색의 결과가 서로 다른 경우 사서함을 배치하여 콘텐츠를 보존하고, 사용량이 적은 시간에 검색을 실행하며, 대용량 전자 메일을 가져오고 나서 인덱싱 시간을 정하는 것이 좋습니다.

## 원본 위치 eDiscovery 검색 로깅

원본 위치 eDiscovery 검색에 사용할 수 있는 로깅 유형에는 두 가지가 있습니다.

  - **기본 로깅**   기본 로깅은 모든 원본 위치 eDiscovery 검색에 대해 기본적으로 사용됩니다. 여기에는 검색과 검색을 수행한 사람에 대한 정보가 포함됩니다. 기본 로깅에서 캡처되는 정보는 검색 결과가 저장되는 사서함으로 보내는 전자 메일 메시지의 본문에 표시됩니다. 이 메시지는 검색 결과를 저장하기 위해 만든 폴더에 있습니다.

  - **전체 로깅**   전체 로깅에는 검색에서 반환된 모든 메시지에 대한 정보가 포함됩니다. 이 정보는 기본 로깅 정보를 포함하는 전자 메일 메시지에 첨부된 .csv(쉼표로 구분된 값) 파일로 제공됩니다. .csv 파일 이름으로는 검색 이름이 사용됩니다. 이 정보는 준수 또는 레코드 보관 목적으로 필요할 수 있습니다. 전체 로깅을 사용하도록 설정하려면 EAC에서 검색 사서함에 검색 결과를 복사할 때 **전체 로깅 사용** 옵션을 선택해야 합니다. 셸을 사용하는 경우 *LogLevel* 매개 변수를 사용하여 전체 로깅 옵션을 지정합니다.


> [!NOTE]
> 셸을 사용하여 원본 위치 eDiscovery 검색을 만들거나 수정할 때 로깅을 사용하지 않도록 설정할 수도 있습니다.



검색 결과를 검색 사서함에 복사할 때 포함되는 검색 로그 외에도 Exchange에서는 원본 위치 eDiscovery 검색을 생성, 수정 또는 제거하기 위해 EAC 또는 셸에서 사용된 cmdlet을 기록합니다. 이 정보는 관리자 감사 로그 항목에 기록됩니다. 자세한 내용은 [관리자 감사 로깅](administrator-audit-logging-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

## 원본 위치 eDiscovery 및 원본 위치 유지

eDiscovery 요청의 일부로서 소송이나 조사가 완결될 때까지 사서함 콘텐츠를 보존해야 할 수도 있습니다. 사서함 사용자 또는 프로세스에 의해 삭제 또는 수정된 메시지도 보존해야 합니다. Exchange 2013에서는 원본 위치 유지에 의해 이루어집니다. 자세한 내용은 [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md)를 참조하십시오.

Exchange 2013에서는 새로운 **원본 위치 eDiscovery 및 유지** 마법사를 사용하여 eDiscovery에 필요할 때까지 또는 기타 비즈니스 요구 사항을 충족하기 위해 필요한 항목을 검색하고 보존할 수 있습니다. 원본 위치 eDiscovery와 원본 위치 유지에 동일한 검색을 사용하는 경우 다음 사항을 고려해야 합니다.

  - 모든 사서함을 검색하는 옵션을 사용할 수 없습니다. 사서함 또는 메일 그룹을 선택해야 합니다.

  - 원본 위치 eDiscovery 검색이 원본 위치 유지에도 사용되는 경우에는 해당 검색을 제거할 수 없습니다. 먼저 검색에서 원본 위치 유지 옵션을 해제한 후 검색을 제거해야 합니다.

## 원본 위치 eDiscovery를 위해 사서함 보존

직원이 조직을 떠나는 경우 사서함을 사용하지 않도록 설정하거나 제거하는 것이 일반적입니다. 사서함을 사용하지 않도록 설정하고 나면 해당 사서함이 사용자 계정에서 연결이 끊어지지만 특정 기간(기본적으로 30일) 동안 사서함에 남아 있게 됩니다. 관리되는 폴더 도우미는 이 기간 동안 적용되지 않은 보존 정책 및 연결이 끊어진 사서함을 처리하지 않습니다. 연결이 끊어진 사서함의 콘텐츠는 검색할 수 없습니다. 사서함 데이터베이스에 대해 구성된 삭제된 사서함 보존 기간에 도달하면 사서함이 사서함 데이터베이스에서 제거됩니다.


> [!IMPORTANT]
> Exchange Online에서 원본 위치 eDiscovery는 비활성 사서함의 콘텐츠를 검색할 수 있습니다. 비활성 사서함은 원본 위치 유지나 소송 보존에 있었지만 제거된 사서함을 나타냅니다. 비활성 사서함은 유지되는 동안에는 보존됩니다. 비활성 사서함이 원본 위치 보존에서 제거되었거나 소송 보존이 사용하지 않도록 설정된 경우에는 이 사서함은 영구 삭제됩니다. 자세한 내용은 <A href="https://technet.microsoft.com/ko-kr/library/dn144876(v=exchg.150)">Exchange Online에서 비활성 사서함 관리</A>을 참조하세요.



온 프레미스 배포에서, 조직에서 더 이상 조직에 속하지 않는 직원의 메시지에 보존 설정을 적용해야 하는 경우 또는 진행 중인 eDiscovery 검색이나 향후 검색을 위해 그만둔 직원의 사서함을 보존해야 할 경우 사서함을 사용하지 않도록 설정하거나 제거해서는 안 됩니다. 사서함에 액세스할 수 없도록 하고 새 메시지가 해당 사서함에 배달되지 않도록 하려면 다음 단계를 수행합니다.

1.  **Active Directory 사용자 및 컴퓨터**나 다른 Active Directory 또는 계정 프로비전 도구나 스크립트를 사용하여Active Directory 사용자 계정을 사용하지 않도록 설정합니다. 이렇게 하면 연결된 사용자 계정을 사용하여 사서함에 로그온할 수 없습니다.
    

    > [!IMPORTANT]
    > 모든 권한 사서함 권한이 있는 사용자는 사서함에 계속 액세스할 수 있습니다. 다른 사용자가 액세스할 수 없도록 하려면 사서함에서 "모든 권한" 권한을 제거해야 합니다. 사서함에서 "모든 권한" 사서함 권한을 제거하는 방법에 대한 자세한 내용은 <A href="manage-permissions-for-recipients-exchange-online-help.md">받는 사람에 대 한 사용 권한 관리</A>를 참조하십시오.



2.  사서함 사용자가 보내거나 받을 수 있는 메시지의 메시지 크기 제한을 매우 낮은 값(예: 1KB)으로 설정합니다. 이렇게 하면 새 메일이 사서함을 통해 배달되지 않습니다. 자세한 내용은 [사서함에 대 한 메시지 크기 제한 구성](configure-message-size-limits-for-a-mailbox-exchange-2013-help.md)을 참조하십시오.

3.  사서함에 아무도 메시지를 보낼 수 없도록 사서함의 배달 제한을 구성합니다. 자세한 내용은 [사서함에 대 한 메시지 배달 제한 구성](configure-message-delivery-restrictions-for-a-mailbox-exchange-2013-help.md)을 참조하십시오.


> [!IMPORTANT]
> 조직에 필요한 다른 계정 관리 프로세스와 함께 앞의 단계를 수행하되, 사서함을 사용하지 않도록 설정 또는 제거하거나 연결된 사용자 계정을 제거해서는 안 됩니다.



MRM(메시지 보존 관리) 또는 원본 위치 eDiscovery에 대한 사서함 보존을 구현하려면 직원 이직률을 고려해야 합니다. 그만둔 직원의 사서함을 장기간 보존하려면 사서함 서버에 추가 저장소가 필요할 뿐만 아니라 연결된 사용자 계정이 동일한 기간 동안 필요하기 때문에 Active Directory 데이터베이스도 증가하게 됩니다. 또한 조직의 계정 프로비전 및 관리 프로세스도 변경해야 할 수 있습니다.

맨 위로 이동

## 원본 위치 eDiscovery 한계 및 제한 정책

Exchange 2013 및 Exchange Online에서는 제한 정책을 사용하여 원본 위치 eDiscovery가 사용할 수 있는 리소스를 제어합니다.

기본 제한 정책에는 다음과 같은 매개 변수가 포함되어 있습니다.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>매개 변수</th>
<th>설명</th>
<th>기본값</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DiscoveryMaxConcurrency</p></td>
<td><p>조직에서 동시에 실행할 수 있는 원본 위치 eDiscovery 검색의 최대 수입니다.</p></td>
<td><p>2</p>

> [!NOTE]
> 두 이전 검색 여전히 실행 되는 동안 eDiscovery 검색 시작 된 경우 대신 실패와 세번째 검색 대기 되지 않습니다. 새 검색을 성공적으로 시작 하기 전에 이전 검색 결과 중 하나를 완료할 때까지 기다려야 합니다.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxMailboxes</p></td>
<td><p>단일 원본 위치 eDiscovery 검색에서 검색 가능한 최대 사서함 수입니다.</p></td>
<td><p>Exchange Online: 10,0001</p>
<p>Exchange 2013: 5,000</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxStatsSearchMailboxes</p></td>
<td><p>여전히 키워드 통계를 볼 수 있도록 하는 단일 원본 위치 eDiscovery 검색에서 검색할 수 있는 사서함의 최대 수입니다.</p></td>
<td><p>100</p>

> [!NOTE]
> EDiscovery 검색 예상을 실행 하 고 나면 키워드 통계를 볼 수 있습니다. 이러한 통계 검색 쿼리에 사용 되는 각 키워드에 대해 반환 되는 항목 수에 대 한 세부 정보를 표시 합니다. 100 개가 넘는 원본 사서함의 검색에 포함 된, 키워드 통계를 확인 하려고 하면 오류가 반환 됩니다.


</td>
</tr>
<tr class="even">
<td><p>DiscoveryMaxKeywords</p></td>
<td><p>단일 원본 위치 eDiscovery 검색에서 지정 가능한 최대 키워드 수입니다.</p></td>
<td><p>500</p></td>
</tr>
<tr class="odd">
<td><p>DiscoveryMaxSearchResultsPageSize</p></td>
<td><p>원본 위치 eDiscovery 검색 결과를 미리 볼 때 한 페이지에 표시되는 최대 항목 수입니다.</p></td>
<td><p>200</p></td>
</tr>
<tr class="even">
<td><p>DiscoverySearchTimeoutPeriod</p></td>
<td><p>시간이 초과되기 전에 원본 위치 eDiscovery 검색을 실행할 시간(분)입니다.</p></td>
<td><p>10분</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> 1 SharePoint Online Office 365 조직에서의 eDiscovery Center에서 eDiscovery 검색을 시작 하는 경우 단일 검색에서 최대 1, 500 사서함을 검색할 수 있습니다.



Exchange Server 2013에서 요구 사항에 맞게 해당 매개 변수의 기본값을 변경하거나 추가 제한 정책을 만들어서 검색 관리 권한이 위임된 사용자에게 할당할 수 있습니다. IExchange Online에서는 이 같은 제한 매개 변수의 기본값을 변경할 수 없습니다.

## 원본 위치 eDiscovery 설명서

다음 표에는 원본 위치 eDiscovery에 대해 자세히 확인할 수 있는 항목에 대한 링크가 포함되어 있습니다.


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
<td><p><a href="assign-ediscovery-permissions-in-exchange-exchange-2013-help.md">Exchange eDiscovery 사용 권한 할당</a></p></td>
<td><p>EAC에서 원본 위치 eDiscovery를 사용하여 Exchange 사서함을 검색하는 권한을 사용자에게 제공하는 방법을 설명합니다. 사용자를 검색 관리 역할 그룹에 추가해도 해당 사용자가 SharePoint 2013 및 SharePoint Online에서 eDiscovery 센터를 사용하여 Exchange 사서함을 검색할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-discovery-mailbox-exchange-2013-help.md">검색 사서함 만들기</a></p></td>
<td><p>셸을 사용하여 검색 사서함을 만들고 액세스 권한을 할당하는 방법을 설명합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="create-an-in-place-ediscovery-search-exchange-2013-help.md">원본 위치 eDiscovery 검색 만들기</a></p></td>
<td><p>원본 위치 eDiscovery 검색을 만드는 방법과 eDiscovery 검색 결과를 예상하고 미리 보는 방법을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=506799">메시지 속성 및 원본 위치 ediscovery 검색 연산자</a></p></td>
<td><p>원본 위치 eDiscovery를 사용하여 검색할 수 있는 전자 메일 메시지 속성을 알아봅니다. 이 항목에서는 각 속성의 구문 예, <strong>AND</strong> 및 <strong>OR</strong>과 같은 검색 연산자에 대한 정보와 큰따옴표(&quot; &quot;) 및 접두사 와일드카드 사용과 같은 기타 검색 쿼리 방법에 대한 정보가 제공됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://technet.microsoft.com/ko-kr/library/dn798915(v=exchg.150)">Exchange Online에서 원본 위치 ediscovery 검색 제한</a></p></td>
<td><p>도움이 되는 Exchange Online 의 설명에 전체 eDiscovery 한계 상태 및 Office 365 조직에 대해 eDiscovery 서비스의 품질을 유지 합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="start-or-stop-an-in-place-ediscovery-search-exchange-2013-help.md">시작 하거나 원본 위치 eDiscovery 검색을 중지 합니다.</a></p></td>
<td><p>eDiscovery 검색을 시작, 중지 및 다시 시작하는 방법을 설명합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">원본 위치 eDiscovery 검색 수정</a></p></td>
<td><p>기존 eDiscovery 검색을 수정하는 방법을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="copy-ediscovery-search-results-to-a-discovery-mailbox-exchange-2013-help.md">EDiscovery 검색 결과 검색 사서함으로 복사</a></p></td>
<td><p>eDiscovery 검색의 결과를 검색 사서함으로 복사하는 방법을 설명합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="export-ediscovery-search-results-to-a-pst-file-exchange-2013-help.md">PST 파일로 eDiscovery 검색 결과 내보내기</a></p></td>
<td><p>eDiscovery 검색의 결과를 PST 파일로 내보내는 방법을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-a-custom-management-scope-for-in-place-ediscovery-searches-exchange-2013-help.md">원본 위치 eDiscovery 검색의 사용자 지정 관리 범위 만들기</a></p></td>
<td><p>사용자 지정 관리 범위를 사용하여 검색 관리자가 검색할 수 있는 사서함을 제한하는 방법을 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="remove-an-in-place-ediscovery-search-exchange-2013-help.md">원본 위치 eDiscovery 검색 제거</a></p></td>
<td><p>eDiscovery 검색을 삭제하는 방법을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="search-for-and-delete-messages-admin-help-exchange-2013-help.md">메시지-관리자 도움말에 대 한 검색 및 삭제</a></p></td>
<td><p>검색 한 다음 전자 메일 메시지를 삭제 하려면 <strong>Search-Mailbox</strong> cmdlet을 사용 하는 방법에 알아봅니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="reduce-the-size-of-a-discovery-mailbox-in-exchange-exchange-2013-help.md">Exchange에서 검색 사서함의 크기 줄이기</a></p></td>
<td><p>50GB보다 큰 검색 사서함의 크기를 줄이려면 이 프로세스를 사용합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="delete-and-re-create-the-default-discovery-mailbox-in-exchange-exchange-2013-help.md">Exchange에서 기본 검색 사서함 삭제 및 다시 만들기</a></p></td>
<td><p>기본 검색 사서함을 삭제한 후 다시 만든 다음 사용 권한을 할당하는 방법을 알아봅니다. 이 사서함이 50GB 제한을 초과하며 검색 결과가 필요하지 않은 경우에는 이 절차를 사용합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="re-create-the-discovery-system-mailbox-exchange-2013-help.md">검색 시스템 사서함을 다시 만들려면</a></p></td>
<td><p>검색 시스템 사서함을 다시 만드는 방법을 설명합니다. 이 작업은 Exchange 2013 조직에만 적용됩니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md">OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원</a></p></td>
<td><p>Exchange 하이브리드 배포에서 OAuth 인증을 구성해야 하는 eDiscovery 시나리오에 대해 설명합니다.</p></td>
</tr>
<tr class="odd">
<td><p><a href="configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md">SharePoint eDiscovery 센터에 대한 Exchange 구성</a></p></td>
<td><p>SharePoint 2013에서 eDiscovery 센터를 사용하여 Exchange 사서함을 검색할 수 있도록 Exchange 2013을 구성하는 방법을 설명합니다.</p></td>
</tr>
<tr class="even">
<td><p><a href="unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md">Exchange eDiscovery의 검색할 수 없는 항목</a></p></td>
<td><p>Exchange 검색을 통해 인덱싱할 수 없으며 eDiscovery 검색 결과에서 검색할 수 없는 항목으로 반환되는 사서함 항목에 대해 설명합니다.</p></td>
</tr>
</tbody>
</table>


Office 365, Exchange 2013, SharePoint 2013 및 Lync 2013의 eDiscovery에 대 한 자세한 내용은 [eDiscovery FAQ](https://go.microsoft.com/fwlink/p/?linkid=386633)를 참조 하십시오.

맨 위로 이동

