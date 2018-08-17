﻿---
title: '하이브리드 구성 마법사를 사용하여 하이브리드 배포 만들기: Exchange 2013 Help'
TOCTitle: 하이브리드 구성 마법사를 사용하여 하이브리드 배포 만들기
ms:assetid: 997a25d3-7fb3-4d4e-bb28-defcbf542c99
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ200787(v=EXCHG.150)
ms:contentKeyID: 50484633
ms.date: 03/15/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 하이브리드 구성 마법사를 사용하여 하이브리드 배포 만들기

이 항목은 진행 중입니다.  

_<strong>적용 대상:</strong>Exchange Online, Exchange Server 2013, Exchange Server 2016_

_<strong>마지막으로 수정된 항목:</strong>2016-12-09_

하이브리드 배포를 설정하면 기존 온-프레미스 Exchange Server 조직의 풍부한 기능과 관리 제어 능력을 클라우드로 확장할 수 있습니다. 하이브리드 배포는 또한 Exchange Online Archiving을 통해 온-프레미스 사서함에 대해 클라우드 기반 보관 솔루션을 지원하며, 온-프레미스 사서함을 Exchange Online으로 완전히 마이그레이션하기 위한 중간 단계 역할도 수행합니다.

이 항목에서는 대기업용 Office 365에서 하이브리드 구성 마법사를 사용하여 온-프레미스 Exchange 조직 및 Exchange Online 조직에 대해 하이브리드 배포를 구성하는 방법에 대해 설명합니다. 이 항목에서는 다음 조직 구성에 대해 하이브리드 배포를 만듭니다.

  - 온-프레미스 조직이 단일 포리스트 온-프레미스 Exchange 조직입니다.

  - 온-프레미스 조직이 온-프레미스 보호를 위해 기존의 Microsoft EOP(Exchange Online Protection) 서비스를 사용하지 않습니다.

  - 온-프레미스 조직에 Edge 전송 서버가 배포되어 있지 않습니다. 하이브리드 구성 마법사는 하이브리드 배포의 일부로서 Edge 전송 서버 구성을 지원하지만, 마법사에서 Edge 전송 서버를 구성하는 방법은 이 항목에서 다루지 않습니다.


> [!IMPORTANT]
> 하이브리드 구성 마법사로 하이브리드 배포를 구성하는 경우, 마법사를 성공적으로 완료하고 하이브리드 배포 기능이 올바르게 작동하도록 하려면 몇 가지 중요한 선행 조건이 필요합니다. 하이브리드 구성 마법사를 사용하여 하이브리드 배포를 만들고 구성하기 전에 <A href="hybrid-deployment-prerequisites-exchange-2013-help.md">하이브리드 배포 필수 구성 요소</A>에 요약되어 있는 모든 선행 조건을 완료해야 합니다.<BR>또한 <A href="http://technet.microsoft.com/exdeploy2013">Exchange Server 배포 도우미</A>는 온-프레미스 조직 및 Office 365 간에 하이브리드 배포를 구성하거나 Office 365로 완전히 마이그레이션하도록 도와주는 무료 웹 기반 도구입니다. 이 도구는 몇 가지 단순한 질문을 제기한 다음 사용자의 답변에 따라 하이브리드 배포 구성 지침이 담긴 사용자 지정 검사 목록을 만듭니다. 배포 도우미를 사용해서 특정 조직의 요구에 맞는 사용자 지정 하이브리드 배포 검사 목록을 생성하는 것이 좋습니다.



하이브리드 배포와 관련된 추가 관리 작업에 대한 자세한 내용은 [하이브리드 배포 절차](hybrid-deployment-procedures-exchange-2013-help.md) 항목을 참조하세요.

