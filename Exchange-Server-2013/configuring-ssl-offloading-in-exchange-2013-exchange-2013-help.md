---
title: 'SSL 오프 로딩 Exchange 2013 구성: Exchange 2013 Help'
TOCTitle: SSL 오프 로딩 Exchange 2013 구성
ms:assetid: 654cc2c2-918b-48fc-9532-9c8e3012810d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn635115(v=EXCHG.150)
ms:contentKeyID: 61203322
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# SSL 오프 로딩 Exchange 2013 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-08-22_

이 문서를 통해 SP1(서비스 팩 1)이 설치된 Exchange 2013 클라이언트 액세스 서버에서 프로토콜 및 관련 서비스에 대해 SSL 오프로딩을 구성하는 방법을 파악할 수 있습니다. 클라이언트 액세스 서버가 여러 개인 경우 온-프레미스 조직의 SP1이 설치된 모든 클라이언트 액세스 서버에서 각 프로토콜 또는 서비스에 대해 필요한 단계를 수행해야 합니다. 또한 조직의 각 클라이언트 액세스 서버는 동일하게 구성해야 합니다. 최신 CU(누적 업데이트) 또는 서비스 팩으로 업그레이드하고 있으며 SSL 오프로딩을 계속 사용하려면 Exchange 2013 클라이언트 액세스 서버에서 해당 업데이트를 적용하거나 업그레이드를 수행한 후 다음 단계를 다시 수행해야 합니다.

사용하는 인증서를 보다 쉽게 관리할 수 있다는 것이 SSL 오프로딩의 가장 큰 이점입니다. SP1이 설치된 각 클라이언트 액세스 서버에 대해 개별 SSL 인증서를 사용하는 대신 단일 SSL 인증서를 모든 클라이언트 액세스 서버로 가져와서 사용할 수 있습니다. 기존 SSL 인증서를 사용할 수도 있고 새로 만든 SSL 인증서를 사용할 수도 있습니다.


> [!WARNING]
> 인터넷 정보 서비스 (IIS) 관리자, Exchange 관리 셸 또는 명령줄 인터페이스를 사용 하 여 SSL 오프 로딩을 구성 하려면 <STRONG>기본 웹사이트</STRONG> 와 <STRONG>Exchange 백엔드</STRONG> 사이트 것을 확인할 합니다. SSL 오프 로딩을 대 한 <STRONG>기본 웹사이트</STRONG> 를 구성 하 고 변경 하지 않은 <STRONG>Exchange 백엔드</STRONG> 사이트에만 합니다.



**목차**

Configuring SSL offloading for Outlook Web App

Configuring SSL offloading for the Exchange Admin Center (EAC)

Configuring SSL offloading for Outlook Anywhere

Configuring SSL offloading for the Offline Address Book (OAB)

Configuring SSL offloading for Exchange ActiveSync (EAS)

Configuring SSL offloading for Exchange Web Services (EWS)

Configuring SSL offloading for the Autodiscover service

Configuring SSL offloading for the Mailbox Replication Proxy Service (MRSProxy)

Outlook 클라이언트(MAPI 가상 디렉터리)에 대해 SSL 오프로딩 구성

Using a Shell script to enable SSL offloading for all protocols and services

Configuring coexistence with Exchange 2007 and Exchange 2010

