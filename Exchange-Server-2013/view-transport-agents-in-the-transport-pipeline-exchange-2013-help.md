---
title: '전송 파이프라인에 보기 전송 에이전트: Exchange 2013 Help'
TOCTitle: 전송 파이프라인에 보기 전송 에이전트
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51407728
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전송 파이프라인에 보기 전송 에이전트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Exchange 관리 셸을 사용하여 Microsoft Exchange Server 2013 사서함 서버와 클라이언트 액세스 서버에서 전송 파이프라인의 전송 에이전트 목록을 확인할 수 있습니다. 구체적으로는 **Get-TransportPipeline** cmdlet이 전송 파이프라인에 있는 다음과 같은 유형의 전송 에이전트에 대한 정보를 표시합니다.

  - 사서함 서버의 전송 서비스에 있는 **SmtpReceiveAgent**, **RoutingAgent**, **DeliveryAgent** 및 **StorageAgent** 클래스 기반 에이전트

  - 사서함의 사서함 전송 배달 서비스에 있는 **SmtpReceiveAgentClass** 기반 에이전트

  - 클라이언트 액세스 서버의 프런트 엔드 전송 서비스에 있는 **SmtpReceiveAgentClass** 기반 에이전트

전송 파이프라인에서 메시지가 발생한 모든 활성화된 전송 에이전트의 목록과 등록되어 있는 SMTP 이벤트를 볼 수 있습니다. 전송 에이전트에 대한 자세한 내용은 [전송 에이전트](transport-agents-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "전송 에이전트" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 전송 파이프라인의 전송 에이전트 목록 보기

셸을 사용하여 Exchange 서버의 전송 파이프라인에 있는 전송 에이전트 목록을 보려면 다음 명령을 실행합니다.

    Get-TransportPipeline | Format-List

C:\\My Documents\\Transport Agents.txt 텍스트 파일로 결과를 내보내려면 다음 명령을 실행합니다.

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## 작동 여부는 어떻게 확인합니까?

Transport Service가 시작된 시간과 **Get-TransportPipeline** cmdlet이 실행된 시간 사이에 전송 파이프라인에서 메시지가 발견된 전송 에이전트만 cmdlet에 표시됩니다. 전송 파이프라인에서 메시지가 발생하지 않은 전송 에이전트는 해당 전송 에이전트가 활성화되어 있더라도 **Get-TransportPipeline** cmdlet에서 표시한 결과에 나타나지 않습니다.

