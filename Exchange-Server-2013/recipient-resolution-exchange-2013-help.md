---
title: '받는 사람 확인: Exchange 2013 Help'
TOCTitle: 받는 사람 확인
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 52058049
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람 확인

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-03-17_

*받는 사람 확인*은 메시지의 모든 받는 사람을 확장 및 확인하는 프로세스입니다. 받는 사람 확인 작업에서는 Microsoft Exchange 조직의 해당하는 Active Directory 개체에 받는 사람을 일치시킵니다. 받는 사람 확장을 수행하면 모든 메일 그룹이 개별 받는 사람 목록으로 확장됩니다. 받는 사람 확인을 통해 메시지 제한 및 대체 받는 사람을 각 받는 사람에게 올바르게 적용할 수 있습니다.

Microsoft Exchange Server 2013 조직에서는 사서함 서버의 전송 서비스 분류기를 통해 받는 사람 확인이 수행됩니다. 새로 도착한 메시지가 전송 큐에 배치되고 나면 각 메시지에 대한 분류가 수행됩니다. 받는 사람 확인은 내용 변환 및 라우팅과 함께 메시지가 배달 큐에 배치되기 전에 수행됩니다. 분류기는 라우팅을 수행하기 전에 받는 사람 확인을 수행합니다. 받는 사람 확인을 수행하는 분류기 구성 요소를 보통 *해결 프로그램*이라고도 합니다.

**목차**

Top-level resolution

Expansion

Bifurcation and controlling recipient expansion

Recipient resolution diagnostics

## 최상위 확인

*최상위 확인*은 받는 사람 확인의 첫 단계로, 이 과정에서는 받는 메시지의 각 받는 사람이 Active Directory의 일치하는 받는 사람 개체에 연결됩니다. 최상위 확인 중에 분류기는 메시지 내에 있는 확장되지 않은 초기 받는 사람 전자 메일 주소와 보낸 사람이 포함된 목록을 만듭니다. 그런 다음 분류기는 해당 전자 메일 주소 목록을 사용하여 Active Directory를 쿼리해 전자 메일 주소 특성이 일치하는 메일 사용이 가능한 개체를 찾습니다. 일치하는 항목이 발견되면 나중에 사용할 수 있도록 일치하는 Active Directory 개체의 속성이 캐시되며 모든 보낸 사람 메시지 제한도 적용됩니다.

## 받는 사람 전자 메일 주소

최상위 확인은 메시지 및 *메시지 봉투*에 있는 확장되지 않은 초기의 받는 사람 목록으로 시작됩니다. 메시지 봉투에는 SMTP 메시징 서버 사이에서 메시지를 전송할 때 사용되는 명령이 포함됩니다. 보낸 사람의 전자 메일 주소는 **MAIL FROM:**  명령에 포함되어 있습니다. 각 받는 사람의 전자 메일 주소는 개별 **RCPT TO:**  명령에 포함되어 있습니다. 봉투 보낸 사람과 봉투 받는 사람은 보통 메시지 헤더의 `To:`, `From:`, `Cc:` 및 `Bcc:` 헤더 필드에서 만들어집니다. 그러나 항상 그런 것은 아닙니다. 메시지의 `To:`, `From:`, `Cc:` 및 `Bcc:` 헤더 필드는 쉽게 위조할 수 있으며 메시지를 전송하는 데 사용된 실제 보낸 사람 또는 받는 사람 전자 메일 주소와 일치하지 않을 수도 있습니다.

## 캡슐화된 전자 메일 주소

표준 SMTP 전자 메일 주소는 chris@contoso.com과 같이 RFC 2821 및 RFC 2822의 규격을 따릅니다. 그러나 전자 메일 주소는 유효한 SMTP 주소에 캡슐화된 비 SMTP 전자 메일 주소일 수도 있습니다. Exchange는 IMCEA(Internet Mail Connector Encapsulated Address) 캡슐화 방법을 사용하는 캡슐화된 주소를 지원합니다.

이 캡슐화 방법을 사용하려면 SMTP 전자 메일 주소에서 무효인 모든 문자를 인코딩해야 합니다. 영숫자, 등호(=) 및 하이픈(-)에는 인코딩이 필요 없고, 나머지 문자에는 다음 인코딩 구문이 사용됩니다.

  - 슬래시( / )는 밑줄( \_ )로 바뀝니다.

  - 기타 US-ASCII 문자는 더하기 기호(+)로 바뀌며 두 자리의 해당 ASCII 값은 16진수로 기록됩니다. 예를 들어 공백의 인코딩된 값은 `+20`입니다.

IMCEA 캡슐화 방식에서는 다음 구문을 사용합니다. `IMCEA<Type>-<address>@<domain>`

\<*Type*\> 자리 표시자는 `EX`, `X400` 또는 `FAX`와 같은 비 SMTP 주소 유형을 식별합니다.


