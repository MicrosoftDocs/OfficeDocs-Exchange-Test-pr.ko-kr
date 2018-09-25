---
title: '페더레이션 트러스트를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 페더레이션 트러스트를 구성 합니다.
ms:assetid: 7c2b539f-faed-4374-8578-9f329ca628db
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657462(v=EXCHG.150)
ms:contentKeyID: 50483485
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 페더레이션 트러스트를 구성 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2017-07-26_

페더레이션 트러스트 Microsoft Exchange 2013 조직과 Azure Active Directory 인증 시스템 간에 트러스트 관계를 설정 합니다. 페더레이션 트러스트를 구성 하 여 받는 사람에 게 일정 약속 있음/없음 정보를 공유할 다른 페더레이션 Exchange 조직과 페더레이션 공유를 구성할 수 있습니다. 두 페더레이션된 Exchange 2013 조직 간에 또는 페더레이션된 Exchange 2013 조직 및 페더레이션된 Exchange 2010 조직 간의 페더레이션 공유를 구성할 수 있습니다. Office 365 조직과 공유 설정할 수 있습니다.


> [!NOTE]
> 페더레이션 트러스트를 만드는 단계는 Exchange 조직에서 페더레이션 공유를 설정하는 여러 단계 중 하나입니다. 모든 단계를 검토하려면 <A href="configure-federated-sharing-exchange-2013-help.md">페더레이션 공유 구성</A>을 참조하십시오.



페더레이션과 관련된 추가 관리 작업에 대한 자세한 내용은 [페더레이션 프로시저](federation-procedures-exchange-2013-help.md)를 참조하십시오.


> [!IMPORTANT]
> Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 "페더레이션 및 인증서" 권한 항목입니다.

  - 페더레이션 트러스트를 설정하는 데 사용되는 도메인을 인터넷에서 확인할 수 있어야 합니다. 이렇게 하려면 도메인 등록 기관에 도메인을 등록해야 하고 인터넷에서 액세스할 수 있는 DNS 서버에 도메인의 DNS(Domain Name System) 영역을 호스트해야 합니다. 조직이 도메인에 대한 인터넷 전자 메일을 받는 경우 이러한 요구 사항이 이미 충족된 것입니다.

  - 공용 DNS에 TXT 레코드를 추가해야 합니다. 공용 DNS 레코드를 호스트하는 조직의 TXT 레코드 추가를 위한 요구 사항을 검토하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

  - 페더레이션된 공유 관계에 두 Exchange 조직 자신의 페더레이션 트러스트에 대 한 동일한 Azure AD 인증 시스템을 사용 해야 합니다. 두 온-프레미스 Exchange 조직 간에 또는 온-프레미스 Exchange 조직 및 Office 365https://go.microsoft.com/fwlink/?linkId=392576.

  - Exchange 2013 조직에 대 한 Azure AD 인증 시스템과 페더레이션 트러스트를 만들 때 페더레이션 트러스트 Azure AD 인증 시스템의 비즈니스 인스턴스를 사용 합니다. 그러나 다른 페더레이션 Exchange 조직과과 이전 버전의 Exchange와 기존 페더레이션 트러스트 Azure AD 인증 시스템의 비즈니스 또는 소비자 인스턴스를 사용 중일 수 있습니다.
    
    다음 Exchange 조직은 기본적으로 Azure AD 인증 시스템의 비즈니스 인스턴스를 사용 합니다.
    
      - **페더레이션 트러스트 사용** 마법사와 페더레이션 트러스트에 자체 서명된 인증서를 사용하는 Exchange 2013 조직
    
      - Exchange 2010 SP1 또는 페더레이션 트러스트에 대 한 **새 페더레이션 트러스트** 마법사와 자체 서명 된 인증서를 사용 하 여 이상의 조직입니다.
    
      - Exchange Online 등 Office 365에서 호스팅하는 Exchange 조직
    
    다음 Exchange 조직은 기본적으로 Azure AD 인증 시스템의 소비자 인스턴스를 사용 합니다.
    
      - (RTM) 버전의 타사 인증 기관에서 발급 한 인증서를 사용 하 여 Exchange 2010 조직 제조를 해제 합니다.
    
    모든 Exchange 조직에서는 페더레이션 트러스트에 대 한 Azure AD 인증 시스템의 비즈니스 인스턴스를 사용 하는 것이 좋습니다. 두 Exchange 조직 간의 페더레이션 공유를 구성 하기 전에 모든 기존 페더레이션 트러스트에 대 한 각 Exchange 조직을 사용 하는 Azure AD 인증 시스템 인스턴스를 확인 해야 합니다. 기존 페더레이션 트러스트에 대 한 Exchange 조직을 사용 하는 Azure AD 인증 시스템 인스턴스를 확인 하려면 다음 셸 명령을 실행 합니다.
    
    ```powershell
    Get-FederationInformation -DomainName <hosted Exchange domain namespace>
    ```
    
    비즈니스 인스턴스는 *TokenIssuerURIs* 매개 변수에 대해 `<uri:federation:MicrosoftOnline>`의 값을 반환합니다.
    
    소비자 인스턴스는 *TokenIssuerURIs* 매개 변수에 대해 `<uri:WindowsLiveID>`의 값을 반환합니다.
    
    Azure AD 인증 시스템의 비즈니스 인스턴스를 사용 하는 기존 페더레이션 트러스트 된 Exchange 조직과 페더레이션 공유를 구성 하려면이 항목의 단계를 수행 합니다. 이러한 단계는 두 Exchange 2013 조직 간에 또는 Exchange 2013 조직 및 이미 사용 중인 Exchange 2010 조직 간의 페더레이션 공유를 사용 하 여 사용할 수 있는 페더레이션 트러스트를 만들기 위해 수행 해야하는 모든는 Azure AD 인증 시스템의 비즈니스 인스턴스.
    
    Exchange 2013 조직 및 Azure AD 인증 시스템의 소비자 인스턴스를 사용 하는 기존 페더레이션 트러스트 된 Exchange 조직 간의 페더레이션 공유를 구성 하려면 사용 하 여 Exchange 조직 Exchange 2010 s p 2를 설치 해야 소비자 인스턴스 또는 나중에 또는 Exchange 2013 로 업그레이드 합니다. 하려는 경우 Exchange 2010 s p 2를 설치 하거나 나중에 **새 페더레이션 트러스트** 마법사를 사용 하 여 제거 하 고 다시 기존 페더레이션된 도메인 및 페더레이션 트러스트를 만듭니다. 페더레이션 트러스트를 다시 만든 경우, Azure AD 인증 시스템의 비즈니스 인스턴스 사용 됩니다.

