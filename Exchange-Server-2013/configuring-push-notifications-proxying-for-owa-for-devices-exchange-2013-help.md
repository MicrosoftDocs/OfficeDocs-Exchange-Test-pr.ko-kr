---
title: '장치용 OWA에 대 한 푸시 알림 프록시 구성: Exchange 2013 Help'
TOCTitle: 장치용 OWA에 대 한 푸시 알림 프록시 구성
ms:assetid: c0f4912d-8bd3-4a54-9097-03619c645c6a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn511017(v=EXCHG.150)
ms:contentKeyID: 59954060
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 장치용 OWA에 대 한 푸시 알림 프록시 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

Microsoft Exchange 2013의 온-프레미스 배포에 대해 장치용 OWA 푸시 알림(iPhone/iPad용 OWA)을 사용하도록 설정하면 사용자가 사용자 받은 편지함에서 확인하지 않은 메시지 수를 나타내는 Outlook Web App 아이콘 업데이트를 iPhone/iPad용 OWA에서 받을 수 있습니다. 푸시 알림을 구성하고 사용하도록 설정하지 않으면 장치용 OWA 사용자가 앱을 시작해야 받은 편지함에 확인하지 않은 메시지가 있음을 알 수 있습니다. 새 메시지가 있으면 사용자 장치에서 장치용 OWA 배지가 업데이트되어 다음과 같이 표시됩니다.

![장치용 OWA 배지](images/Dn511017.f399ba74-5395-4d24-ae7d-d16bf0ac7b35(EXCHG.150).png "장치용 OWA 배지")

## 푸시 알림을 사용하도록 설정하는 방법

푸시 알림을 사용하도록 설정하려면 온-프레미스 Exchange 2013 서버가 Office 365 푸시 알림 서비스에 연결하여 iPhone과 iPad에 푸시 알림을 보내야 합니다. Exchange 2013 온-프레미스 서버는 Office 365 알림 서비스를 통해 업데이트 알림을 라우팅하므로 타사 푸시 알림 서비스에 개발자 계정을 등록할 필요가 없습니다. 다음 다이어그램에는 iPhone 및 iPad 사용자가 확인하지 않은 메시지에 대해 배지 업데이트를 받는 프로세스가 나와 있습니다.

![푸시 알림 프로세스](images/Dn511017.36764ce6-7351-492f-a17e-c42b781e2781(EXCHG.150).jpg "푸시 알림 프로세스")

푸시 알림을 사용하도록 설정하려면 관리자는 다음을 수행해야 합니다.

1.  Office 365 비즈니스 에디션에서 조직을 등록합니다.

2.  모든 온-프레미스 서버를 Exchange Server 2013 CU3(누적 업데이트 3) 이상으로 업데이트합니다.

3.  온-프레미스 Exchange 2013에서 Office 365 인증으로 설정

4.  온-프레미스 Exchange Server 2013에서 Office 365로의 푸시 알림을 사용하도록 설정하고 해당 푸시 알림이 작동하는지 확인합니다.

## Office 365 비즈니스 에디션에서 조직 등록

Office 365는 강력한 보안, 안정성 및 사용자 생산성에 대한 조직의 요구 사항에 부합하도록 설계된 클라우드 기반 서비스로, Office 응용 프로그램 및 인터넷(클라우드 서비스)을 통해 사용 가능한 Lync 웹 회의 및 비즈니스용 Exchange Online 호스팅 전자 메일과 같은 기타 생산성 서비스 액세스 권한이 포함된 요금제가 적용됩니다.

