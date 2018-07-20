---
title: '관리 역할 이해 (영문): Exchange 2013 Help'
TOCTitle: 관리 역할 이해 (영문)
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 50483582
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 관리 역할 이해 (영문)

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

관리 역할은 Microsoft Exchange Server 2013에서 사용되는 RBAC(역할 기반 액세스 제어) 권한 모델의 일부입니다. 역할은 사서함, 전송 규칙 및 받는 사람과 같이 Exchange 2013 구성 요소의 구성을 보거나 수정할 수 있는 권한을 제공하기 위해 결합되는 cmdlet의 논리 그룹으로 작동합니다. 관리 역할은 기능 영역과 받는 사람 구성을 관리하는 데 사용되는 관리 역할 그룹과 관리 역할 할당 정책이라는 더 큰 그룹으로 추가로 결합될 수 있습니다. 역할 그룹과 역할 할당 정책은 각각 관리자와 최종 사용자에게 권한을 할당합니다. 관리 역할 그룹 및 관리 역할 할당 정책에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 이 항목에서는 고급 RBAC 기능에 대해 중점적으로 설명합니다. EAC(Exchange 2013 관리 센터)를 사용하여 구성원을 역할 그룹에 추가 및 역할 그룹에서 제거, 역할 그룹 생성과 수정 또는 역할 할당 정책 생성과 수정과 같은 기본 Exchange 권한을 관리하려면, <A href="permissions-exchange-2013-help.md">사용 권한</A>를 참조하세요.



**목차**

Built-in management roles

Unscoped top-level management roles

Custom management roles

Management role hierarchy

Management role entries

Unscoped top-level role entries

Management role types

For more information

관리 역할 범위 및 관리 역할 할당은 관리 역할 작업의 중요한 구성 요소입니다. 이러한 구성 요소에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

관리 역할과 관련된 관리 작업에 대한 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md)을 참조하십시오.

## 기본 제공 관리 역할

Exchange 2013은 조직 관리에 사용할 수 있는 다수의 기본 제공 관리 역할을 제공합니다. 각 역할에는 사용자가 특정 Exchange 구성 요소를 관리하는 데 필요한 cmdlet과 매개 변수가 포함되어 있습니다. 몇 가지 기본 제공 관리 역할의 예는 다음과 같습니다.

  - **메일 받는 사람**   관리자가 사서함, 연락처 및 메일 사용자를 관리할 수 있습니다.

  - **전송 규칙**   역할이 할당된 관리자 또는 전문가 사용자가 전송 규칙 기능을 관리할 수 있습니다.

  - **메일 그룹**   역할이 할당된 관리자 또는 전문가 사용자가 메일 그룹 및 메일 그룹 구성원을 관리할 수 있습니다.

  - **MyPersonalInformation**   최종 사용자가 자신의 집 전화 번호와 웹 사이트 주소를 수정할 수 있습니다.

Exchange 2013에 포함된 관리 역할의 전체 목록을 보려면 [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)을 참조하십시오.

Exchange 2013과 함께 제공되는 기본 제공 역할을 가져와서 원하는 대로 결합하여 비즈니스에 적합한 권한 모델을 만들 수 있습니다. 예를 들어 특정 역할 그룹의 구성원이 받는 사람 및 공용 폴더를 관리하도록 하려면 해당 역할 그룹에 메일 받는 사람 역할과 공용 폴더 역할을 모두 할당합니다. 역할은 대개 역할 그룹이나 역할 할당 정책에 할당합니다. 권한을 더 세부적으로 제어하고자 하는 경우에는 사용자에게 직접 관리 역할을 할당할 수도 있습니다. 권한 모델을 간소화하려면 사용자 역할에 직접 권한을 할당하는 것보다 역할 그룹과 역할 할당 정책을 사용하는 것이 좋습니다.


> [!NOTE]
> 최종 사용자 관리 역할은 역할 할당 정책에만 할당할 수 있습니다.



기본 제공 관리 역할은 변경할 수 없습니다. 하지만 기본 제공 관리 역할을 기반으로 관리 역할을 만든 다음 새 역할을 역할 그룹이나 역할 할당 정책에 할당할 수 있습니다. 그런 다음 필요에 따라 새 관리 역할을 변경할 수 있습니다. 이 작업은 수행 빈도가 매우 낮은 고급 작업입니다.

기본 제공 Exchange 역할을 기반으로 사용자 지정 역할을 만드는 방법에 대한 자세한 내용은 이 항목 뒷부분에 나오는 Custom Management Roles을 참조하십시오.

관리 역할이 작동하도록 하려면 먼저 관리 역할을 할당해야 합니다. 관리 역할은 대개 역할 그룹 및 역할 할당 정책에 할당합니다. 상황에 따라 역할을 직접 사용자에 할당할 수도 있지만, 이는 수행 빈도가 매우 낮은 고급 작업입니다.

