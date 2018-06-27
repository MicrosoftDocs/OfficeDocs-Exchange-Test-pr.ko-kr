---
title: '주소 Edge 전송 서버에서 다시 쓰기: Exchange 2013 Help'
TOCTitle: 주소 Edge 전송 서버에서 다시 쓰기
ms:assetid: 23f1eaf6-247a-4671-ad72-aae19d9b511d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996806(v=EXCHG.150)
ms:contentKeyID: 61060544
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소 Edge 전송 서버에서 다시 쓰기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-03-09_

주소 다시 쓰기를 수행하면 Edge 전송 서버를 통해 조직에서 보내거나 받는 메시지의 보낸 사람과 받는 사람 전자 메일 주소가 수정됩니다. Edge 전송 서버에서 다시 쓰기 기능을 제공하는 두 전송 에이전트는 주소 다시 쓰기 인바운드 에이전트와 주소 다시 쓰기 아웃바운드 에이전트입니다. 아웃바운드 메시지의 경우 기본적으로 외부 받는 사람에게 일관된 단일 전자 메일 도메인을 표시하기 위해 주소를 다시 씁니다. 인바운드 메시지의 경우에는 기본적으로 올바른 받는 사람에게 메시지를 배달하기 위해 주소를 다시 씁니다.

*주소 다시 쓰기 항목*을 작성하여 내부 주소인 변경할 전자 메일 주소 및 외부 주소인 메시지를 보낼 최종 전자 메일 주소를 지정합니다. 전자 메일 주소를 다시 쓸 메시지(인바운드 및 아웃바운드 메시지 또는 아웃바운드 메시지만)를 지정할 수 있습니다. 주소 쓰기 항목은 단일 사용자에 대해(chris@contoso.com에서 support@contoso.com으로), 단일 도메인의 모든 사용자에 대해(contoso.com에서 fabrikam.com으로), 또는 예외를 지정하여 여러 하위 도메인의 모든 사용자에 대해(legal.fabrikam.com을 제외하고 \*.fabrikam.com에서 contoso.com으로) 만들 수 있습니다.


> [!IMPORTANT]
> 주소 다시 쓰기를 사용하려는 방법에 관계없이 주소가 중복되지 않도록 다시 쓰기를 통해 생성되는 전자 메일 주소가 조직에서 고유한지를 확인해야 합니다. 이는 주소 다시 쓰기에서 다시 쓴 전자 메일 주소가 고유한지를 확인하지 않기 때문입니다.



**목차**

Address rewriting scenarios

Message properties modified by address rewriting

What address rewriting doesn't change

Considerations for outbound-only address rewriting

Considerations for inbound and outbound address rewriting

Considerations for rewriting addresses in multiple domains

Priority of address rewrite entries

Digitally signed, encrypted, and rights-protected messages

## 주소 다시 쓰기 시나리오