## EAC를 사용하여 페더레이션 트러스트 만들기 및 구성

1.  온-프레미스 조직의 Exchange 2013 서버에서 **조직** \> **공유**로 이동합니다.

2.  **사용**을 클릭하고 **페더레이션 트러스트 사용** 마법사를 시작합니다.

3.  마법사가 완료되면 **닫기**를 클릭합니다.

4.  **공유** 탭의 **페더레이션 트러스트** 섹션에서 **수정**을 클릭합니다.

5.  **1단계** 옆의 **공유 사용 가능 도메인**에서 **찾아보기**를 클릭합니다.

6.  **허용 도메인 선택**의 목록에서 기본 공유 정책을 선택하고 **확인**을 클릭합니다.
    

    > [!NOTE]
    > 선택한 도메인이 페더레이션 트러스트의 OrgID를 구성하는 데 사용됩니다. OrgID에 대한 자세한 내용은 <A href="federation-exchange-2013-help.md">페더레이션</A> 항목을 참조하십시오.



7.  기본 공유 도메인에 대해 생성 되는 페더레이션된 도메인 증명을 기록해둡니다. 공용 DNS 서버에서 TXT 레코드를 만들려면이 문자열을 사용 합니다.
    

    > [!IMPORTANT]
    > 페더레이션된 도메인 증명은 영숫자 문자열입니다. 입력된 오류를 방지 하려면 EAC에서 문자열을 복사 하 고 메모장 같은 텍스트 편집기에 붙여넣은 것이 좋습니다. 다음 텍스트 편집기에서 클립보드에 복사 하 고 TXT 레코드를 만들 때에 <STRONG>텍스트</STRONG> 필드에 붙여넣을 수 있습니다. 잘못 된 페더레이션 도메인 증명 문자열을 사용 하 여 TXT 레코드를 만드는 경우 Azure AD 인증 시스템 도메인 소유권 증명을 확인 하려면 수 없으며 페더레이션된 조직 식별자에 추가할 수 없습니다.



