---
title: '범위가 지정되지 않은 역할 만들기: Exchange 2013 Help'
TOCTitle: 범위가 지정되지 않은 역할 만들기
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 50483183
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 범위가 지정되지 않은 역할 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-06-09_

범위가 지정되지 않은 관리 역할을 사용하면 관리자와 전문가 사용자에게 Windows Powershell 스크립트 및 비 Exchange cmdlet에 대한 액세스 권한을 제공할 수 있습니다. 범위가 지정되지 않은 최상위 수준의 역할을 만들고 해당 역할에 스크립트 또는 비 Exchange cmdlet을 추가할 수도 있고, 범위가 지정되지 않은 기존의 최상위 수준 역할을 기반으로 하는 역할을 만들 수도 있습니다. 범위가 지정되지 않은 역할을 만들고 사용자 지정한 후 관리 역할 그룹, 사용자 및 USG(유니버설 보안 그룹)에 할당할 수 있습니다. 관리 역할 할당 정책에는 범위가 지정되지 않은 역할을 할당할 수 없습니다. 범위가 지정되지 않은 역할에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.


> [!WARNING]
> 범위가 지정되지 않은 역할은 이름에서 알 수 있듯이 관리 범위가 적용되지 않았기 때문에 강력할 수 있습니다. 즉 범위가 지정되지 않은 역할에 포함된 스크립트와 비 Exchange cmdlet을 Exchange 조직의 어떤 개체에 대해서도 실행할 수 있습니다. 범위가 지정되지 않은 역할에 스크립트 또는 비 Exchange cmdlet을 추가할 때와 범위가 지정되지 않은 역할을 할당할 때 이점을 고려하십시오.




> [!NOTE]
> Exchange cmdlet이 포함된 역할을 만들려면 기존 관리 역할을 기반으로 하는 역할을 만들어야 합니다. Exchange cmdlet이 포함된 역할을 만드는 방법에 대한 자세한 내용은 <A href="create-a-role-exchange-2013-help.md">역할 만들기</A>를 참조하십시오.



역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 관리 역할 그룹에는 기본적으로 범위가 지정되지 않은 역할을 만드는 기능이 포함되어 있지 않습니다. 범위가 지정되지 않은 역할 관리 역할을 먼저 사용자에게 또는 사용자가 구성원으로 있는 USG나 역할 그룹에 할당해야만 해당 사용자가 역할 그룹을 만들 수 있습니다. 사용자, USG 또는 역할 그룹에 역할 추가에 대한 자세한 내용은 다음 항목을 참조하십시오.
    
      - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)
    
      - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 범위가 지정되지 않은 최상위 관리 역할 만들기

조직의 관리자 또는 전문가가 사용할 수 있는 스크립트나 비 Exchange cmdlet을 만들려면 범위가 지정되지 않은 최상위 역할을 만들어야 합니다. 범위가 지정되지 않은 초기 역할은 다른 역할에서 상속되지 않으므로 스크립트나 비 Exchange cmdlet은 최상위 역할로서 만들어진, 범위가 지정되지 않은 역할에만 추가할 수 있습니다. 그러면 범위가 지정되지 않은 새로운 최상위 역할은 추가된 스크립트와 비 Exchange cmdlet도 사용할 수 있는, 범위가 지정되지 않은 다른 역할에 대한 상위가 될 수 있습니다.

범위가 지정되지 않은 최상위 역할을 만드는 단계는 다음과 같습니다.

## 1단계: 범위가 지정되지 않은 최상위 역할 만들기

범위가 지정되지 않은 최상위 역할에는 상위 역할이 없습니다. 상위가 없는 역할을 만들려면 *UnscopedTopLevel* 스위치를 지정해야 합니다. 다음 구문을 사용하여 새 역할을 만듭니다.

    New-ManagementRole <name of new role> -UnscopedTopLevel

이 예제에서는 IT 스크립트의 범위가 지정되지 않은 최상위 역할을 만듭니다.

    New-ManagementRole "IT Scripts" -UnscopedTopLevel

역할을 만든 후 스크립트나 비 Exchange cmdlet을 추가할 때까지는 역할이 비어 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd298073\(v=exchg.150\))를 참조하십시오.

## 2a단계: 스크립트 관리 역할 항목 추가

범위가 지정되지 않은 새로운 역할에 스크립트를 추가하려면 이 단계를 사용하십시오. 범위가 지정되지 않은 새로운 역할에 비 Exchange cmdlet을 추가하려면 Step 2b를 사용하십시오.