다음 시나리오는 주소 다시 쓰기를 사용할 수 있는 방법의 예입니다.

  - **그룹 통합**   일부 조직은 비즈니스나 기술적 요구 사항을 기준으로 내부 비즈니스를 별도의 도메인으로 분리합니다. 이러한 구성으로 인해 전자 메일 메시지가 별도의 그룹 또는 별도의 조직에서 보낸 것처럼 표시될 수 있습니다.
    
    다음 예에서는 Contoso, Ltd. 조직이 내부 하위 도메인을 외부 받는 사람이 볼 수 없도록 숨기는 방법을 보여 줍니다.
    
      - northamerica.contoso.com, europe.contoso.com 및 asia.contoso.com 도메인에서 보내는 아웃바운드 메시지를 다시 써서 단일 도메인 contoso.com에서 보내는 것으로 표시되도록 합니다. 모든 메시지는 전체 조직과 인터넷 간에 SMTP 연결을 제공하는 Edge 전송 서버를 통과할 때 다시 쓰여집니다.
    
      - contoso.com 받는 사람에게 보내는 인바운드 메시지는 Edge 전송 서버에 의해 사서함 서버로 릴레이됩니다. 메시지는 받는 사람의 사서함에 구성된 프록시 주소를 기준으로 올바른 받는 사람에게 배달됩니다.

  - **합병 및 인수**   인수된 회사가 별도의 비즈니스 단위로 계속 운영될 수도 있지만 주소 다시 쓰기를 사용하면 두 조직이 하나의 통합된 조직인 것처럼 표시되도록 할 수 있습니다.
    
    다음 예에서는 Contoso, Ltd.가 새로 인수한 회사 Fourth Coffee의 전자 메일 도메인을 숨기는 방법을 보여 줍니다.
    
      - Contoso, Ltd.는 Fourth Coffee에서 Exchange 조직의 모든 아웃바운드 메시지가 contoso.com에서 보낸 것처럼 표시하려고 합니다. 두 조직에서 보내는 모든 메시지는 Contoso, Ltd.의 Edge 전송 서버를 통해 전송됩니다. Edge 전송 서버는 전자 메일 메시지를 *user*@fourthcoffee.com에서 *user*@contoso.com으로 다시 씁니다.
    
      - 또한 *user*@contoso.com에게 보내는 인바운드 메시지를 다시 써서 *user*@fourthcoffee.com 사서함으로 라우팅합니다. *user*@fourthcoffee.com으로 전송되는 인바운드 메시지는 Fourth Coffee의 전자 메일 서버로 직접 라우팅됩니다.

  - **파트너**   많은 조직에서는 외부 파트너를 통해 고객이나 다른 파트너 또는 조직 자체에 서비스를 제공합니다. 이러한 경우 혼란을 피하려면 파트너 조직의 전자 메일 도메인을 자체 조직의 전자 메일 도메인으로 대체해야 합니다.
    
    다음 예에서는 Contoso, Ltd.가 파트너의 전자 메일 도메인을 숨기는 방법을 보여 줍니다.
    
      - Contoso, Ltd.는 보다 큰 규모의 Wingtip Toys 조직에 지원을 제공합니다. Wingtip Toys는 고객에게 통합된 전자 메일 환경을 제공하고자 하며, Contoso, Ltd.의 지원 담당자가 보내는 모든 메시지가 Wingtip Toys에서 전송된 것처럼 표시해야 합니다. Wingtip Toys와 관련된 모든 아웃바운드 메시지는 Wingtip Toys의 Edge 전송 서버를 통해 전송되며 모든 contoso.com 전자 메일 주소를 wingtiptoys.com 전자 메일 주소로 다시 씁니다.
    
      - support@wingtiptoys.com으로 전송된 인바운드 메시지는 Wingtip Toys의 Edge 전송 서버에서 수락되고 다시 쓰여진 다음 support@contoso.com 전자 메일 주소로 라우팅됩니다.

맨 위로 이동

## 주소 다시 쓰기를 통해 수정되는 메시지 속성

표준 SMTP 전자 메일 메시지는 *메시지 봉투*와 메시지 내용으로 구성됩니다. 메시지 봉투에는 SMTP 메일 서버 간에 메시지를 전송 및 배달하는 데 필요한 정보가 있습니다. 메시지 내용에는 메시지 헤더 필드(통칭 *메시지 헤더*) 및 메시지 본문이 들어 있습니다. 메시지 봉투는 RFC 2821에 설명되어 있고 메시지 헤더는 RFC 2822에 설명되어 있습니다.

보낸 사람이 전자 메일 메시지를 작성하여 배달하도록 전송하는 경우 메시지에는 보낸 사람, 받는 사람, 메시지가 작성된 날짜 및 시간, 제목 줄(옵션) 및 메시지 본문(옵션) 등 SMTP 표준을 준수하는 데 필요한 기본 정보가 포함됩니다. 이러한 정보는 메시지 자체에 포함되어 있으며 정의에 따라 메시지 헤더에 있습니다.

