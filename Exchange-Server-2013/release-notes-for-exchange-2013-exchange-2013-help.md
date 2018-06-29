---
title: 'Exchange Server 2013 릴리스 정보: Exchange 2013 Help'
TOCTitle: Exchange Server 2013 릴리스 정보
ms:assetid: 1879fd5e-3d63-4264-9cc2-9c050c6ab3c5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150489(v=EXCHG.150)
ms:contentKeyID: 50482612
ms.date: 04/17/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exchange Server 2013 릴리스 정보

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2018-04-16_

Microsoft Exchange Server 2013을 시작합니다. 이 항목에는 Exchange 2013을 성공적으로 배포하기 위해 알아 두어야 할 중요한 정보가 포함되어 있습니다. 배포를 시작하기 전에 이 항목을 자세히 읽으십시오.

이 항목에서 다루는 섹션은 다음과 같습니다.

  - 설치 및 배포

  - Exchange 관리 셸

  - 사서함

  - 공용 폴더

  - 메일 흐름

  - 클라이언트 연결

  - Exchange 2010 동시 사용

## 설치 및 배포

  - **msExchProductId에서 설치된 Exchange 2013의 릴리스 버전을 반영하지 않음** Exchange가 Active Directory 스키마를 확장하고 Exchange용 Active Directory를 준비하면 여러 속성이 업데이트되어 준비가 완료되었음을 나타냅니다. 이러한 속성 중 하나는 `Configuration` 명명 컨텍스트의 `CN=<your organization>, CN=Microsoft Exchange, CN=Services, CN=Configuration, DC=<domain>` 컨테이너에 있는 *msExchangeProductId*입니다. Active Directory 스키마의 변경 사항이 Exchange 2013 릴리스에 포함되어 있지 않으면, 이 속성이 업데이트되지 않거나 예기치 않은 값이 표시될 수도 있습니다. 설치 중인 Exchange 2013 버전과 값이 일치하지 않으면 혼동이 야기될 수 있습니다.
    
    이 동작은 *msExchProductId*의 값이 설치 중인 Exchange 2013 버전을 반영하지 않은 경우 예상됩니다. 이 속성은 마지막으로 Active Directory 스키마를 변경한 Exchange 2013 버전을 반영합니다. 혼동을 피하려면 [Active Directory 및 도메인 준비](prepare-active-directory-and-domains-exchange-2013-help.md)의 [작동 여부 확인 방법](prepare-active-directory-and-domains-exchange-2013-help.md)의 단계에 따라 Active Directory가 업데이트되어 있고 설치 중인 Exchange 2013의 릴리스 준비가 완료되었음을 확인할 수 있습니다.

  - **설치 프로그램에서 .NET Framework 4.0을 잘못 요구함**   컴퓨터에 .NET Framework를 설치하지 않은 상태로 Exchange 2013을 설치하려고 하면 설치 프로그램은 실제로 .NET Framework 4.5 이상이 필요할 때 .NET Framework 4.0을 설치하라는 잘못된 메시지가 표시됩니다.
    
    이 문제를 해결하려면 .NET Framework 4.5 이상을 설치합니다. .NET Framework 4.0은 설치할 필요가 없습니다. 전체 필수 구성 요소 목록을 보려면 [Exchange 2013 필수 구성 요소](exchange-2013-prerequisites-exchange-2013-help.md)을 참조하십시오.

  - **누적 업데이트 설치 중에 Exchange XML 응용 프로그램 구성 파일을 덮어씀**   Exchange 누적 업데이트 또는 서비스 팩을 설치하면 Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 또는 사서함 서버의 EdgeTransport.exe.config 파일)의 모든 사용자 지정 서버 단위 설정을 덮어씁니다. 설치 후에 서버를 다시 구성하기 쉽도록 이 정보를 저장해야 합니다. Exchange 누적 업데이트 또는 서비스 팩을 설치한 후에 이러한 설정을 다시 구성해야 합니다.

  - **대리인 관리 권한을 사용하여 Exchange를 설치하면 설치 프로그램이 실패할 수 있음** 위임된 설치 프로그램 역할 그룹에 대해서만 구성원인 사용자가 미리 프로비전된 서버에 Exchange를 설치하려고 하면 설치 프로그램이 실패합니다. 이는 위임된 설치 프로그램 그룹에 Active Directory의 특정 개체를 만들고 구성하는 데 필요한 권한이 부족하기 때문입니다.
    
    이 문제를 해결하려면 다음 중 하나를 수행합니다.
    
      - 사용자가 설치하고 있는 Exchange를 Domain Admins Active Directory 보안 그룹에 추가합니다.
    
      - 조직 관리 역할 그룹의 구성원인 사용자를 통해 Exchange를 설치합니다.

