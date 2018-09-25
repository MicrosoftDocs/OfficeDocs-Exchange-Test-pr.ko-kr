---
title: 'Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성: Exchange 2013 Help'
TOCTitle: Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성
ms:assetid: f703e153-98e2-4268-8a6e-07a86b0a1d22
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn594521(v=EXCHG.150)
ms:contentKeyID: 61170870
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 및 Exchange Online 조직 간의 OAuth 인증 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Exchange 2013 전용 하이브리드 배포는 하이브리드 구성 마법사를 사용할 때 OAuth 인증을 구성합니다. 혼합된 Exchange 2013/2010 및 Exchange 2013/2007 하이브리드 배포에서는 하이브리드 구성 마법사에 의해 Office 365와 온-프레미스 Exchange 조직 간에 새로운 하이브리드 배포 OAuth 기반 인증 연결이 구성되지 않습니다. 이러한 배포는 기본적으로 페더레이션 트러스트 프로세스를 계속 사용합니다. 그러나 특정 Exchange 2013 기능은 새 Exchange OAuth 인증 프로토콜을 사용해야만 조직 내에서 완전히 사용 가능합니다.

새 Exchange OAuth 인증 프로세스를 통해 현재 다음 Exchange 기능을 사용할 수 있습니다.

  - MRM(메시지 권한 관리)

  - Exchange 원본 위치 eDiscovery

  - Exchange 내부 보관

Exchange 2013 및 Exchange Online과의 하이브리드 배포를 구현하는 모든 혼합 Exchange 조직에서는 하이브리드 구성 마법사를 사용하여 하이브리드 배포를 구성한 후에 Exchange OAuth 인증을 구성하는 것이 좋습니다.