보낸 사람의 메일 서버에서 메시지 헤더에 있는 보낸 사람과 받는 사람 정보를 사용하여 메시지의 메시지 봉투를 생성합니다. 그런 다음 받는 사람의 메일 서버로 배달할 수 있도록 인터넷에 메시지를 전송합니다. 메시지 봉투는 메시지 전송 프로세스에 의해 생성되며 실제로는 메시지의 일부가 아니기 때문에 받는 사람은 메시지 봉투를 볼 수 없습니다.

주소 다시 쓰기에서는 메시지 헤더 또는 메시지 봉투의 특정 필드를 다시 써서 전자 메일 주소가 변경됩니다. 주소를 다시 쓰면 아웃바운드 메시지에서는 여러 필드가 변경되지만 인바운드 전자 메일 메시지에서는 필드 하나만 변경됩니다. 다음 표에는 아웃바운드 메시지와 인바운드 메시지에서 다시 쓰여지는 SMTP 헤더 필드가 나와 있습니다.

### 아웃바운드 메시지와 인바운드 메시지에 다시 쓰여지는 메시지 필드

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>필드 이름</th>
<th>위치</th>
<th>아웃바운드 메시지</th>
<th>인바운드 메시지</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>MAIL FROM</strong></p></td>
<td><p>메시지 봉투</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="even">
<td><p><strong>RCPT TO</strong></p></td>
<td><p>메시지 봉투</p></td>
<td><p>다시 쓰여지지 않음</p></td>
<td><p>다시 쓰여짐</p></td>
</tr>
<tr class="odd">
<td><p><strong>To</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="even">
<td><p><strong>Cc</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="odd">
<td><p><strong>From</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="even">
<td><p><strong>Sender</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reply-To</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="even">
<td><p><strong>Return-Receipt-To</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="odd">
<td><p><strong>Disposition-Notification-To</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="even">
<td><p><strong>Resent-From</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
<tr class="odd">
<td><p><strong>Resent-Sender</strong></p></td>
<td><p>메시지 헤더</p></td>
<td><p>다시 쓰여짐</p></td>
<td><p>다시 쓰여지지 않음</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 주소 다시 쓰기에서 변경되지 않는 항목

주소 다시 쓰기에서는 수정 시 SMTP 기능이 중단되는 메시지 헤더 필드는 수정하지 않습니다. 예를 들어 특정 헤더 필드를 수정하면 라우팅 루프 검색이 영향을 받거나 서명이 무효화되거나 권한으로 보호된 메시지를 읽지 못하게 될 수 있습니다. 따라서 다음과 같은 헤더 필드는 주소 다시 쓰기를 통해 수정되지 않습니다.

  - **Return-Path**

  - **Received**

  - **Message-ID**

  - **X-MS-TNEF-Correlator**

  - **Content-Type Boundary=string**

  - MIME 본문 부분 내부에 있는 헤더 필드

주소 다시 쓰기에서는 Exchange 조직에서 제어하지 않는 도메인을 무시합니다. 즉, 주소를 다시 써도 Exchange 조직에서 신뢰할 수 없는 도메인이 포함된 헤더 필드는 다시 쓰지 않습니다. 이러한 도메인을 다시 쓰면 제어할 수 없는 형식의 메시지 릴레이가 수행되기 때문입니다.

또한 주소 다시 쓰기에서는 다른 메시지에 포함되어 있는 메시지의 헤더 필드를 수정하지 않습니다. 메시지가 보낸 사람과 받는 사람 간에 구현되는 전송 규칙을 트리거하지 않는 한 보낸 사람과 받는 사람은 포함된 메시지가 수정 없이 그대로 유지된 상태에서 배달되기를 원하기 때문입니다.

맨 위로 이동

## 아웃바운드 전용 주소 다시 쓰기 관련 고려 사항

