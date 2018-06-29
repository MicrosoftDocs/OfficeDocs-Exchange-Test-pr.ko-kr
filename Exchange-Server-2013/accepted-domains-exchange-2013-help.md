---
title: '허용 도메인: Exchange 2013 Help'
TOCTitle: 허용 도메인
ms:assetid: c1839a5b-49f9-4c53-b247-f4e5d78efc45
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124423(v=EXCHG.150)
ms:contentKeyID: 50484079
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 허용 도메인

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-06-16_

허용 도메인은 Microsoft Exchange Server 2013 조직에서 전자 메일을 주고받는 SMTP 네임스페이스입니다. 허용 도메인에는 Exchange 조직이 신뢰할 수 있는 도메인이 포함됩니다. Exchange 조직은 허용 도메인에 속한 받는 사람의 메일 배달을 처리할 때 신뢰할 수 있습니다. 또한 허용 도메인은 Exchange 조직이 메일을 받은 다음 받는 사람에게 배달하기 위해 조직 외부에 있는 전자 메일 서버로 릴레이하는 도메인을 포함합니다.

**목차**

Configuring accepted domains

Authoritative domains

Relay domains

Internal relay domain

External relay domain

Accepted domains and email address policies

## 허용 도메인 구성

허용 도메인은 Exchange 조직에 대한 전역 설정으로 구성됩니다. Exchange 조직에서 메시지를 릴레이하거나 배달하는 모든 도메인을 조직의 허용 도메인으로 구성해야 합니다.

허용 도메인에는 다음과 같은 세 가지 유형 즉, 신뢰할 수 있는 도메인, 내부 릴레이 도메인 및 외부 릴레이 도메인이 있습니다. 이러한 허용 도메인 유형은 다음 섹션에서 설명합니다.


> [!NOTE]
> 경계 네트워크에 구독된 Edge 전송 서버가 있는 경우 Exchange 조직의 사서함 서버에 허용 도메인을 구성합니다. 허용 도메인 구성은 EdgeSync 동기화 중에 Edge 전송 서버로 복제됩니다. 자세한 내용은 <A href="edge-subscriptions-exchange-2013-help.md">Edge 구독</A>을 참조하세요.



## 신뢰할 수 있는 도메인

조직에 SMTP 도메인이 둘 이상 있을 수 있습니다. 조직의 전자 메일 도메인 집합은 신뢰할 수 있는 도메인입니다. Exchange 2013에서 허용 도메인은 Exchange 조직이 이 SMTP 도메인에서 받는 사람의 사서함을 호스트할 때 신뢰할 수 있는 것으로 간주합니다.

기본적으로 첫 번째 Exchange 2013 사서함 서버가 설치될 때 하나의 허용 도메인이 Exchange 조직의 신뢰할 수 있는 도메인으로 구성됩니다. 기본 허용 도메인은 포리스트 루트 도메인의 FQDN(정규화된 도메인 이름)이 됩니다. 대부분의 경우 내부 도메인 이름은 외부 도메인 이름과 다릅니다. 예를 들어, 내부 도메인 이름은 contoso.local이지만 외부 도메인 이름은 contoso.com이 될 수 있습니다. 조직의 DNS MX(메일 교환기) 레코드는 contoso.com을 참조합니다. Contoso.com은 전자 메일 주소 정책을 만들 때 사용자에게 할당하는 SMTP 네임스페이스입니다. 허용 도메인은 외부 도메인 이름과 일치하도록 만들어야 합니다.

자세한 내용은 다음을 참조하세요.

  - [신뢰할 수 있는 페이지로 Exchange 조직 내에서 허용된 도메인 구성](configure-an-accepted-domain-within-your-exchange-organization-as-authoritative-exchange-2013-help.md)

  - [신뢰할 수 있는 여러 도메인에 대 한 메일을 수락 하도록 Exchange 구성](configure-exchange-to-accept-mail-for-multiple-authoritative-domains-exchange-2013-help.md)

## 릴레이 도메인

일반적으로 대부분의 인터넷 연결 서버는 다른 도메인이 해당 서버를 통해 릴레이되지 않도록 구성됩니다. 그러나 파트너 또는 계열사에서 Exchange 서버를 통해 전자 메일을 릴레이하도록 해야 하는 시나리오가 있습니다. Exchange 2013에서는 허용 도메인을 릴레이 도메인으로 구성할 수 있습니다. 조직에서는 전자 메일 메시지를 받은 다음 메시지를 다른 전자 메일 서버로 릴레이합니다.