> [!NOTE]
> 이론적으로는 &lt;<EM>Type</EM>&gt;에 대해 <CODE>SMTP</CODE> 및 <CODE>X500</CODE>도 올바른 값이지만, Exchange 받는 사람 확인 과정에서 이러한 유형을 사용하며 IMCEA로 인코딩된 주소는 거부됩니다.



\<*address*\> 자리 표시자는 인코딩된 원래 주소입니다. \<*domain*\> 자리 표시자는 contoso.com 같은 비 SMTP 주소를 캡슐화하는 데 사용되는 SMTP 도메인을 나타냅니다.

IMCEA 캡슐화 방식을 사용하는 경우 도메인이 Exchange 조직의 신뢰할 수 있는 기본 도메인과 일치하는 경우에만 주소의 캡슐화가 해제됩니다. 허용 도메인에 대한 자세한 내용은 [허용 도메인](accepted-domains-exchange-2013-help.md)를 참조하십시오.

Exchange에서 SMTP 전자 메일 주소의 최대 길이는 571자입니다. 이 제한에는 다음이 포함됩니다.

  - 주소의 이름 부분: 315자

  - 도메인 이름: 255자

  - 주소의 이름 부분과 도메인 이름을 구분하는 @ 문자

Exchange에서는 주소의 이름 부분이 315자를 넘으면 전체 전자 메일 주소가 571자보다 짧아도 IMCEA 캡슐화 방식을 사용하여 인코딩된 메시지가 지원되지 않습니다.

## 주소 확인

각 메시지에 대해 보낸 사람 전자 메일 주소와 모든 받는 사람 전자 메일 주소가 Active Directory를 쿼리하는 데 사용되는 목록에 추가됩니다. 그리고 캡슐화된 주소의 경우 전자 메일 주소 목록에 추가되기 전에 캡슐화가 해제됩니다. Active Directory 쿼리는 한 번에 최대 20개의 전자 메일 주소에 대해 수행됩니다. Active Directory 쿼리에서 일시적인 오류가 발견되면 메시지는 전송 큐로 반환되며, Microsoft Exchange Transport Service와 연결된 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML 응용 프로그램 구성 파일의 *ResolverRetryInterval* 키로 지정된 시간 동안 지연됩니다. 기본값은 30분입니다.

다음 표에서는 Active Directory에 있는 받는 사람 개체에 대해 설명합니다. Exchange 받는 사람 유형에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)를 참조하십시오.

### Active Directory의 받는 사람 개체

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Active Directory 받는 사람 유형</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DistributionGroup</p></td>
<td><p>메일 사용 가능 그룹 개체. 메일 그룹 개체 유형은 다음과 같습니다.</p>
<ul>
<li><p><strong>MailUniversalDistributionGroup</strong>   유니버설 메일 그룹 개체</p></li>
<li><p><strong>MailUniversalSecurityGroup</strong>   전자 메일 주소가 있는 USG(유니버설 보안 그룹) 개체</p></li>
<li><p><strong>MailNonUniversalGroup</strong>   전자 메일 주소가 있는 로컬 보안 그룹 개체 또는 글로벌 보안 그룹 개체</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DynamicDistributionGroup</p></td>
<td><p>Active Directory 클래스 <strong>msExchDynamicDistributionList</strong>가 있는 개체. 자세한 내용은 <a href="https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/manage-dynamic-distribution-groups">동적 메일 그룹 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>Mailbox</p></td>
<td><p>전자 메일 주소와 정의된 <em>Database</em> 매개 변수가 있는 사용자 개체</p></td>
</tr>
<tr class="even">
<td><p>MailUser</p></td>
<td><p>전자 메일 주소에 정의된 <em>Database</em> 매개 변수가 없는 사용자 개체. 자세한 내용은 <a href="https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-mail-users">메일 사용자 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="odd">
<td><p>MailContact</p></td>
<td><p>전자 메일 주소가 있는 연락처 개체. 보통 메일 연락처는 Exchange 조직 외부에 있는 받는 사람에 대해 사용됩니다. 또한 크로스 포리스트 Exchange 환경에도 사용됩니다. 자세한 내용은 <a href="https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-mail-contacts">메일 연락처 관리</a>를 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>MailPublicFolder</p></td>
<td><p>전자 메일 주소가 있는 공용 폴더 개체</p></td>
</tr>
<tr class="odd">
<td><p>MicrosoftExchangeRecipient</p></td>
<td><p>Active Directory 클래스 <strong>msExchExchangeServerRecipient</strong>가 있는 개체. Microsoft Exchange 받는 사람 개체에 대한 자세한 내용은 <a href="recipients-exchange-2013-help.md">받는 사람</a>을 참조하십시오.</p></td>
</tr>
<tr class="even">
<td><p>SystemAttendantMailbox</p></td>
<td><p>Active Directory 클래스 <strong>exchangeAdminService</strong>가 있는 개체. Exchange 조직에는 시스템 수행자 사서함이 하나만 있어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>SystemMailbox</p></td>
<td><p>전자 메일 주소가 있으며 Microsoft Exchange System Objects 컨테이너에 있는 사용자 개체. Exchange 조직의 각 사서함 데이터베이스에는 시스템 사서함이 하나만 있어야 합니다.</p></td>
</tr>
</tbody>
</table>


