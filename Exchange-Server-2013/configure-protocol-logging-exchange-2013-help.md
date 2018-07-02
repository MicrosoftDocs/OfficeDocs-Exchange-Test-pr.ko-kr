---
title: '프로토콜 로깅 구성: Exchange 2013 Help'
TOCTitle: 프로토콜 로깅 구성
ms:assetid: c81cac9c-b990-492a-b899-5be8d08a6068
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124531(v=EXCHG.150)
ms:contentKeyID: 50484147
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 프로토콜 로깅 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-03-15_

프로토콜 로깅은 메시지 배달의 일부로 송신 커넥터와 수신 커넥터에서 발생하는 SMTP 대화를 기록합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 서비스", "프런트 엔드 전송 서비스", "사서함 전송 서비스", "수신 커넥터" 및 "송신 커넥터" 항목

  - EAC(Exchange 관리 센터)를 사용하여 사서함 서버의 전송 서비스에서 송신 커넥터와 수신 커넥터에 대해, 그리고 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에서 수신 커넥터에 대해 프로토콜 로깅을 사용하거나 사용하지 않도록 설정할 수 있습니다. 또한 EAC를 사용하여 전송 서비스에 대한 프로토콜 로그 경로를 구성할 수도 있습니다. 다른 모든 프로토콜 로깅 옵션에 대해서는 셸을 사용해야 합니다.

  - 프로토콜 로깅은 커넥터에 따라 활성화 또는 비활성화됩니다. Exchange 서버의 모든 수신 커넥터는 동일한 프로토콜 로그 파일과 프로토콜 로그 옵션을 공유합니다. 이러한 프로토콜 로그 설정은 동일한 서버에 있는 송신 커넥터 로그 파일 및 프로토콜 로그 옵션과는 별개입니다.

  - UNRESOLVED\_TOKENBLOCK\_VAL(ALERT\_Do 수행 하지이 구독 된에 지 서버)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 프로토콜 로깅 구성

EAC를 사용하여 사서함 서버의 전송 서비스에 있는 송신 커넥터 또는 수신 커넥터에서, 또는 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 있는 수신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정하려면 다음을 수행합니다.

1.  EAC에서 **메일 흐름** \> **송신 커넥터** 또는 **메일 흐름** \> **수신 커넥터**로 이동합니다.

2.  구성할 커넥터를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **일반** 탭의 **프로토콜 로깅 수준** 섹션에서 다음 옵션 중 하나를 선택합니다.
    
      - **없음**   커넥터에서 프로토콜 로깅을 사용하지 않습니다.
    
      - **자세한 정보**   커넥터에서 프로토콜 로깅을 사용합니다.
    
    작업을 마치면 **저장**를 클릭합니다.

EAC를 사용하여 사서함 서버의 전송 서비스에서 송신 커넥터 및 수신 커넥터에 대한 프로토콜 로그 경로를 구성하려면 다음을 수행합니다.

1.  EAC에서 **서버** \> **서버**로 이동합니다.

2.  구성하려는 사서함 서버를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **전송 로그**를 클릭합니다.

4.  **프로토콜 로그** 섹션에서 다음 설정을 변경합니다.
    
      - **송신 프로토콜 로그 경로**   지정하는 값은 로컬 Exchange 서버에 있어야 합니다. 해당 폴더가 없는 경우 **저장**을 클릭하면 만들어집니다.
    
      - **수신 프로토콜 로그 경로**   지정하는 값은 로컬 Exchange 서버에 있어야 합니다. 해당 폴더가 없는 경우 **저장**을 클릭하면 만들어집니다.
    
    작업을 마치면 **저장**를 클릭합니다.

## 작동 여부는 어떻게 확인합니까?

EAC를 사용해 프로토콜 로그 설정이 구성되었는지 확인하려면 다음 중 하나를 수행합니다.

1.  송신 커넥터 또는 수신 커넥터 프로토콜 로그에 대해 지정한 위치로 이동합니다.

2.  프로토콜 로깅을 사용하도록 설정했으면 로그 파일이 만들어졌는지 확인합니다. 프로토콜 로깅을 사용하지 않도록 설정했으면 최신 로그 파일이 업데이트되지 않았음을 확인합니다.

## 셸을 사용하여 송신 커넥터 또는 수신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정

송신 커넥터 또는 수신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

    <Set-SendConnector |Set-ReceiveConnector> <ConnectorIdentity> -ProtocolLoggingLevel <Verbose | None>

이 예에서는 Contoso.com에서 Connection이라는 수신 커넥터에 대해 프로토콜 로깅을 사용하도록 설정합니다.

    Set-ReceiveConnector "Connection from Contoso.com" -ProtocolLoggingLevel Verbose

## 작동 여부는 어떻게 확인합니까?

프로토콜 로깅이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        <Get-SendConnector |Get-ReceiveConnector> | Format-List Name,ProtocolLoggingLevel

2.  표시된 값이 구성한 값인지 확인합니다.

## 셸을 사용하여 조직 내 송신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정

사서함 서버의 전송 서비스 및 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 있는 보이지 않는 암시적 조직 내 송신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

    <Set-TransportService | Set-FrontEndTransportService> -IntraOrgConnectorProtocolLoggingLevel <Verbose | None>

