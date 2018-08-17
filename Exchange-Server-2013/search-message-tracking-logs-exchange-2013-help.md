---
title: '메시지 추적 로그 검색: Exchange 2013 Help'
TOCTitle: 메시지 추적 로그 검색
ms:assetid: e1678327-bcd5-42d4-a363-67f33067fe9a
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124926(v=EXCHG.150)
ms:contentKeyID: 51407757
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# 메시지 추적 로그 검색

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2013-02-25_

Microsoft Exchange Server 2013에서 메시지 추적 로그는 사서함 서버의 전송 서비스, 사서함 서버의 사서함 및 Edge 전송 서버를 오고가는 메시지 전송 시 수행되는 모든 메시지 작업에 대한 상세 레코드입니다.

Exchange 관리 셸의 <strong>Get-MessageTrackingLog</strong> cmdlet을 사용하여 특정 검색 조건으로 메시지 추적 로그의 항목을 검색할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요.[메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "메시지 추적" 항목

  - 메시지 추적 로그를 검색하려면 Microsoft Exchange Transport Log Search Service가 실행 중이어야 합니다. 이 서비스를 사용하지 않도록 설정하거나 중지하면 메시지 추적 로그를 검색하거나 배달 보고서를 실행할 수 없습니다. 그러나 이 서비스를 중지해도 Exchange의 다른 기능에는 영향을 주지 않습니다.

  - <strong>Get-MessageTrackingLog</strong> cmdlet의 결과로 표시된 필드 이름은 메시지 추적 로그에 사용되는 실제 필드 이름과 유사합니다. 가장 큰 차이점은 다음과 같습니다.
    
      - 필드 이름에서 대시가 제거됩니다. 예를 들어 <strong>internal-message-id</strong>는 `InternalMessageId`로 표시됩니다.
    
      - <strong>date-time</strong> 필드는 `Timestamp`로 표시됩니다.
    
      - <strong>recipient-address</strong> 필드는 `Recipients`로 표시됩니다.
    
      - <strong>sender-address</strong> 필드는 `Sender`로 표시됩니다.

  - 메시지 추적 로그의 <strong>date-time</strong> 필드에는 정보가 UTC(Coordinated Universal Time)로 저장됩니다. 그러나 *Start* 또는 *End* 매개 변수에 대한 날짜-시간 검색 조건은 검색을 수행하는 데 사용하는 컴퓨터의 국가별 날짜-시간 형식으로 입력해야 합니다.

  - <strong>Get-MessageTrackingLog</strong> cmdlet을 사용하여 다른 Exchange 서버에서 메시지 추적 로그 파일을 복사한 다음 검색할 수는 없습니다. 또한 기존 메시지 추적 로그 파일을 수동으로 저장하면 해당 파일의 날짜-시간 스탬프가 변경되어 Exchange에서 메시지 추적 로그를 검색하는 데 사용하는 쿼리 논리가 손상됩니다.

  - Exchange 2013<strong>Get-MessageTrackingLog</strong> cmdlet으로 동일한 Active Directory 사이트에 있는 Exchange 2007 및 Exchange 2010 서버의 메시지 추적 로그를 검색할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 메시지 추적 로그 검색

특정 이벤트에 대한 메시지 추적 로그 항목을 검색하려면 다음 구문을 사용합니다.

    Get-MessageTrackingLog [-Server <ServerIdentity.] [-ResultSize <Integer> | Unlimited] [-Start <DateTime>] [-End <DateTime>] [-EventId <EventId>] [-InternalMessageId <InternalMessageId>] [-MessageId <MessageId>] [-MessageSubject <Subject>] [-Recipients <RecipientAddress1,RecipientAddress2...>] [-Reference <Reference>] [-Sender <SenderAddress>]

서버에서 최근 메시지 추적 로그 항목 1,000개를 보려면 다음 명령을 실행합니다.

    Get-MessageTrackingLog

이 예제에서는 메시지 보낸 사람이 pat@contoso.com인 모든 <strong>FAIL</strong> 이벤트에 대해 로컬 서버의 메시지 추적 로그에서 2013년 3월 28일 오전 8시에서 2013년 3월 28일 오후 5시 사이의 모든 항목을 검색합니다.

    Get-MessageTrackingLog -ResultSize Unlimited -Start "3/28/2013 8:00AM" -End "3/28/2013 5:00PM" -EventId "Fail" -Sender "pat@contoso.com"

## 셸을 사용하여 메시지 추적 로그 검색의 출력 제어

다음 구문을 사용합니다.

    Get-MessageTrackingLog <SearchFilters> | <Format-Table | Format-List> [<FieldNames>] [<OutputFileOptions>]

이 예제에서는 다음 검색 조건을 사용하여 메시지 추적 로그를 검색합니다.

  - 처음 1,000개 <strong>Send</strong> 이벤트에 대한 결과를 반환합니다.

  - 결과를 목록 형식으로 표시합니다.

  - `Send` 또는 `Recipient`로 시작하는 필드 이름만 표시합니다.

  - `D:\Send Search.txt`라는 새 파일에 출력을 씁니다.

<!-- end list -->

    Get-MessageTrackingLog -EventId Send | Format-List Send*,Recipient* > "D:\Send Search.txt"

## 셸을 사용하여 메시지 추적 로그에서 여러 서버의 메시지 항목 검색

일반적으로 <strong>MessageID:</strong>  헤더 필드의 값은 메시지가 Exchange 조직 전체를 이동하는 과정에서 일정하게 유지됩니다. 이 값의 이름은 큐 뷰어 유틸리티에서는 <strong>InternetMessageId</strong>이고 메시지 추적 로그 유틸리티에서는 <strong>MessageId</strong>입니다. 특정 메시지의 `MessageID:` 값을 확인한 후에는 Exchange 조직의 모든 사서함 서버에 있는 메시지 추적 로그에서 해당 메시지에 대한 정보를 검색할 수 있습니다.

모든 사서함 서버에서 특정 메시지에 대한 모든 메시지 추적 로그 항목을 검색하려면 다음 구문을 사용합니다.

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId <MessageID> | Select-Object <CommaSeparatedFieldNames> | Sort-Object -Property <FieldName>

이 예에서는 다음 검색 조건을 사용하여 모든 Exchange 2013 사서함 서버에서 메시지 추적 로그를 검색합니다.

  - <strong>MessageID:</strong>  값이 `<ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com>`인 메시지와 관련된 모든 항목을 찾습니다. 꺾쇠 괄호 문자(`<>`)는 생략할 수 있습니다. 생략하지 않을 경우 전체 <strong>MessageID:</strong>  값을 따옴표로 묶어야 합니다.

  - 각 항목에 대해 필드 <strong>date-time</strong>, <strong>server-hostname</strong>, <strong>client-hostname</strong>, <strong>source</strong>, <strong>event-id</strong> 및 <strong>recipient-address</strong>를 표시합니다.

  - 결과를 <strong>date-time</strong> 필드 기준으로 정렬합니다.

<!-- end list -->

    Get-ExchangeServer | where {$_.isHubTransportServer -eq $true -or $_.isMailboxServer -eq $true} | Get-MessageTrackingLog -MessageId ba18339e-8151-4ff3-aeea-87ccf5fc9796@mailbox01.contoso.com | Select-Object Timestamp,ServerHostname,ClientHostname,Source,EventId,Recipients | Sort-Object -Property Timestamp

## EAC를 사용하여 메시지 추적 로그 검색

EAC(Exchange 관리 센터)의 관리자용 배달 보고서 기능을 사용하여 메시지 추적 로그에서 조직의 특정 사서함이 보냈거나 받은 메시지에 대한 정보를 검색할 수 있습니다. 자세한 내용은 [배달 보고서로 메시지 추적](track-messages-with-delivery-reports-exchange-2013-help.md)을 참조하세요.

