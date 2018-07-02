---
title: '페더레이션 트러스트 관리: Exchange 2013 Help'
TOCTitle: 페더레이션 트러스트 관리
ms:assetid: 0439839f-2052-4bc9-9d30-aa6e7d51b733
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673036(v=EXCHG.150)
ms:contentKeyID: 50482400
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션 트러스트 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-01_

페더레이션 트러스트 Microsoft Exchange 2013 조직 및 Azure Active Directory 인증 시스템 간에 트러스트 관계를 설정 하 고 다른 페더레이션 Exchange 조직과 페더레이션 공유를 지원 합니다. 일반적으로를 관리 하거나 만든 후 페더레이션 트러스트를 수정 해야 하면 안됩니다. 그러나 추가 (영문) 또는 페더레이션된 도메인을 제거 하거나 다시 설정 하는 OrgID (조직 식별자)는 페더레이션 트러스트를 구성 하는 데 사용 하는 도메인을 필요로 하는 경우에 있을 수 있습니다.


> [!NOTE]
> 기존 페더레이션 트러스트, 특히 OrgID를 정의하는 데 사용된 기본 공유 도메인을 수정하면 페더레이션 Exchange 조직 간의 페더레이션 공유나 Office 365 조직이 있는 하이브리드 배포의 페더레이션 공유가 손상될 수 있습니다.



페더레이션과 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md) 항목을 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 *Federation and certificates* 권한 항목을 참조하십시오.

  - 페더레이션 트러스트에 새로 추가된 페더레이션 도메인 각각의 TXT 레코드를 공용 DNS에 추가해야 합니다. 공용 DNS 레코드를 호스트하는 조직의 TXT 레코드 추가를 위한 요구 사항을 검토하십시오.

  - 이 항목의 목적에 따라 기존 페더레이션 트러스트는 다음 설정을 사용하여 구성되었습니다.
    
      - **Contoso.com**은 페더레이션 트러스트에 대한 기본 공유 도메인입니다. (이 도메인은 변경되지 않습니다.)
    
      - 페더레이션 도메인 **service.contoso.com** 및 **sales.contoso.com**은 기존 페더레이션 트러스트에 포함되어 있습니다.
    
      - **Marketing.contoso.com**은 Exchange 조직의 허용 도메인입니다.

  - 이 항목에서는 셸에서 페더레이션 트러스트 매개 변수 정보 보기, 페더레이션 트러스트에 사용된 인증서 보기 및 관리 등의 기타 페더레이션 관리 작업도 다룹니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 페더레이션 트러스트 관리

1.  온-프레미스 조직의 Exchange 2013 서버에서 **조직** \> **공유**로 이동합니다.

2.  **페더레이션 트러스트** 섹션에서 **수정**을 클릭합니다.

3.  기본 공유 도메인이 변경되지 않기 때문에 **공유 사용 가능 도메인**에서 **1단계**를 건너뜁니다.

4.  **2단계**에서 **service.contoso.com** 도메인을 선택하고 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하여 페더레이션 트러스트에서 도메인을 제거합니다.

5.  **2단계**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

6.  **허용 도메인 선택**의 허용 도메인 목록에서 **marketing.contoso.com**을 선택하고 **확인**을 클릭하여 페더레이션 트러스트에 도메인을 추가합니다.
    

    > [!IMPORTANT]
    > <STRONG>marketing.contoso.com</STRONG> 도메인에 대한 페더레이션 도메인 증명 문자열이 생성됩니다. 공용 DNS에 이 도메인의 TXT 레코드를 별도로 만들어야 합니다.



7.  **marketing.contoso.com** 도메인에 대해 만든 페더레이션 도메인 증명 문자열을 사용하면 공용 DNS 서버에 TXT 레코드가 생성됩니다. 공용 DNS 호스트의 업데이트 일정에 따라 DNS 변경 사항 복제에 15분 이상 걸릴 수 있습니다.

8.  TXT 레코드가 생성되어 복제되면 **업데이트**를 클릭합니다.

## 셸을 사용하여 페더레이션 트러스트 관리

1.  이 예에서는 페더레이션 트러스트에서 service.contoso.com 도메인을 제거합니다.
    
        Remove-FederatedDomain -DomainName service.contoso.com

2.  이 예에서는 페더레이션 트러스트에 marketing.contoso.com 도메인을 추가합니다.
    
        Add-FederatedDomain -DomainName marketing.contoso.com