범위가 지정되지 않은 최상위 역할에 Windows Powershell 스크립트를 추가하려면 역할에 관리 역할 항목을 추가해야 합니다. 역할 항목에는 역할에서 사용하려는 스크립트의 스크립트 이름과 매개 변수가 포함되어 있습니다.

이 스크립트는 스크립트를 실행하기 위해 사용자가 연결할 수 있는 Exchange 2013을 실행하는 모든 서버에서 Microsoft Exchange Server 2013 설치 경로에 있는 `RemoteScripts` 디렉터리에 있어야 합니다. 사용자에게 스크립트를 실행할 수 있는 액세스 권한이 있지만 사용자를 연결할 Exchange 2013 서버에 스크립트가 없는 경우 오류가 발생합니다. 기본적으로 `RemoteScripts` 디렉터리 경로는 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\RemoteScripts입니다.

적절한 Exchange 2013 서버에 스크립트를 복사하고 사용해야 할 스크립트 매개 변수를 결정한 후 다음 구문을 사용하여 역할 항목을 만듭니다.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

이 예에서는 *Name* 및 *Location* 매개 변수를 사용하여 IT Scripts 역할에 BulkProvisionUsers.ps1 스크립트를 추가합니다.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> cmdlet은 기본 유효성 검사를 수행하여 스크립트에 있는 매개 변수만 추가하는지 확인합니다. 하지만 역할 항목이 추가되고 나면 이후 유효성 검사가 수행되지 않습니다. 나중에 매개 변수가 추가되거나 제거되면 스크립트를 포함한 역할 항목을 수동으로 업데이트해야 합니다.



## 2b단계: 비 Exchange cmdlet 역할 항목 추가

범위가 지정되지 않은 새로운 역할에 비 Exchange cmdlet을 추가하려면 이 단계를 사용하십시오. 범위가 지정되지 않은 새로운 역할에 스크립트를 추가하려면 Step 2a를 사용하십시오.

범위가 지정되지 않은 최상위 역할에 Exchange 이외의 cmdlet을 추가하려면 역할에 관리 역할 항목을 추가해야 합니다. 역할 항목에는 역할에서 사용하려는 cmdlet의 cmdlet 스냅인, cmdlet 이름 및 매개 변수가 포함되어 있습니다.

새 역할에 Exchange 이외의 cmdlet을 추가하는 경우에는 사용자가 cmdlet 실행을 위해 연결할 수 있는 모든 Exchange 2013 서버에 cmdlet을 설치해야 합니다. 사용할 cmdlet이 들어 있는 Windows Powershell 스냅인을 제대로 설치하고 등록하는 방법에 대한 자세한 내용은 제품 설명서를 참조하십시오.

적절한 Windows 서버에 cmdlet이 포함된 Exchange 2013 Powershell 스냅인을 설치하고 사용해야 할 cmdlet 매개 변수를 결정했으면 다음 구문을 사용하여 역할 항목을 만듭니다.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

이 예에서는 *Database* 및 *Size* 매개 변수를 사용하여 Widget cmdlet 역할에 Contoso.Admin.Cmdlets 스냅인의 **Set-WidgetConfiguration** cmdlet을 추가합니다.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> cmdlet은 기본 유효성 검사를 수행하여 cmdlet에 있는 매개 변수만 추가하는지 확인합니다. 하지만 역할 항목이 추가되고 나면 이후 유효성 검사가 수행되지 않습니다. cmdlet이 나중에 변경되고 매개 변수가 추가되거나 제거되면 cmdlet을 포함한 역할 항목을 수동으로 업데이트해야 합니다.



## 3단계: 관리 역할 할당

역할을 만들고 구성할 때 가장 마지막 단계는 역할을 역할 담당자에게 할당하는 것입니다.


> [!IMPORTANT]
> 범위가 지정되지 않은 역할을 할당하는 역할 할당에 관리 범위를 구성할 수는 없습니다. 역할 할당을 역할 그룹, 사용자 또는 USG에 대해 만들도록 선택할지 여부에 상관없이 관리 범위 없이 역할 할당을 만드는 옵션을 선택해야 합니다.



역할 그룹, 사용자 또는 USG에 새 역할을 할당할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## 범위가 지정되지 않은 다른 역할을 기반으로 범위가 지정되지 않은 역할 만들기

