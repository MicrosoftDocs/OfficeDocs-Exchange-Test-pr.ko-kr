---
title: '사용자 또는 USG에는 역할을 추가 합니다.: Exchange 2013 Help'
TOCTitle: 사용자 또는 USG에는 역할을 추가 합니다.
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 50483924
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 또는 USG에는 역할을 추가 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

관리 역할 할당은 사용자 또는 USG(유니버설 보안 그룹)에 관리 역할을 할당할 수 있습니다. 사용자 또는 USG에 역할을 할당하면 이러한 사용자가 관리 역할에 정의된 cmdlet 또는 스크립트 및 매개 변수에 따라 작업을 수행하도록 할 수 있습니다.

관리 역할 그룹 또는 관리 역할 할당 정책에 역할을 할당하려면 다음 항목을 참조하십시오.

  - [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)

  - [역할 할당 정책 관리](manage-role-assignment-policies-exchange-2013-help.md)

역할 그룹에 구성원을 추가하거나 최종 사용자에게 역할 할당 정책을 할당하려면 다음 항목을 참조하십시오.

  - [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md)

  - [사서함에 할당 정책 변경](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오.

역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 할당" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 사용자 및 USG에 직접 역할을 할당할 수도 있지만 관리 역할 그룹 및 관리 역할 할당 정책을 사용하여 관리자 및 최종 사용자에게 사용 권한을 부여하는 것이 권장되는 방법입니다. 역할 그룹 및 할당 정책을 사용하면 사용 권한 모델이 간소화됩니다.

  - 역할 할당은 누적됩니다. 따라서 모든 역할은 평가될 때 함께 추가됩니다. 한 사용자에게 두 역할이 할당되고, 한 역할에는 cmdlet이 포함되어 있지만 다른 역할에는 포함되지 않은 경우 사용자는 cmdlet을 계속 사용할 수 있습니다.
    
    기본적으로 역할 할당은 다른 사용자에게 역할을 할당할 수 있는 권한을 부여하지 않습니다. 사용자가 다른 사용자 또는 USG에 역할을 할당하도록 허용하려면 [대리인 역할 할당](delegate-role-assignments-exchange-2013-help.md)을 참조하십시오.

  - 범위가 있는 할당을 만들면 이 범위가 역할의 암시적인 쓰기 범위를 재정의합니다. 하지만 역할의 암시적 읽기 범위가 계속 적용됩니다. 새 범위는 역할의 암시적 읽기 범위를 벗어난 개체는 반환할 수 없습니다. 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 모든 절차에서는 *SecurityGroup* 매개 변수를 사용하여 USG에 역할을 할당합니다. 특정 사용자에게 역할을 할당하려는 경우 *SecurityGroup* 매개 변수 대신 *User* 매개 변수를 사용합니다. 다른 모든 각 명령의 구문은 동일합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 범위가 없는 역할 할당 만들기

범위가 없는 역할 할당을 만들 수 있습니다. 이 때 역할의 암시적인 읽기 범위 및 암시적인 쓰기 범위가 적용됩니다.

범위 없이 USG에 역할을 할당하려면 다음 구문을 사용합니다.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

이 예에서는 SeattleAdmins USG에 Exchange 서버 역할을 할당합니다.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 미리 정의된 상대 범위가 있는 역할 할당 만들기

미리 정의된 상대 범위가 업무 요구 사항에 맞는 경우 사용자 지정 범위를 만들지 않고 해당 범위를 역할 할당에 적용할 수 있습니다. 미리 정의된 범위와 그 설명에 대한 목록은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

미리 정의된 범위를 사용하여 USG에 역할을 할당하려면 다음 구문을 사용합니다.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

이 예에서는 SeattleAdmins USG에 Exchange 서버 역할을 할당하고 미리 정의된 범위 Organization을 적용합니다.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 받는 사람 필터 기반 범위를 사용하여 역할 할당 만들기

받는 사람 필터 기반 범위를 만들고 이를 역할 할당에 사용하려는 경우 *CustomRecipientWriteScope* 매개 변수를 사용하여 USG에 역할을 할당하는 데 사용되는 명령에 범위를 포함해야 합니다. *CustomRecipientWriteScope* 매개 변수를 사용하는 경우에는 *RecipientOrganizationalUnitScope* 매개 변수를 사용할 수 없습니다.

역할 할당에 범위를 추가하려면 먼저 범위를 만들어야 합니다. 자세한 내용은 [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)를 참조하십시오.

받는 사람 필터 기반 범위를 사용하여 USG에 역할을 할당하려면 다음 구문을 사용합니다.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

이 예에서는 Seattle Recipient Admins USG에 Mail Recipients 역할을 할당하고 Seattle Recipients 범위를 적용합니다.

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 서버나 데이터베이스 필터 또는 목록 기반 구성 범위를 사용하여 역할 할당 만들기

서버나 데이터베이스 필터 또는 목록 기반 구성 범위를 만들고 이를 역할 할당에 사용하려는 경우 *CustomConfigWriteScope* 매개 변수를 사용하여 USG에 역할을 할당하는 데 사용되는 명령에 범위를 포함해야 합니다.

역할 할당에 범위를 추가하려면 먼저 범위를 만들어야 합니다. 자세한 내용은 [일반 또는 배타적 범위 만들기](create-a-regular-or-exclusive-scope-exchange-2013-help.md)를 참조하십시오.

구성 범위를 사용하여 USG에 역할을 할당하려면 다음 구문을 사용합니다.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

이 예에서는 MailboxAdmins USG에 Exchange 서버 역할을 할당하고 Mailbox Servers 범위를 적용합니다.

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

앞의 예에서는 서버 구성 범위가 있는 역할 할당을 추가하는 방법을 보여 줍니다. 데이터베이스 구성 범위를 추가하는 구문은 동일합니다. 서버 범위 대신 데이터베이스 범위의 이름을 지정합니다.

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## OU 범위를 사용하여 역할 할당 만들기

OU(조직 구성 단위)에 역할의 쓰기 범위를 적용하려는 경우 *RecipientOrganizationalUnitScope* 매개 변수에 직접 OU를 지정할 수 있습니다. *RecipientOrganizationalUnitScope* 매개 변수를 사용하는 경우에는 *CustomRecipientWriteScope* 매개 변수를 사용할 수 없습니다.

USG에 역할을 할당하고 역할의 쓰기 범위를 특정 OU로 제한하려면 다음 구문을 사용합니다.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

이 예에서는 SalesRecipientAdmins USG에 Mail Recipients 역할을 할당하고 contoso.com 도메인의 Sales/Users OU에 대한 할당 범위를 지정합니다.

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## 받는 사람 또는 구성의 단독 범위를 사용하여 역할 할당 만들기

받는 사람 또는 구성의 단독 범위를 사용하여 단독 역할 할당을 만들려면 Create a role assignment with a recipient filter-based scope 및 Create a role assignment with a server or database filter or list-based configuration scope 섹션에 나와 있는 절차를 사용하면 됩니다. 한 가지 차이점은 단독 범위를 사용하여 역할 할당을 만들 때 단독 받는 사람 범위 또는 단독 구성 범위를 사용하는지에 따라 다음 단독 매개 변수를 지정해야 한다는 점입니다.

  - **받는 사람의 단독 범위**   *CustomRecipientWriteScope* 매개 변수 대신 *ExclusiveRecipientWriteScope* 매개 변수를 사용합니다.

  - **구성의 단독 범위**   *CustomConfigWriteScope* 매개 변수 대신 *ExclusiveConfigWriteScope* 매개 변수를 사용합니다.

이 절차를 수행할 때 역할을 할당받은 역할 담당자는 단독 범위에 포함된 개체에 대해 작업을 수행할 수 있습니다. 단독 범위에 대한 자세한 내용은 [배타적 범위 이해 (영문)](understanding-exclusive-scopes-exchange-2013-help.md)를 참조하십시오.

단독 범위 및 일반 범위를 둘 다 사용하여 역할 할당을 만들 수는 없습니다.

이 예에서는 Protected User Admins USG에 Mail Recipients 역할을 할당하고 Protected Users 단독 범위를 적용합니다.

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