이 예에서는 Mailbox01이라는 사서함 서버의 전송 서비스에 있는 조직 내 송신 커넥터에서 프로토콜 로깅을 사용하도록 설정합니다.

    Set-TransportService Mailbox01 -IntraOrgConnectorProtocolLoggingLevel Verbose

## 작동 여부는 어떻게 확인합니까?

조직 내 송신 커넥터에서 프로토콜 로깅이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        <Get-TransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List IntraOrgConnectorProtocolLoggingLevel

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 사서함 배달 송신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정

사서함 서버의 사서함 전송 서비스에 있는 보이지 않는 암시적 사서함 배달 송신 커넥터에서 프로토콜 로깅을 사용하거나 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

    Set-MailboxTransportService -MailboxDeliveryConnectorProtocolLoggingLevel <Verbose | None>

이 예에서는 Mailbox01이라는 사서함 서버의 사서함 전송 서비스에 있는 사서함 배달 수신 커넥터에서 프로토콜 로깅을 사용하도록 설정합니다.

    Set-MailboxTransportService Mailbox01 -MailboxDeliveryConnectorProtocolLoggingLevel Verbose

## 작동 여부는 어떻게 확인합니까?

사서함 배달 커넥터에서 프로토콜 로깅이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-MailboxTransportService <ServerIdentity> | Format-List MailboxDeliveryConnectorProtocolLoggingLevel

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 프로토콜 로깅 설정 구성

프로토콜 로그 설정을 구성하려면 다음 명령을 실행합니다.

    <Set-TransportService | Set-MailboxTransportService | Set-FrontEndTransportService> <ServerIdentity> -ReceiveProtocolLogPath <LocalFilePath> -SendProtocolLogPath <LocalFilePath> -ReceiveProtocolLogMaxFileSize <Size> -SendProtocolLogMaxFileSize <Size> -ReceiveProtocolLogMaxDirectorySize <Size> -SendProtocolLogMaxDirectorySize <Size> -ReceiveProtocolLogMaxAge <dd.hh:mm:ss> -SendProtocolLogMaxAge <dd.hh:mm:ss>

이 예에서는 Mailbox01이라는 사서함 서버의 전송 서비스에서 다음 프로토콜 로그 설정을 설정합니다.

  -  
    모든 수신 커넥터 프로토콜 로그의 위치를 D:\\Hub Receive SMTP Log로 설정하고 모든 송신 커넥터 프로토콜 로그의 위치를 D:\\Hub Send SMTP Log로 설정합니다. 해당 폴더가 없는 경우 새로 만들어집니다.

  -  
    수신 커넥터 프로토콜 로그 파일 및 송신 커넥터 프로토콜 로그 파일의 최대 크기를 20MB로 설정합니다.

  -  
    수신 커넥터 프로토콜 로그 폴더 및 송신 커넥터 프로토콜 로그 폴더의 최대 크기를 400MB로 설정합니다.

  -  
    수신 커넥터 프로토콜 로그 파일 및 송신 커넥터 프로토콜 로그 파일의 최대 기간을 45일로 설정합니다.

<!-- end list -->

    Set-TransportService Mailbox01 -ReceiveProtocolLogPath "D:\Hub Receive SMTP Log" -SendProtocolLogPath "D:\Hub Send SMTP Log" -ReceiveProtocolLogMaxFileSize 20MB -SendProtocolLogMaxFileSize 20MB -ReceiveProtocolLogMaxDirectorySize 400MB -SendProtocolLogMaxDirectorySize 400MB -ReceiveProtocolLogMaxAge 45.00:00:00 -SendProtocolLogMaxAge 45.00:00:00


> [!NOTE]
> <UL>
> <LI>
> <P>사서함 서버의 사서함 전송 서비스에 프로토콜 로그 설정을 구성하려면 <STRONG>Set-MailboxTransportService</STRONG> cmdlet을 사용합니다. 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 프로토콜 로그 설정을 구성하려면 <STRONG>Set-FrontEndTransportService</STRONG> cmdlet을 사용합니다.</P>
> <LI>
> <P><EM>SendProtocolLogPath</EM> 또는 <EM>ReceiveProtocolLogPath</EM> 매개 변수의 값을 <CODE>$null</CODE>로 설정하면 서버의 모든 송신 커넥터 또는 모든 수신 커넥터의 프로토콜 로깅이 사용하지 않도록 설정됩니다. 그러나 조직 내 송신 커넥터 또는 사서함 배달 송신 커넥터를 비롯하여 해당 서버의 다른 커넥터에 대해 프로토콜 로깅을 사용하도록 설정한 경우 이러한 매개 변수를 <CODE>$null</CODE>로 설정하면 이벤트 로그 오류가 생성됩니다.</P>
> <LI>
> <P><EM>ReceiveProtocolLogMaxAge</EM> 또는 <EM>SendProtocolLogMaxAge</EM> 매개 변수의 값을 <CODE>00:00:00</CODE>으로 설정하면 기간 만료로 인해 프로토콜 로그 파일이 자동으로 제거되는 것을 방지할 수 있습니다.</P></LI></UL>



## 작동 여부는 어떻게 확인합니까?

프로토콜 로그 설정이 구성되었는지 확인하려면 다음을 수행합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        <Get-TransportService | Get-MailboxTransportService | Get-FrontEndTransportService> <ServerIdentity> | Format-List SendConnectorProtocolLog*,ReceiveConnectorProtocolLog*

2.  표시된 값이 구성한 값인지 확인합니다.

