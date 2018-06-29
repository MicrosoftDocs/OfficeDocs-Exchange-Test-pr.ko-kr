---
title: '역할에 역할 항목 추가: Exchange 2013 Help'
TOCTitle: 역할에 역할 항목 추가
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 50482777
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할에 역할 항목 추가

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-04_

cmdlet에 대한 액세스 권한을 부여하려면 연결된 관리 역할 항목을 관리 역할에 추가해야 합니다. 역할에 역할 항목을 추가하면 해당 역할이 할당된 사용자가 cmdlet에 액세스할 수 있습니다. Microsoft Exchange Server 2013의 관리 역할 항목에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

기본 제공 역할에는 역할 항목을 추가할 수 없습니다. 역할을 사용자 지정하려면 새 역할을 만들어야 합니다. 새 역할을 만드는 방법에 대한 자세한 내용은 [역할 만들기](create-a-role-exchange-2013-help.md)를 참조하십시오.


> [!NOTE]
> 이 항목에서는 범위가 지정되지 않은 관리 역할에 범위가 지정되지 않은 관리 역할 항목을 추가하는 방법에 대해서는 설명하지 않습니다. 범위가 지정되지 않은 역할 항목을 추가하는 방법에 대한 자세한 내용은 <A href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">범위가 지정 되지 않은 최상위 역할을 역할 항목 추가</A>를 참조하십시오.



역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 관리 역할에 추가할 역할 항목이 해당 역할의 바로 상위 관리 역할에 있어야 합니다.

  - 이 항목에서는 파이프라이닝을 사용합니다. 파이프라이닝에 대한 자세한 내용은 [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 상위 역할의 단일 역할 항목 추가

다음 구문을 사용하면 역할 항목을 상위 역할에 표시되는 대로 역할에 추가할 수 있습니다.

    Add-ManagementRoleEntry <child role name>\<cmdlet>

이 예에서는 Recipient Administrators 역할에 **Set-Mailbox** cmdlet을 추가합니다.

    Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"

이 명령은 상위 역할을 확인하고 역할 항목이 있으면 하위 역할에 추가합니다. 역할 항목이 이미 하위 역할에 있는 경우에는 *Overwrite* 매개 변수를 포함하여 기존 역할 항목을 덮어쓸 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Add-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351236\(v=exchg.150\))를 참조하십시오.

## 상위 역할의 단일 역할 항목 추가 및 특정 매개 변수만 포함

상위 역할의 역할 항목을 추가하지만 하위 역할의 역할 항목에 특정 매개 변수만 포함하려면 다음 구문을 사용합니다.

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

이 예에서는 Help Desk 역할에 **Set-Mailbox** cmdlet을 추가하지만 하위 역할의 항목에 *DisplayName* 및 *EmailAddresses* 매개 변수만 포함합니다.

    Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses

이 명령은 상위 역할을 확인하고 역할 항목이 있으면 하위 역할에 추가합니다. 역할 항목이 이미 하위 역할에 있는 경우에는 *Overwrite* 매개 변수를 포함하여 기존 역할 항목을 덮어쓸 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Add-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351236\(v=exchg.150\))를 참조하십시오.

## 상위 역할의 여러 역할 항목 추가

역할에 둘 이상의 역할 항목을 추가하려면 상위 역할에서 하위 역할에 추가할 항목 목록을 검색한 후 하위 역할에 추가해야 합니다. 이렇게 하려면 **Get-ManagementRoleEntry** cmdlet을 사용하여 상위 역할의 역할 항목 목록을 검색합니다. 그런 다음 **Get-ManagementRoleEntry** cmdlet의 출력을 **Add-ManagementRoleEntry** cmdlet에 파이프합니다. 여러 역할 항목을 검색하려면 와일드카드 문자(\*)를 사용해야 합니다.

상위 역할의 여러 항목을 하위 역할에 추가하려면 다음 구문을 사용합니다.

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

이 예에서는 Mail Recipients 상위 역할에서 cmdlet 이름에 `Mailbox` 문자열이 포함된 모든 역할 항목을 Seattle Mail Recipients 하위 역할에 추가합니다.

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

하위 역할에 역할 항목이 이미 있는 경우 *Overwrite* 매개 변수를 포함하여 기존 역할 항목을 덮어쓸 수 있습니다.

관리 역할 항목 목록 검색에 대한 자세한 내용은 [역할 항목 보기](view-role-entries-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\)) 및 [Add-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351236\(v=exchg.150\))를 참조하십시오.