관리 역할 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [역할 할당 정책 관리](manage-role-assignment-policies-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

관리 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 범위가 지정되지 않은 최상위 관리 역할

범위가 지정되지 않은 최상위 관리 역할은 RBAC를 사용하는 사용자에게 사용자 지정 스크립트 및 비 Exchange cmdlet에 대한 액세스 권한을 부여할 수 있게 해주는 특수한 관리 역할 유형입니다. 일반 관리 역할은 Exchange cmdlet에 대한 액세스 권한만 제공합니다. Exchange 서버에서 실행되는 비 Exchange cmdlet에 대한 액세스 권한을 제공하거나 사용자가 실행할 수 있는 스크립트를 게시해야 하는 경우에는, 이러한 권한과 스크립트를 범위가 지정되지 않은 역할에 추가해야 합니다. 범위가 지정되지 않은 역할을 다른 부모 역할에서 파생하지 않고 만들면 부모가 없고 Exchange 2013에서 제공하는 기본 제공 관리 역할과 동위를 이루므로 최상위 역할이라고 합니다. 범위가 지정되지 않은 최상위 역할 항목을 만들고자 함을 나타내려면 **New-ManagementRole** cmdlet에 *UnscopedTopLevel* 스위치를 사용해야 합니다.

범위가 지정되지 않은 역할이라는 이름은 일반 관리 역할과 달리 특정 대상으로 범위를 지정할 수 없으므로 지어진 것입니다. 범위가 지정되지 않은 역할은 항상 조직 전체에 적용됩니다. 즉, 범위가 지정되지 않은 역할이 할당된 사람은 Exchange 2013 조직에서 어느 개체든 수정할 수 있습니다. 따라서 범위가 지정되지 않은 역할을 통해 사용할 수 있게 되는 스크립트와 cmdlet을 철저하게 테스트하여 이들을 통해 수정될 내용을 파악해야 하며, 범위가 지정되지 않은 역할을 신중하게 할당해야 합니다.

범위가 지정되지 않은 역할은 역할 그룹, 관리 역할, 사용자 및 USG(유니버설 보안 그룹)와 같은 역할 담당자에게 할당할 수 있습니다. 관리 역할 할당 정책에는 범위가 지정되지 않은 역할을 할당할 수 없습니다.

Exchange cmdlet을 범위가 지정되지 않은 역할의 관리 역할 항목으로 추가할 수는 없지만 역할 항목으로 추가된 스크립트에 포함할 수는 있습니다. 따라서 Exchange 작업을 수행하는 사용자 지정 스크립트를 만들고 해당 작업을 사용자에게 할당할 수 있습니다. 유용한 시나리오의 예를 들면, 사용자가 일반적인 관리 수준을 벗어나는 특별한 권한이 필요한 작업을 수행해야 하며 새 관리 역할이나 역할 그룹을 만들기가 곤란한 경우입니다. 이 특정 기능을 수행하는 스크립트를 만들어 범위가 지정되지 않은 역할에 추가한 다음 범위가 지정되지 않은 역할을 사용자에게 할당할 수 있습니다. 그러면 사용자는 스크립트로 제공되는 특정 기능만 수행할 수 있습니다.

범위가 지정되지 않은 역할에 추가하는 역할 항목도 범위가 지정되지 않은 최상위 역할 항목으로 지정해야 합니다. 범위가 지정되지 않은 최상위 역할 항목에 대한 자세한 내용은 이 항목 뒷부분에 나오는 Unscoped Top-Level Role Entries을 참조하십시오.

조직 관리 역할 그룹에는 기본적으로 범위가 지정되지 않은 역할 그룹을 만들거나 관리할 권한이 없습니다. 이는 범위가 지정되지 않은 역할 그룹을 실수로 만들거나 수정하는 일을 방지하기 위한 조치입니다. 조직 관리 역할 그룹은 범위가 지정되지 않은 역할 관리의 관리 역할을 자신이나 다른 역할 담당자에게 위임할 수 있습니다. 범위가 지정되지 않은 최상위 관리 역할을 만드는 방법에 대한 자세한 내용은 [범위가 지정되지 않은 역할 만들기](create-an-unscoped-role-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 사용자 지정 관리 역할

기본 제공 관리 역할이 사용자의 요구에 맞지 않을 경우에는 기본 제공 Exchange 역할을 기반으로 사용자 지정 관리 역할을 만들 수 있습니다. 사용자 지정 관리 역할을 만들면 새로운 자식 역할이 부모 역할의 모든 관리 역할 항목을 상속받습니다. 그런 다음 사용자 지정 관리 역할에 남겨 둘 관리 역할 항목을 선택하고 원하지 않는 항목은 모두 제거할 수 있습니다.

사용자 지정 역할은 새 역할을 만드는 데 사용되는 역할의 자식이 됩니다. 부모 역할에도 존재하는 관리 역할 항목만 새 자식 역할에서 사용할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 나오는 다음 섹션을 참조하십시오.

  - Management Role Hierarchy

  - Management Role Entries

사용자 지정 관리 역할을 만들려면 여러 단계를 거쳐야 하며, 수행 빈도가 매우 낮은 고급 작업을 수행해야 합니다. 사용자 지정 관리 역할을 만들기 전에 기존의 기본 제공 관리 역할 중에서 필요한 권한을 제공하는 것이 없는지 확인하십시오. 기본 제공 관리 역할에 대한 자세한 내용을 보거나 사용자 지정 관리 역할을 만들려면 다음 항목을 참조하십시오.

  - [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)

  - [고급 사용 권한](advanced-permissions-exchange-2013-help.md)

관리 역할을 만드는 방법에 대한 자세한 내용은 [역할 만들기](create-a-role-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 관리 역할 계층

관리 역할은 부모 및 자식 계층에 존재합니다. 계층의 최상위에는 Exchange 2013에서 제공하는 기본 제공 관리 역할이 있습니다. 역할을 만들면 부모 역할의 복사본이 만들어집니다. 새 역할은 복사한 원래 역할의 자식입니다. 그런 다음 역할을 할당하려는 관리자나 사용자의 요구에 맞게 새 역할을 사용자 지정할 수 있습니다.

사용자 지정된 역할을 사용하여 역할을 만들 수 있습니다. 기존 사용자 지정 역할에서 역할을 만들면 기존 사용자 지정 역할은 부모 역할의 자식으로 남아 있으면서 동시에 새 역할의 부모가 됩니다. 역할을 복사할 때마다 새 자식 역할은 바로 위 부모 역할에 있는 역할 항목만 포함할 수 있습니다.

각 관리 역할에는 변경할 수 없는 역할 유형이 지정됩니다. 역할 유형은 역할에 대한 기본 사용 컨텍스트를 정의합니다. 역할 유형은 자식 역할이 만들어질 때 부모 역할에서 복사됩니다.

**관리 역할 계층**

![RBAC 관리 역할 계층 구조 다이어그램](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "RBAC 관리 역할 계층 구조 다이어그램")

위의 그림은 여러 관리 역할의 계층적 관계를 보여 줍니다. Mail Recipients 및 Help Desk 역할은 기본 제공 역할입니다. 이러한 역할에서 파생된 모든 자식 역할은 각 기본 제공 역할의 역할 유형을 상속받습니다. 예를 들어 Mail Recipients 역할에서 직접 또는 간접적으로 파생된 모든 자식 역할은 `MailRecipients` 역할 유형을 상속받습니다.

Seattle Recipient Administrators 사용자 지정 역할은 메일 받는 사람 기본 제공 역할의 자식이지만 Seattle Sales Recipient Administrators 사용자 지정 역할과 Seattle Legal Recipient Administrators 사용자 지정 역할의 부모이기도 합니다. Seattle Recipient Administrators 사용자 지정 역할은 Mail Recipients 역할에서 사용할 수 있는 cmdlet의 일부만 포함합니다. Seattle Recipient Administrators 사용자 지정 역할의 자식 역할은 Seattle Recipient Administrators 사용자 지정 역할에도 있는 cmdlet만 포함할 수 있습니다. 예를 들어 특정 cmdlet이 Mail Recipients 역할에는 있지만 Seattle Recipient Administrators 사용자 지정 역할에는 없는 경우, Seattle Sales Recipient Administrators 사용자 지정 역할에 해당 cmdlet을 추가할 수 없습니다.

모든 사용자 지정 역할은 앞에서 설명한 역할과 같은 패턴을 따릅니다. 관리 역할에서 cmdlet에 대한 액세스를 제어하는 방법에 대한 자세한 내용은 이 항목의 다음에 나오는 Management Role Entries을 참조하십시오.

맨 위로 이동

## 관리 역할 항목

사용자 지정 Exchange 역할이든 범위가 지정되지 않은 역할이든, 모든 관리 역할에는 관리 역할 항목이 하나 이상 있어야 합니다. 항목은 cmdlet 하나와 해당 매개 변수, 스크립트 또는 사용하도록 허용할 특수 권한으로 구성됩니다. cmdlet 또는 스크립트가 관리 역할에 항목으로 나타나지 않으면 그 역할을 통해 해당 cmdlet 또는 스크립트에 액세스할 수 없습니다. 마찬가지로 매개 변수가 항목에 없으면 그 역할을 통해 해당 cmdlet 또는 스크립트의 매개 변수에 액세스할 수 없습니다.

Exchange 2013에서는 기본 제공 Exchange 관리 최상위 역할 기반의 역할 항목 및 범위가 지정되지 않은 최상위 관리 역할 기반의 역할 항목을 관리할 수 있습니다. 기본 제공 Exchange 최상위 역할 기반의 역할은 Exchange 2013 cmdlet인 역할 항목만 포함할 수 있습니다. 사용자가 사용할 수 있도록 사용자 지정 스크립트나 비 Exchange cmdlet을 추가하려면, 범위가 지정되지 않은 최상위 역할에 범위가 지정되지 않은 역할 항목으로 추가해야 합니다. 범위가 지정되지 않은 역할 항목에 대한 자세한 내용은 이 항목의 뒷부분에 나오는 Unscoped Top-Level Role Entries을 참조하십시오.

역할 항목이 Exchange cmdlet 기반 역할 항목이든 범위가 지정되지 않은 역할 항목이든, 모든 역할 항목은 다음 단원에서 설명하는 것과 동일한 원칙을 따릅니다.

역할 항목 관리에 대한 자세한 내용은 [관리 역할 및 역할 항목](management-roles-and-role-entries-exchange-2013-help.md)를 참조하십시오.

## 상위 및 하위 관리 역할 관계

앞에서 언급했듯이 cmdlet 및 매개 변수를 포함하는 관리 역할 항목이 바로 위의 부모 역할에 있어야만 해당 항목을 자식 역할에 추가할 수 있습니다. 예를 들어 부모 역할에 **New-Mailbox**에 대한 항목이 없는 경우에는 자식 역할에 그 cmdlet을 할당할 수 없습니다. 또한 **Set-Mailbox**가 부모 역할에 있지만 항목에서 *Database* 매개 변수를 제거한 경우에는 **Set-Mailbox** cmdlet의 *Database* 매개 변수를 자식 역할의 항목에 추가할 수 없습니다.

관리 역할 항목이 부모 역할에 나타나지 않으면 해당 항목을 자식 역할에 추가할 수 없으며 역할은 특정 역할 유형을 기반으로 하므로, 새 사용자 지정 역할을 만들 때에는 복사할 부모 역할을 신중하게 선택해야 합니다.

맨 위로 이동

## 관리 역할 항목 이름

관리 역할 항목 이름은 연결된 관리 역할과 cmdlet 또는 스크립트의 이름을 결합하여 만듭니다. 역할 이름과 cmdlet 또는 스크립트는 백슬래시 문자(\\)로 구분됩니다. 예를 들어 Mail Recipients 역할에 있는 **Set-Mailbox** cmdlet의 역할 항목 이름은 `Mail Recipients\Set-Mailbox`입니다. 역할 항목 이름에 공백이 있으면 이름을 큰따옴표(")로 묶습니다.

역할 항목 이름에 와일드카드 문자(\*)를 사용하면 입력한 내용과 일치하는 모든 역할 항목을 반환할 수 있습니다. 와일드카드 문자는 백슬래시 문자의 어느 쪽에나 사용할 수 있습니다. 다음 표에서는 역할 항목 이름에 와일드카드 문자를 사용하는 방법 몇 가지를 소개합니다.

**와일드카드 문자가 포함된 관리 역할 항목 이름**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>예</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>모든 역할에 대한 모든 역할 항목의 목록을 반환합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p><strong>Set-Mailbox</strong> cmdlet이 포함된 모든 역할 항목의 목록을 반환합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>Mail Recipients 역할에 있는 모든 역할 항목의 목록을 반환합니다.</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>Mail Recipients 역할에 있으면서 Mailbox로 끝나는 cmdlet이 포함된 모든 항목의 목록을 반환합니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>My로 시작하는 모든 역할에서 cmdlet 이름에 Group이라는 문자열이 포함된 모든 역할 항목의 목록을 반환합니다.</p></td>
</tr>
</tbody>
</table>


## 범위가 지정되지 않은 최상위 역할 항목

범위가 지정되지 않은 최상위 역할 항목은 범위가 지정되지 않은 최상위 관리 역할과 함께 사용자 지정 스크립트나 비 Exchange cmdlet 기반의 역할을 만드는 데 사용됩니다. 범위가 지정되지 않은 각 역할 항목은 단일 사용자 지정 스크립트나 비 Exchange cmdlet에 연결됩니다. 범위가 지정되지 않은 역할에 범위가 지정되지 않은 역할 항목을 만들고자 함을 나타내려면 **Add-ManagementRoleEntry** cmdlet에 *UnscopedTopLevel* 매개 변수를 지정해야 합니다.

범위가 지정되지 않은 역할 항목을 추가할 때에는 스크립트나 비 Exchange cmdlet과 함께 사용할 수 있는 모든 매개 변수를 지정해야 합니다. Exchange는 사용자가 역할 항목을 추가할 때 제공하는 매개 변수를 확인하려고 시도합니다. 범위가 지정되지 않은 역할이 할당된 사용자는 역할 항목을 만들 때 추가한 매개 변수만 사용할 수 있습니다. 스크립트나 비 Exchange cmdlet에 매개 변수를 추가하는 경우 또는 매개 변수 이름을 바꾼 경우에는 역할 항목을 수동으로 업데이트해야 합니다. Exchange는 범위가 지정되지 않은 역할 항목의 기존 매개 변수가 변경되었는지 여부를 확인하지 않습니다. 스크립트에서 역할 항목에 있는 매개 변수가 변경된 경우 그 매개 변수를 사용하려고 하면 명령이 실패합니다.

범위가 지정되지 않은 역할 항목에 추가하는 스크립트는 관리자와 사용자가 Exchange 2013 관리 셸을 사용하여 연결하는 모든 서버의 Exchange 스크립트 디렉터리에 있어야 합니다. 역할 항목을 추가하기 위해 사용하는 서버의 Exchange 2013 스크립트 디렉터리에 존재하지 않는 스크립트를 기반으로 범위가 지정되지 않은 역할 항목을 추가하려고 하면 오류가 발생합니다. Exchange 2013 스크립트 디렉터리의 기본 설치 위치는 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts입니다.

범위가 지정되지 않은 역할 항목에 추가하는 비 Exchange cmdlet은, 관리자와 사용자가 셸을 사용하여 연결되고 cmdlet을 사용하고자 하는 모든 Exchange 2013 서버에 설치되어 있어야 합니다. 역할 항목을 추가하기 위해 사용하는 Exchange 서버에 설치되지 않은 비 Exchange 2013 cmdlet을 기반으로 범위가 지정되지 않은 역할 항목을 추가하려고 하면 오류가 발생합니다. 비 Exchange cmdlet을 추가할 때에는 비 Windows cmdlet이 포함된 Exchange PowerShell 스냅인 이름을 지정해야 합니다.

범위가 지정되지 않은 관리 역할 항목을 추가하는 방법에 대한 자세한 내용은 [역할에 역할 항목 추가](add-a-role-entry-to-a-role-exchange-2013-help.md)를 참조하십시오.

맨 위로 이동

## 관리 역할 유형

관리 역할 유형은 모든 관리 역할의 기초입니다. 유형은 지정된 역할 유형의 모든 관리 역할에 정의되는 암시적 범위를 정의하며 관련된 역할을 논리적으로 그룹화하는 기능도 수행합니다. 부모 기본 제공 관리 역할에서 파생되는 모든 관리 역할은 동일한 역할 유형을 갖습니다. 이러한 관계를 보려면 이 항목의 앞부분에 있는 관리 역할 계층 그림을 참조하십시오. 또한 관리 역할 유형은 역할 유형과 관련된 역할에 추가할 수 있는 cmdlet과 해당 매개 변수의 최대 집합을 나타냅니다.

관리 역할 유형은 다음과 같은 범주로 나뉩니다.

  - **관리 또는 전문가**   관리 또는 전문가 역할 유형과 관련된 역할은 Exchange 조직에서 더 넓은 범위에 영향을 줍니다. 이 역할 유형의 역할을 사용하면 서버 또는 받는 사람 관리, 조직 구성, 준수 관리, 감사 등의 작업을 수행할 수 있습니다.

  - **사용자 집중**   사용자 집중 역할 유형과 관련된 역할은 영향 범위가 개별 사용자와 밀접하게 연결되어 있습니다. 이 역할 유형의 역할을 사용하면 사용자 프로필 구성 및 자체 관리, 사용자가 소유한 메일 그룹 관리 등의 작업을 수행할 수 있습니다.
    
    사용자 집중 역할 유형과 관련된 역할의 이름 및 사용자 집중 역할 유형 이름은 My로 시작됩니다.

  - **특수**   특수 역할 유형과 관련된 역할을 사용하면 관리 또는 사용자 집중 역할 유형에 해당되지 않는 작업을 수행할 수 있습니다. 이 역할 유형의 역할을 사용하면 응용 프로그램 가장, 비 Exchange cmdlet 또는 스크립트 사용 등의 작업을 수행할 수 있습니다.

다음 표에서는 Exchange 2013에 있는 모든 관리 역할 유형 목록과 역할 유형에서 허용되는 구성이 Exchange 조직 전체에 적용되는지 개별 서버에만 적용되는지를 확인할 수 있습니다. 각 역할 설명, 역할 할당을 통해 혜택을 받는 사람, 기타 정보 등 이러한 역할 유형과 관련된 각 관리 역할에 대한 자세한 내용은 [기본 제공 관리 역할](built-in-management-roles-exchange-2013-help.md)을 참조하십시오.

**관리 역할 유형**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할 유형</th>
<th>기본 제공 관리 역할</th>
<th>설명</th>
<th>조직 또는 서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Active Directory 권한 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 Active Directory 권한을 구성하도록 해주는 역할과 연결됩니다. Active Directory 권한이나 ACL(액세스 제어 목록)을 사용하는 기능에는 전송 수신 및 송신 커넥터, 사서함의 다른 사람 이름으로 보내기 및 대신 보내기 권한이 포함됩니다.</p>

> [!NOTE]
> Active Directory 개체에 직접 설정된 권한은 RBAC를 통해 적용하지 못할 수 있습니다.


</td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">주소 목록 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 주소 목록, GAL(전체 주소 목록) 및 오프라인 주소 목록을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">ApplicationImpersonation 역할</a></p></td>
<td><p>이 역할 유형은 응용 프로그램이 조직의 사용자를 가장하여 사용자 대신 작업을 수행할 수 있게 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">ArchiveApplication 역할</a></p></td>
<td><p>이 역할 유형은 파트너 응용 프로그램이 조직의 사용자 사서함에 항목을 보관하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">감사 로그 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 감사 로깅 구성을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Cmdlet 확장 에이전트 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 cmdlet 확장 에이전트를 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">데이터 손실 방지 역할</a></p></td>
<td><p>이 역할 유형은 조직에서 DLP(데이터 손실 방지) 정책과 해당 정책 내의 규칙을 만들고 관리하는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">데이터베이스 가용성 그룹 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 DAG(데이터베이스 가용성 그룹)를 관리하도록 해주는 역할과 연결됩니다. 이 역할이 직접 또는 간접적으로 할당된 관리자는 조직의 고가용성 구성을 책임지는 최상위 수준 관리자입니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">데이터베이스 복사본 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 데이터베이스 복사본을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">데이터베이스 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 사서함 데이터베이스를 만들고, 관리하고, 탑재 및 분리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">재해 복구 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사서함과 사서함 데이터베이스를 복원하고 사서함 데이터베이스를 만들며 데이터베이스 가용성 그룹에 대한 데이터 센터 전환 및 다시 전환을 수행하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">메일 그룹 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 메일 그룹 및 메일 그룹 구성원을 만들고 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Edge 구독 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 Exchange 2010 Edge 전송 서버와는 조직에서 Exchange 2013 사서함 서버 사이의 edge 동기화 및 구독 구성을 관리 하도록 해 주는 역할과 연결 됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">전자 메일 주소 정책 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 전자 메일 주소 정책을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Exchange 커넥터 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 배달 에이전트 커넥터를 만들고, 수정하고, 보고, 제거할 수 있도록 하는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Exchange 서버 인증서 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 Exchange 서버 인증서를 만들고, 가져오고, 내보내도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Exchange 서버 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 Exchange 서버 구성을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Exchange 가상 디렉터리 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 Outlook Web App, Microsoft ActiveSync, OAB(오프라인 주소록), 자동 검색, Windows PowerShell 및 Exchange 관리 센터 가상 디렉터리를 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">페더레이션된 공유 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 크로스 포리스트 및 교차 조직 공유를 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">정보 권한 관리 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 Exchange의 IRM(정보 권한 관리) 기능을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">저널링 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 저널링 구성을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">법적 보존 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사서함에 있는 데이터를 소송 목적으로 유지할지 여부를 구성하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Mailbox Import Export 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 사서함 콘텐츠를 가져오고 내보내고 필요 없는 콘텐츠를 사서함에서 제거할 수 있게 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">사서함 검색 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 하나 이상의 사서함의 내용을 검색하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">MailboxSearchApplication 역할</a></p></td>
<td><p>이 역할 유형은 파트너 응용 프로그램이 조직에서 사서함의 법적 보유 상태를 설정하고 확인하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">메일 사용 가능 공용 폴더 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 개별 공용 폴더에 대해 메일 사용 여부를 구성하도록 해주는 역할과 연결됩니다.</p>
<p>이 역할 유형을 사용하면 공용 폴더의 전자 메일 속성만 관리할 수 있습니다. 전자 메일 속성이 아닌 공용 폴더 속성은 관리할 수 없습니다. 전자 메일 속성이 아닌 공용 폴더 속성을 관리하려면 <code>PublicFolders</code> 역할 유형과 연결된 역할을 할당받아야 합니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Mail Recipient Creation 역할</a></p>
<p></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사서함, 메일 사용자, 메일 연락처, 메일 그룹 및 동적 메일 그룹을 만들도록 해주는 역할과 연결됩니다. 이 역할 유형과 관련된 역할을 <code>MailRecipients</code> 역할 유형과 관련된 역할과 결합하면 받는 사람을 만들고 관리할 수 있습니다.</p>
<p>이 역할 유형으로 공용 폴더에서 메일을 사용하도록 설정할 수는 없습니다. 공용 폴더에서 메일을 사용하도록 설정하려면 <code>MailEnabledPublicFolders</code> 역할 유형과 관련된 역할의 할당이 필요합니다.</p>
<p>조직에서 받는 사람을 만드는 그룹과 받는 사람을 관리하는 그룹이 나누어진 사용 권한 분할 모델을 사용하는 경우에는 받는 사람을 만드는 그룹에 <code>MailRecipientCreation</code> 역할을 할당하고 받는 사람을 관리하는 그룹에 <code>MailRecipients</code> 역할을 할당합니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">메일 받는 사람에 게 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 기존 사서함, 메일 사용자, 메일 연락처, 메일 그룹 및 동적 메일 그룹을 관리하도록 해주는 역할과 연결됩니다. 이 역할 유형과 관련된 역할로 받는 사람을 만들 수는 없지만 <code>MailRecipientCreation</code> 역할 유형과 관련된 역할과 결합하면 받는 사람을 만들고 관리할 수 있습니다.</p>
<p>이 역할 유형을 사용하여 메일 사용 가능 공용 폴더 또는 메일 그룹을 관리할 수는 없습니다. 메일 사용 가능 공용 폴더를 관리하려면 <code>MailEnabledPublicFolders</code> 역할 유형과 관련된 역할의 할당이 필요합니다. 배포 그룹을 관리하려면 <code>DistributionGroups</code> 역할 유형과 관련된 역할의 할당이 필요합니다.</p>
<p>조직에서 받는 사람을 만드는 그룹과 받는 사람을 관리하는 그룹이 나누어진 사용 권한 분할 모델을 사용하는 경우에는 받는 사람을 만드는 그룹에 <code>MailRecipientCreation</code> 역할을 할당하고 받는 사람을 관리하는 그룹에 <code>MailRecipients</code> 역할을 할당합니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">메일 팁 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 메일 설명을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">메시지 추적 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 메시지를 추적하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">마이그레이션 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 서버에서 사서함 및 사서함 내용을 양방향으로 마이그레이션하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">역할을 모니터링</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 Microsoft Exchange 서비스 및 구성 요소 가용성을 모니터링하도록 해주는 역할과 연결됩니다. 관리자 외에도, 이 역할 유형과 관련된 역할을 응용 프로그램 모니터링에 사용되는 서비스 계정과 함께 사용하여 Exchange 서버 상태에 대한 정보를 수집할 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">사서함 역할 이동</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에 있는 서버 사이에서, 그리고 로컬 조직과 다른 조직의 서버 사이에서 사서함을 이동하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">OfficeExtensionApplication 역할</a></p></td>
<td><p>이 역할 유형은 Microsoft Office 확장 응용 프로그램이 조직의 사용자 사서함에 액세스하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">조직 사용자 지정 앱 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 해당 조직의 사용자 지정 응용 프로그램을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">Org 마켓플레이스 앱 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 해당 조직의 마켓플레이스 앱을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">조직의 클라이언트 액세스 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 클라이언트 액세스 서버 설정을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">조직 구성 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 조직의 전반적인 설정을 관리하도록 해주는 역할과 연결됩니다. 이 역할 유형으로 제어할 수 있는 조직 구성에는 다음을 비롯한 여러 가지가 있습니다.</p>
<ul>
<li><p>조직에 메일 설명을 사용할 것인지 여부</p></li>
<li><p>관리되는 폴더 홈 페이지의 URL</p></li>
<li><p>Microsoft Exchange 받는 사람 SMTP 주소 및 대체 전자 메일 주소</p></li>
<li><p>리소스 사서함 속성 스키마 구성</p></li>
<li><p>Exchange 관리 센터 및 Outlook Web App에 대한 도움말 URL</p></li>
</ul>
<p>이 역할 유형에는 <code>OrganizationClientAccess</code> 또는 <code>OrganizationTransportSettings</code> 역할 유형에 포함된 권한이 포함되어 있지 않습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">조직 전송 설정 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 시스템 메시지, Active Directory 사이트 구성 및 기타 조직 범위 전송 설정을 관리하도록 해주는 역할과 연결됩니다.</p>
<p>이 역할이 있다고 해서 전송 수신 또는 송신 커넥터, 큐, 방역, 에이전트, 원격 및 허용 도메인 또는 규칙을 만들거나 관리할 수 있는 것은 아닙니다. 각 전송 기능을 만들거나 관리하려면 다음 역할 유형과 관련된 역할의 할당이 필요합니다.</p>
<ul>
<li><p><strong>수신 커넥터</strong>   <code>ReceiveConnectors</code></p></li>
<li><p><strong>송신 커넥터</strong>   <code>SendConnectors</code></p></li>
<li><p><strong>전송 큐</strong>   <code>TransportQueues</code></p></li>
<li><p><strong>전송 방역</strong>   <code>TransportHygiene</code></p></li>
<li><p><strong>전송 에이전트</strong>   <code>TransportAgents</code></p></li>
<li><p><strong>원격 및 허용 도메인</strong>   <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>전송 규칙</strong>   <code>TransportRules</code></p></li>
</ul></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">POP3 및 IMAP4 프로토콜 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 인증 및 연결 설정 등의 POP3 및 IMAP4 구성을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">공용 폴더 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 공용 폴더를 관리하도록 해주는 역할과 연결됩니다.</p>
<p>이 역할 유형으로 공용 폴더의 메일 사용 설정 여부를 관리할 수는 없습니다. 공용 폴더의 메일 사용 여부를 설정하려면 <code>MailEnabledPublicFolders</code> 역할 유형과 관련된 역할의 할당이 필요합니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">수신 커넥터 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 크기 제한 등의 전송 수신 커넥터 구성을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">받는 사람 정책 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 프로비전 및 모바일 장치 정책 등의 받는 사람 정책을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">원격 및 허용 도메인 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 원격 및 허용 도메인을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">암호 역할을 다시 설정</a></p></td>
<td><p>이 역할 유형은 사용자가 조직에서 자신의 암호를 원래대로 설정하거나 관리자가 사용자의 암호를 원래대로 설정하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">보존 관리 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 보존 정책을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">역할 관리 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 관리 역할 그룹, 역할 할당 정책, 관리 역할, 역할 항목, 할당 및 범위를 관리하도록 해주는 역할과 연결됩니다.</p>
<p>이 역할 유형과 관련된 역할이 할당된 사용자는 속성에 의해 <strong>role group managed by</strong>을 다시 정의하고, 역할 그룹을 구성하고, 역할 그룹에서 구성원을 추가 또는 제거할 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">보안 그룹 만들기 및 멤버 자격 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 USG 및 그 구성원을 만들고 관리하도록 해주는 역할과 연결됩니다.</p>
<p>조직에서 USG 만들기 및 관리를 수행하는 그룹과 Exchange 서버를 관리하는 그룹이 나누어진 사용 권한 분할 모델을 사용하는 경우에는 이 역할 유형과 관련된 역할을 해당 그룹에 할당합니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">커넥터 역할을 보내기</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 전송 송신 커넥터를 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Support Diagnostics 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 Microsoft 지원 서비스의 지시에 따라 고급 진단을 수행하도록 해주는 역할과 연결됩니다.</p>

> [!WARNING]
> 이 역할 유형과 관련된 역할은 Microsoft 고객 지원 서비스의 지시에 의해서만 사용할 수 있는 cmdlet 및 스크립트에 권한을 부여합니다.


</td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">팀 사서함 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사이트 사서함 프로비전 정책을 하나 이상 정의하고 사이트 사서함을 관리하도록 해주는 역할과 연결됩니다. 이 역할 유형과 연결된 역할을 할당받은 관리자는 자신의 소유가 아닌 사이트 사서함도 관리할 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">TeamMailboxLifecycleApplication 역할</a></p></td>
<td><p>이 역할 유형은 파트너 응용 프로그램이 조직에서 사이트 사서함의 수명 주기 상태를 업데이트하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">전송 에이전트 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 전송 에이전트를 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">전송 방역 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 스팸 방지 및 맬웨어 방지 기능을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">전송 큐 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 개별 서버에서 전송 큐를 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>서버</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">전송 규칙 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 전송 규칙을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">UM 사서함 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사서함 및 다른 받는 사람의 UM(통합 메시징) 구성을 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">UM 음성 안내 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사용자 지정 UM 음성 안내를 만들고 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">통합된 메시징 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 통합 메시징 서비스를 관리하도록 해주는 역할과 연결됩니다.</p>
<p>이 역할이 있다고 해서 UM 관련 사서함 구성이나 UM 음성 안내를 관리할 수 있는 것은 아닙니다. UM별 사서함 구성을 관리하려면 <code>UMMailboxes</code> 역할 유형과 관련된 역할을 사용합니다. UM 음성 안내를 관리하려면 <code>UMPrompts</code> 역할 유형과 관련된 역할을 사용합니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">범위가 지정 되지 않은 역할 관리 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 범위가 지정되지 않은 최상위 관리 역할을 만들고 관리하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">사용자 옵션 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 사용자의 Outlook Web App 옵션을 볼 수 있게 해주는 역할과 연결됩니다. 이 역할 유형과 관련된 역할은 사용자가 자신의 구성 문제를 진단하도록 돕기 위해 사용할 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">UserApplication 역할</a></p></td>
<td><p>이 역할 유형은 파트너 응용 프로그램이 조직에서 최종 사용자를 대신하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">보기 전용 감사 로그 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 감사 로그를 검색하도록 해주는 역할과 연결됩니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">보기 전용 구성 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 받는 사람 이외의 모든 Exchange 구성 설정을 볼 수 있게 해주는 역할과 연결됩니다. 볼 수 있는 구성의 예로는 서버 구성, 전송 구성, 데이터베이스 구성 및 조직 전체 구성이 있습니다.</p>
<p>이 역할 유형과 관련된 역할을 <code>ViewOnlyRecipients</code> 역할 유형과 관련된 역할과 결합하면 조직에 있는 모든 개체를 볼 수 있는 역할을 만들 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">보기 전용 받는 사람에 게 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 사서함, 메일 사용자, 메일 연락처, 메일 그룹 및 동적 메일 그룹 등의 받는 사람 구성을 볼 수 있게 해주는 역할과 연결됩니다.</p>
<p>이 역할 유형과 관련된 역할을 <code>ViewOnlyConfiguration</code> 역할 유형과 관련된 역할과 결합하면 조직에 있는 모든 개체를 볼 수 있는 역할을 만들 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">WorkloadManagement 역할</a></p></td>
<td><p>이 역할 유형은 관리자가 조직에서 작업 관리 정책을 관리하도록 해주는 역할과 연결됩니다. 관리자는 리소스 상태 정의, 작업 분류를 구성하고 작업 관리를 사용하거나 사용하지 않도록 설정할 수 있습니다.</p></td>
<td><p>조직</p></td>
</tr>
</tbody>
</table>


다음 표에는 Exchange 2013에 있는 사용자 집중 관리 역할 유형 및 연결된 관리 역할이 모두 나열되어 있습니다.

**사용자 집중 역할 유형**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>관리 역할 유형</th>
<th>기본 제공 사용자 집중 역할</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">MyBaseOptions 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 자신의 사서함 및 관련 설정의 기본 구성을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">MyAddressInformation 역할</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">MyContactInformation 역할</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">MyMobileInformation 역할</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">MyPersonalInformation 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 연락처 정보를 수정하도록 해주는 역할과 연결됩니다. 이 정보에는 주소 및 전화 번호가 포함됩니다.</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">사용자 지정 앱의 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 자신의 사용자 지정 앱을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">MyDiagnostics 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 사서함에서 일정 진단 정보 검색과 같은 기본 진단을 수행할 수 있도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">MyDistributionGroupMembership 역할</a></p></td>
<td><p>이 역할 유형은 메일 그룹에서 그룹 구성원을 조작할 수 있는 경우 개별 사용자가 조직에서 메일 그룹 구성원을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">MyDistributionGroups 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 메일 그룹을 만들고 수정하고 보고, 자신이 소유한 메일 그룹에서 구성원을 수정하고 보고 제거하고 추가하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">MyDisplayName 역할</a></p>
<p><a href="myname-role-exchange-2013-help.md">MyName 역할</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">MyProfileInformation 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 자신의 이름을 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">내 마켓플레이스 앱 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 자신의 마켓플레이스 앱을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">MyRetentionPolicies 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 보존 태그를 보고, 보존 태그 설정 및 기본값을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">MyTeamMailboxes 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 사이트 사서함을 만들어 Microsoft SharePoint 사이트에 연결하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">MyTextMessaging 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 텍스트 메시징 설정을 만들고 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">MyVoiceMail 역할</a></p></td>
<td><p>이 역할 유형은 개별 사용자가 음성 메일 설정을 보고 수정하도록 해주는 역할과 연결됩니다.</p></td>
</tr>
</tbody>
</table>


맨 위로 이동

## 자세한 내용

[New-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/ko-kr/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335173\(v=exchg.150\))