주요 속성이 없거나 잘못된 개체는 Active Directory 쿼리에서 잘못된 개체로 분류됩니다. 예를 들어 전자 메일 주소가 없는 동적 메일 그룹 개체는 잘못된 개체로 간주됩니다. 잘못된 개체로 분류된 받는 사람에게 메시지를 보내면 NDR(배달 못 함 보고서)이 생성됩니다.

각 전자 메일 주소에 대해 단일 초기 쿼리가 받는 사람 식별자, 받는 사람 유형, 메시지 제한, 전자 메일 주소, 대체 받는 사람 등 가능한 모든 받는 사람 속성에 대해 수행됩니다. 그리고 받는 사람에 대해 적용 가능한 속성은 나중에 사용할 수 있도록 캐시됩니다. 받는 사람 확인 과정에서는 받는 사람이 확인되는 방법의 유사성 및 적용 가능한 받는 사람 속성의 유사성을 기준으로 받는 사람을 분류합니다.

주소 확인에 사용되는 LDAP 필터는 다음과 같이 설명할 수 있습니다.

  - **EX** 전자 메일 주소 유형의 경우 LDAP 필터는 받는 사람의 **legacyExchangeDN** Active Directory 특성이나 받는 사람의 **proxyAddresses** Active Directory 특성을 기준으로 합니다. **legacyExchangeDN** Active Directory 특성이 우선합니다.

  - 다른 모든 전자 메일 주소 유형의 경우에는 받는 사람의 **proxyAddresses** Active Directory 특성이 LDAP 필터로 사용됩니다.

메시지에 사용된 전자 메일 주소가 해당 Active Directory 개체의 기본 SMTP 주소와 일치하지 않으면 분류기가 기본 SMTP 주소와 일치하도록 메시지에 전자 메일 주소를 다시 씁니다. 원래 전자 메일 주소는 메시지 봉투의 **RCPT TO:**  명령에 있는 `ORCPT=` 항목에 저장됩니다.

## 보낸 사람 메시지 제한

보낸 사람 메시지 크기 제한에 사용되는 크기는 메시지 헤더의 **X-MS-Exchange-Organization-OriginalSize:**  헤더 필드 값입니다. Exchange에서는 이 헤더 필드를 사용하여 메시지가 Exchange 조직에 들어갈 때의 원본 메시지 크기를 기록합니다. 해당 메시지를 지정된 메시지 크기 제한과 비교하여 검사할 때는 항상 현재 메시지 크기 또는 원본 메시지 크기 헤더 중 더 작은 값이 사용됩니다. 내용 변환, 인코딩, 에이전트 처리 등으로 인해 메시지의 크기는 변경될 수 있습니다. 이 헤더 필드는 없는 경우 현재 메시지 크기 값을 사용하여 만들어집니다. 메시지 크기가 너무 크면 NDR이 생성되며 추가 메시지 처리가 중지됩니다.

보낸 사람/받는 사람 제한은 메시지를 처리하는 첫 번째 사서함 서버의 전송 서비스에서만 적용됩니다. 확장되지 않은 원본 메시지 봉투의 받는 사람 수를 보낸 사람/받는 사람 제한과 비교합니다. 확장되지 않은 원본 메시지 봉투의 받는 사람 수는 중첩된 메일 그룹에서 원격 확장 서버를 사용한 경우 Microsoft Exchange Server 2003에서 발생하는 부분적인 메시지 배달 문제를 방지하는 데 사용됩니다.

메시지의 확장 속성을 스탬프 처리하면 메시지 보낸 사람과 모든 받는 사람을 확인된 사람으로 표시합니다. 메시지에 대해 받는 사람 확인을 다시 수행해야 하는 경우 이 확장 속성을 사용하면 메시지는 최상위 확인을 무시합니다. Microsoft Exchange Transport Service가 다시 시작되는 경우 메시지에 대해 받는 사람 확인을 다시 수행해야 할 수 있습니다.

맨 위로 이동

## 확장

확장은 최상위 확인 이후에 수행되며 중첩된 수준의 받는 사람을 개별 받는 사람으로 완전히 확장합니다. 모든 받는 사람을 확장하려면 확장 프로세스를 여러 번 수행해야 할 수 있습니다. 모든 받는 사람을 확장해야 하는 것은 아니지만 모든 받는 사람에 대해 확장 프로세스를 수행해야 합니다. 또한 확장 프로세스에서는 모든 종류의 받는 사람에 대해 받는 사람 메시지 제한이 적용됩니다.

