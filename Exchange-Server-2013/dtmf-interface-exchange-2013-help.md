---
title: 'DTMF 인터페이스: Exchange 2013 Help'
TOCTitle: DTMF 인터페이스
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54651784
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DTMF 인터페이스

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

UM(통합 메시징)에서 발신자는 터치톤이라고도 하는 DTMF(복합 주파수 부호) 또는 음성 입력을 사용하여 시스템과 상호 작용할 수 있습니다. 발신자가 사용할 수 있는 방법은 UM 다이얼 플랜 및 자동 전화 교환이 구성된 방식에 따라 다릅니다.

DTMF 인터페이스는 발신자가 다이얼 플랜에 구성된 Outlook Voice Access 번호 또는 자동 전화 교환에 구성된 전화 번호로 전화를 걸 때 전화 키패드를 사용하여 사용자를 찾고 UM 음성 메일 메뉴 시스템을 탐색할 수 있도록 합니다. 이 항목에서는 DTMF 인터페이스에 대해 설명하고 발신자가 이 인터페이스를 사용하여 사용자를 찾고 UM 음성 메일 메뉴 시스템을 탐색하는 방법에 대해 설명합니다.

**목차**

DTMF overview

UM dial plans and dial by name

DTMF maps

DTMF maps for users who aren't enabled for Unified Messaging

DTMF maps for users who are enabled for Unified Messaging

For more information

## DTMF 개요

DTMF에서 발신자는 통합 메시징 메뉴 옵션에 해당하는 전화 키패드의 키를 누르거나 키의 문자로 사용자 이름이나 전자 메일 별칭을 눌러 해당 이름이나 별칭을 입력해야 합니다. 발신자는 ARS(자동 음성 인식)가 사용할 수 없게 설정되었거나 음성 명령을 사용하려고 했으나 실패했기 때문에 DTMF를 사용할 수 있습니다. 이러한 경우 메뉴를 탐색하고 사용자를 검색하는 데 DTMF 입력이 사용됩니다.

기본적으로 UM에서 DTMF 입력은 다이얼 플랜에 사용되며 UM 자동 전화 교환에 대한 기본 발신자 인터페이스입니다.

발신자는 다음과 같은 경우에 DTMF 입력을 사용할 수 있습니다.

  - Outlook Voice Access를 사용한 다이얼 플랜 전화 접속 액세스

  - 사용자를 찾기 위한 다이얼 플랜 디렉터리 조회 및 검색

  - 음성 사용이 가능하지 않은 자동 전화 교환

  - DTMF 대체 자동 전화 교환이 구성되었거나 구성되지 않은 음성 사용이 가능한 자동 전화 교환

  - DTMF 대체 자동 전화 교환(음성 사용 불가능)

## UM 다이얼 플랜 및 이름으로 전화 걸기

UM 다이얼 플랜을 만들 때 발신자가 사용자를 검색하거나 사용자에게 연락하려고 할 때 이름을 조회하는 데 사용할 기본 및 보조 입력 방법을 구성할 수 있습니다. 이러한 설정은 다이얼 플랜의 **설정** 페이지에 있으며 **이름 검색 기본 방법** 및 **이름 검색 보조 방법**이라고 합니다. 이름 검색 기본 방법 및 이름 검색 보조 방법 둘 다에 대해 다음 옵션을 사용할 수 있습니다.

  - 성 이름

  - 이름 성

  - SMTP 주소

또한 이름 검색 보조 방법에서는 **없음** 옵션도 사용할 수 있습니다.

기본적으로 이름 검색 기본 방법으로는 **성 이름**이 선택되고 이름 검색 보조 방법으로는 **SMTP 주소**가 선택됩니다. 따라서 발신자가 UM 다이얼 플랜에 구성되어 있는 Outlook Voice Access 번호로 전화를 걸면 다이얼 플랜의 환영 메시지가 재생되고 교환원의 "안녕하세요. Contoso Outlook Voice Access입니다. 사서함에 액세스하려면 내선 번호를 입력하십시오. 다른 사람과 연결하려면 우물정자를 누르십시오."라는 음성 안내가 나옵니다. 발신자가 \# 키를 누르면 시스템에서 "통화하려는 사람의 이름을 성부터 입력하십시오. 전자 메일 별칭을 입력하려면 \# 키를 두 번 누르십시오."라고 응답합니다. 이 시나리오에서 다이얼 플랜의 구성 방식에 따라 시스템은 발신자에게 사용자의 성과 이름 순서로(성 먼저) 입력하거나 도메인 이름을 제외한 전자 메일 별칭을 입력하도록 음성으로 안내합니다. 예를 들어 사용자의 전자 메일 별칭이 tsmith@contoso.com이면 발신자는 tsmith를 입력합니다.

