---
title: '범위가 지정 되지 않은 최상위 역할의 역할 항목 변경: Exchange 2013 Help'
TOCTitle: 범위가 지정 되지 않은 최상위 역할의 역할 항목 변경
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 50483300
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 범위가 지정 되지 않은 최상위 역할의 역할 항목 변경

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

범위가 지정되지 않은 최상위 관리 역할의 관리 역할 항목은 역할이 할당된 사용자가 사용하게 될 스크립트와 비 Exchange cmdlet 및 해당 매개 변수를 참조합니다. 역할 항목에서 사용 가능한 매개 변수를 변경함으로써 역할이 할당된 사용자가 스크립트 또는 비 Exchange cmdlet을 사용하여 수행할 수 있는 작업을 제어하게 됩니다. 범위가 지정되지 않은 역할 항목에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> Exchange cmdlet이 포함된 관리 역할에서 역할 항목을 변경하려면 <A href="change-a-role-entry-exchange-2013-help.md">역할 항목 변경</A>을 참조하십시오.



역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 범위가 지정되지 않은 최상위 역할에서 역할 항목을 변경하는 기능은 기본적으로 어떤 관리 역할 그룹에도 포함되어 있지 않습니다. 범위가 지정되지 않은 역할 관리 역할을 먼저 사용자 또는 사용자가 구성원으로 있는 USG(유니버설 보안 그룹)나 역할 그룹에 할당해야만 해당 사용자가 범위가 지정되지 않은 최상위 역할 항목을 변경할 수 있습니다. 사용자, USG 또는 역할 그룹에 역할 추가에 대한 자세한 내용은 다음 항목을 참조하십시오.
    
      - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)
    
      - [사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 역할 항목에 하나 이상의 매개 변수 추가

범위가 지정되지 않은 최상위 역할 항목에 매개 변수를 추가하려면 다음을 수행해야 합니다.

  - *Parameters* 매개 변수를 사용하여 추가할 매개 변수를 지정합니다.

  - *AddParameter* 매개 변수를 지정하여 추가 작업을 수행하고자 함을 나타냅니다.

  - 범위가 지정되지 않은 최상위 역할에서 역할 항목을 변경함을 나타내는 *UnscopedTopLevel* 매개 변수를 지정합니다. 범위가 지정되지 않은 역할에서 역할 항목을 변경할 때 이 매개 변수를 지정하지 않으면 오류가 발생합니다.

역할 항목에 매개 변수를 추가하려면 다음 구문을 사용합니다.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

이 예에서는 Recipient Administrators 범위가 지정되지 않은 역할의 **CreateUsers.ps1** 스크립트에 *EmailAddress* 및 *City* 매개 변수를 추가합니다.

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 역할 항목에서 하나 이상의 매개 변수 제거

역할 항목에서 매개 변수를 제거하려면 다음을 수행해야 합니다.

  - *Parameters* 매개 변수를 사용하여 제거할 매개 변수를 지정합니다.

  - *RemoveParameter* 매개 변수를 지정하여 제거 작업을 수행하고자 함을 나타냅니다.

  - 범위가 지정되지 않은 최상위 역할에서 역할 항목을 변경함을 나타내는 *UnscopedTopLevel* 매개 변수를 지정합니다. 범위가 지정되지 않은 역할에서 역할 항목을 변경할 때 이 매개 변수를 지정하지 않으면 오류가 발생합니다.


> [!WARNING]
> 제거 작업은 실행 취소할 수 없습니다. 실수로 역할 항목에서 매개 변수를 제거한 경우에는 수동으로 다시 추가해야 합니다.



역할 항목에서 매개 변수를 제거하려면 다음 구문을 사용하십시오.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

이 예에서는 Tier 1 Server Administrators 역할의 **Start-Widget** 비 Exchange cmdlet에서 *Delay*, *Force* 및 *Credential* 매개 변수를 제거합니다.

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 역할 항목에서 모든 매개 변수 제거

역할 항목에서 모든 매개 변수를 제거하려면 다음을 수행해야 합니다.

  - *Parameters* 매개 변수에서 값 `$Null`을 지정합니다. *RemoveParameter* 매개 변수는 포함하지 않아도 됩니다.

  - 범위가 지정되지 않은 최상위 역할에서 역할 항목을 변경함을 나타내는 *UnscopedTopLevel* 매개 변수를 지정합니다. 범위가 지정되지 않은 역할에서 역할 항목을 변경할 때 이 매개 변수를 지정하지 않으면 오류가 발생합니다.

역할 항목에서 모든 매개 변수를 제거하는 작업은 스크립트 또는 비 Exchange cmdlet에서 몇 개의 매개 변수만 사용 가능하게 설정하고 다른 매개 변수는 모두 제외하려는 경우 가장 유용합니다.

역할이 스크립트 또는 비 Exchange cmdlet에 액세스하지 못하게 하려면 단순히 매개 변수만 제거하는 것이 아니라 역할에서 연결된 역할 항목을 완전히 제거해야 합니다. 역할에서 역할 항목을 제거하는 방법에 대한 자세한 내용은 [역할에서 역할 항목을 제거 합니다.](remove-a-role-entry-from-a-role-exchange-2013-help.md)를 참조하십시오.


> [!WARNING]
> 제거 작업은 실행 취소할 수 없습니다. 실수로 역할 항목에서 모든 매개 변수를 제거한 경우에는 수동으로 다시 추가해야 합니다.



역할 항목에서 모든 매개 변수를 제거하려면 다음 구문을 사용합니다.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

이 예에서는 Recipient Administrators 역할의 FindMailboxesOverQuota.ps1 스크립트에서 모든 매개 변수를 제거합니다.

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 특정 매개 변수 집합 적용

역할 항목에 특정 매개 변수 집합만 포함하려면 다음을 수행해야 합니다.

  - *Parameters* 매개 변수만 지정합니다. *AddParameter* 또는 *RemoveParameter* 매개 변수는 포함하지 마십시오.

  - *UnscopedTopLevel* 매개 변수를 지정하여 범위가 지정되지 않은 역할에서 역할 항목을 변경 중임을 나타냅니다. 범위가 지정되지 않은 최상위 역할에서 역할 항목을 변경할 때 이 매개 변수를 지정하지 않으면 오류가 발생합니다.


> [!WARNING]
> <EM>Parameters</EM> 매개 변수만 지정하는 경우 명령에서 지정한 매개 변수만 역할 항목에 포함됩니다. 그 밖의 모든 매개 변수는 제거됩니다.



특정 매개 변수 집합을 지정하려면 다음 구문을 사용하십시오.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

이 예에서는 Seattle Mail Recipient Admins 역할의 **Set-Widget** cmdlet에 *Alias*, *DisplayName*, *WidgetConfig* 및 *Enabled* 매개 변수만 포함합니다.

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 다른 작업

범위가 지정되지 않은 최상위 역할에서 역할 항목을 변경했으면 다음 작업을 수행할 수 있습니다.

[역할에 역할 항목 추가](add-a-role-entry-to-a-role-exchange-2013-help.md)

[역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

[역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)

[사용자 또는 USG에는 역할을 추가 합니다.](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[사용자 또는 USG에서 역할을 제거 합니다.](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