다음 목록에서는 확장해야 하는 받는 사람 종류에 대해 설명합니다.

  - **메일 그룹 및 동적 메일 그룹**   메일 그룹은 **memberOf** Active Directory 속성을 기반으로 확장됩니다. 그리고 동적 메일 그룹은 Active Directory 쿼리 정의를 사용하여 확장됩니다. 그룹에 대해 *ExpansionServer* 매개 변수가 설정된 경우에는 현재 서버에 의해 그룹이 확장되지 않습니다. 이러한 메일 그룹은 확장을 위해 지정된 서버로 라우팅됩니다.
    

    > [!NOTE]
    > 조직의 특정 전송 서버를 확장 서버로 선택하면 메일 그룹의 사용은 확장 서버의 가용성에 따라 좌우됩니다. 확장 서버를 사용할 수 없으면 메일 그룹으로 전송되는 모든 메시지를 배달할 수 없습니다. 메일 그룹에 대해 특정 확장 서버를 사용하여 서비스 중단 위험을 줄이려는 경우 이러한 서버에 대해 고가용성 솔루션을 구현하는 것을 고려해야 합니다.



  - **대체 받는 사람**   *ForwardingAddress* 매개 변수가 사서함 및 메일 사용이 가능한 공용 폴더에 대해 설정되어 있을 수 있습니다. *ForwardingAddress* 매개 변수는 모든 메시지를 지정된 대체 받는 사람으로 리디렉션합니다. 이를 *전달된 받는 사람*이라고 합니다. *ForwardingAddress* 매개 변수에 대체 배달 주소가 지정되어 있고 *DeliverToMailboxAndForward* 매개 변수가 `$true`로 설정되어 있으면 메시지가 원래 받는 사람 및 대체 받는 사람에게 배달됩니다. 이를 *배달 및 전달된 받는 사람*이라고 합니다.

  - **연락처 체인**   *연락처 체인*은 *ExternalEmailAddress* 매개 변수가 Exchange 조직에 있는 다른 받는 사람의 전자 메일 주소로 설정된 메일 사용자 또는 메일 연락처입니다.

## 받는 사람 루프 검색

메일 그룹, 다른 받는 사람 및 연락처 체인을 확장하면 분류기가 *받는 사람 루프*를 확인합니다. 받는 사람 루프는 동일한 받는 사람에게 끊임 없이 메시지가 배달되는 받는 사람 구성 문제입니다. 다음 목록에서는 여러 유형의 받는 사람 루프에 대해 설명합니다.

  - **무해한 받는 사람 루프**   무해한 받는 사람 루프가 발생하면 메시지가 배달됩니다. 다음 목록에서는 무해한 받는 사람 루프가 발생하는 두 가지 시나리오를 설명합니다.
    
      - 두 메일 그룹이 서로를 구성원으로 포함하는 경우.
    
      - 사서함 또는 메일 사용 가능 공용 폴더가 서로 간에 배달 및 전달이 이루어지도록 설정된 경우. 두 받는 사람의 *DeliverToMailboxAndForward* 매개 변수가 모두 `$true`로 설정되어 있고 *ForwardingAddress* 매개 변수를 서로에게로 설정한 경우에 이 상황이 발생합니다.
    
    무해한 받는 사람 루프가 검색되면 메시지는 받는 사람에게 배달되지만 해당 메시지를 동일한 받는 사람에게 배달하기 위한 추가 시도는 발생하지 않습니다.

  - **중단된 받는 사람 루프**   중단된 받는 사람 루프가 발생하면 메시지가 배달되지 않습니다. 중단된 받는 사람 루프의 예로는 사서함이나 메일 사용이 가능한 공용 폴더의 *ForwardingAddress* 매개 변수가 서로에게로 설정되어 있는 경우입니다. 분류기가 중단된 받는 사람 루프를 검색하면 현재 받는 사람에 대한 확장 작업이 중지되고 해당 받는 사람에 대해 NDR이 생성됩니다.

받는 사람 루프가 검색되어도 메시지가 중복 배달될 수 있습니다. 예를 들어 다음 조건에 해당하는 경우 메일 그룹 C에는 메시지가 중복 배달됩니다.

  - 메일 그룹 B 및 메일 그룹 C가 메일 그룹 A의 구성원인 경우.

  - 메일 그룹 C도 메일 그룹 B의 구성원인 경우.

## 메일 그룹에 대한 배달 보고서 리디렉션

메일 그룹이 확장되면 메시지가 배달 보고서 메시지인지를 확인하기 위해 메시지 유형을 검사합니다. 해당 메시지가 배달 보고서이면 메일 그룹의 리디렉션 설정을 검사하여 배달 보고서를 리디렉션해야 하는지를 확인합니다. 배달 보고서를 사용하는 경우 메일 그룹 및 해당 구성원에 대한 원치 않는 정보가 공개될 수도 있으므로 배달 보고서를 생략할 수 있습니다.

