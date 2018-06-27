---
title: '외부 커넥터: Exchange 2013 Help'
TOCTitle: 외부 커넥터
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 50482651
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 외부 커넥터

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-09-25_

외부 커넥터는 SMTP를 기본 전송 메커니즘으로 사용하지 않는 외부 시스템 또는 서버로 메시지를 배달합니다. 팩스 게이트웨이 서버를 예로 들 수 있습니다. 외부 커넥터는 로컬 또는 공유 Drop 디렉터리를 사용하여 아웃바운드 메시지를 파일 전송을 통해 외부 시스템으로 전송합니다. 외부 커넥터는 Microsoft Exchange Server 2013 사서함 서버의 전송 서비스에서 생성됩니다.

외부 게이트웨이 서버는 사서함 서버의 전송 서비스에 있는 Pickup 또는 Replay 디렉터리를 사용하여 메시지를 Exchange 2013 조직으로 보낼 수 있습니다. 올바른 형식의 전자 메일 파일을 각 디렉터리로 복사하면 해당 파일은 Exchange 사서함으로 배달되기 위해 제출됩니다.


> [!TIP]
> SMTP 이외 시스템으로 아웃바운드 메시지를 전달해야 하는 대부분의 경우에는 메시지의 큐 관리에 허용되고, 메시지를 파일 시스템에 쓸 필요가 없는 등, 여러 이점이 있으므로 배달 에이전트 커넥터가 권장됩니다. <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">배달 에이전트 및 배달 에이전트 커넥터</A> 항목에서 보다 자세한 내용을 제공합니다.



## 자세한 내용

[비 SMTP 팩스 게이트웨이에 메시지 배달에 대 한 외부 커넥터 만들기](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[배달 에이전트 및 배달 에이전트 커넥터](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/ko-kr/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/ko-kr/library/bb123789\(v=exchg.150\))