범위가 지정되지 않은 기존 최상위 역할이 있거나 범위가 지정되지 않은 새 역할의 기반으로 사용할 기타 범위가 지정되지 않은 역할이 있는 경우, 범위가 지정되지 않은 하위 역할을 만들 수 있습니다. 범위가 지정되지 않은 하위 역할에는 범위가 지정되지 않은 상위 역할에 있는 스크립트나 cmdlet의 하위 집합을 포함할 수 있습니다. 이 기능은 예를 들어 덜 숙련된 관리자에게 범위가 지정되지 않은 상위 역할에서 사용할 수 있는 스크립트나 cmdlet의 하위 집합만 제공하려는 경우 유용합니다.

범위가 지정되지 않은 하위 역할을 만드는 단계는 다음과 같습니다.

## 1단계: 범위가 지정되지 않은 하위 역할 만들기

범위가 지정되지 않은 새로운 하위 역할은 범위가 지정되지 않은 기존 역할을 기반으로 할 수 있습니다. 역할을 만들 때 기존 역할과 해당 관리 역할 항목이 새 역할에 복사됩니다. 기존 역할은 새 하위 역할에 대한 상위가 됩니다. 범위가 지정되지 않은 다른 역할을 기반으로 하는 범위가 지정되지 않은 역할을 만드는 경우, 사용해야 할 모든 cmdlet과 매개 변수를 모두 포함한 역할을 선택한 다음 원하지 않는 cmdlet과 매개 변수를 제거해야 합니다. 범위가 지정되지 않은 하위 역할에는 상위 역할에 없는 관리 역할 항목을 포함할 수 없습니다.


> [!NOTE]
> 범위가 지정되지 않은 다른 역할에 없는 스크립트나 비 Exchange cmdlet이 포함된 범위가 지정되지 않은 역할을 만들어야 하는 경우에는 범위가 지정되지 않은 최상위 역할을 만드십시오. 자세한 내용은 이 항목 앞부분의 Create an unscoped top-level management role를 참조하십시오.



다음 구문을 사용하여 새 역할을 만듭니다.

    New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>

이 예에서는 IT Global Scripts 역할과 해당 관리 역할 항목을 Diagnostic IT Scripts 역할에 복사합니다.

    New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd298073\(v=exchg.150\))를 참조하십시오.

## 2단계: 역할의 관리 역할 항목 변경

역할을 만든 후에는 역할 항목을 변경해야 합니다. 전체 역할 항목을 제거할 수 있는데, 이렇게 하면 연관된 스크립트나 비 Exchange cmdlet에 대한 액세스 권한이 완전히 제거됩니다. 또는 역할 항목에서 매개 변수를 제거하여 연관된 스크립트나 비 Exchange cmdlet에서 이러한 특정 매개 변수에 대한 액세스 권한을 제거할 수 있습니다.

역할 항목이나 역할 항목에 있는 매개 변수가 상위 역할에 없는 경우에는 이러한 항목 또는 매개 변수를 추가할 수 없습니다. 1단계에서 상위 역할에서 역할을 만들었으므로 역할 항목에 추가 역할 항목이나 매개 변수를 추가할 수 없습니다. 추가 역할 항목이나 매개 변수가 상위 역할에는 없기 때문입니다.

역할에서 역할 항목을 변경할 때 다음 중 하나를 수행할 수 있습니다.

  - 한 개의 전체 역할 항목을 제거합니다.

  - 여러 개의 전체 역할 항목을 제거합니다.

  - 역할 항목에서 매개 변수를 제거합니다.

새 역할에서 역할 항목을 제거하려면 [역할에서 역할 항목을 제거 합니다.](remove-a-role-entry-from-a-role-exchange-2013-help.md)를 참조하십시오.

## 3단계: 관리 역할 할당

역할을 만들고 구성할 때 가장 마지막 단계는 역할을 역할 담당자에게 할당하는 것입니다.


> [!IMPORTANT]
> 범위가 지정되지 않은 역할을 할당하는 역할 할당에 관리 범위를 구성할 수는 없습니다. 역할 할당을 역할 그룹, 사용자 또는 USG에 대해 만들도록 선택할지 여부에 상관없이 관리 범위 없이 역할 할당을 만드는 옵션을 선택해야 합니다.



역할 그룹, 사용자 또는 USG에 새 역할을 할당할 수 있습니다. 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