다음 목록에서는 메일 그룹 및 동적 메일 그룹에 사용할 수 있는 배달 보고서 리디렉션 설정에 대해 설명합니다.

  - **ReportToManagerEnabled**   이 매개 변수를 사용하면 배달 보고서를 메일 그룹 관리자에게 보낼 수 있습니다. 유효한 값은 `$true` 또는 `$false`입니다. 기본값은 `$false`입니다. 메일 그룹의 경우 관리자는 **Set-Group** cmdlet의 *ManagedBy* 매개 변수에 의해 제어됩니다. 그리고 동적 메일 그룹의 경우 관리자는 **Set-DynamicDistributionGroup** cmdlet의 *ManagedBy* 매개 변수에 의해 제어됩니다.

  - **ReportToOriginatorEnabled**   이 매개 변수를 사용하면 이 메일 그룹으로 전송된 전자 메일 메시지의 보낸 사람에게 배달 보고서를 보낼 수 있습니다. 유효한 값은 `$true` 또는 `$false`입니다. 기본값은 `$true`입니다.
    

    > [!NOTE]
    > <EM>ReportToManagerEnabled</EM> 매개 변수와 <EM>ReportToOriginatorEnabled</EM> 매개 변수의 값이 모두 <CODE>$true</CODE>일 수는 없습니다. 한 매개 변수를 <CODE>$true</CODE>로 설정하면 다른 매개 변수는 <CODE>$false</CODE>로 설정해야 합니다. 그러나 두 매개 변수의 값을 모두 <CODE>$false</CODE>로 설정할 수는 있습니다. 그러면 모든 배달 보고서 메시지를 리디렉션하지 않습니다.



다음 목록에서는 사용 가능한 배달 보고서 메시지에 대해 설명합니다.

  - **DR(배달 확인)**   이 보고서는 메시지가 해당 받는 사람에게 배달되었음을 확인합니다.

  - **DSN(배달 상태 알림)**   이 보고서는 메시지 배달 시도의 결과를 설명합니다. DSN 메시지에 대한 자세한 내용은 [Exchange 2013의 Dsn 및 Ndr](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md)을 참조하십시오.

  - **MDN(메시지 처리 알림)**   이 보고서는 메시지를 받는 사람에게 배달한 후의 상태를 설명합니다. MDN 메시지의 예로는 RN(읽음 알림) 및 NRN(읽지 않음 알림)이 있습니다. MDN 메시지는 RFC 2298에 정의되어 있으며 메시지 헤더의 **Disposition-Notification-To:**  헤더 필드에 의해 제어됩니다. `Disposition-Notification-To:` 헤더 필드를 사용하는 MDN 설정은 다양한 메시지 서버와 호환됩니다. Microsoft Outlook 및 Exchange의 MAPI 속성을 사용하여 MDN 설정을 정의할 수도 있습니다.

  - **NDR(배달 못 함 보고서)**   이 보고서는 메시지를 받도록 지정된 사람에게 메시지를 배달하지 못했음을 메시지 보낸 사람에게 알립니다.

  - **NRN(읽지 않음 알림)**   이 보고서는 메시지를 읽지 않고 삭제했음을 나타냅니다.

  - **OOF(부재 중)**   이 보고서는 받는 사람이 전자 메일 메시지에 응답하지 않을 것임을 나타냅니다. 이 보고서의 약어인 OOF는 초기 Microsoft 메시징 시스템에서 유래했는데, 예전에는 이 알림의 이름이 "Out of Facility"였습니다.

  - **RN(읽음 알림)**   이 보고서는 메시지를 읽었음을 나타냅니다.

  - **회수 보고서**   이 보고서는 해당 받는 사람에 대한 회수 요청 상태를 나타냅니다. 회수 요청이란 보낸 사람이 Outlook을 사용하여 보낸 메시지를 회수하려는 것을 나타냅니다.

배달 보고서 메시지를 메일 그룹으로 보낼 때 다음과 같이 설정되어 있으면 보고서 메시지가 삭제됩니다.

  - 보고서 리디렉션이 설정되어 있지 않거나 메시지 보낸 사람으로 설정되어 있는 경우

  - 보고서 리디렉션이 메일 그룹 관리자로 설정되어 있고 배달 보고서 메시지가 NDR이 아닌 경우.

배달 보고서 메시지를 메일 그룹으로 보낼 때 배달 보고서 메시지가 메일 그룹 관리자에게 배달될 수 있습니다. 보고서 리디렉션이 메일 그룹 관리자로 설정되어 있고 보고서 메시지가 NDR인 경우 이 작업이 수행됩니다.