8.  **2 단계** 페더레이션된 공유 기능을 필요로 하는 조직에서 사용자가 사용 되는 전자 메일 주소에 대 한 페더레이션된 트러스트에 추가 도메인을 추가 하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 를 클릭 합니다. 예, sales.contoso.com 등 자신의 전자 메일 주소에 대 한 하위 도메인을 사용 하는 사용자가 페더레이션 트러스트에 sales.contoso.com 도메인을 추가 됩니다.
    

    > [!NOTE]
    > 선택한 각 추가 도메인에 대해 페더레이션 도메인 증명 문자열이 만들어집니다. 공용 DNS에 각 추가 도메인에 대한 개별 TXT 레코드를 만들어야 합니다.



9.  각 도메인에 대해 만들어진 페더레이션 도메인 증명 문자열을 사용하여 공용 DNS 서버에서 이러한 각 도메인에 대한 TXT 레코드를 만듭니다. 공용 DNS 호스트의 업데이트 일정에 따라 DNS 변경 사항 복제에 15분 이상 걸릴 수 있습니다.

10. TXT 레코드가 만들어지고 복제된 후 **업데이트**를 클릭합니다.

## 셸을 사용하여 페더레이션 트러스트 만들기 및 구성

1.  페더레이션 트러스트 인증서에 대 한 고유 주체 키 식별자를 만들기 위해이 명령을 실행 합니다.
    
    ```powershell
    $ski = [System.Guid]::NewGuid().ToString("N")
    ```
2.  페더레이션 트러스트에 대 한 자체 서명 된 인증서를 만들려면이 구문을 사용 합니다.
    
    ```powershell
    New-ExchangeCertificate -FriendlyName "<Descriptive Name>" -DomainName <domain> -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    ```    
    이 예제에서는 Azure AD 인증 시스템과 페더레이션 트러스트에 대 한 자체 서명 된 인증서를 만듭니다. Exchange 페더레이션 공유를 친숙 한 이름 값을 사용 하 여 인증서 및 **USERDNSDOMAIN** 환경 변수에서 도메인 값을 검색 합니다.
    
    ```powershell
    New-ExchangeCertificate -FriendlyName "Exchange Federated Sharing" -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
    ```
3.  페더레이션 트러스트를 만들고 조직에 Exchange 서버에 이전 단계에서 만든 자체 서명 된 인증서를 자동으로 배포 하려면 다음이 구문을 사용 합니다.
    
    ```powershell
    Get-ExchangeCertificate | ?{$_.FriendlyName -eq "<FriendlyName>"} | New-FederationTrust -Name "<Descriptive Name>"
    ```
    
    Azure AD 인증 이라는 페더레이션 트러스트를 만들고 Exchange 페더레이션 공유 라는 자체 서명 된 인증서를 배포 하는이 예제입니다.
    
    ```powershell
    Get-ExchangeCertificate | ?{$_.FriendlyName -eq "Exchange Federated Sharing"} | New-FederationTrust -Name "Azure AD Authentication"
    ```

4.  페더레이션 트러스트에 대해 구성할 수 있는 모든 도메인에 대 한 필요한 TXT 레코드 도메인 소유권 증명을 반환 하려면 다음이 구문을 사용 합니다.
    
    ```powershell
    Get-FederatedDomainProof -DomainName <domain>
    ```    
    이 예에서는 contoso.com 기본 공유 도메인에 대 한 필요한 TXT 레코드 도메인 소유권 증명을 반환 합니다.
    
    ```powershell
    Get-FederatedDomainProof -DomainName contoso.com
    ```    
    **참고**:
    
      - 각 도메인 또는 하위 도메인 페더레이션 트러스트 TXT 레코드 도메인 소유권 증명 필요 하는이 실행 해야 하므로 대해 구성 된 여러 번 다른 *DomainName* 값을 사용 하 여 명령을 실행 됩니다.
    
      - 셸에서 마우스 오른쪽 단추로 클릭, **기호** 를 선택 하, **증명** 값을 선택 하 고 Enter 키를 눌러 TXT 레코드를 만들 때 사용할 수 있도록 여 도메인 증명 문자열을 복사 하는 것이 좋습니다. 잘못 된 페더레이션된 도메인 증명 문자열로 TXT 레코드를 만드는 경우 Azure AD 인증 시스템은 도메인의 사용자 소유권을 확인할 수 없습니다 및 페더레이션된 조직 식별자에 추가할 수 없습니다.

