---
title: 'SharePoint eDiscovery 센터에 대한 Exchange 구성: Exchange 2013 Help'
TOCTitle: SharePoint eDiscovery 센터에 대한 Exchange 구성
ms:assetid: 795c1a3b-295c-4ee5-ade9-52cf3fda3f19
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ218665(v=EXCHG.150)
ms:contentKeyID: 50483497
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SharePoint eDiscovery 센터에 대한 Exchange 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange Server 2013에는 *파트너 응용 프로그램*이라고 하는 Microsoft SharePoint Server 2013 및 Microsoft Lync Server 2013에서 작동하는 기능이 포함되어 있습니다. 이러한 파트너 응용 프로그램이 각 리소스에 서로 액세스할 수 있도록 하려면 서버 간 인증을 구성해야 합니다.

이 항목에서는 사용자가 SharePoint 2013 에서 eDiscovery 센터를 사용 하 여 Exchange Server 2013 사서함 콘텐츠를 검색할 수 있도록 Exchange 2013 사이의 SharePoint 2013 서버-서버 인증을 구성 하는 방법을 보여줍니다. 이 기능을 완벽 하 게 사용 하려면 SharePoint 2013 의 추가 단계를 완료 해야 합니다. 자세한 내용은 [SharePoint 2013에서 Configure eDiscovery](https://go.microsoft.com/fwlink/?linkid=257727)를 참조 합니다.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 30분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 서로 다른 도메인 또는 포리스트에 Exchange 2013과 SharePoint 2013을 설치할 수 있습니다. Exchange 포리스트와 SharePoint 포리스트 간의 Windows 트러스트 관계는 필요하지 않은데, 이 경우 Exchange와 SharePoint가 OAuth 2.0 프로토콜을 사용하여 서로 트러스트하기 때문입니다.

  - SharePoint 2013 사이트가 SSL(Secure Sockets Layer)을 사용하도록 구성되어 있어야 합니다.

  - [Exchange 웹 서비스 관리 API](https://go.microsoft.com/fwlink/?linkid=257726) SharePoint 2013 를 실행 하는 모든 서버에 설치 해야 합니다. 설치 후 인터넷 정보 서버 (IIS)를 다시 설정 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: SharePoint Server 2013을 실행하는 서버에서 Exchange 2013에 대한 서버 간 인증 구성

다음 명령을 실행하여 Exchange 2013에서 SharePoint 2013을 신뢰할 수 있는 보안 토큰 발급자로 만듭니다.

    New-SPTrustedSecurityTokenIssuer -Name Exchange -MetadataEndPoint https://<Exchange Server Name or FQDN>/autodiscover/metadata/json/1

## 2단계: Exchange 2013을 실행하는 서버에서 SharePoint 2013에 대한 서버 간 인증 구성

Exchange 2013 서버에서 이 단계를 수행합니다. 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[공유 및 공동 작업 사용 권한](sharing-and-collaboration-permissions-exchange-2013-help.md)의 "파트너 응용 프로그램 - 구성" 항목

다음 명령을 실행하여 SharePoint 파트너 응용 프로그램을 구성합니다.

    cd c:\'Program Files'\Microsoft\'Exchange Server'\V15\Scripts
    .\Configure-EnterprisePartnerApplication.ps1 -AuthMetadataUrl <path to SharePoint AuthMetadataUrl> -ApplicationType SharePoint

## 3단계: 검색 관리 역할 그룹에 권한 있는 사용자 추가

SharePoint 2013을 사용하여 eDiscovery 검색을 수행해야 하는 사용자를 Exchange 2013의 검색 관리 역할 그룹에 추가합니다. 자세한 내용은 [Exchange eDiscovery 사용 권한 할당](assign-ediscovery-permissions-in-exchange-exchange-2013-help.md)를 참조하십시오.


> [!WARNING]
> 검색 관리 역할 그룹에 사용자를 추가하면 해당 사용자는 원본 위치 eDiscovery를 사용하여 모든 Exchange 2013 사서함을 검색하고 사용자 사서함의 중요한 전자 메일 내용에 잠재적으로 액세스할 수 있습니다. 기본적으로 이 사용 권한은 조직 관리 역할 그룹의 구성원을 포함하여 어떠한 사용자에게도 할당되지 않습니다. 사용자에게 이 사용 권한을 할당하기 전에 조직의 법무 또는 HR 부서에 문의하십시오.


