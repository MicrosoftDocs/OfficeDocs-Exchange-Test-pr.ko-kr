---
title: '페더레이션: Exchange 2013 Help'
TOCTitle: 페더레이션
ms:assetid: 0046e2eb-6940-4941-bd5b-cbe6bffa3b94
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335047(v=EXCHG.150)
ms:contentKeyID: 50482382
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

정보 근로자는 외부 받는 사람, 공급업체, 파트너 및 고객과 공동 작업을 하고 약속 있음/없음(일정 있음/없음이라고도 함) 정보를 공유해야 하는 경우가 많습니다. Microsoft Exchange Server 2013의 페더레이션은 이러한 공동 작업에 도움이 됩니다. *페더레이션*은 *페더레이션 공유*를 지원하는 기본 트러스트 인프라를 나타내며 사용자가 다른 외부 페더레이션 조직의 받는 사람과 일정 정보를 쉽게 공유할 수 있는 방법입니다. 페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



**목차**

Key terminology

Azure AD 인증 시스템

Federation trust

Federated organization identifier

Federation example

Certificate requirements for Federation

Transitioning to a new certificate

Firewall Considerations for Federation

## 주요 용어

다음 표에서는 Exchange 2013의 페더레이션과 관련된 핵심 구성 요소를 정의합니다.

  - **AppID(응용 프로그램 식별자)**  
    하는 고유 번호 Azure Active Directory 인증 시스템에서 생성 된 Exchange 조직을 식별할 수 있습니다. AppID는 Azure Active Directory 인증 시스템과 페더레이션 트러스트를 만들 때 자동으로 생성 됩니다.

<!-- end list -->

  - **위임 토큰**  
    하나의 페더레이션된 조직에서 사용자가 다른 페더레이션된 조직을 신뢰 하도록 허용 하는 Azure Active Directory 인증 시스템에서 발급 한 보안 어설션을 SAML (Markup Language) 토큰입니다. 위임 토큰 사용자의 전자 메일 주소, 변경할 수 없는 식별자 및 연관 된 작업에 대 한 발급 토큰을 제공 하는 정보를 포함 합니다.

<!-- end list -->

  - **외부 페더레이션 조직**  
    외부 Exchange 조직 Azure Active Directory 인증 시스템과 페더레이션 트러스트가 설정 된입니다.

<!-- end list -->

  - **페더레이션 공유**  
    Exchange 조직 전체에서 작동 하도록 Azure Active Directory 인증 시스템과 페더레이션 트러스트를 활용 하는 Exchange 기능 그룹을 포함 하 여 크로스-프레미스 Exchange 배포 합니다. 함께 이러한 기능은 여러 Exchange 조직에서 사용자를 대신 하 여 서버 간에 인증 된 요청을 만드는 사용 됩니다.

<!-- end list -->

  - **페더레이션 도메인**  
    Exchange 조직에 대한 OrgID(조직 식별자)에 추가되는 신뢰할 수 있는 허용 도메인입니다.

<!-- end list -->

  - **도메인 증명 암호화 문자열**  
    조직 Azure Active Directory 인증 시스템과 함께 사용 되는 도메인을 담당 하는 증거를 제공 하는 Exchange 조직에서 사용 되는 암호화 된 보안 문자열입니다. 문자열은 자동으로 생성 때 **페더레이션 트러스트 사용** 마법사를 사용 하 여 또는 **Get-FederatedDomainProof** cmdlet을 사용 하 여 생성 될 수 있습니다.

<!-- end list -->

  - **페더레이션 공유 정책**  
    사용자가 설정한 일정 정보의 개인 간 공유를 사용하도록 설정하고 제어하는 조직 수준의 정책입니다.

<!-- end list -->

  - **페더레이션**  
    공통의 목적을 달성하기 위해 두 Exchange 조직 간에 신뢰를 기반으로 맺은 계약입니다. 페더레이션을 통해 두 조직은 한 조직의 인증 어설션이 다른 조직에서 인식되기를 원합니다.

<!-- end list -->

  - **페더레이션 트러스트**  
    Exchange 조직에 대 한 다음과 같은 구성 요소를 정의 하는 Azure Active Directory 인증 시스템과 관계입니다.
    
      - 계정 네임스페이스
    
      - AppID(응용 프로그램 식별자)
    
      - OrgID(조직 식별자)
    
      - 페더레이션 도메인
    
    다른 페더레이션된 Exchange 조직과 페더레이션 공유를 구성 하려면 Azure Active Directory 인증 시스템과 페더레이션 트러스트를 설정 해야 합니다.