Edge 전송 서버에서 아웃바운드 전용 주소 다시 쓰기를 수행하면 Exchange 조직에서 메시지를 보낼 때 보낸 사람의 전자 메일 주소가 수정됩니다. 단일 사용자(chris@contoso.com에서 support@contoso.com으로) 또는 단일 도메인의 모든 사용자(contoso.com에서 fabrikam.com으로)에 대해 아웃바운드 전용 주소 다시 쓰기를 구성할 수 있습니다. 여러 하위 도메인의 사용자에 대해서는 아웃바운드 전용 주소 다시 쓰기를 구성해야 합니다(\*.fabrikam.com에서 .contoso.com으로).

다시 쓴 전자 메일 주소는 해당되는 받는 사람에 대해 프록시 주소로 구성해야 합니다. 예를 들어 laura@sales.contoso.com을 laura@contoso.com으로 다시 쓴 경우 Laura의 사서함에서 프록시 주소 laura@contoso.com을 구성해야 합니다. 이렇게 하면 회신 및 인바운드 메시지가 올바르게 배달됩니다.

맨 위로 이동

## 인바운드 및 아웃바운드 주소 다시 쓰기 관련 고려 사항

Edge 전송 서버에서 인바운드 및 아웃바운드, 즉 *양방향* 주소 다시 쓰기를 수행하면 Exchange 조직에서 보내는 메시지의 보낸 사람 전자 메일 주소도 수정되고 Exchange 조직으로 들어오는 메시지의 받는 사람 전자 메일 주소도 수정됩니다.

단일 사용자(chris@contoso.com에서 support@contoso.com으로) 및 단일 도메인의 모든 사용자(contoso.com에서 fabrikam.com으로)에 대해서는 아웃바운드 전용 주소 다시 쓰기를 구성할 수 있습니다. 여러 하위 도메인의 사용자에 대해서는 양방향 주소 다시 쓰기를 구성할 수 없습니다(\*.fabrikam.com에서 contoso.com으로).

맨 위로 이동

## 여러 도메인의 전자 메일 주소 다시 쓰기 관련 고려 사항

여러 내부 도메인 또는 하위 도메인을 단일 외부 도메인으로 평면화할 때는 다음 요인을 고려해야 합니다.

  - **고유한 별칭 확인**   모든 전자 메일 별칭, 즉 @ 왼쪽 부분은 모든 하위 도메인에서 고유해야 합니다. 예를 들어 joe@sales.contoso.com이라는 주소가 있는 경우 joe@marketing.contoso.com이라는 주소가 있을 수 없습니다. 이 두 사용자에 대해 다시 쓴 전자 메일 주소는 모두 joe@contoso.com이 되기 때문입니다.

  - **프록시 주소 추가**   해당되는 도메인의 해당되는 모든 보낸 사람에 대해 다시 쓴 전자 메일 주소를 프록시 주소로 구성해야 합니다. 예를 들어 joe@sales.contoso.com을 joe@contoso.com으로 다시 쓰는 경우 프록시 주소 joe@contoso.com을 Joe의 사서함에 추가해야 합니다. 이렇게 하면 회신 및 인바운드 메시지가 올바르게 배달됩니다.

  - **Exchange가 아닌 조직의 메일 연락처**   Exchange가 아닌 전자 메일 시스템의 전자 메일 주소를 다시 쓰는 경우 Exchange가 아닌 전자 메일 시스템의 사용자를 표시하도록 Exchange에서 전자 메일 연락처를 만들어야 합니다. 이러한 전자 메일 연락처에는 원래 전자 메일 주소와 다시 쓴 전자 메일 주소가 포함되어야 합니다. 예를 들어 joe@unix.contoso.com을 joe@contoso.com으로 다시 쓰는 경우 joe@unix.contoso.com이 외부 전자 메일 주소이고 joe@contoso.com이 프록시 주소인 메일 연락처를 만들어야 합니다.

## 고유한 별칭 확인

여러 하위 도메인의 전자 메일 주소를 다시 쓸 때는 모든 전자 메일 별칭이 모든 하위 도메인에서 고유한지 확인해야 합니다. 예를 들어 다음 구성을 검토해 보겠습니다.

