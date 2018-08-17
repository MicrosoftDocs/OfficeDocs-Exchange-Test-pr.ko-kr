---
title: 'Get-QueueDigest 구성: Exchange 2013 Help'
TOCTitle: Get-QueueDigest 구성
ms:assetid: f730c520-4ba5-4a15-8846-132bff500bb8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dn505733(v=EXCHG.150)
ms:contentKeyID: 59635552
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Get-QueueDigest 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-12-16_

**Get-QueueDigest** cmdlet을 사용하면 한 가지 명령을 사용하여 Exchange 조직의 큐 정보를 일부 또는 전부 볼 수 있습니다.

기본적으로 **Get-QueueDigest** cmdlet에서 반환된 결과는 1~2분 후에 나타납니다. 이러한 값은 다음과 같은 설정에 따라 제어됩니다.

  - **EdgeTransport.exe.config의 QueueLoggingInterval 키**   이 키는 큐 데이터가 기록되는 빈도와 **Get-QueueDigest**에서의 사용 가능성을 지정합니다. 기본값은 `00:01:00`(1분)입니다. 값을 지정하려면 이 값을 기간으로, 즉 *hh:mm:ss*와 같이 입력합니다. 여기서 *h* = 시간, *m* = 분, *s* = 초를 나타냅니다. 기본적으로 이 키는 EdgeTransport.exe.config 파일에 없습니다.

  - **Set-TransportConfig의 QueueDiagnosticsAggregationInterval 매개 변수**   이 매개 변수는 큐 데이터가 사서함 서버 간에 공유되는 빈도를 지정합니다. 기본값은 `00:01:00`(1분)입니다. 값을 지정하려면 이 값을 기간으로, 즉 *hh:mm:ss*와 같이 입력합니다. 여기서 *h* = 시간, *m* = 분, *s* = 초를 나타냅니다.

**QueueLoggingInterval** 키 및 *QueueDiagnosticsAggregationInterval* 매개 변수 값의 합은 **Get-QueueDigest**에서 반환된 결과의 최대 보존 기간을 결정합니다.

또한 **Get-QueueDigest**는 큐의 유형 및 상태에 따라 결과를 다르게 반환합니다. 예를 들어 다음 큐가 메시지를 하나 이상 포함하면 결과에 표시됩니다.

  - 전송 큐, 연결할 수 없는 큐 및 포이즌 메시지 큐(영구 큐)

  - Suspended 상태에 있는 배달 큐(관리자가 수동으로 일시 중단한 큐)

기본적으로 상태가 Active, Connecting, Ready 또는 Retry인 배달 큐는 해당 큐에 메시지가 10개 이상 포함된 경우에만 결과에서 반환됩니다. 이 값은 EdgeTransport.exe.config 파일의 **QueueLoggingThreshold** 키로 제어됩니다. 더 적거나 큰 정수 값을 지정할 수 있습니다. 기본적으로 이 키는 EdgeTransport.exe.config 파일에 없습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 필요한 Exchange 권한을 보려면 Exchange 관리 셸의 **Set-TransportConfig**를 실행하여 [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)에 항목에 있는 "전송 구성" 항목을 참조하세요.

  - Exchange 권한은 EdgeTransport.exe.config 파일을 수정하고 Microsoft Exchange Transport Service를 다시 시작하는 데 적용하지 않습니다. 이 절차는 Exchange Server의 운영 체제에서 수행됩니다.

  - EdgeTransport.exe.config 파일에 저장하는 변경 내용은 Microsoft Exchange Transport Service를 다시 시작하고 나면 적용됩니다. 이 서비스를 다시 시작하면 서버의 메일 흐름이 일시적으로 중단됩니다.

  - Exchange XML 응용 프로그램 구성 파일(예: 클라이언트 액세스 서버의 web.config 파일 또는 사서함 서버의 EdgeTransport.exe.config 파일)에 설정하는 사용자 지정된 모든 서버 단위 설정은 Exchange CU(누적 업데이트)를 설치하면 덮어쓰게 됩니다. 설치 후 서버를 쉽게 다시 구성할 수 있도록 이 정보를 저장했는지 확인하세요. 이러한 설정은 Exchange CU를 설치한 후에 다시 구성해야 합니다.

  - **Set-TransportConfig**를 사용하여 내용을 변경하면 조직에 있는 모든 사서함 서버에 영향을 줍니다. EdgeTransport.exe.config 파일에서 내용을 변경하면 로컬 사서함 서버에만 영향을 줍니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## Get-QueueDigest 구성

1.  명령 프롬프트 창에서 다음 명령을 실행하여 EdgeTransport.exe.config 파일을 메모장에서 엽니다.
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  `<appSettings>` 섹션에서 다음 키 중 한 개 또는 두 개 모두 추가합니다.
    
        <add key="QueueLoggingThreshold" value="<integer>" />
        <add key="QueueLoggingInterval" value="<hh:mm:ss>" />
    
    예를 들어 **QueueLoggingThreshold** 값을 1로 설정하고 **QueueLoggingInterval** 값을 30초로 설정하려면 다음 값을 사용합니다.
    
        <add key="QueueLoggingThreshold" value="1" />
        <add key="QueueLoggingInterval" value="00:00:30" />

3.  작업이 완료되면 저장하고 EdgeTransport.exe.config 파일을 닫습니다.

4.  다음 명령을 실행하여 Microsoft Exchange Transport Service를 다시 시작합니다.
    
        net stop MSExchangeTransport && net start MSExchangeTransport

5.  Exchange 관리 셸에서 *QueueDiagnosticsAggregationInterval* 매개 변수의 값을 변경하려면 다음 구문을 사용합니다.
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval <hh:mm:ss>
    
    예를 들어 값을 30초로 설정하려면 다음 명령을 실행합니다.
    
        Set-TransportConfig -QueueDiagnosticsAggregationInterval 00:00:30

## 작동 여부를 확인하는 방법

**Get-QueueDigest**가 구성되었는지 확인하려면 다음을 수행합니다.

1.  EdgeTransport.exe.config 파일에서 **QueueLoggingThreshold** 값과 **QueueLoggingInterval** 키를 확인합니다. 키가 없는 경우 기본값이 사용됩니다.

2.  다음 명령을 실행하여 *QueueDiagnosticsAggregationInterval* 매개 변수의 값을 확인합니다.
    
        Get-TransportConfig | Format-List *queue*

