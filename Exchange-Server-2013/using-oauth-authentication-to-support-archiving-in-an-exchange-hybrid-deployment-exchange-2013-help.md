---
title: 'OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 보관 지원: Exchange 2013 Help'
TOCTitle: OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 보관 지원
ms:assetid: deb882b1-1ae2-40f3-a71c-423fafe3d66a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn689104(v=EXCHG.150)
ms:contentKeyID: 62247284
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 보관 지원

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange 2013 하이브리드 배포에 있으며 Exchange Server용 EOA(Exchange Online Archiving)를 사용하는 경우 Exchange 2013 CU5(누적 업데이트 5)로 업그레이드한 후에 온-프레미스 및 Exchange Online 조직 간에 OAuth 인증을 구성해야 합니다. EOA는 온-프레미스 사서함이 있는 사용자에 대해 클라우드 기반 보관을 허용합니다. 이 시나리오에서 온-프레미스 사서함 서버의 MRM(메시징 레코드 관리) 도우미는 보관 정책을 적용하고 사용자의 사서함에서 클라우드 기반 보관 저장소로 메시지를 자동으로 이동합니다. Exchange 2013 CU5에서는 OAuth 인증이 사용됩니다.

OAuth 인증 구성을 위한 단계별 지침은 [Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)을 참조하세요.

## OAuth 인증이란?

OAuth 인증은 응용 프로그램이 서로 인증할 수 있도록 하는 서버 간 인증 프로토콜입니다. OAuth 인증을 사용할 경우 사용자 자격 증명 및 암호가 한 컴퓨터에서 다른 컴퓨터로 전달되지 않습니다. 대신 인증 및 권한 부여는 보안 토큰이 교환되면서 수행됩니다. 이러한 토큰은 일정 시간 동안 특정 리소스 집합에 대한 액세스 권한을 부여합니다.

OAuth 인증 일반적으로 세 당사자: 단일 인증 서버와 서로 통신 하는 두 영역입니다. 보안 토큰에; 통신 하는 두 영역에는 인증 서버 (라고도 하는 보안 토큰 서버)에서 발급 한 이러한 토큰에 다른 영역에서 한 영역에서 들어오는 통신을 신뢰 해야 하는지 확인 합니다. 온-프레미스 Exchange 조직 및 Exchange Online 간에 OAuth 인증을 사용 하는 경우에 인증 서버의 함수 Azure Active Directory ACS(액세스 제어 서비스) Office 365 조직에서에서 제공 됩니다. 예 크로스-프레미스 eDiscovery 검색을 하는 동안 Azure Active Directory ACS 관리자가 다음을 확인 하는 토큰을 발급 또는 규정 준수 담당자가 Exchange에서 온-프레미스 조직이 Exchange Online 조직 및 그 반대의 경우에는 사서함에 액세스할 수 있습니다.

## 보관을 지원하도록 OAuth 인증 구성

앞서 설명한 것처럼 Exchange 하이브리드 배포에서 보관을 지원하도록 OAuth 인증을 구성하기 위한 지침을 보려면 [Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성](configure-oauth-authentication-between-exchange-and-exchange-online-organizations-exchange-2013-help.md)을 참조하세요.

Exchange 하이브리드 배포에 대해 OAuth이 구성되지 않은 경우 온-프레미스 조직에 있는 사용자의 기본 사서함의 항목을 Exchange Online에 있는 사용자의 클라우드 기반 보관 저장소로 자동으로 이동하는 보관 정책을 사용할 수 없습니다.

## 추가 정보

  - 또한 단일 eDiscovery 검색에서 온-프레미스 및 클라우드 기반 사서함의 크로스 프레미스 eDiscovery 검색을 수행하도록 OAuth 인증을 구성해야 합니다. [OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원](using-oauth-authentication-to-support-ediscovery-in-an-exchange-hybrid-deployment-exchange-2013-help.md)을 참조하세요.

  - SharePoint 2013 및 Lync Server 2013과 같은 기타 응용 프로그램이 Exchange 2013에서 인증되도록 OAuth을 구성할 수도 있습니다. 자세한 내용은 [SharePoint 2013 및 Lync 2013 OAuth 인증 구성](configure-oauth-authentication-with-sharepoint-2013-and-lync-2013-exchange-2013-help.md)을 참조하세요.

  - 관리자 및 규정 준수 담당자가 SharePoint 2013의 eDiscovery 센터를 사용하여 Exchange 2013 사서함을 검색할 수 있도록 Exchange 2013 및 SharePoint 2013 사이에 서버 간 인증을 구성할 수 있습니다. 자세한 내용은 [SharePoint eDiscovery 센터에 대한 Exchange 구성](configure-exchange-for-sharepoint-ediscovery-center-exchange-2013-help.md)을 참조하세요.

  - Exchange 2013 에서 하이브리드 구성 마법사를 사용 하 여 Exchange 하이브리드 배포를 구성할 수 있습니다. 사용자 지정, 단계별 하이브리드 배포 구성 검사 목록에 대 한 [Exchange Server 배포 도우미](https://go.microsoft.com/fwlink/p/?linkid=277105)를 참조 하십시오.