기본 설정이 요구에 맞지 않아 변경하려는 경우 발신자가 사용자의 전자 메일 별칭을 먼저 입력하거나 사용자의 이름과 성 순서로 입력할 수 있게 변경할 수 있습니다. 이러한 경우에는 **이름 검색 기본 방법**에는 **SMTP 주소**를, **이름 검색 보조 방법**에는 **이름 성** 설정을 구성할 수 있습니다. 이름으로 전화 걸기 방법에 대한 설정은 다이얼 플랜과 관련된 모든 UM 자동 전화 교환에도 적용됩니다. 발신자가 DTMF 입력이나 전화 키패드의 키를 사용하여 사용자의 이름을 입력할 수 있게 하려면 사용자의 DTMF 맵 및 값이 조직 디렉터리 내에 있어야 합니다.

UM 다이얼 플랜에서 이름으로 전화 걸기 기본 방법 및 보조 방법을 변경하는 방법에 대한 자세한 내용은 [Outlook Voice Access 사용자가 검색할 수에 대 한 기본 방식으로 구성](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md) 및 [Outlook Voice Access 사용자가 검색할 수에 대 한 보조 방법 구성](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md)을 참조하십시오.

맨 위로 이동

## DTMF 맵

Exchange 조직에서 **msExchUMDtmfMap** 특성은 디렉터리에서 만들어지는 각 사용자와 연결됩니다. 이 특성은 통합 메시징에서 사용자의 이름, 성 및 전자 메일 별칭을 숫자 집합에 매핑하는 데 사용됩니다. 이러한 매핑을 DTMF 맵이라고 합니다. DTMF 맵을 사용하면 발신자가 사용자 이름이나 전자 메일 별칭 문자에 해당하는 전화 키패드의 숫자를 입력할 수 있습니다. 이 특성은 사용자의 이름과 성, 사용자의 성과 이름 및 사용자의 전자 메일 별칭에 대한 DTMF 맵을 만드는 데 필요한 값을 포함합니다.

다음 표에서는 이름이 Tony Smith이고 별칭이 tsmith@contoso.com인 UM 사용 가능 사용자의 **msExchUMDtmfMap** 특성에 대해 Active Directory에 저장되는 DTMF 맵 값을 보여줍니다.

**이름이 Tony Smith인 UM 사용 가능 사용자에 대해 저장되는 DTMF 값**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>디렉터리 항목</th>
<th>사용자 이름</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>tonysmith</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>smithtony</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>tsmith</p></td>
</tr>
</tbody>
</table>


이름과 전자 메일 별칭은 쉼표, 하이픈, 밑줄 또는 마침표와 같은 영숫자 이외의 문자를 포함할 수 있습니다. 사용자의 DTMF 맵에는 이러한 문자가 사용되지 않습니다. 예를 들어 Tony Smith의 전자 메일 별칭이 tony-smith@contoso.com이면 DTMF 맵 값은 866976484가 되고 하이픈은 포함되지 않습니다. 그러나 사용자의 전자 메일 별칭에 tonysmith123@contoso.com과 같이 숫자가 하나 이상 포함되어 있는 경우 해당 숫자는 만들어진 DTMF 맵에서 사용됩니다. tonysmith123의 DTMF 맵은 866976484123이 될 수 있습니다.

발신자가 사용자의 이름이나 전자 메일 별칭을 입력하려면 해당 사용자의 DTMF 맵이 있어야 합니다. 그러나 사용자 계정에 DTMF 맵이 연결되지 않는 사용자도 있습니다.

맨 위로 이동

## 통합 메시징을 사용할 수 없는 사용자의 DTMF 맵

사서함 사용 가능 사용자를 비롯한 사용자는 기본적으로 통합 메시징을 사용할 수 없도록 설정되어 있습니다. **msExchUMDtmfMap** 특성에는 UM을 사용할 수 없는 사용자의 DTMF 맵에 필요한 값이 채워집니다. 기본적으로 모든 사용자에 대해 사서함을 만들면 다음과 같은 DTMF 맵이 만들어집니다.

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

