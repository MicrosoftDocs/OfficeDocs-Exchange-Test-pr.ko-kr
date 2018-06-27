---
title: '범위가 지정 되지 않은 최상위 역할을 역할 항목 추가: Exchange 2013 Help'
TOCTitle: 범위가 지정 되지 않은 최상위 역할을 역할 항목 추가
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 50483110
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 범위가 지정 되지 않은 최상위 역할을 역할 항목 추가

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

범위가 지정되지 않은 기존 역할에 새 스크립트나 비 Exchange cmdlet을 사용할 수 있게 하려면 범위가 지정되지 않은 최상위 관리 역할에 스크립트와 비 Exchange cmdlet을 추가할 수 있습니다. 이러한 스크립트와 비 Exchange cmdlet은 범위가 지정되지 않은 최상위 관리 역할에 관리 역할 항목으로 추가됩니다. 이렇게 추가된 항목은 범위가 지정되지 않은 최상위 역할 항목이나 최상위 역할에서 파생된 범위가 지정되지 않은 역할에서 사용할 수 있게 됩니다. 범위가 지정되지 않은 역할 항목에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> Exchange cmdlet이 포함된 관리 역할에서 역할 항목을 변경하려면 <A href="change-a-role-entry-exchange-2013-help.md">역할 항목 변경</A>을 참조하십시오.



역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 범위가 지정되지 않은 최상위 역할에 역할 항목을 추가하는 기능은 기본적으로 어떤 관리 역할 그룹에도 포함되어 있지 않습니다. 범위가 지정되지 않은 역할 관리 역할을 먼저 사용자 또는 사용자가 구성원으로 있는 USG(유니버설 보안 그룹)나 역할 그룹에 할당해야만 해당 사용자가 범위가 지정되지 않은 최상위 역할 항목을 추가할 수 있습니다. 역할 그룹, 사용자 또는 USG에 역할을 추가하는 방법에 대한 자세한 내용은 다음 항목을 참조하십시오.
    
      - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)
    
      - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 범위가 지정되지 않은 최상위 역할에 스크립트 역할 항목 추가

범위가 지정되지 않은 기존 역할에 스크립트를 추가하려면 이 절차를 사용하십시오. 범위가 지정되지 않은 기존 역할에 비 Exchange cmdlet을 추가하려면 이 항목 뒷부분에 있는 "범위가 지정되지 않은 최상위 역할에 비 Exchange cmdlet 역할 항목 추가"를 참조하십시오.

범위가 지정되지 않은 최상위 역할에 Windows PowerShell 스크립트를 추가하려면 역할에 관리 역할 항목을 추가해야 합니다. 역할 항목에는 역할에서 사용하려는 스크립트의 스크립트 이름과 매개 변수가 포함되어 있습니다.

이 스크립트는 스크립트를 실행하기 위해 사용자가 연결할 수 있는 Exchange Server 2013을 실행하는 모든 서버에서 Microsoft Exchange 2013 설치 경로에 있는 Scripts 디렉터리에 있어야 합니다. 사용자에게 스크립트를 실행할 수 있는 액세스 권한이 있지만 사용자를 연결할 Exchange 2013 서버에 스크립트가 없는 경우 오류가 발생합니다. 기본적으로 Scripts 디렉터리의 경로는 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Scripts입니다.

적절한 Exchange 2013 서버에 스크립트를 복사하고 사용해야 할 스크립트 매개 변수를 결정한 후 다음 구문을 사용하여 역할 항목을 만듭니다.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

이 예에서는 *Name* 및 *Location* 매개 변수를 사용하여 IT Scripts 역할에 BulkProvisionUsers.ps1 스크립트를 추가합니다.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> cmdlet은 기본 유효성 검사를 수행하여 스크립트에 있는 매개 변수만 추가하는지 확인합니다. 하지만 역할 항목이 추가되고 나면 이후 유효성 검사가 수행되지 않습니다. 나중에 매개 변수가 추가되거나 제거되면 스크립트를 포함한 역할 항목을 수동으로 업데이트해야 합니다.



## 범위가 지정되지 않은 최상위 역할에 비 Exchange cmdlet 역할 항목 추가

범위가 지정되지 않은 기존 역할에 비 Exchange cmdlet을 추가하려면 이 절차를 사용하십시오. 범위가 지정되지 않은 기존 역할에 스크립트를 추가하려면 이 항목 앞부분에 있는 "범위가 지정되지 않은 최상위 역할에 스크립트 역할 항목 추가"를 참조하십시오.

범위가 지정되지 않은 최상위 역할에 Exchange 이외의 cmdlet을 추가하려면 역할에 관리 역할 항목을 추가해야 합니다. 역할 항목에는 역할에서 사용하려는 cmdlet의 cmdlet 스냅인, cmdlet 이름 및 매개 변수가 포함되어 있습니다.

새 역할에 Exchange 이외의 cmdlet을 추가하는 경우에는 사용자가 cmdlet 실행을 위해 연결할 수 있는 모든 Exchange 2013 서버에 cmdlet을 설치해야 합니다. 사용할 cmdlet이 들어 있는 Windows PowerShell 스냅인을 제대로 설치하고 등록하는 방법에 대한 자세한 내용은 제품 설명서를 참조하십시오.

적절한 Windows 서버에 cmdlet이 포함된 Exchange 2013 PowerShell 스냅인을 설치하고 사용해야 할 cmdlet 매개 변수를 결정했으면 다음 구문을 사용하여 역할 항목을 만듭니다.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

이 예에서는 *Database* 및 *Size* 매개 변수를 사용하여 Widget Cmdlet 역할에 Contoso.Admin.Cmdlets 스냅인의 **Set-WidgetConfiguration** cmdlet을 추가합니다.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> <STRONG>Add-ManagementRoleEntry</STRONG> cmdlet은 기본 유효성 검사를 수행하여 cmdlet에 있는 매개 변수만 추가하는지 확인합니다. 하지만 역할 항목이 추가되고 나면 이후 유효성 검사가 수행되지 않습니다. cmdlet이 나중에 변경되고 매개 변수가 추가되거나 제거되면 cmdlet을 포함한 역할 항목을 수동으로 업데이트해야 합니다.



## 다른 작업

범위가 지정되지 않은 최상위 역할에 역할 항목을 추가했으면 다음 작업을 수행할 수 있습니다.

[역할에 역할 항목 추가](add-a-role-entry-to-a-role-exchange-2013-help.md)

[역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

[역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)

[사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[사용자 또는 USG에서 역할을 제거 합니다.](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