하이브리드 배포에 대한 자세한 내용은 [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 참조하십시오. Office 365에 대한 자세한 내용은 [Office 365란?](http://go.microsoft.com/fwlink/?linkid=266712)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분
    

    > [!IMPORTANT]
    > 하이브리드 배포를 위한 요구 사항을 구성하는 데에는 이 항목에서 설명한 하이브리드 구성 마법사 절차를 완료하기 위한 예상 시간보다 훨씬 더 오랜 시간이 걸립니다. 예를 들어 대기업용 Office 365에 등록하고, Active Directory 동기화를 구성하고, Exchange Online 라이선스를 할당하려면 상당히 많은 시간을 투자해야 하며 네트워크 토폴로지도 변경해야 할 수 있습니다. 종단 간 하이브리드 배포 구성을 완료하기 위한 전체적인 시간에 이 절차의 완료에 걸리는 것으로 표시된 시간보다 더 많은 시간을 계획해야 합니다.



  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[Exchange 및 셸 인프라 권한](https://technet.microsoft.com/ko-kr/library/dd638114\(v=exchg.150\)) 항목의 "하이브리드 배포" 항목을 참조하십시오.

  - 지원되는 최신 릴리스의 Exchange를 실행하는 컴퓨터에서 하이브리드 구성 마법사를 실행해야 합니다. 하이브리드 구성 마법사에서 Exchange OAuth 인증을 구성하기 위한 최종 단계에서는 온-프레미스 Exchange 또는 도메인 가입 서버나 워크스테이션에서 작업을 수행해야 합니다. 또한 OAuth 인증 프로세스는 데스크톱 버전의 Internet Explorer 11 이상을 사용할 때 가장 잘 작동합니다.

  - [Exchange Server 하이브리드 배포](exchange-server-hybrid-deployments-exchange-2013-help.md)를 검토하고, 하이브리드 배포 구성의 영향을 받게 될 영역을 파악합니다.

  - [하이브리드 배포 필수 구성 요소](hybrid-deployment-prerequisites-exchange-2013-help.md)에 설명된 모든 하이브리드 배포 요구 사항을 검토하고 완료합니다.

  - Microsoft 원격 연결 분석기 도구는 온-프레미스 Exchange 조직의 외부 연결을 확인하여 하이브리드 배포를 구성할 준비가 되었는지 확인합니다. 하이브리드 구성 마법사로 하이브리드 배포를 구성하기 전에 원격 연결 분석기 도구를 사용하여 온-프레미스 조직을 확인하는 것이 좋습니다. 자세한 내용은 [원격 연결 분석기 도구](http://go.microsoft.com/fwlink/p/?linkid=167905)를 참조하십시오.

  - Azure Active Directory Connect 암호 동기화를 사용하여 이 Single Sign-On을 구성하는 것이 좋습니다. Single Sign-On을 사용하면 사용자는 단일 사용자 이름과 암호로 온-프레미스 조직과 Exchange Online 조직 모두에 액세스할 수 있습니다. 또한 Exchange Online Archiving을 사용하는 경우 Exchange Online 조직에 저장된 콘텐츠에 액세스할 때 자격 증명을 입력하라는 메시지가 표시되지 않습니다. 암호 동기화에 대 한 자세한 내용은 [Azure AD 연결 동기화: 암호 동기화 구현](http://go.microsoft.com/fwlink/p/?linkid=723513)을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](https://technet.microsoft.com/ko-kr/library/jj150484\(v=exchg.150\))을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Exchange 관리 센터 및 하이브리드 구성 마법사를 사용하여 하이브리드 배포 만들기

하이브리드 배포를 만들고 구성하려면 다음 절차를 사용합니다.

1.  온-프레미스 조직에 있는 Exchange 서버의 EAC에서 **하이브리드** 노드로 이동합니다.

2.  **하이브리드** 노드에서 **구성**을 클릭하여 Office 365 자격 증명을 입력합니다.
    

    > [!IMPORTANT]
    > 온-프레미스 조직이 중국에 있으며 Office 365 테넌트를 21Vianet에서 호스팅하는 경우 <STRONG>내 Office 365 조직을 21Vianet에서 호스팅</STRONG> 확인란을 선택해야 합니다. Office 365 테넌트가 21Vianet에서 호스팅되는데 이 확인란을 선택하지 않으면 하이브리드 구성 마법사가 21Vianet 서비스에 연결되지 않으며 Office 365 계정 자격 증명이 인식되지 않고 마법사도 제대로 완료되지 않습니다.



3.  Office 365에 로그인하라는 메시지가 표시되면 **Office 365에 로그인**을 선택하고 계정 자격 증명을 입력합니다. 로그인하는 계정은 Office 365의 전역 관리자여야 합니다.

4.  하이브리드 구성 마법사를 시작하려면 **구성**을 다시 클릭합니다.

5.  **Microsoft Office 365 하이브리드 구성 마법사 다운로드** 페이지에서 **여기를 클릭**하여 마법사를 다운로드합니다. 메시지가 표시되면 **응용 프로그램 설치** 대화 상자에서 **설치**를 클릭합니다.

6.  **다음**을 선택한 후 **온-프레미스 Exchange Server 조직** 섹션에서 **Exchange 2013 CAS 또는 2016 Exchange를 실행하는 서버 검색**을 선택합니다. 마법사가 온-프레미스 Exchange 서버를 검색합니다. 마법사가 Exchange 서버를 검색하지 못하는 경우 또는 다른 서버를 사용하려는 경우 **Exchange 2013 CAS 또는 Exchange 2016을 실행하는 서버 지정**을 선택한 다음 Exchange 사서함 서버의 내부 FQDN을 지정합니다.

7.  **Office 365 Exchange Online** 섹션에서 **Microsoft Office 365**를 선택한 후 **다음**을 클릭합니다.

8.  **자격 증명** 페이지의 **온-프레미스 계정 자격 증명 입력** 섹션에서 온-프레미스 Active Directory 및 Exchange 서버에 액세스하기 위해 로그인하는 계정을 마법사가 사용하도록 **현재 Windows 자격 증명 사용**을 선택합니다. 다른 자격 증명 집합을 지정하려면 **현재 Windows 자격 증명 사용**을 선택 취소하고 사용하려는 Active Directory 계정의 사용자 이름과 암호를 지정합니다. 어느 계정을 사용하든 해당 계정은 Enterprise Admins 보안 그룹의 구성원이어야 합니다.

9.  **Office 365 자격 증명 입력** 섹션에서 전역 관리자 권한이 있는 Office 365 계정의 사용자 이름과 암호를 지정합니다. **다음**을 클릭합니다.

10. **연결 및 자격 증명 유효성 검사** 페이지에서 마법사가 하 여 온-프레미스 조직과 Office 365 조직 모두에 연결하여 자격 증명의 유효성을 확인하고 두 조직의 현재 구성을 검사합니다. 완료되면 **다음**을 클릭합니다.

11. **하이브리드 도메인**에서 하이브리드 배포에 포함할 도메인을 선택합니다. 대부분의 배포에는 각 도메인의 **자동 검색** 열의 설정을 **False**로 그대로 둘 수 있습니다. 특정 도메인의 자동 검색 정보를 마법사가 강제로 사용하도록 해야 하는 경우 도메인 옆에 있는 **True**만 선택합니다. **다음**을 클릭합니다.
    

    > [!IMPORTANT]
    > 하이브리드 구성 마법사를 실행할 때 이러한 도메인 선택 단계가 나타날 수도 있고 나타나지 않을 수도 있습니다.<BR>다음과 같은 경우에는 이 단계가 나타나지 않습니다. 
    > <UL>
    > <LI>
    > <P>Office&nbsp;365 테넌트에 추가된 온-프레미스 허용 도메인이 하나뿐인 경우. 이것이 하이브리드 배포 구성에 사용할 수 있는 유일한 도메인이므로 자동으로 선택되고 마법사에서 이 단계가 생략됩니다.</P>
    > <LI>
    > <P>Office&nbsp;365 테넌트에 추가된 온-프레미스 허용 도메인이 없는 경우. 이 경우 오류 메시지가 표시되며, 계속 진행하려면 Office&nbsp;365 테넌트에 적어도 하나의 도메인을 추가해야 합니다. 이렇게 하려면 Office&nbsp;365 관리 포털을 사용하거나 선택적으로 온-프레미스 조직에서 AD&nbsp;FS(Active Directory Federation Services)를 구성할 수 있습니다.</P></LI></UL>Office&nbsp;365 테넌트에 추가된 온-프레미스 허용 도메인이 둘 이상인 경우 이 단계가 나타납니다.



12. **페더레이션 트러스트** 페이지에서 **사용**, **다음**을 차례로 클릭합니다.

13. **도메인 소유** 페이지에서 **클립보드에 복사**를 클릭하여 하이브리드 배포에 포함하기 위해 선택한 도메인에 대한 도메인 증명 토큰 정보를 복사합니다. 메모장과 같은 텍스트 편집기를 열고 이러한 도메인에 대한 토큰 정보를 붙여넣습니다. 하이브리드 구성 마법사를 계속 진행하기 전에 이 정보를 사용하여 공용 DNS의 각 도메인에 대해 TXT 레코드를 만들어야 합니다. TXT 레코드를 DNS 영역에 추가하는 방법에 대한 자세한 내용은 DNS 호스트 도움말을 참조하세요. TXT 레코드가 생성되고 DNS 레코드가 복제된 후 **다음**을 클릭합니다.

14. **전송 인증서** 페이지의 **참조 서버 선택** 필드에서 검사 목록의 앞부분에서 구성한 인증서가 있는 Exchange 서버를 선택합니다.

15. **인증서 선택** 필드에서 보안 메일 전송에 사용할 인증서를 선택합니다. 이 목록에는 이전 단계에서 선택한 사서함 서버에 설치된, 타사 CA(인증 기관)에서 발급한 디지털 인증서가 표시됩니다. **다음**을 클릭합니다.

16. **조직 FQDN** 페이지에서 인터넷 연결 Exchange 서버에 대해 외부에서 액세스할 수 있는 FQDN을 입력합니다. Office 365는 이 FQDN을 사용하여 Exchange 조직 간 보안 메일 전송을 위한 서비스 커넥터를 구성합니다. 예를 들어 “mail.contoso.com”을 입력합니다. **다음**을 클릭합니다.

17. 하이브리드 배포 구성 선택 사항이 업데이트되었으며, Exchange 서비스 변경과 하이브리드 배포 구성을 시작할 준비가 되었습니다. **업데이트**를 클릭하여 구성 프로세스를 시작합니다. 하이브리드 구성 프로세스가 실행 중인 동안에는 하이브리드 배포에 대해 구성 중인 기능 및 서비스 영역이 업데이트됨에 따라 마법사에 표시됩니다.

18. 마법사에 완료 메시지가 표시되고 **닫기** 단추가 표시됩니다. **닫기**를 클릭하여 하이브리드 배포 구성 프로세스를 완료하고 마법사를 닫습니다.

## Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성

혼합된 Exchange 2013/2010 및 Exchange 2013/2007 하이브리드 배포에서는 하이브리드 구성 마법사에 의해 Office 365와 온-프레미스 Exchange 조직 간에 새로운 하이브리드 배포 OAuth 기반 인증 연결이 구성되지 않습니다. 이러한 배포는 기본적으로 페더레이션 트러스트 프로세스를 계속 사용합니다. 그렇지만 MRM(메시지 레코드 관리), Exchange 원본 위치 보관 및 원본 위치 eDiscovery와 같은 특정 Exchange 2013 기능은 새로운 Exchange OAuth 인증 프로토콜을 사용해야만 조직에서 완전히 사용 가능해집니다. Exchange Online에서 새 하이브리드 배포의 일부로 이러한 기능을 구현하려는 모든 혼합 Exchange 2013/2010 및 Exchange 2013/2007 조직은 하이브리드 구성 마법사를 사용하여 하이브리드 배포를 구성한 후에 Exchange OAuth 인증을 구성하는 것이 좋습니다.

자세한 구성 단계는 [Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성](https://technet.microsoft.com/ko-kr/library/dn594521\(v=exchg.150\))을 참조하세요.

OAuth 인증을 사용하는 Exchange 보안 및 규정 준수 기능에 대한 자세한 내용은 다음을 참조하세요.

  - [OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 보관 지원](https://technet.microsoft.com/ko-kr/library/dn689104\(v=exchg.150\))

  - [OAuth 인증을 사용하여 Exchange 하이브리드 배포에서 eDiscovery 지원](https://technet.microsoft.com/ko-kr/library/dn497703\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

하이브리드 구성 마법사의 성공적인 완료는 하이브리드 구성 단계가 완료를 향해 예상대로 진행되고 있음을 나타내는 첫 번째 표시입니다.

하이브리드 배포를 성공적으로 만들고 구성했는지를 더 확인하려면 다음을 수행합니다.

  - 온-프레미스 조직용 Exchange 관리 셸에서 다음 명령을 실행합니다. 이 명령을 실행하면 하이브리드 배포 구성 값과 설정, 하이브리드 기능 및 전송 끝점이 표시됩니다. 이러한 값이 올바른지 확인합니다.
    
        Get-HybridConfiguration

  - 하이브리드 구성 로그를 검사하여 하이브리드 구성 마법사가 모든 구성 단계를 완료했는지 확인합니다. 기본적으로 로그는 온-프레미스 사서함 서버의 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Update-HybridConfiguration에 있습니다.

  - 기존의 온-프레미스 사서함을 Exchange Online 조직으로 이동하여 사서함 이동 기능 지원을 테스트하거나, Exchange Online 조직에 새로운 사용자 사서함을 만들어 두 조직 간 약속 있음/없음 일정 공유를 테스트합니다. 두 사서함 작업 중 하나를 수행하면 온-프레미스 조직과 Exchange Online 조직 간 메시지 배달이 올바르게 작동하는지, 메시지 배달이 안전하며 Exchange 조직으로 가는 내부 메시지로 처리되는지 테스트하고 확인할 수 있습니다.
    
      - EAC를 사용하고 **엔터프라이즈** \> **받는 사람** \> **사서함**으로 이동하여 Exchange Online에 새 원격 사서함을 만듭니다.
    
      - EAC를 사용하고 **Office 365** \> **받는 사람** \> **마이그레이션**으로 이동하여 기존 사서함을 Exchange Online으로 이동합니다.

