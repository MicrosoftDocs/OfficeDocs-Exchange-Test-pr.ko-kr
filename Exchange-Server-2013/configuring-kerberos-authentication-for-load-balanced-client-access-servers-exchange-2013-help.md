---
title: '부하 분산 된 클라이언트 액세스 서버에 대 한 Kerberos 인증 구성: Exchange 2013 Help'
TOCTitle: 부하 분산 된 클라이언트 액세스 서버에 대 한 Kerberos 인증 구성
ms:assetid: 8f4faeea-a825-438d-97dc-1c398ce7aba5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ff808312(v=EXCHG.150)
ms:contentKeyID: 62835901
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 부하 분산 된 클라이언트 액세스 서버에 대 한 Kerberos 인증 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

**요약:**  Kerberos 인증 부하 분산 된 클라이언트 액세스 서버와 Exchange 2013에서 사용 하는 방법에 설명 합니다.

부하 분산 된 클라이언트 액세스 서버와 Kerberos 인증을 사용 하는 순서로이 문서에 설명 된 구성 단계를 완료 해야 합니다.

## Active Directory 도메인 서비스에 대체 서비스 계정 자격 증명을 만들기

동일한 네임 스페이스 및 Url을 공유 하는 모든 클라이언트 액세스 서버는 동일한 대체 서비스 계정 자격 증명을 사용 해야 합니다. 일반적으로 각 버전의 Exchange에 대 한 포리스트에 대 한 단일 계정이 충분 한 됩니다. *대체 서비스 계정 자격 증명* 또는 *ASA 자격 증명*입니다.


> [!IMPORTANT]
> Exchange 2010과 Exchange 2013 동일한 ASA 자격 증명을 공유할 수 없습니다. Exchange 2013에 대 한 새 ASA 자격 증명을 만들 해야 합니다.




> [!IMPORTANT]
> 공유 네임 스페이스에 대 한 CNAME 레코드는 지원 되는 동안에 A 레코드를 사용 하는 것이 좋습니다. 이렇게 하면 클라이언트 공유 이름 및 서버 FQDN에 따라 Kerberos 티켓 요청을 올바르게 시킵니다.



ASA 자격 증명을 설정 하는 경우 다음이 지침 사항에 유의 해야 합니다.

  - **계정 유형을.** 사용자 계정이 아닌 컴퓨터 계정을 만드는 것이 좋습니다. 컴퓨터 계정을 대화형 로그온을 허용 하지 않고 및 사용자 계정 보다 간단 보안 정책 있을 수 있습니다. 컴퓨터 계정을 만들 경우 암호 만료 되지 않습니다 하지만 암호 업데이트 주기적으로 계속 하는 것이 좋습니다. 로컬 그룹 정책을 사용 하 여 컴퓨터 계정 및 현재 정책을 충족 하지 않는 컴퓨터 계정을 정기적으로 삭제 하는 스크립트에 대 한 최대 사용 기간을 지정 수 있습니다. 로컬 보안 정책 결정 암호를 변경 해야 합니다. 컴퓨터 계정을 사용 하 여이 좋지만 사용자 계정을 만들 수 있습니다.

  - **계정 이름.** 계정 이름에 대 한 요구 사항은 합니다. 사용자 이름 지정 체계를 준수 하는 모든 이름과 사용할 수 있습니다.

  - **그룹 계정.** ASA 자격 증명을 사용 하는 계정에는 특별 한 보안 권한이 필요 하지 않습니다. 컴퓨터 계정을 사용 하는 경우 다음는 계정은 도메인 컴퓨터 보안 그룹의 구성원 이어야 합니다. 사용자 계정을 사용 하는 경우 다음는 계정은 Domain Users 보안 그룹의 구성원 이어야 합니다.

  - **계정 암호.** 계정을 만들 때 사용자가 제공 하는 암호 사용 됩니다. 계정을 만들 때 복잡 한 암호를 사용 하 고 암호 조직의 암호 요구 사항에 맞는지 확인 해야 합니다.

컴퓨터 계정으로 ASA 자격 증명을 만들려면

1.  도메인에 가입 된 컴퓨터에서 Windows PowerShell 또는 Exchange 관리 셸을 실행 합니다.
    
    **Import-Module** cmdlet을 사용 하 여 Active Directory 모듈을 가져올 수 있습니다.
    
    ```powershell
Import-Module ActiveDirectory
```