<!-- end list -->

  - **비 페더레이션 조직**  
    페더레이션 트러스트가 Azure Active Directory 인증 시스템과 설정 되어있지 않은 조직입니다.

<!-- end list -->

  - **OrgID(조직 식별자)**  
    페더레이션에 사용 되는 조직에 구성 된 신뢰할 수 있는 허용된 도메인을 정의 합니다. OrgID에 구성 된 페더레이션된 도메인으로 구성 된 전자 메일 주소를가지고 있는 받는 사람만 Azure Active Directory 인증 시스템에서 인식 되는 및 페더레이션 공유 기능 사용할 수 있습니다. OrgID은 미리 정의 된 문자열 및 **페더레이션 트러스트 사용** 마법사의 페더레이션에 대해 선택 된 첫번째 허용된 도메인의 조합입니다. 예, 조직의 기본 SMTP 도메인으로 contoso.com 페더레이션된 도메인을 지정 하는 경우 계정 네임 스페이스 FYDIBOHF25SPDLT.contoso.com 자동으로 만들어집니다 페더레이션 트러스트에 대 한 OrgID로 합니다.

<!-- end list -->

  - **조직 관계**  
    받는 사람에 게 약속 있음/없음 (일정 사용 가능 여부) 정보를 공유할 수 있게 하는 두 페더레이션된 Exchange 조직 간의 일대일 관계입니다. 조직 관계를 Azure Active Directory 인증 시스템과 페더레이션 트러스트 차지 하며 Exchange 조직 간의 Active Directory 포리스트 또는 도메인 트러스트를 사용 하 여 필요성을 대체 합니다.

<!-- end list -->

  - **Azure Active Directory 인증 시스템**  
    무료, 클라우드 기반 identity 서비스 역할을 연결 된 Microsoft Exchange 조직 간의 트러스트 브로커입니다. 다른 페더레이션된 Exchange 조직의 받는 사람에 게에서 정보를 요청 하면 Exchange 받는 사람에 게 위임 토큰을 발행을 담당 합니다. 자세한 내용은 [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)를 참조 하십시오.

## Azure AD 인증 시스템