Exchange 2013 설치 방법에 대한 자세한 내용은 [계획 및 배포](planning-and-deployment-for-exchange-2013-installation-instructions.md)를 참조하세요.

## Exchange 관리 셸

  - **셸에서 예기치 않게 Exchange 2007 또는 Exchange 2010 cmdlet을 로드함** 이전에는 Exchange 2013 서버에서 셸을 열면 셸에서 로컬 서버 또는 Exchange 2013을 실행하는 다른 서버에 대한 연결이 열렸습니다. 연결이 실행되면 Exchange 2013 cmdlet이 로드됩니다. Exchange 2013 CU11부터는 로그온한 사용자의 사서함이 있는 Exchange 서버에 셸이 연결됩니다. 로그온한 사용자에게 사서함이 없는 경우 SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 중재 사서함이 있는 서버에 셸이 연결됩니다. 대상 서버는 Exchange의 지원되는 모든 버전일 수 있습니다. 이는 로그온한 사용자의 사서함이 Exchange 2010 서버에 있는 경우 셸이 서버에 연결되고 Exchange 2010 cmdlet을 로드합니다. Exchange 2010 cmdlet은 Exchange 2013 구성이나 서버를 관리할 수 없으므로 특정 작업을 수행하지 못할 수도 있습니다.
    
    Exchange 2013 CU11부터 이 동작은 기본 사항입니다. 셸이 Exchange 2013 cmdlet을 로드하도록 하려면 로그온한 사용자 사서함을 Exchange 2013으로 이동합니다. 로그온한 사용자에게 사서함이 없는 경우 SystemMailbox{bb558c35-97f1-4cb9-8ff7-d53741dc928c} 중재 사서함을 Exchange 2013 서버로 이동합니다.
    
    중재 사서함 이동 방법에 대한 자세한 내용은 Exchange Team 블로그에서 [Exchange 관리 셸 및 사서함 위치 고정](https://go.microsoft.com/fwlink/?linkid=717722)을 참조하세요.

## 사서함

  - **다른 버전의 Exchange를 실행하는 사서함 서버는 동일한 데이터베이스 가용성 그룹에 추가될 수 있음** **Add-DatabaseAvailabilityGroupServer** cmdlet 및 Exchange 관리 센터에서 Exchange 2013 서버를 Exchange 2016 기반 DAG(데이터베이스 가용성 그룹)에 추가하도록 혹은 그 반대로 추가하도록 잘못 허용합니다. Exchange는 동일한 버전(예: Exchange 2013 대 Exchange 2016)을 실행하는 사서함 서버를 DAG에 추가하는 작업만 지원합니다. 또한 Exchange 관리 센터에는 DAG에 추가할 수 있는 서버 목록에 Exchange 2013 및 Exchange 2016 서버가 모두 표시됩니다. 따라서 관리자가 무심코 호환되지 않는 Exchange 버전을 DAG에 추가할 수 있습니다(예: Exchange 2013 서버를 Exchange 2016 기반 DAG에 추가).
    
    현재 이 문제를 해결할 수 있는 방법이 없습니다. 관리자는 사서함 서버를 DAG에 추가할 때 유심히 살펴야 합니다. Exchange 2013 서버만 Exchange 2013 기반 DAG에 추가하고 Exchange 2016 서버만 Exchange 2016 기반 DAG에 추가합니다. Exchange 관리 센터의 서버 목록에 있는 **버전** 열만 보고도 각 Exchange 버전을 구분할 수 있습니다. 다음은 Exchange 2013 및 Exchange 2016의 서버 버전입니다.
    
      - **Exchange 2013** 15.0(빌드 xxx.xx)
    
      - **Exchange 2016** 15.1(빌드 xxx.xx)

  - **이전 Exchange 버전에서 마이그레이션할 때 사서함 크기 증가**   사서함을 이전 버전의 Exchange에서 Exchange 2013으로 이동하면 사서함 크기가 30~40% 증가하여 보고될 수 있습니다. 사서함 데이터베이스에 사용되는 디스크 공간은 증가하지 않고 각 사서함에 사용되는 공간 속성만 증가되었습니다. 사서함 크기의 증가는 할당량 계산에 모든 항목 속성이 포함되어 사서함 내의 항목이 사용하는 공간을 보다 정확히 계산하기 때문에 발생합니다. 이러한 증가로 인해 사서함을 Exchange 2013으로 이동할 때 일부 사용자의 사서함 크기 할당량이 초과될 수 있습니다.
    
    사용자의 사서함 크기 할당량이 초과되지 않게 하려면 새 할당량 계산을 수용하도록 데이터베이스 또는 사서함 할당량 값을 늘립니다. 데이터베이스 또는 사서함 할당량 값을 구성하려면 **Set-MailboxDatabase** 및 **Set-Mailbox** cmdlet에서 각각 *IssueWarningQuota*, *ProhibitSendQuota* 및 *ProhibitSendReceiveQuota* 매개 변수를 사용합니다.

  - **Outlook 2007 및 Outlook 2010 클라이언트가 오프라인 주소록을 다운로드하지 못할 수 있음**   OAB(오프라인 주소록) 내부 URL을 인터넷에서 액세스할 수 없는 경우 Outlook 2007 및 Outlook 2010 클라이언트가 OAB를 다운로드하지 못할 수 있습니다.
    
    Outlook 2007 및 Outlook 2010 클라이언트에 대해 이 문제를 해결하려면 인터넷에서 OAB 내부 URL에 액세스할 수 있도록 설정합니다. Outlook 2013은 이 문제의 영향을 받지 않습니다.

  - **기존 Exchange 조직에서 Exchange 2013을 설치하면 모든 클라이언트가 OAB를 다운로드할 수 있음**   기존 Exchange 2007 또는 Exchange 2010 조직에 Exchange 2013 서버를 처음으로 설치하면 조직의 모든 클라이언트가 새 OAB 복사본을 다운로드하여 네트워크 포화 상태 및 서버 성능 문제가 발생할 수 있습니다. 이 문제가 발생하는 이유는, Exchange 2013에서 Exchange 2007 또는 Exchange 2010 OAB보다 우선하는 새 기본 OAB를 조직에 만들기 때문입니다. 특정 OAB가 할당되어 있지 않은 사서함 또는 특정 OAB가 할당되지 않은 사서함 데이터베이스에 있는 사서함은 새 기본 OAB를 다운로드합니다.
    
    Exchange 2013 설치 시 클라이언트가 새 OAB 복사본을 다운로드하지 않도록 하려면 모든 사서함 또는 사서함이 있는 사서함 데이터베이스에 OAB를 할당합니다. 이 작업은 조직에 Exchange 2013을 설치하기 전에 수행해야 합니다.

  - **사용자들은 요청된 OAB를 담당하지 않는 OAB 생성 사서함으로 라우팅될 수 있음**   Exchange 2013 CU5 및 이후 버전의 CU는 OAB가 OAB 생성 사서함에 연결되는 방식을 변경합니다. 이렇게 변경하면 사용자는 요청 중인 OAB를 담당하지 않는 OAB 생성 사서함으로 라우팅될 수 있습니다. 이러한 상황은 다음 모든 조건에 해당하는 경우 발생할 수 있습니다.
    
      - 조직에 여러 개의 OAB 생성 사서함이 있는 경우
    
      - 클라이언트 액세스 서버를 업그레이드하기 전에 OAB 생성 사서함을 호스팅하는 사서함 서버를 업그레이드하는 경우
    
      - CU5 이전 릴리스에서 CU5 이후 릴리스로 Exchange 2013 서버를 업그레이드하는 경우(예를 들어 Exchange 2013 CU3에서 Exchange 2013 CU6으로 업그레이드)
    
      - 클라이언트 액세스 서버에서 CU5 이전 릴리스를 실행하고 있는 경우
    
    이 문제를 해결하려면 사서함 서버를 업그레이드하기 전에 클라이언트 액세스 서버를 Exchange 2013 CU6 이상으로 업그레이드해야 합니다. 이렇게 하면 클라이언트 액세스 서버는 사용자의 OAB 생성을 담당하는 OAB 생성 사서함으로 요청을 프록시하는 방법을 알게 됩니다.
    
    Exchange 2013 CU5의 OAB 변경 사항에 대한 자세한 내용은 [Exchange 2013 누적 업데이트 5의 향상된 OAB](https://go.microsoft.com/fwlink/p/?linkid=400642)를 참조하세요.

## 공용 폴더

  - **권한이 없는 보낸 사람은 더 이상 메일 사용이 가능한 공용 폴더에 메시지를 보낼 수 없음** Exchange 2013 CU6 이전에 권한이 없는 보낸 사람이 메일 사용이 가능한 공용 폴더에 메시지를 보낼 수 있었습니다. 이로 인해 외부 보낸 사람이 공용 폴더에 설정된 사용 권한과 관계없이 메일 사용이 가능한 공용 폴더에 메일을 보낼 수 있었습니다.
    
    Exchange 2013 CU6부터 외부 보낸 사람이 메일 사용이 가능한 공용 폴더에 메일을 보내려면 **익명** 사용자가 적어도 **항목 만들기** 권한을 부여해야 합니다. 메일 사용이 가능한 공용 폴더를 설정했지만 아직 해당 작업을 완료하지 않은 경우 외부 보낸 사람은 배달 실패 알림을 받게 되며 메시지가 메일 사용이 가능한 공용 폴더로 배달되지 않습니다.
    
    셸 또는 Outlook을 사용하여 익명 사용자의 사용 권한을 설정할 수 있습니다. 익명 사용자에 사용 권한을 설정하는 방법에 대한 자세한 내용은 [메일 사용이 가능한 또는 공용 폴더 메일-사용 안함](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md)를 참조하세요.

  - 레거시 Exchange 서버에서 Exchange 2013으로 마이그레이션할 수 있는 공용 폴더의 최대 수는 500,000개입니다. 공용 폴더 마이그레이션에 대한 자세한 내용은 [마이그레이션 일괄 처리를 사용 하 여 이전 버전에서 Exchange 2013 공용 폴더 마이그레이션](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)을 참조하세요.

## 메일 흐름

  - **클라이언트 액세스 서버에서 TransportAgent cmdlet을 사용하려면 로컬 Windows PowerShell 필요**   **\*-TransportAgent** cmdlet과 관련된 문제가 있습니다. 즉, Exchange 관리 셸에서 이러한 cmdlet을 사용하면 클라이언트 액세스 서버에서 전송 에이전트를 설치, 제거 및 관리하지 못합니다. 클라이언트 액세스 서버에서 전송 에이전트를 설치, 제거 및 관리하려면 ExchangeWindows PowerShell 스냅인을 수동으로 로드한 다음 **\*-TransportAgent** cmdlet을 실행해야 합니다. Exchange 관리 셸을 사용하여 전송 에이전트를 설치, 제거 또는 관리하려고 하면 연결되어 있는 Exchange 2013 사서함 서버에 변경 내용이 적용됩니다.
    
    클라이언트 액세스 서버에서 전송 에이전트를 설치, 제거 또는 관리하려면 관리하려는 클라이언트 액세스 서버에서 다음을 수행합니다.
    

    > [!WARNING]
    > <CODE>Microsoft.Exchange.Management.PowerShell.SnapIn</CODE>Windows PowerShell 스냅인을 로드하고 <STRONG>*-TransportAgent</STRONG> cmdlet 외의 cmdlet을 실행하는 것은 지원되지 않으며, 이 경우 Exchange 배포에 복구할 수 없는 손상이 발생할 수 있습니다.<BR>전송 에이전트를 설치, 제거 또는 관리할 클라이언트 액세스 서버에서 로컬 관리자여야 합니다. Exchange 파일, 디렉터리 또는 Active Directory 개체에 대한 ACL(액세스 제어 목록)의 수정은 지원되지 않습니다.

    

    > [!IMPORTANT]
    > 클라이언트 액세스 서버에서만 다음 절차를 수행합니다. 사서함 서버에서 전송 에이전트를 관리하려는 경우 ExchangeWindows PowerShell 스냅인을 로드할 필요가 없습니다.

    
    1.  새 Windows PowerShell 창을 엽니다.
    
    2.  다음 명령을 실행합니다.
        
            Add-PSSnapin Microsoft.Exchange.Management.PowerShell.SnapIn
    
    3.  일반적인 전송 에이전트 관리 작업을 수행합니다.
    
    4.  관리하려는 각 클라이언트 액세스 서버에서 이 절차를 반복합니다.

## 클라이언트 연결

  - **도메인에 가입되지 않은 클라이언트에 대한 NTLM 인증이 실패함**   다음과 같은 상황에서는 Windows Live Mail 등의 클라이언트와 Exchange 2013 간의 인증이 실패할 수 있습니다.
    
      - 클라이언트가 사용하는 인증 모드가 NTLM인 경우
    
      - 컴퓨터가 도메인에 가입되어 있지 않은 경우
    
    이 문제를 해결하려면 다음 중 하나를 수행하면 됩니다.
    
      - 클라이언트를 실행 중인 컴퓨터를 도메인에 가입시킵니다.
    
      - 클라이언트가 사용하는 인증 유형을 NTLM에서 TLS를 통한 기본 인증으로 변경합니다.

  - **Send-MailMessage cmdlet과 함께 사용할 때 GSSAPI 인증 실패**Windows PowerShell의 기본 설치에 포함된 **Send-MailMessage** cmdlet을 사용하여 Exchange 2013에 인증된 메일을 보낼 때 GSSAPI(   Generic Security Service Application Program Interface) 인증이 실패할 수 있습니다. 이 경우 연결을 수신한 Exchange 2013 클라이언트 액세스 서버의 **응용 프로그램** 이벤트 로그에 다음 정보가 포함된 항목이 표시됩니다.
    
      - **Source** MSExchangeFrontEndTransport
    
      - **이벤트 ID** 1035
    
      - **설명** 수신 커넥터 클라이언트 프런트 엔드 \<*서버 이름*\>에 대한 `IllegalMessage` 오류로 인해 인바운드 인증에 실패했습니다. 인증 메커니즘은 Gssapi입니다. Exchange 인증을 시도한 클라이언트의 원본 IP 주소는 \[\<*클라이언트 IP 주소*\>\]입니다.
    
    이 문제를 해결하려면 Exchange 2013 클라이언트 액세스 서버의 클라이언트 수신 커넥터에서 `Integrated` 인증 방법을 제거해야 합니다. 클라이언트 수신 커넥터에서 `Integrated` 인증 방법을 제거하려면 **Send-MailMessage** cmdlet을 실행하는 컴퓨터에서 연결을 수신할 수 있는 각 Exchange 2013 클라이언트 액세스 서버에 다음 명령을 실행합니다.
    
        Set-ReceiveConnector "<server name>\Client Frontend <server name>" -AuthMechanism Tls, BasicAuth, BasicAuthRequireTLS

  - **Exchange 2013 SP1로 업그레이드하면 MAPI over HTTP의 성능이 저하될 수 있음**   Exchange 2013 누적 업데이트에서 Exchange 2013 SP1로 업그레이드하고 MAPI over HTTP를 사용하도록 설정하면 해당 프로토콜을 사용하여 Exchange 2013 SP1 서버에 연결하는 클라이언트의 성능이 저하될 수 있습니다. 누적 업데이트에서 Exchange 2013 SP1로 업그레이드하는 동안 필수 설정이 구성되지 않기 때문입니다. Exchange 2013 RTM에서 Exchange 2013 SP1로 업그레이드하거나 Exchange 2013 SP1 이상 서버를 새로 설치하는 경우에는 이 문제가 발생하지 않습니다.
    

    > [!NOTE]
    > 이 문제는 클라이언트 액세스 서버에서 MAPI over HTTP 프로토콜을 사용하도록 설정된 경우에만 발생합니다. 이 프로토콜은 기본적으로 사용하지 않도록 설정됩니다. MAPI over HTTP가 사용하지 않도록 설정된 경우 클라이언트에서 RPC over HTTP 프로토콜이 대신 사용됩니다.

    
    이 문제를 해결하려면 다음을 수행합니다.
    
    1.  클라이언트 액세스 서버 역할을 실행하는 서버의 Windows 명령 프롬프트에서 다음 명령을 실행합니다.
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiFrontEndAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiFrontEndAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiFrontEndAppPool"
    
    2.  사서함 서버 역할을 실행하는 서버의 Windows 명령 프롬프트에서 다음 명령을 실행합니다.
        
            set AppCmdLocation=%windir%\System32\inetsrv
            set ExchangeLocation=%ProgramFiles%\Microsoft\Exchange Server\V15
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiMailboxAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiMailboxAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiMailboxAppPool"
            
            %AppCmdLocation%\appcmd.exe SET AppPool "MSExchangeMapiAddressBookAppPool" /CLRConfigFile:"%ExchangeLocation%\bin\MSExchangeMapiAddressBookAppPool_CLRConfig.config"
            %AppCmdLocation%\appcmd.exe RECYCLE AppPool "MSExchangeMapiAddressBookAppPool"

## Exchange 2010 동시 사용

  - **Exchange 2013 클라이언트 액세스 서버를 통해 프록시 처리되면 Exchange 2010 사서함 액세스 요청이 작동하지 않을 수 있음**   업데이트 롤업이 설치되지 않은 Exchange 2013과 Exchange 2010 SP3(서비스 팩 3) 클라이언트 액세스 서버 간의 프록시 요청이 정상적으로 작동하지 않고 오류가 표시되는 경우가 있습니다. 이러한 상황은 다음 모든 조건에 해당하는 경우 발생할 수 있습니다.
    
      - Exchange 2013 사서함을 소유한 사용자가 다음 방법 중 하나를 사용하여 Exchange 2010 사서함을 열려고 시도하는 경우
        
          - Outlook Web App의 **다른 사서함 열기** 옵션 **또는**
        
          - Exchange 관리 센터의 **다른 사용자** 옵션
    
      - 사용자가 연결한 클라이언트 액세스 서버에서 Exchange 2013을 실행 중인 경우
    
      - Exchange 2010 클라이언트 액세스 서버가 Exchange 2010 RTM(Release To Manufacturing) 버전 또는 이전 Exchange 2010 서비스 팩에서 Exchange 2010 SP3으로 업그레이드된 경우
    
    위의 모든 조건에 해당하는 경우에는 다른 사용자의 Exchange 2010Outlook Web App 옵션에 액세스할 수 없으며 빈 페이지가 표시될 수 있습니다.
    
    이 문제를 해결하려면 각 Exchange 2010 서버에 Exchange 2010 SP3 업데이트 롤업 1 이상을 설치합니다.

