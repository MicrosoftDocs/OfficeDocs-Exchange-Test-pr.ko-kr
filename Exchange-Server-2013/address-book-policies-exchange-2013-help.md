---
title: '주소록 정책: Exchange 2013 Help'
TOCTitle: 주소록 정책
ms:assetid: d0a916a1-e3ed-49ae-b116-a559be0dcce6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529948(v=EXCHG.150)
ms:contentKeyID: 50484212
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 주소록 정책

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-12-09_

전체 주소 목록 Outlook 및 Outlook Web App 에서 사용자 지정 된 Gal을 특정 그룹으로 분할 하는 방법에 대해 알아봅니다.

전체 주소 목록 (gal 전체) 분할 (로 알려져 *GAL 분리*)은 관리자가 해당 조직의 GAL의 사용자 지정된 보기를 제공 하는 특정 모집단으로 사용자를 분리할 수가 하는 프로세스입니다. 주소록 정책 (Abp)을 사용 하면 조직의 전체 주소 목록 (gal 전체)의 사용자 지정된 보기를 제공 하는 특정 그룹으로 세그먼트 사용자에 게 할 수 있습니다. ABP를 만들 때 정책에는 GAL, 오프 라인 주소록 (OAB), 방 목록 및 하나 이상의 주소 목록을 할당 합니다. 그런 다음 Outlook과 Outlook Web App 에서 사용자 지정 된 GAL에 access와 함께 제공 되는 사서함 사용자에 게는 ABP를 할당할 수 있습니다. 여러 Gal을 필요로 하는 온-프레미스 조직에 대해 GAL 분할을 수행 하는 간단한 메커니즘을 제공 하는 목표를 둡니다. .


> [!NOTE]
> ABP의 용도는 사용자들이 조직에서 서로를 보거나 다른 사용자와 통신하기 어렵게 만드는 것이 아니라 각 사용자 그룹에 맞게 GAL 및 주소 목록을 최적화하는 것입니다. ABP는 실질적 분리가 아니라 디렉터리 관점에서 사용자를 가상으로 분리합니다.



**목차**

How ABPs work

ABP example

Entourage, Outlook for Mac, and ABPs

## ABP의 작동 방식

ABP에는 다음과 같은 목록이 포함되어 있습니다.

  - GAL 하나

  - OAB 하나

  - 대화방 목록 하나(예약 목적)

  - 주소 목록 하나 이상

다음 그림에서 주소록 정책 A는 그림의 아래쪽에 표시되어 있는 조직에 있는 다양한 주소 개체의 하위 집합으로 구성됩니다. ABP의 최종 범위는 정책에 포함된 GAL(이 경우 GAL1)의 범위와 동일합니다. ABP를 만들어 사용자에게 할당하면 ABP에 포함된 주소 개체가 사용자가 볼 수 있는 개체 범위가 됩니다.

![주소록 정책 개요](images/Hh529948.68084064-7319-431b-be3b-0cce761258b1(EXCHG.150).gif "주소록 정책 개요")

다음과 같은 방법을 사용하여 개별 사서함 사용자에게 ABP를 할당할 수 있습니다.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>새 사서함 또는 기존 사서함?</th>
<th>셸</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>새 사서함</p></td>
<td><p><em>AddressBookPolicy</em> 매개 변수가 있는 <a href="https://technet.microsoft.com/ko-kr/library/aa997663(v=exchg.150)">New-Mailbox</a> cmdlet</p></td>
</tr>
<tr class="even">
<td><p>기존 사서함</p></td>
<td><p><em>AddressBookPolicy</em> 매개 변수가 있는 <a href="https://technet.microsoft.com/ko-kr/library/bb123981(v=exchg.150)">Set-Mailbox</a> cmdlet</p>
<p></p></td>
</tr>
</tbody>
</table>


Abp은 사용자의 클라이언트 응용 프로그램에 연결 하는 클라이언트 액세스 서버에서 Exchange 2013 때 적용이 됩니다. ABP를 변경 하는 경우 업데이트 된 ABP Exchange 2013 사서함 서버에 대 한 RPC 클라이언트 액세스 서버를 다시 시작 하거나 사용자를 다시 시작 하거나 해당 클라이언트를 다시 연결 될 때까지 영향을 미치지 않습니다.

## 주소록 정책 라우팅 에이전트