온-프레미스 Exchange 2013 조직 및 다른 페더레이션된 Exchange 2010Exchange 2013 효율화 간의 트러스트 브로커도 작동 하며를 Azure Active Directory 인증 시스템, Microsoft에서 제공 하는 무료 클라우드 기반 서비스입니다. Exchange 조직에서 페더레이션 구성 하려는 경우에 사용자의 조직과 페더레이션 파트너를 될 수 있도록 Azure Active Directory 인증 시스템과 일회성 페더레이션 트러스트를 설정 해야 합니다. 전체에서 신뢰로이 Active Directory ( *id 공급자*라고 함)에서 인증 된 사용자가 Azure AD 인증 시스템에 의해 Assertion Markup Language SAML (Security) 위임 토큰을 발급 됩니다. 이러한 위임 토큰에 다른 페더레이션된 Exchange 조직에서 신뢰할 수를 하나 페더레이션된 Exchange 조직에서 사용자를 허용 합니다. 와 트러스트 브로커 역할 Azure AD 인증 시스템에 조직 되지 않은 다른 조직과 여러 개별 트러스트 관계를 설정할 및 필요 사용자 환경에서 single sign-on (SSO) 사용 하는 외부 리소스에 액세스할 수 있습니다. 자세한 내용은 [Azure Active Directory](https://go.microsoft.com/fwlink/?linkid=392500)을 참조 하십시오.

맨 위로 이동

## 페더레이션 트러스트

Exchange 2013 페더레이션 공유 기능을 사용 하려면 Exchange 2013 조직과 Azure AD 인증 시스템 간에 페더레이션 트러스트를 설정 해야 합니다. Azure AD 인증 시스템과 페더레이션 트러스트를 설정 Azure AD 인증 시스템을 통해 조직의 보안 디지털 인증서를 교환 하 고 Azure AD 인증 시스템 인증서와 페더레이션 메타 데이터를 검색 합니다. **페더레이션 트러스트 사용** 마법사에서 Exchange 관리 센터 (EAC) 또는 Exchange 관리 셸 **New-FederationTrust** cmdlet을 사용 하 여 페더레이션 트러스트를 설정할 수 있습니다. 자체 서명 된 인증서의 **페더레이션 트러스트 사용** 마법사에 의해 자동으로 만들어집니다 및 서명 및 Azure AD 인증 시스템에서 위임 토큰에 사용자가 외부 페더레이션된 조직을 신뢰 하도록 허용 하는 암호화에 사용 됩니다. 인증서 요구 사항에 대 한 자세한 내용은,이 항목 뒷부분의 페더레이션에 대 한 인증서 요구 사항 를 참조 하십시오.

Azure AD 인증 시스템과 페더레이션 트러스트를 만들 *응용 프로그램 식별자* (AppID) 자동으로 Exchange 조직에 대해 생성 되 고 **Get-FederationTrust** cmdlet의 출력에 제공 된. AppID는 Azure AD 인증 시스템 Exchange 조직을 고유 하 게 식별 하는데 사용 됩니다. 또한 조직 Azure AD 인증 시스템에 사용 하기 위한 도메인을 소유 하는 증거를 제공 하려면 Exchange 조직에서 사용 됩니다. 이 작업은 각 페더레이션된 도메인에 대 한 공용 도메인 이름 시스템 (DNS) 영역에 있는 텍스트 (TXT) 레코드를 작성 하 여 수행 됩니다.

맨 위로 이동

## 페더레이션 조직 식별자

*페더레이션 조직 식별자* (OrgID) 페더레이션에 사용 되는 조직에 구성 된 신뢰할 수 있는 허용된 도메인을 정의 합니다. OrgID에 구성 된 허용된 도메인으로 구성 된 전자 메일 주소를가지고 있는 받는 사람만 Azure AD 인증 시스템에서 인식 되는 및 페더레이션 공유 기능 사용할 수 있습니다. 새 페더레이션 트러스트를 만들면 사용자는 OrgID Azure AD 인증 시스템을 통해 자동으로 만들어집니다. 이 OrgID은 미리 정의 된 문자열 및 마법사에서 기본 공유 도메인으로 선택 허용된 도메인의 조합입니다. 예, Edit Sharing-Enabled 도메인 마법사에서 조직 전체에서 공유 되는 기본 도메인으로 페더레이션된 도메인 **contoso.com** 을 지정 하는 경우 **FYDIBOHF25SPDLT.contoso.com** 계정 네임 스페이스 자동으로 만들어집니다 Exchange 조직에 대 한 페더레이션 트러스트에 대 한 OrgID로 합니다.

하지만 일반적으로이 도메인 Exchange 조직에 대 한 기본 SMTP 도메인 Exchange 조직에서 허용된 도메인을 지정할 필요가 없습니다 하 고 도메인 이름 시스템 (DNS) 증명 소유 TXT 레코드를 필요 하지 않습니다. 유일한 요구 사항은 페더레이션 수를 선택 하는 허용된 도메인 최대 32 자 제한 한다는 것입니다. 이 하위 도메인의 유일한 목적은 요청 SAML 위임 토큰에 해당 받는 사람에 대 한 고유 식별자를 유지 하기 위해 Azure AD 인증 시스템에 대 한 연결 된 네임 스페이스를 토대로 하는 것입니다. SAML 토큰에 대 한 자세한 내용은 [SAML 토큰 및 클레임](https://go.microsoft.com/fwlink/?linkid=198561) 을 참조 하십시오.

언제든지 허용 도메인을 페더레이션 트러스트에 추가하거나 페더레이션 트러스트에서 제거할 수 있습니다. 조직의 모든 페더레이션 공유 기능을 사용하도록 설정하거나 사용하지 않도록 설정하려면 페더레이션 트러스터에 대한 OrgID를 사용하도록 설정하거나 사용하지 않도록 설정하면 됩니다.


> [!IMPORTANT]
> OrgID, 허용 도메인 또는 페더레이션 트러스트에 사용되는 AppID를 변경하는 경우 조직의 모든 페더레이션 공유 기능이 영향을 받습니다. Exchange Online 및 하이브리드 배포 구성을 포함하여 모든 외부 페더레이션 Exchange 조직도 영향을 받습니다. 이러한 페더레이션 트러스트 구성 설정이 변경되면 모든 외부 페더레이션 파트너에게 해당 사항을 알리는 것이 좋습니다.



맨 위로 이동

## 페더레이션 예

두 Exchange 조직 Contoso, l t d. 및 Fabrikam, Inc. 원하는 일정 약속 있음/없음 정보를 서로 공유할 수 있도록 사용자에 게 있습니다. 각 조직 Azure AD 인증 시스템과 페더레이션 트러스트를 만들고 해당 사용자의 전자 메일 주소 도메인에 대해 사용 되는 도메인을 포함 하도록 계정 네임 스페이스로 구성 합니다.

Contoso 직원 다음 전자 메일 주소 도메인 중 하나를 사용 합니다: contoso.com, contoso.co.uk, 또는 contoso.ca 합니다. Fabrikam 직원 다음 전자 메일 주소 도메인 중 하나를 사용 합니다: fabrikam.com, fabrikam.org, 또는 fabrikam.net 합니다. 두 조직 모두 전자 메일 도메인 Azure AD 인증 시스템과 페더레이션 트러스트에 대 한 계정 네임 스페이스에 포함 된 모든 허용 있는지 확인 하십시오. 두 조직 간에 복잡 한 Active Directory 포리스트 또는 도메인 신뢰 구성 요구를 아닌 두 조직 모두 일정 약속 있음/없음 공유 기능을 사용 하 여 서로 조직 관계를 구성 합니다.

다음 그림은 Contoso, Ltd. 및 Fabrikam, Inc. 사이의 페더레이션 구성을 보여 줍니다.

**페더레이션 공유 예**

![페더레이션 트러스트 및 페더레이션 공유](images/Dd335047.310f0698-b67d-4b0e-91e4-231c6e9db952(EXCHG.150).gif "페더레이션 트러스트 및 페더레이션 공유")

## 페더레이션에 대한 인증서 요구 사항

자체 서명 된 인증서 또는 인증 기관에서 서명한 X.509 인증서를 Azure AD 인증 시스템을 통해 페더레이션 트러스트를 설정 하려면 (CA) 만들고 사용 하는 트러스트를 만들려면 Exchange 2013 서버에 설치 합니다. EAC에서 **페더레이션 트러스트 사용** 마법사를 사용 하 여 설치 및 자동으로 만들어지는 자체 서명 된 인증서를 사용 하는 것이 좋습니다. 이 인증서가 서명 하 고 위임 토큰에 페더레이션 공유에 사용 되는 암호화에 사용 하 고 페더레이션 트러스트 위해 하나만 인증서가 필요 합니다. Exchange 2013 조직에서 다른 모든 Exchange 2013 서버에 인증서를 자동으로 배분합니다.

외부 CA에서 서명한 X.509 인증서를 사용하려는 경우 해당 인증서가 다음 요구 사항을 충족해야 합니다.

  - **신뢰할 수 있는 CA**   가능한 경우 X.509 SSL(Secure Sockets Layer) 인증서는 Windows Live에서 신뢰하는 CA에서 발급해야 합니다. 그러나 Microsoft가 현재 인증하지 않는 CA에서 발급한 인증서도 사용할 수 있습니다. 신뢰할 수 있는 CA의 최신 목록은 [페더레이션 트러스트에 대한 신뢰할 수 있는 루트 인증 기관](trusted-root-certification-authorities-for-federation-trusts-exchange-2013-help.md)을 참조하십시오.

  - **주체 키 식별자**   인증서에는 주체 키 식별자 필드가 있어야 합니다. 상업용 CA에서 발급된 X.509 인증서에는 대부분 이 식별자가 있습니다.

  - **CryptoAPI 암호화 서비스 공급자 (CSP)**   인증서는 CryptoAPI CSP를 사용 해야 합니다. 암호화 API를 사용 하는 인증서: CNG (차세대) 공급자 페더레이션에 대 한 지원 되지 않습니다. Exchange 한 인증서 요청 만들기를 사용 하 여 CryptoAPI 공급자 사용 됩니다. 자세한 내용은 참조 [암호화 API: 차세대](https://go.microsoft.com/fwlink/?linkid=187890)합니다.

  - **RSA 서명 알고리즘**   인증서는 서명 알고리즘으로 RSA를 사용해야 합니다.

  - **내보낼 수 있는 개인 키**   인증서 생성에 사용한 개인 키는 내보낼 수 있어야 합니다. EAC의 **새 Exchange 인증서** 마법사나 셸의 [New-ExchangeCertificate](https://technet.microsoft.com/ko-kr/library/aa998327\(v=exchg.150\)) cmdlet을 사용하여 인증서 요청을 만들 때 개인 키를 내보낼 수 있도록 지정할 수 있습니다.

  - **현재 인증서**   인증서는 현재 인증서여야 합니다. 만료되거나 해지된 인증서를 사용하여 페더레이션 트러스트를 만들 수는 없습니다.

  - **확장된 키 사용**   인증서에는 EKU(확장된 키 사용) 유형 **클라이언트 인증 (1.3.6.1.5.5.7.3.2)**을 포함해야 합니다. 이 사용 유형은 원격 컴퓨터에 ID를 증명하기 위해 사용됩니다. EAC 또는 셸을 사용하여 인증서 요청을 생성하면 이 사용 유형이 기본적으로 포함됩니다.


> [!NOTE]
> 인증서가 인증에 사용되지 않으므로 주체 이름이나 주체 대체 이름 요구 사항은 없습니다. 호스트 이름, 도메인 이름 또는 다른 이름과 동일한 이름의 주체 이름이 지정된 인증서를 사용할 수 있습니다.



맨 위로 이동

## 새 인증서로 전환

페더레이션 트러스트를 만드는 데 사용한 인증서는 현재 인증서로 지정됩니다. 하지만 정기적으로 페더레이션 트러스트에 대한 새 인증서를 설치하고 사용해야 할 수 있습니다. 예를 들어 현재 인증서가 만료되는 경우 또는 새 비즈니스 또는 보안 요구 사항을 충족하도록 하기 위해 새 인증서를 사용해야 할 수 있습니다. 새 인증서로 원활하게 전환하려면 Exchange 2013 서버에 새 인증서를 설치하고 페더레이션 트러스트를 구성하여 새 인증서로 지정해야 합니다. 그러면 Exchange 2013에서 새 인증서를 조직의 다른 모든 Exchange 2013 서버에 자동으로 배포합니다. Active Directory 토폴로지에 따라 인증서 배포에 시간이 오래 걸릴 수도 있습니다. 셸의 [Test-FederationTrustCertificate](https://technet.microsoft.com/ko-kr/library/dd335228\(v=exchg.150\)) cmdlet을 사용하여 인증서 상태를 확인할 수 있습니다.

인증서의 배포 상태를 확인 한 후에 새 인증서를 사용 하 여 트러스트를 구성할 수 있습니다. 인증서로 전환한 후, 현재 인증서가 이전 인증서로 지정 하 고 새 인증서를 현재 인증서로 지정 된 키를 누릅니다. 새 인증서가 Azure AD 인증 시스템에 게시 되 고 Azure AD 인증 시스템을 통해 교환 되는 모든 새 토큰 새 인증서를 사용 하 여 암호화 됩니다.


> [!NOTE]
> 이 인증서 전환 프로세스는 페더레이션에서만 사용됩니다. 인증서를 필요로 하는 다른 Exchange 2013 기능에 동일한 인증서를 사용할 경우에는 새 인증서의 확보, 설치 또는 전환을 계획할 때 기능 요구 사항을 고려해야 합니다.



맨 위로 이동

## 페더레이션에 대한 방화벽 고려 사항

페더레이션 기능을 사용하려면 조직에 있는 사서함 및 클라이언트 액세스 서버에서 HTTPS를 통해 아웃바운드 인터넷 액세스를 해야 합니다. 조직에 있는 모든 Exchange 2013 사서함 및 클라이언트 액세스 서버에서의 아웃바운드 HTTPS 액세스(TCP의 경우 포트 443)를 허용해야 합니다.

외부 조직에서 내부의 약속 있음/없음 정보에 액세스하게 만들려면 클라이언트 액세스 서버 하나를 인터넷에 게시해야 합니다. 그러려면 인터넷에서 클라이언트 액세스 서버로 인바운드 HTTPS 액세스를 해야 합니다. 인터넷에 클라이언트 액세스 서버를 게시하지 않은 Active Directory 사이트의 클라이언트 액세스 서버도 인터넷에서 액세스가 가능한 다른 Active Directory 사이트의 클라이언트 액세스 서버를 사용할 수 있습니다. 인터넷에 게시되지 않은 클라이언트 액세스 서버는 외부 조직에 표시되는 URL로 설정된 웹 서비스 가상 디렉터리의 외부 URL이 있어야 합니다.

[맨 위로 이동](sharing-exchange-2013-help.md)