## 시작하기 전에 알아야 할 내용

  - 조직에 필요한 모든 클라이언트 액세스 서버 및 사서함 서버를 설치합니다.

  - 조직의 각 클라이언트 액세스 서버와 사서함 서버에 SP1(서비스 팩 1)을 설치합니다. SP1을 다운로드하려면 [Exchange 2013용 업데이트](updates-for-exchange-2013-exchange-2013-help.md)를 참조하세요.

  - [기능 사용 권한](feature-permissions-exchange-2013-help.md)을 확인하여 Exchange 2013에 필요한 사용 권한을 결정합니다.

  - 클라이언트 액세스 서버에 필요한 사용 권한을 확인하려면 [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)에서 "클라이언트 액세스 서버 사용 권한"을 참조하세요.

  - 클라이언트 액세스 서버에 필요한 사용 권한을 확인하려면 [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)에서 "Outlook Web App 사용 권한"을 참조하세요.

  - 일부 절차를 수행하려면 셸만 사용해야 할 수 있습니다. 온-프레미스 Exchange 조직에서 셸을 여는 방법을 확인하려면 [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))를 참조하세요.

  - 클라이언트 액세스 서버와 SSL 연결을 끊을 장치에서 기존 인증서를 사용하려면 클라이언트 액세스 서버의 개인 키와 함께 인증서를 내보낸 다음 장치에서 인증서를 설치하거나 가져옵니다. 자세한 내용은 [Export-ExchangeCertificate](https://technet.microsoft.com/ko-kr/library/aa996305\(v=exchg.150\))를 참조하세요.

  - 새 인증서를 사용하려면 EAC 또는 셸을 사용해서 새 인증서를 만들고 가져온 다음 사용하도록 설정해야 합니다. 자세한 내용은 [Exchange 2013 인증서 관리 UI](exchange-2013-certificate-management-ui-exchange-2013-help.md)를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Outlook Web App에 대해 SSL 오프로딩 구성

Outlook Web App에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **owa** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **owa** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **owa** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeOWAAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeOWAAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## EAC(Exchange 관리 센터)에 대해 SSL 오프로딩 구성

EAC에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **ecp** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **ecp** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **ecp** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
        ```
        

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeECPAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeECPAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## 외부에서 Outlook 사용에 대해 SSL 오프로딩 구성

외부에서 Outlook 사용에 대 한 오프 로드 하는 SSL 기본적으로 활성화 됩니다. Outlook Anywhere 클라이언트를 얻을 수 전자 메일 공용 또는 개인 네트워크에서. 기본적으로 내부 호스트 이름 또는 서버의 FQDN을 내부 Outlook 클라이언트가 연결할 수 있도록 사용 됩니다. 그러나 외부에서 Outlook 사용 되지 않습니다 내부적으로 사용 하는 경우 내부 호스트 이름을 제거 해야 합니다. Outlook 클라이언트에 대 한 내부 및 외부 액세스를 허용 하려면 구성 내부 및 외부 호스트 이름, 인증 방법 각각에 대해 설정 하 고 해야 ssl을 사용 하 여 내부 및 외부 클라이언트를 설정 합니다. 외부 클라이언트에 대 한 인증 방법을 구성할 EAC 또는 Exchange 관리 셸을 사용할 수 있지만 내부 클라이언트에 대 한 셸을 사용 해야 합니다.

  - **1 단계**   외부에서 Outlook 사용에 대 한 외부 호스트 이름을 추가 하지 않은 경우 EAC 또는 셸을 사용할 수 있습니다.
    
      - EAC를 사용하여 **서버**로 이동한 다음 목록에서 클라이언트 액세스 서버의 이름을 선택하고 **편집**을 클릭합니다. **Exchange Server** 창에서 **외부에서 Outlook 사용**을 클릭하고 **사용자가 조직에 연결하는 데 사용할 외부 호스트 이름(예: contoso.com)을 지정합니다.** 상자에 외부 호스트 이름을 입력합니다. **SSL 오프로딩 허용** 옵션이 선택되어 있는지 확인하고 **저장**을 클릭합니다.
    
      - Exchange 관리 셸을 사용하여 **시작**을 클릭하고 **시작** 메뉴에서 **Exchange 관리 셸**을 클릭합니다. 창에 다음을 입력하고 Enter 키를 누릅니다.
        
          ```powershell
          Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -Externalhostname ClientAccessServer1.contoso.com -ExternalClientsRequireSsl:$True -ExternalClientAuthenticationMethod Basic
          ```

  - **2단계**   기본적으로 SSL 오프로딩은 사용하도록 설정됩니다. 그러나 SSL 오프로딩이 사용하지 않도록 설정되어 사용하도록 설정하려는 경우에는 EAC 또는 Exchange 관리 셸을 사용할 수 있습니다.
    
      - EAC를 사용하여 **서버**로 이동한 다음 목록에서 클라이언트 액세스 서버의 이름을 선택하고 **편집**을 클릭합니다. **Exchange Sever** 창에서 **외부에서 Outlook 사용**과 **SSL 오프로딩 허용** 옵션을 차례로 클릭하고 **저장**을 클릭합니다.
    
      - 셸을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
          ```powershell
          Set-OutlookAnywhere -Identity ClientAccessServer1\Rpc* -SSLOffloading $true
          ```

  - **3단계**   기본적으로는 **Rpc** 가상 디렉터리에 대해 **SSL 필요**가 선택되지 않지만 SSL을 사용하지 않도록 설정되었음을 확인하려는 경우 IIS(인터넷 정보 서비스) 관리자를 사용할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **Rpc** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택이 취소되어 있는지 확인한 다음 **작업** 창에서 **적용**을 클릭합니다.

  - **4단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeRpcProxyFrontEndAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeRpcProxyFrontEndAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.


> [!IMPORTANT]
> 클라이언트 액세스 서버에서 IIS를 다시 시작하더라도 서비스 호스트 프로세스가 15분마다 IIS(인터넷 정보 서비스)에 Active Directory의 변경 내용을 적용할 때까지 기다려야 합니다.



맨 위로 이동

## OAB(오프라인 주소록)에 대해 SSL 오프로딩 구성

OAB(오프라인 주소록)에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **OAB** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **OAB** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **OAB** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeOABAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeOABAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## EAS(Exchange ActiveSync)에 대해 SSL 오프로딩 구성

EAS(Exchange ActiveSync)에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **Microsoft-Server-ActiveSync** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **Microsoft-Server-ActiveSync** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **Microsoft-Server-ActiveSync** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
          ```powershell
          appcmd set config "Default Web Site/MSExchangeSyncAppPool" /section:access /sslFlags:None /commit:APPHOST
          ```

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeSyncAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeSyncAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## EWS(Exchange 웹 서비스)에 대해 SSL 오프로딩 구성

EWS(Exchange 웹 서비스)에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **EWS** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **EWS** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **EWS** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeServicesAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeServicesAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## 자동 검색 서비스에 대해 SSL 오프로딩 구성

자동 검색 서비스에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **Autodiscover** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **Autodiscover** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **Autodiscover** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd set config "Default Web Site/autodiscover" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeAutodiscoverAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeAutodiscoverAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## MRSProxy(사서함 복제 프록시 서비스)에 대해 SSL 오프로딩 구성

(MRSProxy) 사서함 복제 프록시 서비스는 모든 Exchange 2013 클라이언트 액세스 서버에 설치 됩니다. MRSProxy 도움이으로 온-프레미스 Office 365로 온-프레미스 사서함을 이동 요청 크로스 포리스트 이동을 걸 수 있습니다. 그러나 기본적으로 MRSProxy 비활성화 됩니다. 사용 하는 것을 하는 경우 Office 365로 사서함을 이동 하는 것에 대 한 온-프레미스 Exchange 포리스트 또는 크로스 포리스트, 온-프레미스 사서함 이동에 대 한 원격 Exchange 포리스트에 활성화 해야 합니다. Exchange 웹 서비스 (EWS)에서 실행 하는 MRSProxy 서비스, 하지만 SSL 오프 로딩 구성에 지원 되지 않습니다.

MRSProxy 서비스에서는 트래픽을 서명/암호화해야 하기 때문입니다. 모든 하드웨어 부하 분산 장치 또는 방화벽은 MRSProxy 트래픽을 클라이언트 액세스 서버로 보내기 전에 다시 암호화해야 합니다. 이 경우에는 오프로딩이 작동하도록 SSL 브리징을 구성하는 것이 좋습니다.

**SSL 또는 SSL 브리징 반전**   역방향 SSL 또는 SSL 브리징 하드웨어 부하 분산 장치에서 사용 하도록 설정 하면 각 CAS 서버에서 앞의 단계를 수행할 필요가 없습니다. 그러나 하드웨어 부하 분산 장치에서 역방향 SSL을 설정 하면 SSL 암호화 및 암호 해독 클라이언트 액세스 서버와 머무르는 의미 합니다. 이 경우에 SSL 암호화 및 암호 해독 하드웨어 부하 분산 장치 및 클라이언트 액세스 서버 모두에 발생 합니다. Exchange 2013 SSL을 사용 하도록 선택 (SSL 브리징) 오프 로딩 또는 역방향 SSL은 조직의 목표 및 보안 사례가 구현 해야 합니다. 다음 그림을 클라이언트 연결에 SSL 브리징 (역방향 SSL) 사용 하도록 설정 합니다.

![SSL 브리징](images/Dn635115.a08aacc1-0ab4-46b3-bdae-b9518a3f5748(EXCHG.150).jpg "SSL 브리징")

## Outlook 클라이언트(MAPI 가상 디렉터리)에 대해 SSL 오프로딩 구성

Outlook 클라이언트에 대해 SSL 오프로딩을 사용하도록 설정하려면 **기본 웹 사이트**의 **MAPI** 가상 디렉터리에서 SSL 요구 사항을 제거해야 합니다.

  - **1단계**   IIS(인터넷 정보 서비스) 관리자 또는 명령줄을 사용하여 **MAPI** 가상 디렉터리에서 SSL을 사용하지 않도록 설정할 수 있습니다.
    
      - IIS(인터넷 정보 서비스) 관리자를 사용하여 **사이트** \> **기본 웹 사이트**를 확장하고 **MAPI** 가상 디렉터리를 선택합니다. 결과 창의 **IIS** 아래에서 **SSL 설정**을 두 번 클릭합니다. **SSL 설정** 결과 창에서 **SSL 필요** 확인란 선택을 취소한 다음 **작업** 창에서 **적용**을 클릭합니다.
    
      - 명령줄을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
        ```

  - **2단계**   다음 방법 중 하나를 사용하여 올바른 응용 프로그램 풀을 재활용하거나 인터넷 정보 서비스를 다시 시작해야 합니다.
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        appcmd Recycle AppPool MSExchangeMapiFrontEndAppPool
        ```
    
      - Windows PowerShell cmdlet을 사용하여 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        IIS:\>Restart-WebAppPool MSExchangeMapiFrontEndAppPool
        ```
    
      - 명령줄 사용: **시작** \> **실행**으로 이동하여 **cmd**를 입력하고 Enter 키를 누릅니다. 명령 프롬프트 창에서 다음을 입력하고 Enter 키를 누릅니다.
        
        ```powershell
        iisreset /noforce
        ```
    
      - IIS(인터넷 정보 서비스) 관리자 사용: IIS(인터넷 정보 서비스) 관리자의 **작업** 창에서 **다시 시작**을 클릭합니다.

맨 위로 이동

## 스크립트를 사용하여 모든 프로토콜과 서비스에 대해 SSL 오프로딩을 사용하도록 설정

여러 Exchange 2013 클라이언트 액세스 서버를 사용하는 대규모 조직에서 작업 중인 경우에는 위의 단계를 보다 빠르게 수행할 수 있습니다. 이렇게 하려면 다음 스크립트 중 하나의 명령을 복사하여 메모장에 붙여 넣고 필요한 대로 변경한 다음, 파일을 .ps1 확장명으로 저장하여 Exchange 관리 셸에서 실행하면 됩니다. 필요에 따라서는 이 두 스크립트를 모두 사용하여 단일 클라이언트 액세스 서버 또는 여러 클라이언트 액세스 서버의 모든 프로토콜과 서비스에 대해 SSL 오프로딩을 구성할 수 있습니다.


> [!NOTE]
> <STRONG>Set-OutlookAnywhere</STRONG> cmdlet 항목의 경우 "MyServer를" 클라이언트 액세스 서버 이름으로 바꿉니다.



**Set-WebConfigurationProperty 사용**

  ```powershell
  Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
  Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS:  -Location "Default Web Site/OWA"
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/ecp"
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/EWS"
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Autodiscover"
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/Microsoft-Server-ActiveSync"
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/OAB"
  Set-WebConfigurationProperty -Filter //security/access -name sslflags -Value "None" -PSPath IIS: -Location "Default Web Site/MAPI"
  ```
```powershell
iisreset /noforce
```

**appcmd 사용**


> [!NOTE]
> <STRONG>Set-OutlookAnywhere</STRONG> cmdlet 항목의 경우 "MyServer를" 클라이언트 액세스 서버 이름으로 바꿉니다.



  ```powershell
  Set-OutlookAnywhere -Identity MyServer\Rpc* -Externalhostname MyServer.mail.contoso.com -ExternalClientsRequireSsl $True -ExternalClientAuthenticationMethod Basic
  Set-OutlookAnywhere -Identity MyServer\Rpc* -SSLOffloading $true
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/owa" /section:access /sslFlags:None /commit:APPHOST
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/ecp" /section:access /sslFlags:None /commit:APPHOST
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/EWS" /section:access /sslFlags:None /commit:APPHOST
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Autodiscover" /section:access /sslFlags:None /commit:APPHOST
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/Microsoft-Server-ActiveSync" /section:access /sslFlags:None /commit:APPHOST
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/OAB" /section:access /sslFlags:None /commit:APPHOST
  &$env:systemroot\system32\inetsrv\appcmd set config "Default Web Site/MAPI" /section:access /sslFlags:None /commit:APPHOST
  ```
```powershell
iisreset /noforce
```

맨 위로 이동

## Exchange 2007 및 Exchange 2010 동시 사용 구성

조직에서 Exchange 2003 및 Exchange 2010 서버를 함께 사용하는 동시 사용 시나리오에서 Exchange 2010 클라이언트 액세스 서버를 배포한 후 수행해야 하는 첫 단계 중 하나는 Exchange 2003 사용자가 Exchange 2010 클라이언트 액세스 서버 그룹에서 사서함에 액세스할 수 있도록 DNS를 변경하는 것입니다. 이러한 시나리오에서는 클라이언트 액세스 서버 전체에 클라이언트 트래픽을 분산시키는 데 사용되는 부하 분산 장치에서 SSL 오프로딩을 사용하도록 설정하는 기능이 완전하게 지원됩니다.

**다른 Outlook Web App 버전과 동시 사용**

Exchange 2013 클라이언트 액세스 서버에 대해 SSL 오프로딩이 구성되어 있는 경우 Exchange 2007 및 Exchange 2010과의 동시 사용이 가능합니다.

  - Exchange 2007과 동시에 사용하려면 이전 네임스페이스가 필요하며, Outlook Web App 및 Exchange 웹 서비스에 대해서만 리디렉션됩니다. 자동 검색, 외부에서 Outlook 사용 및 Exchange ActiveSync는 이전 버전으로 프록시됩니다.

  - Exchange 2010과 동시에 사용하려는 경우 외부 URL이 설정되어 있으면 리디렉션되고 그렇지 않으면 프록시됩니다.

맨 위로 이동

