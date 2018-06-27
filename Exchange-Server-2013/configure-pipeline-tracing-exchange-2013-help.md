---
title: '파이프라인 추적 구성: Exchange 2013 Help'
TOCTitle: 파이프라인 추적 구성
ms:assetid: 10293c83-2157-474e-840d-942e064a4672
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ916678(v=EXCHG.150)
ms:contentKeyID: 52058053
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 파이프라인 추적 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

파이프라인 추적에서는 사서함 서버와 Edge 전송 서버의 전송 서비스 또는 사서함 전송 서비스에서 전송 파이프라인을 통과하는 전자 메일 메시지의 복사본을 캡처합니다.

## 시작하기 전에 알아야 할 내용

  - 이 절차의 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 서비스" 및 "사서함 전송 서비스" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 파이프라인 추적은 보낸 사람의 전자 메일 주소에서 보낸 전자 메일 메시지의 전체 콘텐츠를 복사합니다. 기밀 정보가 노출되지 않도록 하려면 파이프라인 추적 폴더의 위치에 대해 적절한 보안 권한을 설정해야 합니다.

  - 파이프라인 추적을 장시간 사용하도록 설정하지 마십시오. 파이프라인 추적을 사용하면 다수의 메시지 스냅숏 파일이 만들어져 빠르게 누적되므로, 파이프라인 추적을 사용하는 경우에는 사용 가능한 디스크 공간을 항상 모니터링하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 파이프라인 추적 사용 및 구성

## 1단계: 셸을 사용하여 파이프라인 추적 보낸 사람 주소 구성

다음 구문을 사용하여 파이프라인 추적 보낸 사람 주소를 구성합니다.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingSenderAddress <SMTPAddress | "<>">

이 예에서는 Mailbox01 사서함 서버의 전송 서비스에서 보낸 사람 chris@contoso.com이 보낸 모든 메시지의 스냅숏을 캡처하도록 파이프라인 추적을 구성합니다.

    Set-TransportService Mailbox01 -PipelineTracingSenderAddress chris@contoso.com

이 예에서는 Mailbox02 사서함 서버의 전송 서비스에서 수신하는 모든 시스템 생성 메시지의 스냅숏을 캡처하도록 파이프라인 추적을 구성합니다.

    Set-TransportService Mailbox02 -PipelineTracingSenderAddress "<>"


> [!WARNING]
> 전송 서비스에서 모든 서버 생성 메시지를 캡처하도록 파이프라인 추적을 구성하면 서버에 대한 부하가 매우 높아지고 사용 가능한 디스크 공간이 빠르게 소모될 수 있습니다. 파이프라인 추적을 사용하는 경우에는 사용 가능한 디스크 공간을 항상 모니터링하십시오.



## 2단계: (옵션) 셸을 사용하여 사용자 지정 파이프라인 추적 폴더 지정

기본 파이프라인 추적 폴더는 파이프라인 추적을 사용하도록 설정해야 만들어지며, *PipelineTracingSenderAddress* 매개 변수를 사용하여 지정하는 조건을 충족하는 메시지는 서버에서 전송 서비스를 통과합니다. 사서함 서버에서 전송 서비스의 기본 위치는 `%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing`입니다. 사서함 서버에서 사서함 전송 서비스의 기본 위치는 `%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing`입니다. 사용자 지정 경로를 지정하는 경우 로컬 Exchange 서버의 경로를 사용해야 합니다.

다음 구문을 사용하여 파이프라인 추적 폴더를 구성합니다.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingPath <LocalFilePath>

다음 예에서는 Mailbox01 사서함 서버의 전송 서비스에 대해 파이프라인 추적 폴더를 D:\\Hub\\Pipeline Tracing으로 설정합니다.

    Set-TransportService Mailbox01 -PipelineTracingPath "D:\Hub\Pipeline Tracing"

## 3단계: 셸을 사용하여 파이프라인 추적을 사용하도록 설정

모든 Exchange 서버에서는 기본적으로 파이프라인 추적이 사용하지 않도록 설정되어 있습니다. 파이프라인 추적을 사용하도록 설정하면 지정된 Exchange 서버의 지정된 전송 서비스에서만 파이프라인 추적을 사용할 수 있습니다. 파이프라인 추적을 사용하도록 설정하기 전에 1단계에서 설명한 대로 보낸 사람 주소를 지정해야 합니다.

다음 구문을 사용하여 파이프라인 추적을 사용하도록 설정합니다.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $true

이 예에서는 Mailbox01 사서함 서버의 전송 서비스에서 파이프라인 추적을 사용하도록 설정합니다.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $true

## 작동 여부는 어떻게 확인합니까?

파이프라인 추적이 구성되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracing*

2.  표시된 값이 구성한 값인지 확인합니다.

3.  전송 서비스 또는 사서함 전송 서비스의 파이프라인 추적 폴더를 점검하여 해당 폴더에 메시지 스냅숏 파일이 만들어지고 있는지 확인합니다.

## 파이프라인 추적을 사용하지 않도록 설정

파이프라인 추적은 사용 시 디스크 공간 및 보안 관련 문제가 발생할 수 있으므로 진단 또는 문제 해결을 위한 일시적인 작업으로만 사용됩니다. 파이프라인 추적을 사용하도록 설정하는 경우에는 항상 작업을 마치고 나서 추적을 사용하지 않도록 설정해야 합니다.

다음 구문을 사용하여 파이프라인 추적을 사용하지 않도록 설정합니다.

    <Set-TransportService | Set-MailboxTransportService> <ServerIdentity> -PipelineTracingEnabled $false

이 예에서는 Mailbox01 사서함 서버의 전송 서비스에서 파이프라인 추적을 사용하지 않도록 설정합니다.

    Set-TransportService Mailbox01 -PipelineTracingEnabled $false

## 작동 여부는 어떻게 확인합니까?

파이프라인 추적이 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        <Get-TransportService | Get-MailboxTransportService> <ServerIdentity> | Format-List PipelineTracingEnabled

2.  *PipelineTracingEnabled* 매개 변수의 값이 $false인지 확인합니다.

3.  파이프라인 추적 폴더를 점검하여 해당 폴더에 메시지 스냅숏 파일이 더 이상 만들어지지 않는지 확인합니다.

