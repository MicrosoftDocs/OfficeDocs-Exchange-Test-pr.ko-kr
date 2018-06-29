---
title: '메시지 다시 시도, 다시 전송, 및 만료 간격 구성: Exchange 2013 Help'
TOCTitle: 메시지 다시 시도, 다시 전송, 및 만료 간격 구성
ms:assetid: 5420124f-aa4c-4702-b493-40a9a7edb786
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998043(v=EXCHG.150)
ms:contentKeyID: 51407697
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시지 다시 시도, 다시 전송, 및 만료 간격 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-12-16_

Microsoft Exchange Server 2013에서는 사서함 서버 및 Edge 전송 서버의 전송 서비스에서 메시지 다시 시도, 다시 전송 및 만료 간격을 구성할 수 있습니다. 이 설정에 대한 자세한 내용은 [메시지 다시 시도, 다시 전송, 및 만료 간격](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 서비스" 및 "Edge 전송 서버" 항목

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EdgeTransport.exe.config를 사용하여 큐 결함 시 다시 시도 횟수, 큐 결함 시 다시 시도 간격, 사서함 배달 큐 다시 시도 간격 및 다시 전송 간격 전 최대 유휴 시간 구성

큐 결함 시 다시 시도 횟수, 큐 결함 시 다시 시도 간격, 사서함 배달 큐 다시 시도 간격 및 다시 전송 간격 전 최대 유휴 시간을 구성하려면 사서함 서버나 Edge 전송 서버에서 %ExchangeInstallPath%Bin\\EdgeTransport.exe.config XML 응용 프로그램 구성 파일의 키를 수정합니다. 이 파일에 저장하는 변경 내용은 Microsoft Exchange Transport Service를 다시 시작하고 나면 적용됩니다. 이 서비스를 다시 시작하면 서버의 메일 흐름이 일시적으로 중지됩니다.

1.  사서함 서버나 Edge 전송 서버의 명령 프롬프트 창에서 다음 명령을 실행하여 메모장에서 EdgeTransport.exe.config 파일을 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  `<appSettings>` 섹션에서 다음 키를 찾습니다.
    
        <add key="QueueGlitchRetryCount" value="<Integer>" />
        <add key="QueueGlitchRetryInterval" value="<hh:mm:ss>" />
        <add key="MailboxDeliveryQueueRetryInterval" value="<hh:mm:ss>" />
        <add key="MaxIdleTimeBeforeResubmit" value="<hh:mm:ss>" />
    
    이 예에서는 큐 결함 시 다시 시도 횟수를 6으로 바꾸고, 큐 결함 시 다시 시도 간격을 30초로 바꾸며, 사서함 배달 큐 다시 시도 간격을 3분으로 바꾸고 다시 전송 간격 전 최대 유휴 시간을 6시간으로 바꿉니다.
    
        <add key="QueueGlitchRetryCount" value="6" />
        <add key="QueueGlitchRetryInterval" value="00:00:30" />
        <add key="MailboxDeliveryQueueRetryInterval" value="00:03:00" />
        <add key="MaxIdleTimeBeforeResubmit" value="6:00:00" />

3.  작업을 마친 후 저장하고 EdgeTransport.exe.config 파일을 닫습니다.

4.  다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작합니다.
    
        net stop MSExchangeTransport && net start MSExchangeTransport

## 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격 구성

일시적 실패 시 다시 시도 횟수는 `QueueGlitchRetryCount` 및 `QueueGlitchRetryInterval` 키에 의해 제어되는 연결 시도가 실패한 후 시도되는 연결 시도 횟수를 지정합니다. 일시적 실패 시 다시 시도 기본 횟수는 6회입니다. 이 매개 변수의 유효한 입력 범위는 0~15입니다. 일시적 실패 시 다시 시도 횟수를 0으로 설정한 경우 다음 연결 시도는 *아웃바운드 연결 실패 시 다시 시도 간격*에 의해 제어됩니다.

일시적 실패 시 다시 시도 간격은 일시적 실패 시 다시 시도 횟수에 의해 지정된 각 연결 간의 시도 간격을 지정합니다. 사서함 서버의 전송 서비스에서 일시적 실패 시 다시 시도 기본 간격은 5분입니다. Edge 전송 서버에서 일시적 실패 시 다시 시도 기본 간격은 10분입니다.

아웃바운드 연결 실패 시 다시 시도 간격은 이전에 실패한 보내는 연결 시도에 대한 다시 시도 간격을 지정합니다. 이전에 실패한 연결 시도는 일시적 실패 시 다시 시도 횟수 및 일시적 실패 시 다시 시도 간격에 의해 제어됩니다. 사서함 전송 서버의 전송 서비스에서 아웃바운드 연결 실패 시 다시 시도 간격 기본값은 10분입니다. Edge 전송 서버의 기본값은 30분입니다.

## EAC를 사용하여 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 또는 아웃바운드 연결 실패 시 다시 시도 간격 구성

1.  EAC(Exchange 관리 센터)에서 **서버** \> **서버**를 클릭하고 서버를 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하고 **전송 제한**을 클릭합니다.

2.  **다시 시도** 섹션에서 **아웃바운드 연결 실패 시 다시 시도 간격(초)**, **일시적 실패 시 다시 시도 간격(분)** 또는 **일시적 실패 시 다시 시도 횟수**에 대해 값을 입력합니다.

3.  작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격 구성

다음 구문을 사용하여 사서함 서버나 Edge 전송 서버의 전송 서비스에서 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격을 구성할 수 있습니다.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

이 예에서는 Exchange01이라는 Edge 전송 서버나 Mailbox01이라는 사서함 서버에서 다음 값을 바꿉니다.

  - 일시적 실패 시 다시 시도 횟수가 8회로 설정됩니다.

  - 일시적 실패 시 다시 시도 간격이 1분으로 설정됩니다.

  - 아웃바운드 연결 실패 시 다시 시도 간격이 45분으로 설정됩니다.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 대해 <STRONG>Set-FrontEndTransportService</STRONG> cmdlet에서 <EM>TransientFailureRetryCount</EM> 및 <EM>TransientFailureRetryInterval</EM> 매개 변수도 사용할 수 있습니다.



## 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격 구성

## EAC를 사용하여 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격 구성

1.  EAC에서 **서버** \> **서버**를 클릭하고 서버를 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하고 **전송 제한**을 클릭합니다.

2.  **다시 시도** 섹션에서 **아웃바운드 연결 실패 시 다시 시도 간격(초)**, **일시적 실패 시 다시 시도 간격(분)** 또는 **일시적 실패 시 다시 시도 횟수**에 대해 값을 입력합니다.

3.  작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격 구성

다음 구문을 사용하여 사서함 서버나 Edge 전송 서버의 전송 서비스에서 일시적 실패 시 다시 시도 횟수, 일시적 실패 시 다시 시도 간격 및 아웃바운드 연결 실패 시 다시 시도 간격을 구성할 수 있습니다.

    Set-TransportService <ServerIdentity> -TransientFailureRetryCount <Integer> -TransientFailureRetryInterval <hh:mm:ss> -OutboundConnectionFailureRetryInterval <dd.hh:mm:ss>

이 예에서는 Exchange01이라는 Edge 전송 서버나 Mailbox01이라는 사서함 서버에서 다음 값을 바꿉니다.

  - 일시적 실패 시 다시 시도 횟수가 8회로 설정됩니다.

  - 일시적 실패 시 다시 시도 간격이 1분으로 설정됩니다.

  - 아웃바운드 연결 실패 시 다시 시도 간격이 45분으로 설정됩니다.

<!-- end list -->

    Set-TransportService Mailbox01 -TransientFailureRetryCount 8 -TransientFailureRetryInterval 00:01:00 -OutboundConnectionFailureRetryInterval 00:45:00


> [!NOTE]
> 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 대해 <STRONG>Set-FrontEndTransportService</STRONG> cmdlet에서 <EM>TransientFailureRetryCount</EM> 및 <EM>TransientFailureRetryInterval</EM> 매개 변수도 사용할 수 있습니다.



## 셸을 사용하여 메시지 다시 시도 간격 구성

기본적으로 메시지 다시 시도 간격은 `00:15:00` (15 분)입니다. Microsoft 고객 서비스 및 지원 하도록 권장할 경우이 작업을 수행 하지 않으면 기본 값을 수정 하지 않는 것이 좋습니다.

다음 구문을 사용하여 메시지 다시 시도 간격을 설정할 수 있습니다.

    Set-TransportService <ServerIdentity> -MessageRetryInterval <dd.hh:mm:ss>

이 예에서는 mailbox01 사서함 서버의 20 분으로 메시지 다시 시도 간격을 변경 합니다.

    Set-TransportService Mailbox01 -MessageRetryInterval 00:20:00

## 지연 DSN 시간 제한 설정 구성

EAC 또는 셸을 사용하여 지연 DSN 알림 시간 제한 간격을 구성할 수 있습니다. 이 설정은 로컬 전송 서버에만 적용됩니다. 내부 보낸 사람 및 외부 보낸 사람에게 지연 DSN 메시지 보내기를 사용하거나 사용하지 않도록 설정하는 작업은 셸을 통해서만 가능합니다. 이 설정은 조직의 모든 전송 서버에 적용됩니다.


> [!NOTE]
> Exchange 2007 허브 전송 서버에서 모든 <EM>ExternalDSN*</EM> 및 <EM>InternalDSN*</EM> 매개 변수는 <STRONG>Set-TransportServer</STRONG> cmdlet에서 사용할 수 있습니다(<STRONG>Set-TransportConfig</STRONG> cmdlet에서는 사용할 수 없음). 조직에 Exchange 2007 허브 전송 서버가 있는 경우 각 Exchange 2007 허브 전송 서버에서 <STRONG>Set-TransportServer</STRONG> cmdlet을 사용하여 이 값을 변경해야 합니다.



## EAC를 사용하여 지연 DSN 메시지 알림 시간 제한 간격 구성

1.  EAC에서 **서버** \> **서버**를 클릭하고 서버를 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하고 **전송 제한**을 클릭합니다.

2.  **알림** 섹션에서 **다음 시간을 초과하여 메시지가 지연되면 보낸 사람에게 알림**에 대해 값을 입력합니다.

3.  작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 지연 DSN 메시지 알림 시간 제한 간격 구성

다음 구문을 사용하여 메시지 다시 시도 간격을 설정할 수 있습니다.

    Set-TransportService <ServerIdentity> -DelayNotificationTimeout <dd.hh:mm:ss>

이 예에서는 Mailbox01이라는 사서함 서버에서 지연 DSN 메시지 알림 시간 제한 간격을 6시간으로 바꿉니다.

    Set-TransportService Mailbox01 -DelayNotificationTimeout 06:00:00

## 셸을 사용하여 외부 또는 내부 메시지 보낸 사람에게 지연 DSN 알림 보내기를 사용하거나 사용하지 않도록 설정

다음 구문을 사용하여 지연 DSN 알림 설정을 구성할 수 있습니다.

    Set-TransportConfig -ExternalDelayDSNEnabled <$true | $false> -InternalDelayDSNEnabled <$true |$false>

이 예에서는 외부 보낸 사람에게 지연 DSN 알림 메시지를 보내지 않도록 차단합니다.

    Set-TransportConfig -ExternalDelayDSNEnabled $false

이 예에서는 내부 보낸 사람에게 지연 DSN 알림 메시지를 보내지 않도록 차단합니다.

    Set-TransportConfig -InternalDelayDSNEnabled $false

## 메시지 만료 시간 제한 간격 구성

## EAC를 사용하여 메시지 만료 시간 제한 간격 구성

1.  EAC에서 **서버** \> **서버**를 클릭하고 서버를 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하고 **전송 제한**을 클릭합니다.

2.  **메시지 만료** 섹션에서 **전송 이후의 최대 시간(일)**에 대해 값을 입력합니다.

3.  작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 메시지 만료 시간 제한 간격 구성

메시지 만료 시간 제한 간격을 구성하려면 다음 구문을 사용합니다.

    Set-TransportService <ServerIdentity> -MessageExpirationTimeout <dd.hh:mm:ss>

이 예에서는 Mailbox01이라는 Exchange 서버에서 메시지 만료 시간 제한 간격을 4일로 바꿉니다.

    Set-TransportService Mailbox01 -MessageExpirationTimeout 4.00:00:00