배달 보고서 메시지가 아닌 메시지를 메일 그룹으로 보내면 해당 메시지는 메일 그룹 구성원에게 배달됩니다. 다음 목록에는 보고서 요청 설정이 요약되어 있습니다.

  - 보고서 리디렉션을 메시지 보낸 사람으로 설정하면 보고서 요청 설정이 수정되지 않습니다.

  - 보고서 리디렉션을 설정하지 않으면 모든 보고서 요청 설정은 생략됩니다. `NOTIFY=NEVER` 항목이 메시지 봉투의 각 받는 사람에 대한 **RCPT TO:** 에 추가됩니다.

  - 보고서 리디렉션을 메일 그룹 관리자로 설정하면 메일 그룹 관리자에게 보내는 NDR 메시지를 제외한 모든 보고서 요청 설정이 생략됩니다.

## 받는 사람에 대한 메시지 제한

확장 프로세스에서는 받는 사람에 대해 구성된 메시지 제한도 적용됩니다. 이러한 제한은 각 받는 사람에 대해 개별적으로 구성할 수도 있고 Exchange 조직의 모든 허브 전송 서버에 대해 조직 차원에서 구성할 수도 있습니다. 다음 표에서는 받는 사람에 대해 구성되는 메시지 제한에 대해 설명합니다.

### 받는 사람에 대한 메시지 제한

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>원본</th>
<th>매개 변수</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p>
<p><strong>Set-TransportConfig</strong></p></td>
<td><p><em>MaxReceiveSize</em></p></td>
<td><p><em>MaxReceiveSize</em> 매개 변수는 받는 사람에 대해 구성되는 메시지 제한에 사용할 크기를 메시지 헤더의 <strong>X-MS-Exchange-Organization-OriginalSize:</strong> 헤더 필드 값으로 지정합니다. Exchange에서는 이 헤더 필드를 사용하여 메시지가 Exchange 조직에 들어갈 때의 원본 메시지 크기를 기록합니다. 해당 메시지를 지정된 메시지 크기 제한과 비교하여 검사할 때는 항상 현재 메시지 크기 또는 원본 메시지 크기 헤더 중 더 작은 값이 사용됩니다. 내용 변환, 인코딩, 에이전트 처리 등으로 인해 메시지의 크기는 변경될 수 있습니다. 이 헤더 필드는 없는 경우 현재 메시지 크기 값을 사용하여 만들어집니다. 메시지 크기가 너무 크면 NDR이 생성되며 추가 메시지 처리가 중지됩니다.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em></p></td>
<td><p><em>RequireSenderAuthenticationEnabled</em> 매개 변수의 경우 받는 사람에게 보내는 모든 메시지는 인증된 보낸 사람이 전송한 것이어야 합니다. 이 매개 변수의 값을 <code>$true</code>로 설정하면 인증되지 않은 보낸 사람이 전송한 메시지는 거부됩니다. 시스템(System) 및 시스템 수행자(System Attendant) 사서함으로 메시지를 보내는 모든 사람은 인증된 사람이어야 합니다.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-DistributionGroup</strong></p>
<p><strong>Set-DynamicDistributionGroup</strong></p>
<p><strong>Set-Mailbox</strong></p>
<p><strong>Set-MailContact</strong></p>
<p><strong>Set-MailPublicFolder</strong></p>
<p><strong>Set-MailUser</strong></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em></p>
<p><em>RejectMessagesFromSendersOrMembers</em></p></td>
<td><p><em>AcceptMessagesOnlyFromSendersOrMembers</em> 매개 변수는 해당 구성원이 받는 사람에게 메시지를 보내도록 허용되는 메일 그룹 또는 보낸 사람을 지정합니다. 이 매개 변수는 이전에 사용되었던 <em>AcceptMessagesOnlyFrom</em> 및 <em>AcceptMessagesOnlyFromDLMembers</em> 매개 변수의 기능을 동시에 제공합니다.</p>
<p><em>RejectMessagesFromSendersOrMembers</em> 매개 변수는 해당 구성원이 받는 사람에게 메시지를 보내도록 허용되지 않는 메일 그룹 또는 보낸 사람을 지정합니다. 이 매개 변수는 이전에 사용되었던 <em>RejectMessagesFrom</em> 및 <em>RejectMessagesFromDLMembers</em> 매개 변수의 기능을 동시에 제공합니다.</p>
<p>분류기는 두 단계에 걸쳐 받는 사람 권한을 검사합니다. 첫 번째 단계에서는 보낸 사람이 <em>AcceptOnlyMessagesFromSendersOrMembers</em> 또는 <em>RejectMessagesFromSendersOrMembers</em> 매개 변수에 있는지를 확인합니다. 이 두 매개 변수에 보낸 사람이 없는 경우 이들 매개 변수에 있는 메일 그룹이 완전히 확장됩니다. 이와 같이 메일 그룹을 완전히 확장하려면 시간이 조금 걸릴 수 있습니다. 그러므로 이들 매개 변수의 중첩된 메일 그룹 수준을 최소화하는 것이 좋습니다.</p></td>
</tr>
</tbody>
</table>