> [!IMPORTANT]
> 온-프레미스 조직의 Exchange 2013 서버 에서만 누적 업데이트 5를 실행 하는 이상이 설치 된 경우에이 항목의 단계를 수행 하는 대신 하이브리드 배포 마법사를 실행 합니다.<BR>Exchange Server 2013의 이 기능은 현재 중국에서 21Vianet에 의해 운영되는 Office 365와는 완전히 호환되지는 않으며 일부 기능 제한이 적용될 수 있습니다. 자세한 내용은 <A href="https://go.microsoft.com/fwlink/?linkid=313640">21Vianet에 의해 운영되는 Office 365 정보</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [Exchange 및 셸 인프라 권한](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) 항목의 "페더레이션 및 인증서" 권한 항목

  - 하이브리드 배포 마법사를 사용 하 여 하이브리드 배포의 구성을 완료 합니다. 자세한 내용은 [Exchange Server 하이브리드 배포](https://technet.microsoft.com/ko-kr/library/jj200581\(v=exchg.150\))을 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 온-프레미스 Exchange 및 Exchange Online 조직 간에 OAuth 인증을 구성하는 방법

## 1단계: Exchange Online 조직용 권한 부여 서버 개체 만들기

이 절차를 수행하려면 Exchange Online 조직용으로 확인된 도메인을 지정해야 합니다. 이 도메인은 클라우드 기반 전자 메일 계정에 사용되는 기본 SMTP 도메인으로 사용하는 것과 같은 도메인이어야 합니다. 다음 절차에서는 이 도메인을 *\<확인된 도메인\>*으로 지칭합니다.

온-프레미스 Exchange 조직의 Exchange 관리 셸(Exchange PowerShell)에서 다음 명령을 실행합니다.

```powershell
New-AuthServer -Name "WindowsAzureACS" -AuthMetadataUrl https://accounts.accesscontrol.windows.net/<your verified domain>/metadata/json/1
```
## 2단계: Exchange Online 조직에 대해 파트너 응용 프로그램을 사용하도록 설정합니다.

온-프레미스 Exchange 조직의 Exchange PowerShell에서 다음 명령을 실행합니다.

```powershell
Get-PartnerApplication |  ?{$_.ApplicationIdentifier -eq "00000002-0000-0ff1-ce00-000000000000" -and $_.Realm -eq ""} | Set-PartnerApplication -Enabled $true
```
## 3단계: 온-프레미스 권한 부여 인증서 내보내기

이 단계에서는 PowerShell 스크립트를 실행하여 온-프레미스 권한 부여 인증서를 내보내야 합니다. 다음 단계에서 이 인증서를 Exchange Online 조직으로 가져옵니다.

1.  **ExportAuthCert.ps1**과 같이 이름을 지정한 PowerShell 스크립트 파일에 다음 텍스트를 저장합니다.
    
    ```powershell
    $thumbprint = (Get-AuthConfig).CurrentCertificateThumbprint
         
    if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
    {
        md $env:SYSTEMDRIVE\OAuthConfig
    }
    cd $env:SYSTEMDRIVE\OAuthConfig
         
    $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.Thumbprint -match $thumbprint}
    $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
    $certBytes = $oAuthCert.Export($certType)
    $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
    [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
    ```
2.  이전 단계에서 만든 PowerShell 스크립트를 온-프레미스 Exchange 조직의 Exchange PowerShell에서 실행합니다. 예를 들면 다음과 같습니다.
    
    ```powershell
    .\ExportAuthCert.ps1
    ```
## 4 단계: Azure Active Directory ACS로 온-프레미스 권한 부여 인증서 업로드

다음으로 Azure Active Directory ACS(액세스 제어 서비스) 에 이전 단계에서 내보낸 온-프레미스 권한 부여 인증서 업로드 하려면 Windows PowerShell을 사용 해야 합니다. 이 작업을 수행 하려면 Windows PowerShell용 Azure Active Directory 모듈 cmdlet를 설치 하는 합니다. 설치 되어있지 않은 경우 Windows PowerShell용 Azure Active Directory 모듈 를 설치 하려면 <https://aka.ms/aadposh> 이동 합니다. Windows PowerShell용 Azure Active Directory 모듈 를 설치한 후 다음 단계를 완료 합니다.

1.  설치 된 Azure AD cmdlet가 있는 Windows PowerShell 작업 영역을 열려면 **Azure Active Directory에 대 한 Windows PowerShell 모듈** 바로 가기를 클릭 합니다. 이 단계에서 모든 명령을 Azure Active Directory 콘솔에 대 한 Windows PowerShell을 사용 하 여 실행할 수 있습니다.

2.  **UploadAuthCert.ps1**과 같이 이름을 지정한 PowerShell 스크립트 파일에 다음 텍스트를 저장합니다.
    
    ```powershell
    Connect-MsolService;
    Import-Module msonlineextended;
        
    $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
    $objFSO = New-Object -ComObject Scripting.FileSystemObject;
    $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($CertFile);
    $binCert = $cer.GetRawCertData();
    $credValue = [System.Convert]::ToBase64String($binCert);
        
    $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
    $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
    New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue
    ```
3.  이전 단계에서 만든 PowerShell 스크립트를 실행합니다. 예를 들면 다음과 같습니다.
    
    ```powershell
    .\UploadAuthCert.ps1
    ```

4.  스크립트를 시작한 후에 자격 증명 대화 상자가 표시 됩니다. Microsoft Online Azure AD 조직에서 테 넌 트 관리자 계정에 대 한 자격 증명을 입력 합니다. 스크립트를 실행 한 후 Windows PowerShell Azure AD 세션에 대 한를 열어 둡니다. 다음 단계에서 PowerShell 스크립트를 실행 하려면이 사용 합니다.

## 5 단계: Azure Active Directory를 사용 하는 외부 온-프레미스 Exchange HTTP 끝점에 대 한 모든 호스트 이름 기관 등록

이 단계에서는 공개적으로 액세스 가능한 온-프레미스 Exchange 조직의 각 끝점에 대해 스크립트를 실행해야 합니다. 가능하면 와일드카드를 사용하는 것이 좋습니다. 예를 들어 외부의 **https://mail.contoso.com/ews/exchange.asmx** 페이지에서 Exchange를 사용할 수 있는 경우 와일드카드 하나를 **\*.contoso.com**과 같이 사용할 수 있습니다. 그러면 autodiscover.contoso.com 및 mail.contoso.com 끝점이 포함됩니다. 그러나 최상위 도메인인 **contoso.com**은 포함되지 않습니다. 최상위 호스트 이름 기관을 사용하여 Exchange 2013 클라이언트 액세스 서버에 외부에서 액세스할 수 있는 경우에는 이 호스트 이름 기관을 **contoso.com**으로도 등록해야 합니다. 외부 호스트 이름 기관은 제한 없이 추가로 등록할 수 있습니다.

온-프레미스 Exchange 조직의 외부 Exchange 끝점에 대해 모르는 경우에는 온-프레미스 Exchange 조직의 Exchange PowerShell에서 다음 명령을 실행하여 외부에 구성된 웹 서비스 끝점 목록을 확인할 수 있습니다.

```powershell
Get-WebServicesVirtualDirectory | FL ExternalUrl
```
> [!NOTE]
> 성공적으로 다음 명령을 실행 스크립트는 Azure Active Directory 에 대 한 Windows PowerShell에 연결 되어 있어야 Microsoft Online Azure AD 테 넌 트를 이전 섹션에는 4 단계에서 설명 했 듯이 합니다.

1.  **RegisterEndpoints.ps1**과 같이 이름을 지정한 PowerShell 스크립트 파일에 다음 텍스트를 저장합니다. 이 예에서는 와일드카드를 사용하여 contoso.com의 모든 끝점을 등록합니다. **contoso.com**은 온-프레미스 Exchange 조직의 호스트 이름 기관으로 바꿉니다.
    
    ```powershell
        $externalAuthority="*.contoso.com"
         
        $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
         
        $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName;
         
        $spn = [string]::Format("{0}/{1}", $ServiceName, $externalAuthority);
        $p.ServicePrincipalNames.Add($spn);
         
        Set-MsolServicePrincipal -ObjectID $p.ObjectId -ServicePrincipalNames $p.ServicePrincipalNames;
    ```

2.  Azure Active Directory 에 대 한 Windows PowerShell에서 이전 단계에서 만든 Windows PowerShell 스크립트를 실행 합니다. 예:
    
    ```powershell
        .\RegisterEndpoints.ps1
    ```

## 6단계: 온-프레미스 조직에서 Office 365로 연결되는 IntraOrganizationConnector 만들기

Exchange Online에서 호스팅되는 사서함의 대상 주소를 정의해야 합니다. 이 대상 주소는 Office 365 테넌트를 만들 때 자동으로 작성됩니다. 예를 들어 Office 365 테넌트에서 호스팅되는 조직의 도메인이 "contoso.com"이면 대상 서비스 주소는 "contoso.mail.onmicrosoft.com"이 됩니다.

Exchange PowerShell을 사용하여 온-프레미스 조직에서 다음 cmdlet을 실행합니다.

```powershell
New-IntraOrganizationConnector -name ExchangeHybridOnPremisesToOnline -DiscoveryEndpoint https://outlook.office365.com/autodiscover/autodiscover.svc -TargetAddressDomains <your service target address>
```

## 7단계: Office 365 테넌트에서 온-프레미스 Exchange 조직으로 연결되는 IntraOrganizationConnector 만들기

온-프레미스 조직에서 호스팅되는 사서함의 대상 주소를 정의해야 합니다. 조직의 기본 SMTP 주소가 "consoto.com"이면 대상 주소도 "contoso.com"입니다.

온-프레미스 조직의 외부 자동 검색 끝점도 정의해야 합니다. 회사의 주소가 "contoso.com"이면 이 끝점은 대개 다음 중 하나입니다.

  - https://autodiscover.\<기본 SMTP 도메인\>/autodiscover/autodiscover.svc

  - https://\<기본 SMTP 도메인\>/autodiscover/autodiscover.svc


> [!NOTE]
> 온-프레미스 및 Office 365 테넌트에서 <A href="https://technet.microsoft.com/ko-kr/library/dn551183(v=exchg.150)">Get-IntraOrganizationConfiguration</A> cmdlet을 사용하여 <A href="https://technet.microsoft.com/ko-kr/library/dn551178(v=exchg.150)">New-IntraOrganizationConnector</A> cmdlet에 필요한 끝점 값을 확인할 수 있습니다.

Windows PowerShell을 사용하여 다음 cmdlet을 실행합니다.

```powershell    
    $UserCredential = Get-Credential
    
    $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection
    
    Import-PSSession $Session
    
    New-IntraOrganizationConnector -name ExchangeHybridOnlineToOnPremises -DiscoveryEndpoint <your on-premises Autodiscover endpoint> -TargetAddressDomains <your on-premises SMTP domain>
```
## 8단계: Exchange 2013 SP1 이전 버전 서버에 대해 AvailabilityAddressSpace 구성

Exchange 2013 이전 조직에서 하이브리드 배포를 구성할 때는 기존 Exchange 조직에서 클라이언트 액세스 및 사서함 서버 역할을 갖는 하나 이상의 Exchange 2013 SP1 이상 서버를 설치해야 합니다. Exchange 2013 클라이언트 액세스 및 사서함 서버는 기존 Exchange 온-프레미스 조직 및 Exchange Online 조직 간에 프런트 엔드 서버로 작동하고 통신을 조정합니다. 이 통신에는 온-프레미스 조직과 Exchange Online 조직 사이의 메시지 전송 및 메시징 기능이 포함됩니다. 온-프레미스 조직에 Exchange 2013 서버를 둘 이상 설치하여 하이브리드 배포 기능의 안정성과 가용성을 높이는 것이 좋습니다.

Exchange 2013/2010 또는 Exchange 2013/2007이 있는 혼합 배포에서는 온-프레미스 조직의 모든 인터넷 연결 프런트 엔드 서버가 Exchange 2013 SP1 이상이 실행되는 클라이언트 액세스 서버인 것이 좋습니다. Office 365 및 Exchange Online에서 시작된 모든 EWS(Exchange Web Services) 요청은 온-프레미스 배포의 Exchange 2013 클라이언트 액세스 서버에 연결되어야 합니다. 또한 Exchange Online에 대해 온-프레미스 Exchange 조직에서 시작된 모든 EWS 요청은 Exchange 2013 SP1 이상이 실행되는 클라이언트 액세스 서버를 통해 프록시되어야 합니다. 이러한 Exchange 2013 클라이언트 액세스 서버는 이와 같이 들어오거나 나가는 추가 EWS 요청을 처리해야 하므로 처리 로드를 가망하고 중복 연결을 제공하기 위한 충분한 Exchange 2013 클라이언트 액세스 서버가 있어야 합니다. 필요한 클라이언트 액세스 서버 수는 EWS 요청의 평균 양에 따라 다르며, 조직 차이도 있을 수 있습니다.

다음 단계를 완료하기 전에 아래 내용을 확인하세요.

  - 프런트 엔드 하이브리드 서버가 Exchange 2013 SP1 이상인지 여부

  - Exchange 2013 서버에 대해 고유한 외부 EWS URL이 있는지 여부. Office 365 테넌트는 하이브리드 기능이 제대로 작동하려면 클라우드 기반 요청이 있을 때 이러한 서버에 순서대로 연결되어야 합니다.

  - 서버에 사서함 및 클라이언트 액세스 서버 역할이 모두 있는지 여부

  - 기존 Exchange 2010/2007 사서함 및 클라이언트 액세스 서버에는 최신 CU(누적 업데이트) 또는 SP(서비스 팩)가 적용되어 있는지 여부
    

    > [!NOTE]
    > 기존 Exchange 2010/2007 사서함 서버는 비하이브리드 기능 연결을 위해 프런트 엔드 서버에 대해 Exchange 2010/2007 클라이언트 액세스 서버를 계속 사용할 수 있습니다. Office 365 테넌트의 하이브리드 배포 기능 요청만 Exchange 2013 서버에 연결해야 합니다.



Exchange 2013 이전 클라이언트 액세스 서버에서는 온-프레미스 Exchange 2013 SP1 클라이언트 액세스 서버의 Exchange Web Services 끝점을 가리키는 *AvailabilityAddressSpace*가 구성되어야 합니다. 이 끝점은 앞서 5단계에서 설명한 것과 동일한 끝점이거나, 온-프레미스 Exchange 2013 SP1 클라이언트 액세스 서버에서 다음 cmdlet을 실행하여 결정할 수 있습니다.

```powershell
Get-WebServicesVirtualDirectory | FL AdminDisplayVersion,ExternalUrl
```

> [!NOTE]
> 가상 디렉터리 정보가 여러 서버에서 반환되는 경우 Exchange 2013 SP1 클라이언트 액세스 서버에 대해 반환된 끝점을 사용해야 합니다. 이 끝점은 <EM>AdminDisplayVersion</EM> 매개 변수가 15.0(빌드 847.32) 이상으로 표시됩니다.

*AvailabilityAddressSpace*를 구성하려면 Exchange PowerShell을 사용하여 온-프레미스 조직에서 다음 cmdlet을 실행합니다.

```powershell
Add-AvailabilityAddressSpace -AccessMethod InternalProxy -ProxyUrl <your on-premises External Web Services URL> -ForestName <your Office 365 service target address> -UseServiceAccount $True
```

## 작동 여부는 어떻게 확인합니까?

[Test-OAuthConnectivity](https://technet.microsoft.com/ko-kr/library/jj218623\(v=exchg.150\)) cmdlet을 사용하면 OAuth 구성이 올바른지 확인할 수 있습니다. 이 cmdlet은 온-프레미스 Exchange 및 Exchange Online 끝점이 서로 간에 보내는 요청을 정상적으로 인증할 수 있는지 확인합니다.


> [!IMPORTANT]
> 원격 PowerShell을 사용하여 Exchange Online 조직에 연결할 때는 <EM>AllowClobber</EM> 매개 변수를 <STRONG>Import-PSSession</STRONG> cmdlet과 함께 사용하여 최신 명령을 로컬 PowerShell 세션으로 가져와야 할 수 있습니다.


온-프레미스 Exchange 조직에서 Exchange Online에 정상적으로 연결할 수 있는지 확인하려면 온-프레미스 조직의 Exchange PowerShell에서 다음 명령을 실행합니다.

```powershell
Test-OAuthConnectivity -Service EWS -TargetUri https://outlook.office365.com/ews/exchange.asmx -Mailbox <On-Premises Mailbox> -Verbose | fl
```
Exchange Online 조직이 온-프레미스 Exchange 조직에 정상적으로 연결할 수 있는지 확인하려면 [원격 PowerShell](https://technet.microsoft.com/ko-kr/library/jj984289\(v=exchg.150\))을 사용하여 Exchange Online 조직에 연결한 후에 다음 명령을 실행합니다.

```powershell
Test-OAuthConnectivity -Service EWS -TargetUri <external hostname authority of your Exchange On-Premises deployment>/metadata/json/1 -Mailbox <Exchange Online Mailbox> -Verbose | fl
```
Test-oauthconnectivity 한 예로 그럴-서비스 EWS TargetUri https://lync.contoso.com/metadata/json/1-사서함 ExchangeOnlineBox1-Verbose | fl


> [!IMPORTANT]
> "SMTP 주소에 연결된 사서함이 없습니다." 오류는 무시하면 됩니다. <EM>ResultTask</EM> 매개 변수가 <STRONG>Success</STRONG> 값을 반환하기만 하면 됩니다. 예를 들어 테스트 출력의 마지막 섹션은 다음과 같습니다.<BR><CODE>ResultType: Success</CODE><BR><CODE>Identity: Microsoft.Exchange.Security.OAuth.ValidationResultNodeId</CODE><BR><CODE>IsValid: True</CODE><BR><CODE>ObjectState: New</CODE>




> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