사용자의 계정에 대해 DTMF 맵 값이 정의되어 있지 않으면 발신자가 UM 자동 전화 교환 메뉴에서 전화 키를 누르거나 디렉터리 검색을 수행할 때 해당 사용자에게 연결할 수 없습니다. 또한 UM 사용 가능 사용자는 ASR(자동 음성 인식)을 사용할 수 없는 경우 DTMF 맵이 없는 사용자에게 메시지를 보내거나 통화를 전송할 수 없습니다. 발신자가 전화 키패드를 사용하여 통화를 전송하거나 UM 사용이 가능하지 않은 사용자에게 연결할 수 있게 하려면 해당 사용자의 DTMF 맵에 대해 필요한 값을 만들어야 합니다. **Set-User** cmdlet에 *-CreateDtmfMap* 매개 변수를 사용하여 단일 사용자의 DTMF 맵을 만들고 업데이트할 수 있으며 DTMF 맵이 이미 만들어진 후에 사용자 이름이 변경된 경우 사용자의 DTMF 맵을 업데이트할 수 있습니다. 필요에 따라 이 cmdlet을 사용하여 Exchange 관리 셸 스크립트를 만들어 여러 사용자의 DTMF 맵 값을 업데이트할 수 있습니다.

**Set-User** cmdlet에 대한 자세한 내용은 [Set-User](https://technet.microsoft.com/ko-kr/library/aa998221\(v=exchg.150\))를 참조하십시오.

맨 위로 이동

## 통합 메시징을 사용할 수 있는 사용자의 DTMF 맵

기본적으로는 사용자가 통합 메시징을 사용할 수 있도록 설정하면 해당 사용자에 대해 DTMF 맵이 만들어집니다. 이 맵은 외부 발신자, UM을 사용할 수 없는 사용자 및 전화 키패드를 사용하여 사용자 이름이나 전자 메일 별칭을 입력하는 기타 UM 사용 가능 사용자로부터 UM 사용 가능 사용자에게 통화가 전송될 수 있도록 합니다.

UM 사용 가능 사용자에 대해 DTMF 맵 값이 만들어지면 발신자는 디렉터리 검색 기능을 사용할 수 있습니다. 발신자는 다음과 같은 상황에서 전화 키패드를 사용할 때 디렉터리 검색을 사용합니다.

  - Outlook Voice Access 번호로 전화를 걸 때 사용자를 식별하거나 검색하는 경우

  - UM 자동 전화 교환으로 전화를 걸 때 UM 사용 가능 사용자를 찾거나 이러한 사용자에게 통화를 전송하는 경우

사용자가 통합 메시징을 사용할 수 있도록 설정하는 방법에 대한 자세한 내용은 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

사용자가 UM을 사용할 수 있도록 설정된 후 사용자의 이름, 성 또는 전자 메일 별칭이 변경될 수 있습니다. 사용자의 DTMF 맵 값은 자동으로 업데이트되지 않습니다. 발신자가 사용자의 새 이름이나 전자 메일 별칭을 입력했는데 해당 이름이나 전자 메일 별칭 변경 내용을 반영하도록 사용자의 DTMF 맵이 업데이트되지 않은 경우, 발신자는 디렉터리에서 해당 사용자를 찾거나 해당 사용자에게 메시지를 보내거나 통화를 전송할 수 없게 됩니다. 사용자가 UM을 사용할 수 있도록 설정된 후 해당 사용자의 DTMF 맵을 업데이트해야 할 경우 **Set-User** cmdlet에 *-CreateDtmfMap* 매개 변수를 사용할 수 있습니다. 또한 여러 명의 UM 사용 가능 사용자의 DTMF 맵을 업데이트하려는 경우 이 cmdlet을 사용하여 Exchange 관리 셸 스크립트를 만들 수 있습니다.


> [!WARNING]
> ADSI 편집과 같은 도구를 사용하면 구성이 불일치하거나 기타 오류가 발생할 수 있으므로 이러한 도구로 사용자의 DTMF 값을 수동으로 변경하지 않는 것이 좋습니다. <STRONG>Set-UMService</STRONG> cmdlet 또는 <STRONG>Set-User</STRONG> cmdlet만 사용하여 사용자의 DTMF 맵을 만들거나 업데이트하는 것이 좋습니다.



## 자세한 내용

[Adsiedit 개요 (영문)](https://go.microsoft.com/fwlink/p/?linkid=73175)