다음 사용자는 하위 도메인 sales.contoso.com, marketing.contoso.com 및 research.contoso.com에 있습니다.

  - maria@sales.contoso.com

  - chris@sales.contoso.com

  - david@marketing.contoso.com

  - brian@marketing.contoso.com

  - chris@research.contoso.com

  - adam@research.contoso.com

하위 도메인 sales.contoso.com, marketing.contoso.com 및 research.contoso.com을 단일 도메인 contoso.com으로 다시 쓴다고 가정하겠습니다.

각 하위 도메인의 전자 메일 주소를 다시 쓰면 chris@sales.contoso.com과 chris@research.contoso.com 두 전자 메일 주소가 모두 chris@contoso.com으로 다시 쓰여지기 때문 충돌이 발생합니다. 이러한 상황을 해결하려면 해당되는 받는 사람 중 하나의 전자 메일 주소를 변경해야 합니다. 예를 들어 chris@research.contoso.com을 christopher@research.contoso.com으로 변경하여 전자 메일 주소가 christopher@contoso.com으로 다시 쓰여지도록 할 수 있습니다.

맨 위로 이동

## 주소 다시 쓰기 항목의 우선 순위

사용자의 전자 메일 주소가 여러 주소 다시 쓰기 항목과 일치하는 경우에는 가장 근접한 일치 항목을 기준으로 전자 메일 주소를 한 번만 다시 씁니다. 다음 목록에서는 주소 다시 쓰기 항목의 우선 순위 순서를 가장 높은 우선 순위부터 차례로 설명합니다.

1.  **개별 전자 메일 주소**   주소 다시 쓰기 항목이 전자 메일 주소 john@contoso.com을 support@contoso.com으로 다시 쓰도록 구성됩니다.

2.  **도메인 또는 하위 도메인 매핑**   주소 다시 쓰기 항목이 모든 contoso.com 전자 메일 주소를 northwindtraders.com으로 다시 쓰거나 모든 sales.contoso.com 전자 메일 주소를 contoso.com으로 다시 쓰도록 구성됩니다.

3.  **도메인 평면화**   주소 다시 쓰기 항목이 \*.contoso.com 전자 메일 주소를 contoso.com으로 다시 쓰도록 구성됩니다.

예를 들어 Edge 전송 서버에서 다음 아웃바운드 주소 다시 쓰기 항목이 구성되어 있다고 가정해 보겠습니다.

  - \*.contoso.com 전자 메일 주소를 contoso.com으로 다시 씁니다.

  - japan.sales.contoso.com 전자 메일 주소를 contoso.jp로 다시 씁니다.

masato@japan.sales.contoso.com에서 전자 메일 메시지를 보내는 경우 주소가 masato@contoso.jp로 다시 쓰여집니다. 해당 항목이 보낸 사람의 전자 메일 주소와 가장 근접하게 일치하기 때문입니다.

맨 위로 이동

## 디지털 서명/암호화/권한으로 보호된 메시지

주소 다시 쓰기는 대부분의 서명된 메시지나 암호화된 메시지 또는 권한이 보호된 메시지에 영향을 미치지 않아야 합니다. 주소 다시 쓰기로 인해 이러한 유형의 메시지 보안 상태가 무효화되거나 변경되는 경우 주소 다시 쓰기가 적용되지 않습니다.

다음 값은 정보가 메시지 서명, 암호화 또는 권한 보호의 일부분이 아니므로 다시 쓸 수 있습니다.

  - 메시지 봉투의 필드

  - 최상위 메시지 본문 머리글

다음 값은 정보가 메시지 서명, 암호화 또는 권한 보호의 일부분이므로 다시 쓰여지지 않습니다.

  - 서명할 수 있는 MIME 본문 부분 내부에 있는 헤더 필드

  - MIME 콘텐츠 형식의 경계 문자열 매개 변수

맨 위로 이동

