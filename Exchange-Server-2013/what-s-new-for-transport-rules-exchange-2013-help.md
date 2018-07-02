---
title: '전송 규칙에 대 한 새로운 기능: Exchange 2013 Help'
TOCTitle: 전송 규칙에 대 한 새로운 기능
ms:assetid: 0c2fc0b5-3cd2-4d79-aa2b-0c7622ae15a8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150483(v=EXCHG.150)
ms:contentKeyID: 50482482
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 규칙에 대 한 새로운 기능

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-10-03_

Microsoft Exchange Server 2013에서는 전송 규칙의 몇 가지 기능이 향상되었습니다. 이 항목에서는 몇 가지 주요 변경 내용과 기능 향상에 대한 간략한 개요를 제공합니다. 전송 규칙에 대한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)항목을 참조하십시오.

## 데이터 손실 방지 정책 지원

Exchange 2013의 DLP(데이터 손실 방지)는 조직이 중요한 데이터의 의도하지 않은 공개를 줄이는 데 도움이 될 수 있습니다. DLP 정책을 함께 제공하여 적용하는 규칙을 만들 수 있도록 전송 규칙이 업데이트되었습니다. 전송 규칙의 DLP 지원에 대한 자세한 내용은 다음 항목을 참조하십시오.

[전송 규칙에 중요 한 정보 규칙 통합 (영문)](integrating-sensitive-information-rules-with-transport-rules-exchange-2013-help.md)

[데이터 손실 방지](technical-overview-of-dlp-data-loss-prevention-in-exchange.md)

## 새 조건자 및 작업

새 조건자 및 작업의 추가를 통해 전송 규칙의 기능이 확장되었습니다. 아래 나열된 각 조건자는 전송 규칙을 만들 때 조건 또는 예외로 사용할 수 있습니다.

이러한 새 조건자 및 작업을 사용하는 방법에 대한 자세한 내용은 [전송 규칙 조건 (조건자)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md) 및 [전송 규칙 동작](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 새 조건자

  -  
    **AttachmentExtensionMatchesWords**   특정 확장명을 가진 첨부 파일을 포함하는 메시지를 검색하는 데 사용됩니다.

  -  
    **AttachmentHasExecutableContent**   실행 가능한 콘텐츠가 있는 첨부 파일을 포함하는 메시지를 검색하는 데 사용됩니다.

  -  
    **HasSenderOverride** 보낸 사람이 DLP 정책 제한을 재정의하도록 선택한 메시지를 검색하는 데 사용됩니다.

  -  
    **MessageContainsDataClassifications**   메시지 본문 및 첨부 파일에서 중요한 정보를 검색하는 데 사용됩니다. 사용 가능한 데이터 분류 목록은 [Exchange의 중요 한 정보 유형 찾아보십시오](what-the-sensitive-information-types-in-exchange-look-for-exchange-online-help.md) 항목을 참조하십시오.

  -  
    **MessageSizeOver**   전체 크기가 지정된 제한보다 크거나 같은 메시지를 검색하는 데 사용됩니다.

  -  
    **SenderIPRanges**   특정 IP 주소 범위 집합에서 보낸 메시지를 검색하는 데 사용됩니다.

## 새 작업

  -  
    **GenerateIncidentReport**   지정된 SMTP 주소로 보내는 인시던트 보고서를 생성합니다. 이 작업에는 IncludeOriginalMail 또는 DoNotIncludeOriginalMail의 두 값 중 하나를 사용할 수 있는 *IncidentReportOriginalMail*이라는 매개 변수도 사용됩니다.

  -  
    **NotifySender** DLP 정책을 위반하는 메시지의 보낸 사람에게 이를 알리는 방법을 지정합니다. 보낸 사람에게 알리기만 하고 메시지를 정상적으로 라우팅할 수도 있고, 메시지를 거부하고 보낸 사람에게 알릴 수도 있습니다.

  -  
    **StopRuleProcessing**   메시지에 대한 모든 후속 규칙 처리를 중지합니다.

  -  
    **ReportSeverityLevel**   인시던트 보고서에 지정된 심각도 수준을 설정합니다. 작업에 대한 값은 정보, 낮음, 중간, 높음 및 해제입니다.

  -  
    **RouteMessageOutboundRequireTLS**   이 메시지를 조직 외부에 라우팅할 때 TLS(전송 계층 보안) 암호화가 필요합니다. TLS 암호화가 지원되지 않는 경우 메시지가 거부되고 배달되지 않습니다.

## 전송 규칙의 기타 변경 내용

  - **확장된 정규식 구문 지원**   Exchange 2013의 전송 규칙은 Microsoft.NET Framework 정규식(regex) 기능을 기반으로 하며 이제 확장된 정규식 구문을 지원합니다.

  - **전송 규칙 에이전트 호출**   Exchange 2013에서 전송 규칙에 대한 주요 아키텍처 변경은 전송 규칙 에이전트가 onResolvedMessage에서 호출된다는 것입니다. Exchange의 이전 버전에서는 규칙 에이전트가 onRoutedMessage에서 호출되었습니다. 이러한 변경 덕분에 메시지가 라우팅되는 방식을 변경할 수 있는 TLS를 요청하는 등의 새 작업을 추가할 수 있습니다. Exchange 2013의 전송 규칙 아키텍처에 대한 자세한 내용은 [메일 흐름 또는 전송 규칙](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md) 항목을 참조하십시오.

  - **메시지 추적 로그의 자세한 전송 규칙 정보**   전송 규칙에 대한 자세한 정보가 이제 메시지 추적 로그에 포함됩니다. 이러한 정보에는 특정 메시지에 대해 트리거된 규칙 및 이러한 규칙 처리의 결과로 수행된 작업이 포함됩니다.

  - **새로운 규칙 모니터링 기능**   Exchange 2013에서는 구성된 전송 규칙을 모니터링하고 규칙을 만들 때와 정기 작업 중에 이러한 규칙을 실행하는 비용을 측정합니다. Exchange에서는 메일 배달에 지연을 일으키는 규칙을 검색하고 규칙에 대한 경고를 생성할 수 있습니다.

