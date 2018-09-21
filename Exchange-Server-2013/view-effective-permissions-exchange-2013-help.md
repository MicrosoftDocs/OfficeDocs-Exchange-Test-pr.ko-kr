---
title: '유효 사용 권한 보기: Exchange 2013 Help'
TOCTitle: 유효 사용 권한 보기
ms:assetid: ae6cb7cf-f998-44a6-a69a-02ad736c8260
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638167(v=EXCHG.150)
ms:contentKeyID: 50483862
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 유효 사용 권한 보기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-09_

Microsoft Exchange Server 2013에서 사용 권한은 관리 역할 그룹에 할당된 관리 역할, 관리 역할 할당 정책, USG(유니버설 보안 그룹)를 사용하여 부여하거나 직접 사용자에게 부여할 수 있습니다. 사용자가 역할 그룹 또는 USG의 구성원이거나 역할 할당 정책이 할당되어 있으면 사용자에게 사용 권한이 부여됩니다.

대부분의 사용 권한은 역할 그룹 구성원 또는 최종 사용자에 대한 할당 정책 할당을 바탕으로 부여됩니다. 역할 그룹 및 할당 정책을 사용하면 손쉽게 많은 수의 사용자에게 사용 권한을 부여할 수 있지만 누가 역할 그룹의 구성원인지 또는 누구에게 할당 정책이 할당되었는지 모르는 경우가 있습니다. 이 경우 **Get-ManagementRoleAssignment** cmdlet의 *GetEffectiveUsers* 스위치가 유용합니다. 여기서 사용자에게 할당된 역할 그룹, 할당 정책 및 USG를 통해 관리 역할이 제공하는 사용 권한이 부여된 사용자를 볼 수 있습니다.

*GetEffectiveUsers* 스위치는 **Get-ManagementRoleAssignment** cmdlet에서 *Role* 매개 변수가 사용될 때 함께 사용됩니다. 이 스위치와 특정 역할을 지정하면 **Get-ManagementRoleAssignment** cmdlet이 역할 그룹, 할당 정책 및 USG와 같이 역할에 할당된 모든 역할 담당자를 조사하고 각각의 구성원을 나열합니다.


> [!NOTE]
> <EM>GetEffectiveUser</EM> 스위치를 사용해도 연결된 외부 역할 그룹의 구성원인 사용자는 나열되지 않습니다. 사용자 목록 대신 연결된 역할 그룹이 발견되는 경우 <STRONG>연결된 모든 그룹 구성원</STRONG>이 표시됩니다. 다중 포리스트의 사용 권한에 대한 자세한 내용은 <A href="understanding-multiple-forest-permissions-exchange-2013-help.md">다중 포리스트 사용 권한을 이해 (영문)</A>을 참조하십시오.



관리 역할, 역할 그룹 및 할당 정책에 대한 자세한 내용은 [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)를 참조하십시오. 관리 역할 할당에 대한 자세한 내용은 [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)를 참조하십시오.