인증된 보낸 사람이 발송하는 특정 유형의 메시지에는 제한이 적용되지 않습니다. 다음 목록에서는 받는 사람 제한이 적용되지 않는 메시지에 대해 설명합니다.

  - **Microsoft Exchange 받는 사람이 보내는 모든 메시지** 이러한 메시지에는 DSN 메시지, 저널 보고서, 할당량 메시지 및 내부 메시지 보낸 사람에게 전송되는 기타 시스템 생성 메시지가 포함됩니다. Microsoft 받는 사람에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)을 참조하십시오.

  - **외부 전자 메일 관리자 주소를 통해 보내는 모든 메시지** 이러한 메시지에는 DSN 메시지 및 외부 메시지 보낸 사람에게 발송되는 기타 시스템 생성 메시지가 포함됩니다. 외부 전자 메일 관리자 주소에 대한 자세한 내용은 [외부 전자 메일 관리자 주소를 구성 합니다.](configure-the-external-postmaster-address-exchange-2013-help.md)를 참조하십시오.

특정 유형의 메시지는 Exchange 조직에서 외부 도메인으로 보내는 경우 차단됩니다. 설정은 **Set-RemoteDomain** cmdlet의 다음 매개 변수에 의해 제어됩니다.

  - *AllowedOOFType*

  - *AutoForwardEnabled*

  - *AutoReplyEnabled*

  - *DeliveryReportEnabled*

  - *NDREnabled*