대부분의 Office 365 요금제에는 사용자가 여러 컴퓨터와 장치에 설치 가능한 최신 Office 응용 프로그램의 데스크톱 버전도 포함됩니다. 모든 Office 365 요금제는 월 단위 또는 연 단위 구독제로 청구됩니다. 자세한 내용을 알아보거나 Office 365에서 조직을 등록하려면 [Office 365 비즈니스 에디션이란?](http://go.microsoft.com/fwlink/?linkid=335705)을 참조하세요. Office 365를 통해 제공되는 각 서비스에 대한 자세한 내용은 [Office 365 서비스 설명](http://go.microsoft.com/fwlink/?linkid=335704)을 참조하세요.

## CU3 이상으로 업데이트

Exchange Server 2013용 CU3(누적 업데이트 3)을 설치하면 Exchange Server 2013 소프트웨어의 RTM 출시 이후 확인된 문제를 해결할 수 있습니다. CU3에는 CU1 및 CU2의 모든 문제 및 수정 사항과 CU2 출시 이후의 기타 수정 사항 및 업데이트가 포함되어 있습니다. 모든 Exchange Server 2013 온-프레미스 고객은 이 업데이트를 설치하는 것이 좋습니다. 푸시 알림을 사용하려는 경우에는 CU3을 반드시 설치해야 합니다. CU3을 포함한 누적 업데이트에 대한 내용은 [Exchange 2013용 업데이트](updates-for-exchange-2013-exchange-2013-help.md)를 참조하세요.

## 온-프레미스 Exchange 2013에서 Office 365 인증으로 설정

Exchange Server 2013에서는 서버 간 인증에 표준화된 단일 방법을 사용합니다. [Exchange Server 2013](http://go.microsoft.com/fwlink/?linkid=290946) 및 [Lync Server 2013](http://go.microsoft.com/fwlink/?linkid=273796)과 [SharePoint 2013](http://go.microsoft.com/fwlink/?linkid=335701) 및 [Office 2013](http://go.microsoft.com/fwlink/?linkid=335696)은 서버 간 인증 및 권한 부여를 위해 OAuth(Open Authorization) 프로토콜을 지원합니다. OAuth를 사용하는 경우 다수의 주요 웹 사이트에서 사용하는 표준 권한 부여 프로토콜, 사용자 자격 증명 및 암호가 컴퓨터 간에 전달되지 않습니다. 대신 OAuth 보안 토큰을 기준으로 인증과 권한 부여가 수행됩니다. 이러한 토큰은 일정 시간 동안 특정 리소스 집합에 대한 액세스 권한을 부여합니다.

OAuth 인증에는 보통 세 가지 구성 요소, 즉 권한 부여 서버 하나와 서로 통신해야 하는 두 개의 영역이 사용됩니다. 보안 토큰은 보안 토큰 서버라고도 하는 권한 부여 서버에서 서로 통신해야 하는 두 영역에 발급됩니다. 이러한 토큰은 특정 영역에서 시작되는 통신을 다른 영역에서 신뢰해야 하는지를 확인합니다. 예를 들어 권한 부여 서버는 특정 Lync Server 2013 영역의 사용자가 지정된 Exchange 2013 영역에 액세스할 수 있는지와 특정 Exchange 2013 영역의 사용자가 지정된 Lync Server 2013 영역에 액세스할 수 있는지를 확인하는 토큰을 발급할 수 있습니다.


> [!TIP]
> 영역은 보안 컨테이너입니다.



그러나 온-프레미스 서버 간 인증에서는 타사 토큰 서버를 사용할 필요가 없습니다. Lync Server 2013 및 Exchange 2013 등의 각 서버 제품에는 서버 간 인증을 지원하는 SharePoint Server 등의 기타 Microsoft 서버와 인증용으로 사용할 수 있는 기본 제공 토큰 서버가 포함되어 있습니다. 예를 들어 Lync Server 2013은 자체적으로 보안 토큰을 발급하고 서명한 다음 해당 토큰을 사용하여 Exchange 2013과 통신할 수 있습니다. 이러한 경우에는 타사 토큰 서버가 필요하지 않습니다.

Exchange Server 2013에서 Office 365로의 온-프레미스 구현에 대해 서버 간 인증을 구성하려면 다음 두 단계를 완료해야 합니다.

  - **1단계 - 온-프레미스 Exchange Server의 기본 제공 토큰 발급자에 인증서를 할당합니다.** 먼저 온-프레미스 Exchange 관리자가 이전에 인증서를 만들지 않은 경우 다음 Exchange 관리 셸 스크립트를 사용하여 인증서를 만든 다음 온-프레미스 Exchange Server의 기본 제공 토큰 발급자에 할당해야 합니다. 이 프로세스는 한 번만 수행하면 되며 인증서를 만든 후에는 다른 인증 시나리오에서도 해당 인증서를 바꾸지 말고 다시 사용해야 합니다. *$tenantDomain*의 값은 도메인 이름으로 업데이트해야 합니다. 이렇게 하려면 다음 코드를 복사하여 붙여 넣습니다.
    
    > [!CAUTION]
    > 코드를 복사하여 메모장 등의 텍스트 편집기에 붙여 넣은 다음 .ps1 확장명으로 저장하면 셸 스크립트를 보다 쉽게 실행할 수 있습니다.
    
    ```powershell
        # Make sure to update the following $tenantDomain with your Office 365 tenant domain.
        
        $tenantDomain = "Fabrikam.com"
        
        # Check whether the cert returned from Get-AuthConfig is valid and keysize must be >= 2048
        
        $c = Get-ExchangeCertificate | ?{$_.CertificateDomains -eq $env:USERDNSDOMAIN -and $_.Services -ge "SMTP" -and $_.PublicKeySize -ge 2048 -and $_.FriendlyName -match "OAuth"}
        If ($c.Count -eq 0)
        {
            Write-Host "Creating certificate for oAuth..."
            $ski = [System.Guid]::NewGuid().ToString("N")
            $friendlyName = "Exchange S2S OAuth"
            New-ExchangeCertificate -FriendlyName $friendlyName -DomainName $env:USERDNSDOMAIN -Services Federation -KeySize 2048 -PrivateKeyExportable $true -SubjectKeyIdentifier $ski
            $c = Get-ExchangeCertificate | ?{$_.friendlyname -eq $friendlyName}
        }
        ElseIf ($c.Count -gt 1)
        {
            $c = $c[0]
        }
        
        $a = $c | ?{$_.Thumbprint -eq (get-authconfig).CurrentCertificateThumbprint}
        If ($a.Count -eq 0)
        {
            Set-AuthConfig -CertificateThumbprint $c.Thumbprint
        }
        Write-Host "Configured Certificate Thumbprint is:"(get-authconfig).CurrentCertificateThumbprint
        
        # Export the certificate
        
        Write-Host "Exporting certificate..."
        if((test-path $env:SYSTEMDRIVE\OAuthConfig) -eq $false)
        {
            md $env:SYSTEMDRIVE\OAuthConfig
        }
        cd $env:SYSTEMDRIVE\OAuthConfig
        
        $oAuthCert = (dir Cert:\LocalMachine\My) | where {$_.FriendlyName -match "OAuth"}
        $certType = [System.Security.Cryptography.X509Certificates.X509ContentType]::Cert
        $certBytes = $oAuthCert.Export($certType)
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        [System.IO.File]::WriteAllBytes($CertFile, $certBytes)
        
        # Set AuthServer
        $authServer = Get-AuthServer MicrosoftSts;
        if ($authServer.Length -eq 0)
        {
            Write-Host "Creating AuthServer Config..."
            New-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        elseif ($authServer.AuthMetadataUrl -ne "https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain")
        {
            Write-Warning "AuthServer config already exists but the AuthMetdataUrl doesn't match the appropriate value. Updating..."
            Set-AuthServer MicrosoftSts -AuthMetadataUrl https://accounts.accesscontrol.windows.net/metadata/json/1/?realm=$tenantDomain
        }
        else
        {
            Write-Host "AuthServer Config already exists."
        }
        Write-Host "Complete."
    ```

    스크립트 실행 결과는 다음 출력과 유사합니다.
    
    ```powershell
        Configured Certificate Thumbprint is: 7595DBDEA83DACB5757441D44899BCDB9911253C
        Exporting certificate...
        Complete.
    ```

    > [!CAUTION]  
    > 계속 하기 전에 Windows PowerShell용 Azure Active Directory 모듈 cmdlet가 필요 합니다. (이전에 Microsoft Online Services 모듈에 대 한 Windows PowerShell 라고 함) Windows PowerShell용 Azure Active Directory 모듈 cmdlet이 설치 된 하지 않은 경우에 <a href="http://aka.ms/aadposh">Windows PowerShell을 사용 하 여 Azure AD 관리</a>에서 설치할 수 있습니다.


  - **2단계 – Exchange 2013 온-프레미스와 통신하도록 Office 365를 구성합니다.** Exchange Server 2013이 통신할 Office 365 서버를 파트너 응용 프로그램으로 구성합니다. 예를 들어 Exchange Server 2013 온-프레미스가 Office 365와 통신해야 하는 경우 Exchange 온-프레미스를 파트너 응용 프로그램으로 구성해야 합니다. 파트너 응용 프로그램은 Exchange 2013이 타사 보안 토큰 서버를 거치지 않고도 보안 토큰을 직접 교환할 수 있는 응용 프로그램입니다. 온-프레미스 Exchange 2013 관리자는 다음 Exchange 관리 셸 스크립트를 사용하여 Exchange 2013이 통신할 Office 365 테넌트를 파트너 응용 프로그램으로 구성해야 합니다. 실행 중에는 Office 365 테넌트 도메인 관리자의 사용자 이름과 암호를 입력하라는 메시지가 표시됩니다(예: administrator@fabrikam.com). 이전 스크립트에서 만들지 않은 경우 *$CertFile* 값은 인증서 위치로 업데이트해야 합니다. 이렇게 하려면 다음 코드를 복사하여 붙여 넣습니다.
    
    ```powershell
        # Make sure to update the following $CertFile with the path to the cert if not using the previous script.
        
        $CertFile = "$env:SYSTEMDRIVE\OAuthConfig\OAuthCert.cer"
        
        If (Test-Path $CertFile)
        {
            $ServiceName = "00000002-0000-0ff1-ce00-000000000000";
        
            $objFSO = New-Object -ComObject Scripting.FileSystemObject;
            $CertFile = $objFSO.GetAbsolutePathName($CertFile);
        
            $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
            $cer.Import($CertFile);
            $binCert = $cer.GetRawCertData();
            $credValue = [System.Convert]::ToBase64String($binCert);
        
            Write-Host "Please enter the administrator user name and password of the Office 365 tenant domain..."
        
            Connect-MsolService;
            Import-Module msonlineextended;
        
            Write-Host "Adding a key to Service Principal..."
        
            $p = Get-MsolServicePrincipal -ServicePrincipalName $ServiceName
            New-MsolServicePrincipalCredential -AppPrincipalId $p.AppPrincipalId -Type asymmetric -Usage Verify -Value $credValue -StartDate $cer.GetEffectiveDateString() -EndDate $cer.GetExpirationDateString()
        }
        Else
        {
            Write-Error "Cannot find certificate."
        } 
    ```

    결과는 다음과 같습니다.
    
    ```powershell
        Please enter the administrator user name and password of the Office 365 tenant domain...
        Adding a key to Service Principal...
        Complete.
    ```

## 푸시 알림 프록시 사용

위의 단계를 수행하여 OAuth 인증을 정상적으로 설정한 후 온-프레미스 관리자는 다음 스크립트를 사용하여 푸시 알림 프록시를 사용하도록 설정해야 합니다. *$tenantDomain*의 값은 도메인 이름으로 업데이트해야 합니다. 이렇게 하려면 다음 코드를 복사하여 붙여 넣습니다.

```powershell
    $tenantDomain = "Fabrikam.com"
    Enable-PushNotificationProxy -Organization:$tenantDomain
```

스크립트 실행 결과는 다음 출력과 유사합니다.

```powershell
    RunspaceId        : 4f2eb5cc-b696-482f-92bb-5b254cd19d60
    DisplayName       : On Premises Proxy app
    Enabled           : True
    Organization      : fabrikam.com
    Uri               : https://outlook.office365.com/PushNotifications
    Identity          : OnPrem-Proxy
    IsValid           : True
    ExchangeVersion   : 0.20 (15.0.0.0)
    Name              : OnPrem-Proxy
    DistinguishedName : CN=OnPrem-Proxy,CN=Push Notifications Settings,CN=First Organization,CN=Microsoft
                        Exchange,CN=Services,CN=Configuration,DC=Domain,DC=extest,DC=microsoft,DC=com
    Guid              : 8b567958-58a4-403c-a8f0-524d7f1e9279
    ObjectCategory    : fabrikam.com/Configuration/Schema/ms-Exch-Push-Notifications-App
    ObjectClass       : {top, msExchPushNotificationsApp}
    WhenChanged       : 8/27/2013 7:23:47 PM
    WhenCreated       : 8/14/2013 1:30:27 PM
    WhenChangedUTC    : 8/28/2013 2:23:47 AM
    WhenCreatedUTC    : 8/14/2013 8:30:27 PM
    OrganizationId    :
    OriginatingServer : server.fabrikam.com
    ObjectState       : Unchanged
```

## 푸시 알림이 작동하는지 확인

위의 단계를 완료한 후 다음 작업 중 하나를 수행하여 푸시 알림을 테스트할 수 있습니다.

  - **사용자 사서함으로 테스트 전자 메일 보내기**
    
    1.  알림에 구독할 모바일 장치에서 장치용 OWA에 계정을 설정합니다.
    
    2.  장치 홈 화면으로 돌아오면 장치용 OWA가 백그라운드에서 실행됩니다.
    
    3.  PC 등의 다른 장치에서 모바일 장치에 설정한 계정의 받은 편지함으로 전자 메일 메시지를 보냅니다.
    
    4.  그러면 몇 분 이내에 앱 아이콘에 확인하지 않은 메시지 수가 표시됩니다.

  - **모니터링 사용.** 푸시 알림을 테스트하거나 알림이 실패하는 이유를 조사하는 또 다른 방법은 조직의 사서함 서버에 대해 모니터링을 사용하도록 설정하는 것입니다. 온-프레미스 Exchange 2013 서버 관리자는 다음 스크립트를 사용하여 푸시 알림 프록시 모니터링을 호출해야 합니다. 이렇게 하려면 다음 코드를 복사하여 붙여 넣습니다.
    
    ```powershell
        # Send a push notification to verify connectivity.
        
        $s = Get-ExchangeServer | ?{$_.ServerRole -match "Mailbox"}
        If ($s.Count -gt 1)
        {
            $s = $s[0]
        }
        If ($s.Count -ne 0)
        {
            # Restart the monitoring service to clear the cache from when push was previously disabled.
            Restart-Service MSExchangeHM
        
            # Give the monitoring service enough time to load.
            Start-Sleep -Seconds:120
        
            Invoke-MonitoringProbe PushNotifications.Proxy\PushNotificationsEnterpriseConnectivityProbe -Server:$s.Fqdn | fl ResultType, Error, Exception
        }
        Else
        {
            Write-Error "Cannot find a Mailbox server in the current site."
        }
    ```

    스크립트 실행 결과는 다음 출력과 유사합니다.
    
    ```powershell
        ResultType : Succeeded
        Error      :
        Exception  :
    ```

