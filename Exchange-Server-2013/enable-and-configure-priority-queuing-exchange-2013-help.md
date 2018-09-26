---
title: '사용 하도록 설정 하 고 우선순위 큐 구성: Exchange 2013 Help'
TOCTitle: 사용 하도록 설정 하 고 우선순위 큐 구성
ms:assetid: 1975d85d-2f1d-4852-8d19-e74ba4ba3853
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ891104(v=EXCHG.150)
ms:contentKeyID: 51407673
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하도록 설정 하 고 우선순위 큐 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-12-16_

*우선 순위 큐*는 Microsoft Outlook 또는 Outlook Web Access에서 보낸 사람이 구성하는 메시지 우선 순위가 사서함 서버의 전송 서비스에 의한 메시지 처리에 적용되도록 설정하는 Microsoft Exchange Server 2013의 기능입니다. 우선 순위 큐를 사용하도록 설정한 경우 높은 우선 순위 메시지는 보통 우선 순위 메시지 전에 전송되며 보통 우선 순위 메시지는 낮은 우선 순위 메시지 전에 전송됩니다. 자세한 내용은 [우선순위 큐](priority-queuing-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이 항목의 절차에는 Exchange 권한이 적용되지 않습니다. 이 절차는 Exchange Server의 운영 체제에서 수행됩니다.

  - EdgeTransport.exe.config 응용 프로그램 구성 파일에 저장하는 변경 내용은 Microsoft Exchange Transport Service를 다시 시작하고 나면 적용됩니다.

  - Microsoft Exchange Transport Service를 다시 시작하면 서버의 메일 흐름이 일시적으로 중지됩니다.

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]  
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 명령 프롬프트를 사용하여 EdgeTransport.exe.config 파일에서 우선 순위 큐 사용 설정 및 구성

1.  명령 프롬프트 창에서 다음 명령을 실행하여 EdgeTransport.exe.config 응용 프로그램 구성 파일을 메모장에서 엽니다.
    
    ```powershell
    Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

2.  `<appSettings>` 섹션의 다음 키를 찾습니다.
    
    ```command line
        <add key="PriorityQueuingEnabled" value="false" />
        <add key="MaxPerDomainHighPriorityConnections" value="3" />
        <add key="MaxPerDomainNormalPriorityConnections" value="15" />
        <add key="MaxPerDomainLowPriorityConnections" value="2" />
        <add key="HighPriorityMessageExpirationTimeout" value="8:00:00" />
        <add key="NormalPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="LowPriorityMessageExpirationTimeout" value="2.00:00:00" />
        <add key="HighPriorityDelayNotificationTimeout" value="00:30:00" />
        <add key="NormalPriorityDelayNotificationTimeout" value="4:00:00" />
        <add key="LowPriorityDelayNotificationTimeout" value="8:00:00" />
        <add key="MaxHighPriorityMessageSize" value="250KB" />
    ```    
    사서함 서버의 전송 서비스에서 우선 순위 큐를 사용하도록 설정하려면 다음 값을 사용합니다.
    
    ```command line
    <add key="PriorityQueuingEnabled" value="true" />
    ```
    
    나머지 우선 순위 큐 값을 구성하거나 기본값으로 유지합니다.

3.  작업을 마친 후 저장하고 EdgeTransport.exe.config 파일을 닫습니다.

4.  다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작합니다.
    
    ```powershell
        net stop MSExchangeTransport && net start MSExchangeTransport
    ```

## 작동 여부는 어떻게 확인합니까?

우선 순위 큐가 사용하도록 설정되었으며 구성되었는지 확인하려면 다음을 수행합니다.

1.  EdgeTransport.exe.config 파일의 **PriorityQueueinEnabled** 키 값이 `"true"`인지 확인합니다.

2.  Outlook을 사용하여 **MaxHighPriorityMessageSize** 키로 지정된 값보다 큰 높은 우선 순위의 테스트 메시지를 만든 다음 해당 메시지가 보통 우선 순위 메시지로 도착하는지 확인합니다.

3.  동일한 받는 사람이나 대상으로 보낸 우선 순위가 높은 메시지가 우선 순위가 낮은 메시지보다 먼저 도착하는지 확인합니다. 여러 사서함을 사용하여 우선 순위 값이 서로 다른 유사 테스트 메시지를 동일한 받는 사람에게 동시에 여러 개 보낼 수 있습니다.