사용 권한 관리와 관련된 다른 관리 작업에 대한 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md)을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - [역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "역할 그룹" 또는 "역할 할당 정책" 항목.

  - 이 항목의 프로시저만 셸에서 수행할 수 있습니다. 실제 사용 권한을 보는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 모든 유효 사용자 나열

관리 역할을 통해 사용 권한이 부여된 모든 사용자를 나열하려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers
```

이 예에서는 Mail Recipients 역할을 통해 사용 권한이 부여된 모든 사용자를 나열합니다.

```powershell
Get-ManagementRoleAssignment -Role "Mail Recipients" -GetEffectiveUsers
```

목록에 반환되는 속성을 변경하거나 목록을 쉼표로 분리된 값(.csv) 파일로 내보내려면 이 항목의 후반부에 나오는 Use the Shell to customize output and display it를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 한 역할에서 특정 사용자 찾기

관리 역할을 통해 사용 권한이 부여된 특정 사용자를 찾으려면 **Get-ManagementRoleAssignment** cmdlet을 사용하여 모든 유효 사용자 목록을 검색한 다음 cmdlet의 출력을 **Where** cmdlet으로 파이프해야 합니다. **Where** cmdlet은 출력을 필터링하고 지정한 사용자만 반환합니다. 다음 구문을 사용합니다.

    Get-ManagementRoleAssignment -Role <role name> -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

이 예에서는 저널링 역할에서 사용자 David Strome을 찾습니다.

    Get-ManagementRoleAssignment -Role Journaling -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" }

목록에서 반환되는 속성을 변경하거나 목록을 .csv 파일로 내보내려면 이 항목의 후반부에 나오는 Use the Shell to customize output and display it를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 모든 역할에서 특정 사용자 찾기

사용자가 사용 권한을 부여받는 모든 역할을 확인하려면 **Get-ManagementRoleAssignment** cmdlet을 사용하여 모든 관리 역할에서 모든 유효 사용자를 검색한 다음 cmdlet의 출력을 **Where** cmdlet으로 파이프해야 합니다. **Where** cmdlet은 출력을 필터링하고 사용자에게 사용 권한을 부여하는 역할 할당만 반환합니다.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "<name of user>" }

이 예에서는 사용자 Kim Akers에게 사용 권한을 부여하는 모든 역할 할당을 찾습니다.

```powershell
Get-ManagementRoleAssignment -GetEffectiveUsers | Where {     Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "Kim Akers" }.EffectiveUserName -Eq "Kim Akers" }
```

목록에서 반환되는 속성을 변경하거나 목록을 CSV 파일로 내보내려면 이 항목 뒷부분의 Use the Shell to customize output and display it를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 출력을 사용자 지정 및 표시

**Get-ManagementRoleAssignment** cmdlet의 기본 출력에는 원하는 정보가 없을 수 있습니다. cmdlet의 출력에는 액세스할 수 있는 여러 추가 속성이 포함되어 있습니다. 다음은 유용하게 사용할 수 있는 몇 가지 속성입니다.

  - **EffectiveUserName**   사용자의 이름.

  - **역할**   권한을 부여하는 역할.

  - **RoleAssigneeName**   역할에 할당되며 `EffectiveUserName` 속성에 사용자를 포함하는 역할 그룹, 할당 정책 또는 USG입니다.

  - **RoleAssigneeType**   역할 할당이 역할 그룹, 할당 정책, USG 또는 사용자 중 어디에 적용되는지 나타냅니다.

  - **AssignmentMethod**   역할 및 역할 담당자 간의 할당이 직접적인지 또는 간접적인지 나타냅니다.

  - **CustomRecipientWriteScope**   역할 할당이 생성될 때 적용된 사용자 지정 받는 사람 쓰기 범위(있는 경우)를 나타냅니다. 이 속성에 지정된 범위는 `RecipientWriteScope` 속성에 지정된 암시적 받는 사람 쓰기 범위보다 우선합니다.

  - **CustomConfigWriteScope**   역할 할당이 생성될 때 적용된 사용자 지정 구성 쓰기 범위(있는 경우)를 나타냅니다. 이 속성에 지정된 범위는 `ConfigWriteScope` 속성에 지정된 암시적 구성 쓰기 범위보다 우선합니다.

  - **RecipientReadScope**   역할에 적용된 암시적 받는 사람 읽기 범위를 나타냅니다.

  - **RecipientWriteScope**   역할에 적용된 암시적 받는 사람 쓰기 범위를 나타냅니다.

  - **ConfigReadScope**   역할에 적용된 암시적 구성 읽기 범위를 나타냅니다.

  - **ConfigWriteScope**   역할에 적용된 암시적 구성 쓰기 범위를 나타냅니다.

목록에 표시할 속성을 선택하려면 Use the Shell to list all effective users, Use the Shell to find a specific user on a role 및 Use the Shell to find a specific user on all roles 섹션에서 사용된 것과 유사한 명령을 사용하면 됩니다. 다른 점은 이러한 명령의 결과를 **Format-Table** 또는 **Select-Object** cmdlet으로 파이프한다는 것입니다. **Format-Table** cmdlet은 결과의 목록을 화면에 출력하는 데 유용합니다. **Select-Object** cmdlet은 결과의 목록을 .csv 파일로 출력하는 데 유용합니다.

두 cmdlet 모두에서 보려고 하는 속성과 해당 순서를 지정할 수 있습니다. 출력을 전혀 수정하지 않는 **Select-Object**과는 다르게 **Format-Table** cmdlet은 화면에 결과를 나열할 때 더 많은 옵션을 제공하므로 목록을 .csv 파일로 파이프할 때 유용합니다.

**Format-Table** 및 **Select-Object** cmdlet에 대한 자세한 내용은 [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)을 참조하십시오.

## 화면에 사용자 지정된 목록 출력

1.  보려는 정보를 선택하고 다음 절차 중 하나에서 관련 명령을 찾습니다.
    
      - Use the Shell to list all effective users
    
      - Use the Shell to find a specific user a role
    
      - Use the Shell to find a specific user on all roles

2.  목록에서 보려는 속성을 선택합니다.

3.  목록을 보려면 다음 구문을 사용합니다.
    
        <command to retrieve list > | Format-Table <property 1>, <property 2>, <property ...>

이 예에서는 모든 역할에 있는 David Strome을 찾고 `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` 및 `CustomConfigWriteScope` 속성을 표시합니다.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Format-Table EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

## .csv 파일에 사용자 지정된 목록 출력

목록을 .csv 파일로 내보내려면 앞서 나열한 적절한 절차에서 **Get-ManagementRoleAssignment** 명령의 결과를 **Select-Object** cmdlet으로 파이프해야 합니다. **Select-Object** cmdlet의 결과는 지정한 파일 이름으로 .csv 출력을 저장하는 **Export-CSV** cmdlet으로 파이프됩니다.

1.  보려는 정보를 선택하고 다음 절차 중 하나에서 관련 명령을 찾습니다.
    
      - Use the Shell to list all effective users
    
      - Use the Shell to find a specific user a role
    
      - Use the Shell to find a specific user on all roles

2.  목록에서 보려는 속성을 선택합니다.

3.  다음 구문을 사용하여 목록을 .csv 파일로 내보냅니다.
    
        <command to retrieve list > | Select-Object <property 1>, <property 2>, <property ...> | Export-CSV <filename>

이 예에서는 모든 역할에 있는 David Strome을 찾고 `EffectiveUserName`, `Role`, `CustomRecipientWriteScope` 및 `CustomConfigWriteScope` 속성을 표시합니다.

    Get-ManagementRoleAssignment -GetEffectiveUsers | Where { $_.EffectiveUserName -Eq "David Strome" } | Select-Object EffectiveUserName, Role, CustomRecipientWriteScope, CustomConfigWriteScope | Export-CSV c:\output.csv

이제 원하는 뷰어에서 .csv 파일을 볼 수 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))를 참조하십시오.