2.  이 cmdlet 구문을 사용 하 여 새 Active Directory 컴퓨터 계정을 만들려면 **New-ADComputer** cmdlet을 사용 합니다.
    
        New-ADComputer [-Name] <string> [-AccountPassword <SecureString>] [-AllowReversiblePasswordEncryption <System.Nullable[boolean]>] [-Description <string>] [-Enabled <System.Nullable[bool]>]
    
    **예제:** 
    
        New-ADComputer -Name EXCH2013ASA -AccountPassword (Read-Host 'Enter password' -AsSecureString) -Description 'Alternate Service Account credentials for Exchange' -Enabled:$True -SamAccountName EXCH2013ASA
    
    여기서 *EXCH2013ASA* 은 계정 이름, 설명 *Alternate Service Account credentials for Exchange* 상관 없이 표시할 수은 하 고이 *SamAccountName* 매개 변수 값 *EXCH2013ASA*경우, 디렉터리에서 고유 해야 합니다.

3.  이 cmdlet 구문을 사용 하 여 Kerberos에서 사용 하는 AES 256 암호화 암호화 지원을 활성화 하려면 **Set-ADComputer** cmdlet을 사용 합니다.
    
        Set-ADComputer [-Name] <string> [-add @{<attributename>="<value>"]
    
    **예제:** 
    
    ```powershell
Set-ADComputer EXCH2013ASA -add @{"msDS-SupportedEncryptionTypes"="28"}
```
    
    다음 암호를 사용 하는 *EXCH2013ASA* 계정의 이름이 고 특성을 수정할 수는 10 진수 값이 28, *msDS-SupportedEncryptionTypes* : r c 4 HMAC, AES128-CTS-HMAC-SHA1-96, AES256-CTS-HMAC-SHA1-96 합니다.

이러한 cmdlet에 대 한 자세한 내용은 [가져오기 모듈](https://technet.microsoft.com/library/hh849725.aspx) 하 고 [새로 만들기 ADComputer](https://technet.microsoft.com/library/ee617245.aspx)를 참조 하십시오.

## 크로스 포리스트 시나리오

크로스 포리스트 또는 리소스 포리스트 배포의 경우 있고 Exchange 포함 된 Active Directory 포리스트 외부에 있는 사용자가 있는 경우 포리스트 간에 포리스트 트러스트 관계를 구성 해야 합니다. 또한 배포에서 각 포리스트에 대 한 해야 하 고 포리스트 간에 포리스트 내 모든 이름 접미사 간에 트러스트를 사용 하도록 설정 하는 라우팅 규칙을 설정 합니다. 크로스 포리스트 트러스트를 관리 하는 방법에 대 한 자세한 내용은 [Managing 포리스트 트러스트](https://technet.microsoft.com/library/cc772440.aspx)을 참조 하십시오.

## ASA 자격 증명에 연결할 서비스 사용자 이름 확인

ASA 자격 증명을 만든 후 ASA 자격 증명으로 Exchange 서비스 사용자 이름 (Spn)에 연결 해야 합니다. Exchange Spn의 목록 구성에 따라 달라질 수 있습니다 하지만 다음 적어도 포함 되어야 합니다.

  - **http /**   HTTP, Exchange 웹 서비스, 자동 검색, 및 오프 라인 주소록을 통해 개발자를 위한 외부에서 Outlook 사용, MAPI이이 SPN을 사용 합니다.

SPN 값은 네트워크 부하 분산 장치에 대신 개별 서버에서 서비스 이름과 일치 해야 합니다. 계획에 도움이 되는 SPN 값을 사용 해야 합니다 다음과 같은 시나리오를 고려 합니다.

  - 단일 Active Directory 사이트

  - 여러 Active Directory 사이트

각이 시나리오에는 클라이언트 액세스 서버 구성원은 내부 Url, 외부 Url과 내부 URI에 사용 되는 자동 검색에 대 한 부하 분산 된, 정규화 된 도메인 이름 (Fqdn) 배포 된 있는지를 가정 합니다. 자세한 내용은 이해 프록시 및 리디렉션을 참조 하십시오.

## 단일 Active Directory 사이트

단일 Active Directory 사이트를 사용 하는 경우 사용자 환경에는 다음 그림에 유사할 수 있습니다.

![여러 AD 사이트와 Kerberos 인증이 포함된 CA 배열](images/Ff808312.97a1a926-f4ac-4498-bc6b-32e7fb1b70f1(EXCHG.150).jpg "여러 AD 사이트와 Kerberos 인증이 포함된 CA 배열")

위 그림에서 내부 Outlook 클라이언트에서 사용 되는 Fqdn을 기반으로 다음 Spn ASA 자격 증명에 연결할 해야 합니다.

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

## 여러 Active Directory 사이트

여러 Active Directory 사이트를 사용 하는 경우 사용자 환경에는 다음 그림에 유사할 수 있습니다.

![여러 AD 사이트와 Kerberos 인증이 포함된 CA 배열](images/Ff808312.95b52bd8-7074-4055-8bd2-e6bf1f112b42(EXCHG.150).jpg "여러 AD 사이트와 Kerberos 인증이 포함된 CA 배열")

이전 그림에는 Outlook 클라이언트에서 사용 되는 Fqdn을 기반으로 해야 ADSite 1에 대 한 클라이언트 액세스 서버에서 사용 되는 ASA 자격 증명으로 다음 Spn을 연결 하려면:

  - http/mail.corp.tailspintoys.com

  - http/autodiscover.corp.tailspintoys.com

다음 Spn ADSite 2에 대 한 클라이언트 액세스 서버에서 사용 되는 ASA 자격 증명에 연결할도 해야 합니다.

  - http/mailsdc.corp.tailspintoys.com

  - http/autodiscoversdc.corp.tailspintoys.com

## 구성 하 고 각 클라이언트 액세스 서버에서 ASA 자격 증명의 구성 확인

계정을 만든 후 계정이 모든 AD DS 도메인 컨트롤러에 복제 되었는지 확인 해야 합니다. 특히, 하는 계정은 ASA 자격 증명에서 사용할 각 클라이언트 액세스 서버에 있는 것입니다. 다음으로 배포에서 각 클라이언트 액세스 서버에서 ASA 자격 증명으로 계정을 구성 합니다.

다음이 절차 중 하나에서 설명한 것 처럼 Exchange 관리 셸을 사용 하 여 ASA 자격 증명을 구성 합니다.

  - 첫번째 Exchange 2013 클라이언트 액세스 서버에 ASA 자격 증명 배포

  - 이후 Exchange 2013 클라이언트 액세스 서버에 ASA 자격 증명 배포

ASA 자격 증명을 배포 하기 위한 유일한 방법은 지원된 RollAlternateServiceAcountPassword.ps1 스크립트를 사용 하는 것입니다. 자세한 내용은 [셸에서 RollAlternateserviceAccountCredential.ps1 스크립트를 사용 하 여](using-the-rollalternateserviceaccountcredential-ps1-script-in-the-shell-exchange-2013-help.md)을 참조 하십시오. 스크립트를 실행 한 후에 모든 대상된 서버 제대로 업데이트 되었는지 확인 하는 것이 좋습니다.

## 첫번째 Exchange 2013 클라이언트 액세스 서버에 ASA 자격 증명 배포

1.  Exchange 2013 서버에서 Exchange 관리 셸을 엽니다.

2.  디렉터리 *\<Exchange 2013 installation directory\>*\\V15\\Scripts를 변경 합니다.

3.  첫번째 Exchange 2013 클라이언트 액세스 서버를 ASA 자격 증명을 배포 하려면 다음 명령을 실행 합니다.
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-1.corp.tailspintoys.com -GenerateNewPasswordFor tailspin\EXCH2013ASA$

4.  대체 서비스 계정에 대 한 암호를 변경 하려면 묻는 때 대 한 **예** 입니다.

다음은 RollAlternateServiceAccountPassword.ps1 스크립트를 실행 하는 경우를 표시 하는 출력 예입니다.

    ========== Starting at 01/12/2015 10:17:47 ==========
    Creating a new session for implicit remoting of "Get-ExchangeServer" command...
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-1                                                   cas-1.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    
    Prior to pushing new credentials, all existing credentials that are invalid or no longer work will be removed from  the destination servers.
    Pushing credentials to server cas-1
    Setting a new password on Alternate Serice Account in Active Directory
    
    Password change
    Do you want to change password for tailspin\EXCH2013ASA$ in Active Directory at this time?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
    Preparing to update Active Directory with a new password for tailspin\EXCH2013ASA$ ...
    Resetting a password in the Active Directory for tailspin\EXCH2013ASA$ ...
    New password was successfully set to Active Directory.
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: {mail.corp.tailspintoys.com}
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-1 Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
              ...
    
    ========== Finished at 01/12/2015 10:20:00 ==========
    
            THE SCRIPT HAS SUCCEEDED

## 다른 Exchange 2013 클라이언트 액세스 서버에 ASA 자격 증명을 배포 합니다.

1.  Exchange 2013 서버에서 Exchange 관리 셸을 엽니다.

2.  디렉터리 *\<Exchange 2013 installation directory\>*\\V15\\Scripts를 변경 합니다.

3.  다른 Exchange 2013 클라이언트 액세스 서버를 ASA 자격 증명을 배포 하려면 다음 명령을 실행 합니다.
    
        .\RollAlternateServiceAccountPassword.ps1 -ToSpecificServer cas-2.corp.tailspintoys.com -CopyFrom cas-1.corp.tailspintoys.com

4.  ASA 자격 증명을 배포 하려는 각 클라이언트 액세스 서버에 대해 3 단계를 반복 합니다.

다음은 RollAlternateServiceAccountPassword.ps1 스크립트를 실행 하는 경우를 표시 하는 출력 예입니다.

    ========== Starting at 01/12/2015 10:34:35 ==========
    Destination servers that will be updated:
    
    Name                                                        PSComputerName
    ----                                                        --------------
    cas-2                                                   cas-2.corp.tailspintoys.com
    
    
    Credentials that will be pushed to every server in the specified scope (recent first):
    
    UserName                                                                                                        
    Password
    --------                                                                                                        
    --------
    tailspin\EXCH2013ASA$                                                                             
    System.Security.SecureString
    
    Prior to pushing new credentials, all existing credentials will be removed from the destination servers.
    Pushing credentials to server cas-2
    Retrieving the current Alternate Service Account configuration from servers in scope
    Alternate Service Account properties:
    
    StructuralObjectClass QualifiedUserName Last Pwd Update       SPNs
    --------------------- ----------------- ---------------       ----
    computer              tailspin\EXCH2013ASA$   1/12/2015 10:19:53 AM
    
    Per-server Alternate Service Account configuration as of the time of script completion:
    
    
       Array: cas-2.corp.tailspintoys.com
    
    Identity  AlternateServiceAccountConfiguration
    --------  ------------------------------------
    cas-2 Latest: 1/12/2015 10:37:59 AM, tailspin\EXCH2013ASA$
              ...
    
    
    ========== Finished at 01/12/2015 10:38:13 ==========
    
            THE SCRIPT HAS SUCCEEDED

## ASA 자격 증명의 배포를 확인 합니다.

  - Exchange 2013 서버에서 Exchange 관리 셸을 엽니다.

  - 클라이언트 액세스 서버에서 설정을 확인 하려면 다음 명령을 실행 합니다.
    
        Get-ClientAccessServer CAS-3 -IncludeAlternateServiceAccountCredentialStatus | Format-List Name, AlternateServiceAccountConfiguration

  - ASA 자격 증명의 배포를 확인 하려면 각 클라이언트 액세스 서버에서 2 단계를 반복 합니다.

다음은 위의 Get-clientaccessserver 명령을 실행 하 고 없는 이전 ASA 자격 증명 설정 된 경우 표시 되는 출력의 예입니다.

    Name                                 : CAS-1
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: <Not set>
                                               ...

다음은 위의 Get-clientaccessserver 명령을 실행 하 고 이전에 ASA 자격 증명 설정 된 경우 표시에 출력 예입니다. 이전 ASA 자격 증명 및 날짜와 시간 설정 된 반환 됩니다.

    Name                                 : CAS-3
    AlternateServiceAccountConfiguration : Latest: 1/12/2015 10:19:22 AM, tailspin\EXCH2013ASA$
                                           Previous: 7/15/2014 12:58:35 PM, tailspin\oldSharedServiceAccountName$
                                               ...

## 서비스 사용자 이름 (Spn) ASA 자격 증명 연결


> [!IMPORTANT]
> 연결 하지 않음 Spn는 ASA 자격 증명으로 배포할 때까지 해당 자격 증명 하나 이상의 Exchange 서버에 배포 첫번째 Exchange 2013 클라이언트 액세스 서버에 ASA 자격 증명의앞부분에서 설명한 것 처럼 합니다. 그렇지 않은 경우 Kerberos 인증 오류가 발생할 수 있습니다.



ASA 자격 증명으로 Spn을 연결 하기 전에 Spn 대상 포리스트에 있는 다른 계정과 사용 하 여 연결 되지 이미 있는지 확인 해야 합니다. 이러한 Spn 연결 된 포리스트에 있는 유일한 계정이 되도록 ASA 자격 증명 필요 합니다. 명령줄에서 **setspn** 명령을 실행 하 여 포리스트에 있는 다른 계정이 없으면 Spn 연관 인지 확인할 수 있습니다.

SPN 아직 연결 되지 않은 포리스트의 계정과 사용 하 여 setspn 명령을 실행 하 여 확인

1.  **시작** 키를 누릅니다. **검색** 상자에 결과 얻으려면의 목록에서 **명령 프롬프트** 다음 입력 **명령 프롬프트** 를 선택 합니다.

2.  명령 프롬프트에 다음 명령을 입력합니다.
    
    ```powershell
setspn -F -Q <SPN>
```
    
    ASA 자격 증명으로 연결 하려는 \< SPN \> SPN입니다. 예를 들어:
    
    ```powershell
setspn -F -Q http/mail.corp.tailspintoys.com
```
    
    이 명령은 아무것도 반환 해야 합니다. 무언가 반환 하는 경우 다른 계정이 이미 SPN와 연결 합니다. ASA 자격 증명으로 연결 하려는 각 SPN에 대 한 후에이 단계를 반복 합니다.

ASA 자격 증명 SPN setspn 명령을 사용 하 여 연결

1.  **시작** 키를 누릅니다. **검색** 상자에 결과 얻으려면의 목록에서 **명령 프롬프트** 다음 입력 **명령 프롬프트** 를 선택 합니다.

2.  명령 프롬프트에 다음 명령을 입력합니다.
    
    ```powershell
setspn -S <SPN> <Account>$
```
    
    여기서 \< SPN \> ASA 자격 증명 연결할 SPN 이며 \< 계정 \> ASA 자격 증명을 연관 된 계정입니다. 예를 들어:
    
    ```powershell
setspn -S http/mail.corp.tailspintoys.com tailspin\EXCH2013ASA$
```
    
    ASA 자격 증명으로 연결 하려는 각 SPN에 대 한 후이 명령을 실행 합니다.

Setspn 명령을 사용 하 여 ASA 자격 증명을 가진 Spn을 연결 확인

1.  **시작** 키를 누릅니다. **검색** 상자에 결과 얻으려면의 목록에서 **명령 프롬프트** 다음 입력 **명령 프롬프트** 를 선택 합니다.

2.  명령 프롬프트에 다음 명령을 입력합니다.
    
    ```powershell
setspn -L <Account>$
```
    
    여기서 \< 계정이 \> ASA 자격 증명을 연관 된 계정입니다. 예를 들어:
    
    ```powershell
setspn -L tailspin\EXCH2013ASA$
```
    
    이 명령은 한번 실행 해야 합니다.

## Outlook 클라이언트에 대 한 Kerberos 인증을 사용 하도록 설정

1.  Exchange 2013 서버에서 Exchange 관리 셸을 엽니다.

2.  외부에서 Outlook 사용 클라이언트에 대 한 Kerberos 인증을 사용 하려면 클라이언트 액세스 서버에서 다음 명령을 실행 합니다.
    
        Get-OutlookAnywhere -server CAS-1 | Set-OutlookAnywhere -InternalClientAuthenticationMethod  Negotiate

3.  HTTP 클라이언트를 통한 MAPI에 대 한 Kerberos 인증을 사용 하려면 Exchange 2013 클라이언트 액세스 서버에서 다음을 실행 합니다.
    
        Get-MapiVirtualDirectory -Server CAS-1 | Set-MapiVirtualDirectory -IISAuthenticationMethods Ntlm, Negotiate

4.  Kerberos 인증을 사용 하려면 각 Exchange 2013 클라이언트 액세스 서버에 대해 2-3 단계를 반복 합니다.

## Exchange 클라이언트 Kerberos 인증의 유효성을 검사합니다

Kerberos 및 ASA 자격 증명 성공적으로 구성한 후에 클라이언트에 이러한 작업의 설명에 따라 성공적으로 인증할 수 있는지 확인 합니다.

## Microsoft Exchange 서비스 호스트 서비스가 실행 되 고 있는지 확인 합니다.

클라이언트 액세스 서버에서 Microsoft Exchange 서비스 호스트 서비스 (MSExchangeServiceHost)는 ASA 자격 증명 관리를 담당 합니다. 이 서비스가 실행 중이 아닌 경우 Kerberos 인증을 할 수 없습니다. 기본적으로 서비스가 구성 되는 컴퓨터를 시작 하는 경우 자동으로 시작 하도록 합니다.

시작 Microsoft Exchange 서비스 호스트 서비스를 확인 하려면

1.  **시작** 을 클릭 하 고 **services.msc** 를 입력 한 다음 목록에서 **services.msc** 를 선택 합니다.

2.  **서비스** 창에서 서비스 목록에서 **Microsoft Exchange 서비스 호스트** 서비스를 찾습니다.

3.  서비스의 상태를 **실행** 해야 합니다. 상태 하지 않으면 **를 실행** 하는 경우 서비스를 마우스 오른쪽 단추로 클릭 한 다음 **시작** 을 클릭 합니다.

## Kerberos는 클라이언트 액세스 서버에서 유효성 검사

각 클라이언트 액세스 서버에서 ASA 자격 증명을 구성 하는 경우는 **set-ClientAccessServer** cmdlet을 실행 합니다. 이 cmdlet을 실행 한 후에 성공적인 Kerberos 연결을 확인 하려면 로그를 사용할 수 있습니다.

해당 Kerberos 유효성을 검사 하려면 제대로 작동 HttpProxy 로그 파일을 사용 하 여

1.  텍스트 편집기에서 HttpProxy 로그에 저장 된 폴더로 이동 합니다. 기본적으로 로그는 다음 폴더에 저장 됩니다.
    
    %ExchangeInstallPath%\\Logging\\HttpProxy\\RpcHttp

2.  가장 최근 로그 파일을 열고 **협상**단어에 대 한 확인 합니다. 로그 파일에서 해당 줄은 다음과 같은 예제:
    
        2014-02-19T13:30:49.219Z,e19d08f4-e04c-42da-a6be-b7484b396db0,15,0,775,22,,RpcHttp,mail.corp.tailspintoys.com,/rpc/rpcproxy.dll,,Negotiate,True,tailspin\Wendy,tailspintoys.com,MailboxGuid~ad44b1e0-e44f-4a16-9396-3a437f594f88,MSRPC,192.168.1.77,EXCH1,200,200,,RPC_OUT_DATA,Proxy,exch2.tailspintoys.com,15.00.0775.000,IntraForest,MailboxGuidWithDomain,,,,76,462,1,,1,1,,0,,0,,0,0,16272.3359,0,0,3,0,23,0,25,0,16280,1,16274,16230,16233,16234,16282,?ad44b1e0-e44f-4a16-9396-3a437f594f88@tailspintoys.com:6001,,BeginRequest=2014-02-19T13:30:32.946Z;BeginGetRequestStream=2014-02-19T13:30:32.946Z;OnRequestStreamReady=2014-02-19T13:30:32.946Z;BeginGetResponse=2014-02-19T13:30:32.946Z;OnResponseReady=2014-02-19T13:30:32.977Z;EndGetResponse=2014-02-19T13:30:32.977Z;,PossibleException=IOException;
    
    **AuthenticationType** 값이 **협상**후 서버는 표시 되 면 성공적으로 만드는 Kerberos 인증 된 연결 합니다.

## ASA 자격 증명을 유지 관리

ASA 자격 증명의 암호를 주기적으로 새로고침을 수행 해야하는 경우이 문서의 ASA 자격 증명을 구성 하기 위한 단계를 사용 합니다. 일반 암호 유지 관리를 수행 하는 예약 된 작업 설정을 것이 좋습니다. 롤오버 시기 적절 하 게 암호를 확인 하 고 가능한 인증 중단을 방지 하려면 예약 된 작업을 모니터링 해야 합니다.

## Kerberos 인증을 해제

Kerberos를 사용 하지 않도록 하 여 클라이언트 액세스 서버를 구성할 연결을 해제 또는 ASA 자격 증명에서 Spn을 제거 합니다. Spn을 제거 하는 경우에 클라이언트에서 Kerberos 인증을 시도할 수 없습니다 및 협상 인증을 사용 하도록 구성 된 클라이언트에서 NTLM이 대신 사용 합니다. Kerberos만 사용 하도록 구성 된 클라이언트 연결할 수 없습니다. Spn 제거 되 면 계정을 삭제 해야 합니다.

ASA 자격 증명을 제거 하려면

1.  Exchange 2013 서버에서 Exchange 관리 셸을 열고 다음 명령을 실행 합니다.
    
    ```powershell
Set-ClientAccessServer CAS-1 -RemoveAlternateServiceAccountCredentials
```

2.  이 작업을 즉시 수행 하지 않아도 있지만 결국를 다시 시작 해야 모든 클라이언트 컴퓨터는 컴퓨터에서 Kerberos 티켓 캐시의 선택을 취소 합니다.