Abp를 사용 하지 않는 한 Exchange 조직에 다음과 같은 작업 Outlook 또는 Outlook Web App 에서 전자 메일은 만들어지고 Exchange 조직에서 다른 받는 사람에 게 전송 하는 경우 발생 합니다.

1.  전자 메일 주소를 확인합니다. 예를 들어 **받는 사람** 필드에 **kweku@contoso.com**을 입력하면 SMTP 전자 메일 주소가 사용자의 표시 이름인 **Kweku Ako-Adjei**로 확인됩니다.

2.  다른 사용자의 대화 상대 카드를 볼 수 있습니다. 이름이 확인되고 나면 사용자 이름을 두 번 클릭하여 사무실 및 전화 번호 등의 연락처 정보를 확인할 수 있습니다.

ABP를 사용하고 있고 서로 다른 가상 조직의 사용자가 서로의 개인 정보를 보지 못하도록 하려면 주소록 정책 라우팅 에이전트를 설정하면 됩니다. ABP 라우팅 에이전트는 조직에서 받는 사람을 확인하는 방법을 제어하는 전송 에이전트입니다. ABP 라우팅 에이전트를 설치 및 구성하면 서로 다른 GAL에 할당된 사용자는 외부 받는 사람의 대화 상대 카드를 볼 수 없으므로 외부 받는 사람으로 표시됩니다.

Exchange Online 에서 ABP 라우팅 에이전트를 설정 하는 방법에 대 한 자세한 내용은, [주소록 정책 \[Online\] 라우팅 설정](https://technet.microsoft.com/ko-kr/library/jj891095\(v=exchg.150\))을 참조 하십시오.

Exchange Server에서 ABP 라우팅 에이전트를 설정하는 방법에 대한 자세한 내용은 [주소 주소록 정책 라우팅 에이전트 설치 및 구성](install-and-configure-the-address-book-policy-routing-agent-exchange-2013-help.md)을 참조하십시오.

## ABP 예

다음 다이어그램에서 Fabrikam과 Tailspin Toys는 동일한 Exchange 조직과 동일한 CEO를 공유합니다. CEO는 두 회사에 공통인 유일한 직원입니다.

![두 회사 한 CEO](images/Hh529948.c87a5654-d456-4688-acb2-0be15ba1cda6(EXCHG.150).gif "두 회사 한 CEO")

이 구성에는 세 개의 ABP가 있습니다.

  - Fabrikam 직원 및 CEO를 포함하는 ABP

  - Tailspin Toys 직원과 CEO를 포함하는 ABP

  - CEO만 포함하는 ABP

ABP는 다음 규칙을 따릅니다.

  - Tailspin Toys의 사용자는 GAL을 찾아볼 때 Tailspin Toys 직원과 CEO만 볼 수 있습니다.

  - Fabrikam의 사용자는 GAL을 찾아볼 때 Fabrikam 직원과 CEO만 볼 수 있습니다.

  - CEO는 GAL을 찾아볼 때 모든 Fabrikam 직원과 Tailspin Toys 직원을 볼 수 있습니다.

  - CEO의 그룹 구성원 자격을 보는 사용자는 자신의 회사에 속한 그룹만 볼 수 있고 다른 회사에 속한 그룹은 볼 수 없습니다.

## Entourage, Outlook for Mac 및 ABP

Abp은 Entourage 사용자 또는 해당 회사 네트워크에 연결 된 Mac 사용자를 위한 Outlook에 대해 작동 하지 않습니다. 회사 네트워크 내에 있을 때 Entourage 및 Mac 클라이언트에 대 한 Outlook에 직접 연결 글로벌 카탈로그 서버와 Active Directory 쿼리는 클라이언트 액세스 서버를 사용 하는 대신 직접 합니다. 그러나 인터넷에서 연결 하는 Mac 2011 클라이언트에 대 한 Outlook는 OAB 또는 Exchange 웹 서비스 (EWS)를 사용할 수 있습니다. 이러한 클라이언트는 GAL을 검색할 수는 결과적으로, 할당 된 ABP.에 따라 Outlook for Mac 2011을 관리 하는 방법에 대 한 자세한 내용은 Outlook for Mac 2011에 대 한 계획[](https://go.microsoft.com/fwlink/p/?linkid=231878)

## 자세한 내용

[시나리오: 주소록 정책 배포](scenario-deploying-address-book-policies-exchange-2013-help.md)

Exchange Online의 [주소록 정책 절차 \[온라인\] 주소](https://technet.microsoft.com/ko-kr/library/jj891096\(v=exchg.150\))