릴레이 도메인을 내부 릴레이 도메인이나 외부 릴레이 도메인으로 구성할 수 있습니다. 이러한 두 가지 릴레이 도메인 유형은 다음 섹션에서 설명합니다.

## 내부 릴레이 도메인

내부 릴레이 도메인을 구성할 경우 이 도메인의 받는 사람 일부 또는 전체의 사서함이 이 Exchange 조직에 없습니다. 따라서 Exchange 조직의 전송 서버를 통해 이 도메인으로 오는 인터넷 메일이 릴레이됩니다. 이 섹션의 시나리오에서는 이 구성을 사용하여 설명합니다.

둘 이상의 서로 다른 메시징 시스템 간에 동일한 SMTP 주소 공간을 공유해야 하는 조직이 있을 수 있습니다. 예를 들어, Exchange와 타사 메시징 시스템 간 또는 여러 Exchange 포리스트에 구성된 Active Directory 환경 간에 SMTP 주소 공간을 공유해야 하는 시나리오의 경우, 각 전자 메일 시스템 사용자의 전자 메일 주소에는 동일한 도메인 접미사가 포함됩니다.

이러한 시나리오를 지원하려면 내부 릴레이 도메인으로 구성되는 허용 도메인을 만들어야 합니다. 또한 사서함 서버에서 만들어져 공유 주소 공간으로 전자 메일을 보내도록 구성된 송신 커넥터를 추가해야 합니다. 허용 도메인이 신뢰할 수 있는 도메인으로 구성되고 받는 사람이 Active Directory에 없으면 보낸 사람에게 NDR(배달 못 함 보고서)이 반환됩니다. 내부 릴레이 도메인으로 구성된 허용 도메인이 Exchange 조직의 받는 사람에게 메시지를 처음 배달하는 경우, 받는 사람이 없으면 주소 공간이 가장 비슷한 송신 커넥터로 메시지가 라우팅됩니다.

조직에 포리스트가 둘 이상 있고 GAL(전체 주소 목록) 동기화를 구성한 경우에는 한 포리스트의 SMTP 도메인을 두 번째 포리스트의 내부 릴레이 도메인으로 구성할 수 있습니다. 인터넷을 통해 내부 릴레이 도메인의 받는 사람에게 배달되는 메시지는 동일한 조직의 사서함 서버로 릴레이됩니다. 그러면 받는 쪽 사서함 서버에서 메시지를 받는 사람 포리스트의 사서함 서버로 라우팅합니다. 해당 도메인에 배달되는 전자 메일을 Exchange 조직에서 수락하도록 하려면 SMTP 도메인을 내부 릴레이 도메인으로 구성합니다. 조직의 커넥터 구성에 따라 메시지 라우팅 방법이 결정됩니다.

자세한 내용은 [Exchange 조직 외부에 사서함이 있는 사업부에 대 한 허용된 도메인 구성](configure-an-accepted-domain-for-a-business-unit-with-mailboxes-outside-your-exchange-organization-exchange-2013-help.md)을 참조하세요.

## 외부 릴레이 도메인

외부 릴레이 도메인을 구성하면 메시지는 Exchange 조직 외부 및 해당 조직의 네트워크 경계 외부에 있는 전자 메일 서버로 릴레이됩니다.

자세한 내용은 [독립 사업부에 대 한 허용된 도메인 구성](configure-an-accepted-domain-for-an-independent-business-unit-exchange-2013-help.md)을 참조하세요.

## 허용된 도메인 및 전자 메일 주소 정책

전자 메일 주소 정책에서 해당 SMTP 주소 공간을 사용 하기 전에 허용된 도메인을 구성 해야 합니다. 허용된 도메인을 만들 때 모든 하위 도메인의 SMTP 주소 공간도 Exchange 조직에서 사용할 수 있는지를 나타내기 위해 주소 공간에 와일드 카드 문자 (\*)를 사용할 수 있습니다. 예: contoso.com 및 모든 하위 도메인 허용 도메인을 구성 하려면 입력 **\*. contoso.com** 으로 SMTP 주소 공간입니다. 허용된 도메인 항목은 자동으로 전자 메일 주소 정책에서 사용 하기 위해 사용할 수 있습니다.

전자 메일 주소 공간에서 사용되는 허용 도메인을 삭제하면 해당 정책은 더 이상 유효하지 않고 해당 SMTP 도메인의 전자 메일 주소를 가진 받는 사람은 전자 메일을 보내거나 받을 수 없습니다.