5.  이전 단계에서 정보를 사용 하 여 페더레이션 트러스트에 포함 될 모든 도메인에서 공용 DNS 서버에서 TXT 레코드를 만듭니다. 공용 DNS 호스트의 업데이트 일정에 따라 DNS 변경 내용 복제 15 분이 걸릴 수 또는 그 이상의 긴 합니다. 새 TXT 레코드를 사용할 수 있는지 확인 한 후에 계속 합니다.

6.  Azure AD 에서 메타 데이터 및 인증서를 검색 하려면이 명령을 실행 합니다.
    
    ```powershell
    Set-FederationTrust -RefreshMetadata -Identity "Azure AD authentication"
    ```

7.  3 단계에서에서 만든 페더레이션 트러스트에 대 한 기본 공유 도메인을 구성 하려면 다음이 구문을 사용 합니다. 지정 된 도메인의 페더레이션 트러스트에 대 한 조직 식별자 (OrgID)를 구성 하려면 사용 됩니다. OrgID 하는 방법에 대 한 자세한 내용은 [페더레이션 조직 식별자](federation-exchange-2013-help.md)를 참조 하십시오.
    
    ```powershell
    Set-FederatedOrganizationIdentifier -DelegationFederationTrust "<Federation Trust Name>" -AccountNamespace <Accepted Domain> -Enabled $true
    ```
    
    이 예에서는 공유를 기본 허용된 도메인 contoso.com 구성 페더레이션 트러스트에 대 한 도메인 이름이 Azure AD 인증 합니다.
    
    ```powershell
    Set-FederatedOrganizationIdentifier -DelegationFederationTrust "Azure AD authentication" -AccountNamespace contoso.com -Enabled $true
    ```

8.  다른 도메인에는 페더레이션 트러스트를 추가 하려면 다음이 구문을 사용 합니다.
    
    ```powershell
    Add-FederatedDomain -DomainName <AdditionalDomain>
    ```    
    이 예제는 sales.contoso.com 도메인의 전자 메일 주소를 가진 사용자가 페더레이션된 공유 기능을 필요로 하기 때문에 페더레이션된 트러스트에 하위 도메인 sales.contoso.com을 추가 합니다.
    
    ```powershell
    Add-FederatedDomain -DomainName sales.contoso.com
    ```
    
    기억 모든 도메인 또는 하위 도메인 페더레이션 트러스트에 추가 하는 TXT 레코드 도메인 소유권 증명 필요

자세한 구문 및 매개 변수 정보에 대 한 [New-ExchangeCertificate](https://technet.microsoft.com/ko-kr/library/aa998327\(v=exchg.150\)), [New-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd351047\(v=exchg.150\)), [Get-FederatedDomainProof](https://technet.microsoft.com/ko-kr/library/ff717833\(v=exchg.150\)), [Set-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd298034\(v=exchg.150\)), [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/ko-kr/library/dd351037\(v=exchg.150\))및 [Add-FederatedDomain](https://technet.microsoft.com/ko-kr/library/dd351208\(v=exchg.150\))를 참조 하십시오.

## 작동 여부는 어떻게 확인합니까?

**페더레이션 트러스트 사용** 및 **공유 사용 가능 도메인** 마법사가 성공적으로 완료되면 페더레이션 트러스트가 예상대로 구성된 것입니다.

페더레이션 트러스트가 만들어지고 구성되었는지 확인하려면 다음을 수행합니다.

1.  페더레이션 트러스트 정보를 확인하려면 다음 셸 명령을 실행합니다.
    
    ```powershell
    Get-FederationTrust | Format-List
    ```

2.  기본 공유 도메인 *\<PrimarySharedDomain\>* 바꿉니다 하 고 조직에서 페더레이션 정보를 검색할 수 있는지 확인 하려면 다음 셸 명령을 실행 합니다.
    
    ```powershell
    Get-FederationInformation -DomainName <PrimarySharedDomain>
    ```

구문과 매개 변수에 대한 자세한 내용은 [Get-FederationTrust](https://technet.microsoft.com/ko-kr/library/dd351262\(v=exchg.150\)) 및 [Get-FederationInformation](https://technet.microsoft.com/ko-kr/library/dd351221\(v=exchg.150\))을 참조하십시오.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


