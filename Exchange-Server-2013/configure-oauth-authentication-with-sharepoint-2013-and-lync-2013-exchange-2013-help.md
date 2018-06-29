---
title: 'SharePoint 2013 및 Lync 2013 OAuth 인증 구성: Exchange 2013 Help'
TOCTitle: SharePoint 2013 및 Lync 2013 OAuth 인증 구성
ms:assetid: ca3c78a3-80cc-4df2-859f-0106bbd57a07
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ649094(v=EXCHG.150)
ms:contentKeyID: 50484141
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SharePoint 2013 및 Lync 2013 OAuth 인증 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-03-03_

Exchange Server 2013에서는 다른 응용 프로그램이 OAuth를 사용하여 Exchange를 인증할 수 있습니다. 해당 응용 프로그램은 Exchange 2013에서 파트너 응용 프로그램으로 구성되어야 합니다.

Exchange 2013에서 SharePoint 2013 및 Lync Server 2013 같은 파트너 응용 프로그램을 통한 OAuth 구성은 `Configure-EnterpriseApplication.ps1` 스크립트를 사용할 때만 지원됩니다. 스크립트는 작업을 자동화하여 파트너 응용 프로그램을 통한 인증을 보다 쉽게 구성할 수 있도록 하고 구성 오류를 줄여 줍니다. 스크립트는 다음 작업을 수행합니다.

1.  OAuth 토큰을 자체 발급하는 Exchange 파트너 응용 프로그램이 Exchange를 성공적으로 인증하도록 구성합니다.

2.  특정 Exchange 웹 서비스 API 호출을 위해 RBAC(역할 기반 액세스 제어) 역할을 파트너 응용 프로그램에 할당하여 인증합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 파트너 응용 프로그램은 Exchange 2013에 대한 인증 메타데이터 문서를 게시하여 이 응용 프로그램에 대한 직접 신뢰를 설정하고 인증 요청을 수락해야 합니다.

  - 이 항목의 예에서는 `\Scripts` 디렉터리의 다음 기본 위치를 사용합니다. `C:\Program Files\Microsoft\Exchange Server\V15\Scripts`.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md)의 "파트너 응용 프로그램 - 구성" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 파트너 응용 프로그램을 통한 OAuth 인증 구성

이 절차에서는 `Configure-EntepririseApplication.ps1` 스크립트를 사용하여 파트너 응용 프로그램을 통한 OAuth 인증을 구성합니다. 리소스 액세스 여부는 파트너 응용 프로그램 및/또는 RBAC를 사용하여 가장하는 사용자에게 할당된 사용 권한에 따라 다릅니다.

Exchange에서 OAuth 인증을 구성하고 나면 파트너 응용 프로그램이 Exchange 2013 리소스를 사용할 수 있습니다. Exchange 2013 또한 파트너 응용 프로그램이 제공하는 리소스에 액세스해야 하는 경우 파트너 응용프로그램에서도 마찬가지로 OAuth 인증을 구성해야 합니다.

이 예에서는 SharePoint 2013에 대한 OAuth 인증을 구성합니다.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://sharepoint.contoso.com/_layouts/15/metadata/json/1 -ApplicationType SharePoint

이 예에서는 Lync Server 2013에 대한 OAuth 인증을 구성합니다.

    Cd C:\Program Files\Microsoft\Exchange Server\V15\Scripts
    Configure-EnterprisePartnerApplication.ps1 -AuthMetaDataUrl https://lync.contoso.com/metadata/json/1 -ApplicationType Lync

## 작동 여부는 어떻게 확인합니까?

엔터프라이즈 파트너 응용 프로그램이 Exchange 2013을 인증하도록 성공적으로 구성했는지 확인하려면 셸에서 [Get-PartnerApplication](https://technet.microsoft.com/ko-kr/library/jj218721\(v=exchg.150\)) cmdlet을 실행하여 구성을 검색하십시오. 또한 [Test-OAuthConnectivity](https://technet.microsoft.com/ko-kr/library/jj218623\(v=exchg.150\)) cmdlet을 실행하여 사용자에 대해 파트너 응용 프로그램을 통한 OAuth 연결을 테스트할 수도 있습니다.

## 추가 정보

  - 하이브리드 배포에서는 온-프레미스 Exchange 2013 조직과 Exchange Online 조직 간에 OAuth 인증을 사용할 수 있습니다. 자세한 내용은 [OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)를 참조하세요.

  - 온-프레미스 배포에서는 관리자 및 준수 담당자가 SharePoint 2013에서 eDiscovery Center를 사용하여 Exchange 2013 사서함을 검색할 수 있도록 Exchange 2013 및 SharePoint 2013 간에 서버 간 인증을 구성할 수 있습니다. 자세한 내용은 [SharePoint eDiscovery 센터에 대한 Exchange 구성](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)를 참조하세요.

