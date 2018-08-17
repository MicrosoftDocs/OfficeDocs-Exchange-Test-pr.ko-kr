---
title: '송신 커넥터: Exchange 2013 Help'
TOCTitle: 송신 커넥터
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 50483381
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 송신 커넥터

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-15_

Microsoft Exchange Server 2013에서 송신 커넥터는 수신 서버에 대한 아웃바운드 메시지의 흐름을 제어합니다. 송신 커넥터는 전송 서비스를 실행하는 사서함 서버에서 구성됩니다. 가장 일반적으로 아웃바운드 메시지를 스마트 호스트로 보내거나 DNS를 사용하여 직접 받는 사람에게 보내도록 송신 커넥터를 구성합니다.

전송 서비스를 실행하는 Exchange 2013 사서함 서버에는 대상 경로에서 다음 홉에 메시지를 배달하기 위해 송신 커넥터가 필요합니다. 사서함 서버에서 만들어지는 송신 커넥터는 Active Directory에 저장되며 조직의 전송 서비스를 실행하는 모든 사서함 서버에 사용할 수 있습니다.


> [!IMPORTANT]
> Exchange 2013을 배포할 경우 아웃바운드 메일을 인터넷에 라우팅하도록 송신 커넥터를 구성할 때까지 아웃바운드 메일 흐름이 발생하지 않습니다. 자세한 내용은 <A href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기</A> 항목을 참조하십시오.



## 송신 커넥터의 유형 선택

일반적으로 EAC(Exchange 관리 센터)의 **메일 흐름** 섹션에서 송신 커넥터를 구성합니다. 새 송신 커넥터를 만들 때 연결 시나리오에 적절하게 사용할 수 있는 **Type**을 선택합니다. 유형에 따라 커넥터에 할당되는 기본 사용 권한 집합이 결정되고 신뢰할 수 있는 보안 주체에게 이러한 권한이 부여됩니다. 보안 주체에는 사용자, 컴퓨터 및 보안 그룹이 포함됩니다.

특정 **유형** 선택을 설명하는 절차는 [스마트 호스트를 통해 아웃 바운드 전자 메일 라우팅에 대 한 송신 커넥터 만들기](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md) 및 [전자 메일을 보낼와 전송 계층 보안 (TLS) 적용 된 파트너에 송신 커넥터 만들기](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md)에 포함되어 있습니다.

EAC에 Exchange 관리 셸을 사용하려면 [New-SendConnector](https://technet.microsoft.com/ko-kr/library/aa998936\(v=exchg.150\)) cmdlet을 사용하여 송신 커넥터를 만들고 유형을 지정합니다.

## Exchange 2013의 새 송신 커넥터 기능

Exchange 2013에서 클라이언트 액세스 서버의 프런트 엔드 전송 서비스와 사서함 서버의 전송 서비스 간의 관계를 통해 송신 커넥터에 대한 새로운 동작이 만들어집니다. 첫 번째로 사서함 서버의 전송 서비스에서 송신 커넥터를 설정하여 로컬 Active Directory 사이트의 프런트 엔드 전송 서버를 통해 아웃바운드 메일을 라우팅할 수 있습니다. 이 작업은 [Set-SendConnector](https://technet.microsoft.com/ko-kr/library/aa998294\(v=exchg.150\)) cmdlet의 *FrontEndProxyEnabled* 매개 변수를 통해 전자 메일이 전송 서비스에서 라우팅되는 방식을 통합하여 수행할 수 있습니다. [메일 라우팅](mail-routing-exchange-2013-help.md)에서는 Exchange 2013의 전송 서비스, 라우팅 동작 및 대상에 대한 세부 정보를 제공합니다. [메일 흐름](mail-flow-exchange-2013-help.md)에서는 전송 파이프라인의 개요와 각 전송 서비스에 대한 설명을 제공합니다.

*IsCoexistenceConnector* 매개 변수는 사용되지 않습니다. 대부분의 경우 하이브리드 환경, 사서함에서 온-프레미스가 호스트되는 위치 및 클라우드에서 호스트되는 부분을 구성할 때 하이브리드 구성 마법사를 사용하는 것이 좋습니다.

*LinkedReceiveConnector*는 사용되지 않습니다. 이 매개 변수는 메시지를 타사 스팸 방지 서비스로 라우팅할 수 있는 커넥터를 만드는 데 사용됩니다. 이제 대부분의 경우 MX 레코드를 통해 메일을 스팸 방지 서비스로 라우팅하므로 연결된 커넥터 동작이 필요하지 않습니다.

*MaxMessageSize* 매개 변수로 지정되는 기본 최대 메시지 크기가 10MB에서 25MB로 늘어났습니다. [Set-SendConnector](https://technet.microsoft.com/ko-kr/library/aa998294\(v=exchg.150\))에서는 송신 커넥터에서 매개 변수를 설정하는 방법에 대한 세부 정보를 제공합니다.

*TlsCertificateName*이 추가되었습니다. 이 매개 변수는 아웃바운드 연결에 사용할 수 있도록 로컬 인증서를 인증하고 인증서 사기의 위험을 최소화하기 위하여 사용됩니다.

