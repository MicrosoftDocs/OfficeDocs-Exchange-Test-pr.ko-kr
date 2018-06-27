---
title: '배달 에이전트 및 배달 에이전트 커넥터: Exchange 2013 Help'
TOCTitle: 배달 에이전트 및 배달 에이전트 커넥터
ms:assetid: 38c942ee-b59d-47ec-87eb-bebad441ada5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638118(v=EXCHG.150)
ms:contentKeyID: 50482883
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 배달 에이전트 및 배달 에이전트 커넥터

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

배달 에이전트는 SMTP Exchange Server 환경에서 SMTP 프로토콜을 사용하지 않는 시스템으로 메시지를 배달할 수 있습니다. 각 배달 에이전트는 배달 에이전트 커넥터와 연결되어 있습니다. 배달 에이전트 커넥터는 처리와 비 SMTP 장치 또는 시스템으로의 배달을 위해 배달 에이전트로 라우팅된 메시지를 큐에 넣습니다.


> [!TIP]
> 외부 커넥터 아키텍처가 Microsoft Exchange 2013에 남아 있으므로 가능한 경우 비 SMTP 시스템으로 메시지를 라우팅할 때에는 배달 에이전트를 사용하는 것이 좋습니다. 이렇게 하는 주요 이유는 메시지에 큐 관리를 사용할 수 있고 Drop 디렉터리로의 파일 전송을 관리할 필요가 없으며 메시지 배달을 확인할 수 있기 때문입니다.



**목차**

Function and benefits of Delivery Agents

Adding Delivery Agents to your organization

Delivery Agent connectors

Default text messaging Delivery Agent connector

## 배달 에이전트의 기능 및 이점

배달 에이전트는 사서함 서버의 전송 서비스에 설치된 구성 요소이며 다음 작업을 수행할 수 있습니다.

  - 외부 시스템에 대해 메시지 배달에 사용할 연결 설정.

  - 사서함 서버의 배달 큐에서 메시지 검색.

  - 외부 시스템에 메시지 배달.

  - 성공적인 각각의 메시지 배달에 대해 승인 제공.

외부 커넥터 아키텍처가 Microsoft Exchange Server 2013에 남아 있으므로 가능한 경우 비 SMTP 시스템으로 메시지를 라우팅할 때에는 배달 에이전트를 사용하는 것이 좋습니다. 배달 에이전트에는 다음과 같은 이점이 있습니다.

  - 외부 시스템에 라우팅된 메시지의 큐 관리를 허용합니다.

  - 더 이상 메시지를 파일 시스템에 쓰고 읽을 필요가 없으므로 메시지 배달 성능이 향상됩니다.

  - 에이전트 개발자를 위한 풍부한 이벤트를 통해 메시지 속성에 대한 액세스를 제공합니다.

  - 배달 에이전트는 Exchange의 메시지 진술 및 관리 기능을 사용할 수 있어 외부 커넥터를 구현하는 것보다 배달 에이전트를 개발하는 쪽이 시간이 적게 걸립니다.

  - 메시지가 단지 Drop 디렉터리에 기록된 것이 아니라 외부 시스템으로 배달되었는지 확인할 수 있습니다.

  - 외부 시스템에 대한 메시지 배달 대기 시간을 추적할 수 있으므로 배달 에이전트 커넥터를 사용한 SLA(서비스 수준 계약) 분석이 가능합니다.

## 조직에 배달 에이전트 추가

조직에서 배달 에이전트를 사용하려면 다음을 완료해야 합니다.

1.  배달 에이전트를 확보합니다. 일반적으로 배달 에이전트는 타사에서 씁니다. Exchange 2013에는 기본적으로 배달 에이전트 커넥터가 텍스트 메시징 배달 에이전트 커넥터 하나만 제공됩니다.

2.  배달 에이전트 커넥터의 원본 서버로 작동할 사서함 서버의 전송 서비스에 배달 에이전트를 설치합니다.

3.  특정 프로토콜에 대해 배달 에이전트 커넥터를 만듭니다.

이러한 단계를 모두 완료하고 나면 외부 시스템으로 가는 메시지가 배달 에이전트 커넥터를 통해 라우팅되어 배달 에이전트에서 처리됩니다.

[Microsoft.Exchange.Data.Transport.Delivery 네임 스페이스](https://go.microsoft.com/fwlink/?linkid=262690) 배달 에이전트를 개발 하는 방법에 대 한 자세한 정보를 제공 합니다.

## 배달 에이전트 커넥터

Exchange 2013의 배달 에이전트 커넥터는 Exchange 2010에 도입된 배달 에이전트 커넥터와 유사하며, SMTP 프로토콜을 사용하지 않는 외부 시스템으로 주소가 지정된 메시지를 라우팅합니다. 메시지가 배달 에이전트 커넥터로 라우트되면 연결된 배달 에이전트가 콘텐츠를 변환하고 메시지를 배달합니다. 일반적으로 배달 에이전트는 타사에서 만들며 조직의 배달 에이전트 커넥터와 작동하도록 구성됩니다.

배달 에이전트 커넥터는 Exchange 관리 센터에서 만들 수 없습니다. 대신 Exchange 관리 셸에서 [New-DeliveryAgentConnector](https://technet.microsoft.com/ko-kr/library/dd351063\(v=exchg.150\)) cmdlet을 사용하여 배달 에이전트 커넥터를 만들고 [Set-DeliveryAgentConnector](https://technet.microsoft.com/ko-kr/library/dd351159\(v=exchg.150\))를 사용하여 배달 에이전트 커넥터의 속성을 편집합니다. 선택적 *SourceTransportServers* 매개 변수를 사용하여 커넥터의 호스트 사서함 서버를 하나 이상 지정할 수 있습니다.

## 기본 텍스트 메시징 배달 에이전트 커넥터

텍스트 메시징 배달 에이전트 커넥터를 사용하여 모바일 장치로 메시지를 라우팅할 수 있습니다. Exchange 서버에서 `Get-DeliveryAgentConnector | fl`을 실행하여 커넥터와 해당하는 모든 매개 변수를 확인합니다. *DeliveryProtocol*이 `MOBILE`로 설정되어 있습니다.