구문과 매개 변수에 대한 자세한 내용은 [Remove-FederatedDomain](https://technet.microsoft.com/ko-kr/library/dd298128\(v=exchg.150\)) 및 [Add-FederatedDomain](https://technet.microsoft.com/ko-kr/library/dd351208\(v=exchg.150\))을 참조하십시오.

페더레이션 트러스트의 다른 측면을 관리하려면 다음 셸 명령을 실행합니다.

1.  **페더레이션 OrgID 및 페더레이션 도메인 보기**
    
    이 예에서는 페더레이션 도메인 및 상태를 비롯한 Exchange 조직의 페더레이션 OrgID와 관련 정보를 표시합니다.
    
        Get-FederatedOrganizationIdentifier

2.  **페더레이션 트러스트 인증서 보기**
    
    이 예에서는 페더레이션 트러스트 "Azure AD authentication"에서 사용하는 이전, 현재 및 다음 인증서를 표시합니다.
    
        Get-FederationTrust "Azure AD authentication" | Select Org*certificate

3.  **페더레이션 인증서 상태 확인**
    
    이 예에서는 조직의 모든 사서함 및 클라이언트 액세스 서버의 페더레이션 인증서 상태를 표시합니다.
    
        Test-FederationTrustCertificate

4.  **인증서를 다음 인증서로 사용하도록 페더레이션 트러스트 구성**
    
    이 예에서는 제공된 지문이 포함된 인증서를 다음 인증서로 사용하도록 페더레이션 트러스트 "Azure AD authentication"을 구성합니다. 조직의 모든 Exchange 서버에 인증서를 배포한 후 *PublishCertificate* 스위치를 사용하여 이 인증서를 현재 인증서로 사용하도록 페더레이션 트러스트를 구성할 수 있습니다.
    
        Set-FederationTrust "Azure AD authentication" -Thumbprint AC00F35CBA8359953F4126E0984B5CCAFA2F4F17

5.  **다음 인증서를 현재 인증서로 사용하도록 페더레이션 트러스트 구성**
    
    이 예에서는 다음 인증서를 현재 인증서로 사용 하 여 페더레이션 트러스트 Azure AD 인증을 구성 하 고 Azure AD 인증 시스템에 게시 합니다.
    
        Set-FederationTrust "Azure AD authentication" -PublishFederationCertificate
    

    > [!WARNING]
    > 다음 인증서를 현재 페더레이션 인증서로 사용하도록 페더레이션 트러스트를 구성하기 전에 조직의 모든 Exchange 서버에 인증서를 배포해야 합니다. <A href="https://technet.microsoft.com/ko-kr/library/dd335228(v=exchg.150)">Test-FederationTrustCertificate</A> cmdlet을 사용하면 인증서의 배포 상태를 확인할 수 있습니다.



6.  **페더레이션 메타 데이터 및 Azure AD 인증 시스템에서 인증서 새로고침**
    
    페더레이션 메타 데이터 및 인증서는 페더레이션 트러스트 Azure AD 인증에 대 한 Azure AD 인증 시스템의 새로 고치는이 예제입니다.
    
        Set-FederationTrust "Azure AD authentication" -RefreshMetadata

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-FederatedOrganizationIdentifier](https://technet.microsoft.com/ko-kr/library/dd298149\(v=exchg.150\))

  - [Get-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd351262\(v=exchg.150\))

  - [Test-FederationTrustCertificate](https://technet.microsoft.com/ko-kr/library/dd335228\(v=exchg.150\))

  - [Set-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd298034\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

**공유 사용 가능 도메인** 마법사가 성공적으로 완료되면 페더레이션 트러스트를 예상대로 구성한 것입니다.

성공 여부를 추가로 확인하려면 다음을 수행합니다.

1.  페더레이션 트러스트 정보를 확인하려면 다음 셸 명령을 실행합니다.
    
        Get-FederationTrust | format-list

2.  조직에서 페더레이션 정보를 검색할 수 있는지 확인하려면 다음 셸 명령을 실행합니다. 예를 들어 *DomainNames* 매개 변수에서 sales.contoso.com 및 marketing.contoso.com 도메인이 반환되는지 확인합니다.
    
        Get-FederationInformation -DomainName <your primary sharing domain>


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