자세한 내용은 [원격 도메인](remote-domains-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 받는 사람 확장 분기 및 제어

받는 사람 확인 과정에서는 전체 메시지 받는 사람 목록이 확장 및 확인되므로 같은 메시지에 대해 복사본을 여러 개 만들어야 하는 경우가 있습니다. 다음 시나리오에서 이러한 경우를 설명합니다.

  - **메시지 받는 사람이 서로 다른 메시지 설정을 필요로 하는 경우**   일부 받는 사람에게는 읽음 확인 등의 메시지 속성을 사용하도록 설정해야 하고 나머지 받는 사람에게는 해당 속성을 차단해야 하는 경우가 있습니다. 이러한 경우를 위해 원본 메시지와 속성이 약간 다른 새 버전의 메시지를 만드는 작업을 *분기*라고 합니다.

  - **단일 메시지의 봉투 받는 사람 수를 제한해야 하는 경우**   대규모 메일 그룹을 확장하는 경우에는 받는 사람 확장 프로세스에서 매우 많은 수의 개별 받는 사람을 생성할 수 있습니다. Exchange에서는 매우 많은 수의 봉투 받는 사람이 있는 메시지 복사본을 하나만 만드는 대신 봉투 받는 사람의 수가 제한되어 있는 동일한 메시지의 복사본을 여러 개 만듭니다.

## 분기

다음 조건에 해당하는 경우 받는 사람 확인 과정에서 메시지 분기가 수행됩니다.

  - 메시지 봉투의 **MAIL FROM:** 에 있는 메시지 보낸 사람을 업데이트하는 경우. 예로는 메일 그룹의 *ReportToManagerEnabled* 매개 변수 값이 `$true`인 경우가 있습니다.

  - DSN, OOF 메시지, 회수 보고서 등의 자동 응답 메시지를 생략해야 하는 경우.

  - 다른 받는 사람을 확장하는 경우.

  - **Resent-From:**  헤더 필드를 메시지 헤더에 추가해야 하는 경우. Resent 헤더 필드는 메시지가 특정 사용자에 의해 전달되었는지 여부를 확인하는 데 사용할 수 있는 정보 헤더 필드입니다. 그리고 Resent 헤더 필드는 메시지가 원래 보낸 사람이 직접 보낸 것처럼 받는 사람에게 나타나도록 하는 데 사용됩니다. 받는 사람은 메시지 헤더을 보고 메시지를 전달한 사람을 알 수 있습니다. Resent 헤더 필드는 RFC 2822의 3.6.6 섹션에 정의되어 있습니다.

  - 메일 그룹 확장 기록을 전송해야 하는 경우.

## 받는 사람 확장 제어

확장된 받는 사람의 수가 너무 많으면 분류기가 메시지를 여러 복사본으로 분할합니다. 이 작업은 메시지 확장 중에 시스템 리소스 사용을 줄이기 위해 수행됩니다. 한 메시지에 대한 최대 봉투 받는 사람 수는 `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` 응용 프로그램 구성 파일의 *ExpansionSizeLimit* 키에 의해 제어됩니다. 기본값은 1000입니다.


> [!WARNING]
> 프로덕션 환경의 Exchange 전송 서버에서는 <EM>ExpansionSizeLimit</EM> 키의 값을 수정하지 않는 것이 좋습니다.



맨 위로 이동

## 받는 사람 확인 진단

받는 사람 확인에 대 한 보고 및 진단 정보는 성능 카운터 및 메시지 추적 로그 항목에서 제공 됩니다. 이러한 원본 식별 하 고 받는 사람 확인 된 문제를 진단할 수 있습니다.

## 받는 사람 확인 성능 카운터

다음 표에서는 받는 사람 확인에 사용할 수 있는 성능 카운터에 대해 설명합니다.

### 받는 사람 확인 성능 카운터

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>카운터 이름</th>
<th>표시 이름</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AmbiguousRecipientsTotal</p></td>
<td><p>Ambiguous Recipients</p></td>
<td><p>받는 사람 확인 중에 검색된 모호한 받는 사람의 총 수입니다. 모호한 받는 사람은 <strong>legacyExchangeDN</strong> Active Directory 특성 또는 <strong>proxyAddresses</strong> Active Directory 특성이 일치하는 서로 다른 받는 사람입니다.</p></td>
</tr>
<tr class="even">
<td><p>AmbiguousSendersTotal</p></td>
<td><p>Ambiguous Senders</p></td>
<td><p>받는 사람 확인 중에 검색된 모호한 보낸 사람 수입니다. 모호한 보낸 사람은 <strong>legacyExchangeDN</strong> Active Directory 특성 또는 <strong>proxyAddresses</strong> Active Directory 특성이 일치하는 서로 다른 보낸 사람입니다.</p></td>
</tr>
<tr class="odd">
<td><p>FailedRecipientsTotal</p></td>
<td><p>Failed Recipients</p></td>
<td><p>받는 사람 확인 중에 검색된 실패한 받는 사람 수입니다.</p></td>
</tr>
<tr class="even">
<td><p>LoopRecipientsTotal</p></td>
<td><p>Loop Recipients</p></td>
<td><p>받는 사람 루프로 인해 받는 사람 확인에 실패한 받는 사람 수입니다.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesChippedTotal</p></td>
<td><p>Messages Chipped</p></td>
<td><p>단일 메시지의 봉투 받는 사람 수를 제어하기 위해 받는 사람 확인 중에 만들어지는 동일한 메시지의 총 복사본 수입니다. Exchange에서는 이 프로세스를 <em>치핑(chipping)</em>이라고 합니다.</p></td>
</tr>
<tr class="even">
<td><p>MessagesCreatedTotal</p></td>
<td><p>Messages Created</p></td>
<td><p>받는 사람 확인 중에 만들어진 메시지 수입니다.</p></td>
</tr>
<tr class="odd">
<td><p>MessagesRetriedTotal</p></td>
<td><p>Messages Retried</p></td>
<td><p>받는 사람 확인 중에 다시 시도하도록 예약된 메시지 수입니다.</p></td>
</tr>
<tr class="even">
<td><p>UnresolvedOrgRecipientsTotal</p></td>
<td><p>Unresolved Org Recipients</p></td>
<td><p>받는 사람 확인 중에 검색된, 신뢰할 수 있는 도메인에서 온 확인되지 않은 받는 사람 수입니다.</p></td>
</tr>
<tr class="odd">
<td><p>UnresolvedOrgSendersTotal</p></td>
<td><p>Unresolved Org Senders</p></td>
<td><p>받는 사람 확인 중에 검색된, 신뢰할 수 있는 도메인에서 온 확인되지 않은 보낸 사람 수입니다.</p></td>
</tr>
</tbody>
</table>


## 메시지 추적 로그의 받는 사람 확인 이벤트

다음 표에서는 메시지 추적 로그에 기록되는 받는 사람 확인 이벤트에 대해 설명합니다.

### 메시지 추적 로그의 받는 사람 확인 이벤트

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>메시지 추적 이벤트</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EXPAND</p></td>
<td><p>이 이벤트는 메일 그룹이 확장되었음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p>REDIRECT</p></td>
<td><p>이 이벤트는 사서함 받는 사람이나 메일 사용이 가능한 공용 폴더 받는 사람에게 보낸 메시지가 <em>ForwardingAddress</em> 매개 변수에서 지정된 대체 받는 사람에게 리디렉션되었음을 나타냅니다.</p></td>
</tr>
<tr class="odd">
<td><p>RESOLVE</p></td>
<td><p>이 이벤트는 받는 사람의 전자 메일 주소가 해당 Active Directory 받는 사람 개체의 기본 SMTP 전자 메일 주소로 변경되었음을 나타냅니다.</p></td>
</tr>
<tr class="even">
<td><p>TRANSFER</p></td>
<td><p>이 이벤트는 메시지 분기나 치핑이 수행되었음을 나타냅니다.</p></td>
</tr>
</tbody>
</table>


메시지 추적에 대한 자세한 내용은 [메시지 추적](message-tracking-exchange-2013-help.md)를 참조하십시오.

