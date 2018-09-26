---
title: 'Exchange 2013 공유 사용 권한 구성: Exchange 2013 Help'
TOCTitle: Exchange 2013 공유 사용 권한 구성
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 50483522
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 공유 사용 권한 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-07_

공유 사용 권한을 사용하면 Microsoft Exchange Server 2013 관리자는 Active Directory 보안 주체(예: 사용자)를 만들어 Exchange 받는 사람으로 구성할 수 있습니다. Exchange 관리자 그룹과 Active Directory 관리자 그룹 간 관리 작업을 나누는 사용 권한 분할 모델과는 달리 공유 사용 권한에는 작업 구분이 없습니다.

사용 권한 공유 및 분할에 대한 자세한 내용은 [분할 권한 이해](understanding-split-permissions-exchange-2013-help.md)를 참조하십시오.

이전에 사용 권한 분할 모델로 조직을 설정한 경우 공유 사용 권한에 맞게 Exchange 2013 조직을 구성할 수 있습니다. 공유 사용 권한을 전환하는 절차는 현재 RBAC(역할 기반 액세스 제어) 사용 권한 분할과 Active Directory 사용 권한 분할 중 어느 것을 사용하는지에 따라 다릅니다. 아래에서 현재 구성에 해당되는 절차를 선택하십시오. 다음 조건에 해당되면 조직에서 Active Directory 사용 권한 분할을 사용하고 있는 것입니다.

  - Microsoft Exchange 보호 그룹 OU(조직 구성 단위)가 있습니다.

  - Exchange Windows 사용 권한 보안 그룹이 Microsoft Exchange 보호 그룹 OU에 있습니다.

  - Exchange Trusted Subsystem 보안 그룹이 Exchange Windows 사용 권한 보안 그룹의 구성원입니다.

  - Mail Recipient Creation 역할 또는 Security Group Creation and Membership 역할에 일반 관리 역할이 할당되지 않았습니다.

이전에 사용 권한 분할 모델로 조직을 구성하지 않은 경우에는 이 절차를 수행하지 않아도 됩니다. Exchange 2013은 기본적으로 공유 사용 권한에 맞게 구성됩니다.

관리 역할 그룹, 관리 역할과, 일반 및 위임 관리 역할 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)

  - [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)

  - [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

사용 권한과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - Windows PowerShell, Windows Command Shell 또는 둘 모두를 사용하여 이러한 절차를 수행해야 합니다. 자세한 내용은 각 절차를 참조하십시오.

  - Exchange 2013 조직이 현재 RBAC 또는 Active Directory 사용 권한 분할 모델로 구성되어 있어야 합니다.

  - 조직에 Microsoft Exchange Server 2010 서버가 있는 경우 선택한 사용 권한 모델이 이러한 서버에도 적용됩니다.

  - Mail Recipient Creation 관리 역할과 Security Group Creation and Membership 관리 역할을 조직 관리 관리 역할 그룹 또는 Mail Recipients 역할이 할당된 또 다른 그룹에 위임할 수 있는 사용 권한이 있어야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## RBAC 사용 권한 분할에서 공유 사용 권한으로 전환

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 그룹" 항목

RBAC 사용 권한 분할을 Exchange 2013 공유 사용 권한으로 전환하려면, Mail Recipients 역할이 할당되고 Exchange 2013 관리자를 구성원으로 가지고 있는 역할 그룹에 Mail Recipient Creation 역할과 Security Group Creation and Membership 역할을 할당해야 합니다. 기본 공유 사용 권한 구성에서 조직 관리 역할 그룹에는 이러한 각 역할이 포함되어 있습니다. 따라서 조직 관리 역할 그룹이 이 절차에 있습니다.

## 공유 사용 권한 구성

조직 관리 역할 그룹에 대해 공유 사용 권한을 구성하려면 Mail Recipient Creation 역할과 Security Group Creation and Membership 역할에 대한 역할 할당을 위임할 수 있는 사용 권한이 있는 계정을 사용하여 다음을 수행합니다.

1.  다음 명령을 사용하여 Mail Recipient Creation 역할과 Security Group Creation and Membership 역할에 대한 위임 역할 할당을 조직 관리 역할 그룹에 추가합니다.
        
```powershell
New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
```    

> [!NOTE]  
> <STRONG>New-ManagementRoleAssignment</STRONG> cmdlet을 실행하려면 Mail Recipient Creation 역할과 Security Group Creation and Membership 역할에 대한 위임 역할 할당이 있는 역할 그룹(이 절차에서는 Active Directory Administrators 역할 그룹)을 Role Management 역할에 할당해야 합니다. Role Management 역할을 위임할 수 있는 역할 담당자는 해당 역할을 Active Directory Administrators 역할 그룹에 할당해야 합니다.

2.  다음 명령을 사용하여 Mail Recipient Creation 역할에 대한 일반 역할 할당을 조직 관리 및 Recipient Management 역할 그룹에 추가합니다.

```powershell    
New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"
```
3.  다음 명령을 사용하여 Security Group Creation and Membership 역할에 대한 일반 역할 할당을 조직 관리 역할 그룹에 추가합니다.
    
```powershell
New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
```
구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

## Active Directory 관리자의 사용 권한 제거(옵션)

Active Directory 관리자가 Exchange 관리 도구를 사용하여 Active Directory 개체를 만들거나 관리하지 못하게 하려면 관리자에게 부여된 사용 권한을 선택적으로 제거할 수 있습니다. Active Directory 관리자의 사용 권한을 제거하려면 다음 절차를 수행합니다.


> [!NOTE]   
> Exchange 관리 도구를 사용하여 Active Directory 개체를 관리하는 Active Directory 관리자의 사용 권한을 제거할 수는 있지만, Active Directory 사용 권한에서 허용하는 경우 Active Directory 관리자는 Active Directory 관리 도구를 사용하여 Active Directory 개체를 계속 관리할 수 있습니다. 하지만 Active Directory 개체의 Exchange 관련 특성은 관리할 수 없게 됩니다. 자세한 내용은 <A href="understanding-split-permissions-exchange-2013-help.md">분할 권한 이해</A>를 참조하십시오.


Active Directory 관리자의 Exchange 관련 분할 사용 권한을 제거하려면 다음을 수행합니다.

1.  다음 명령을 사용하여 Active Directory 관리자가 구성원으로 속해 있는 USG(유니버설 보안 그룹)나 역할 그룹에 Mail Recipient Creation 역할을 할당하는 일반 및 위임 역할 할당을 제거합니다. 이 명령에서는 Active Directory Administrators 역할 그룹을 예로 사용합니다. *WhatIf* 스위치를 사용하면 제거될 역할 할당을 볼 수 있습니다. *WhatIf* 스위치를 제거하고 명령을 다시 실행하면 역할 할당이 제거됩니다.
    
```powershell
Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
```

2.  다음 명령을 사용하여 Active Directory 관리자가 구성원으로 속해 있는 USG나 역할 그룹에 Security Group Creation and Membership 역할을 할당하는 일반 및 위임 역할 할당을 제거합니다. 이 명령에서는 Active Directory Administrators 역할 그룹을 예로 사용합니다. *WhatIf* 스위치를 사용하면 제거될 역할 할당을 볼 수 있습니다. *WhatIf* 스위치를 제거하고 명령을 다시 실행하면 역할 할당이 제거됩니다.
    
```powershell
Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
```

3.  선택 사항입니다. Active Directory 관리자의 Exchange 사용 권한을 모두 제거하려면 해당 관리자가 구성원으로 속해 있는 USG나 역할 그룹을 제거할 수 있습니다. 역할 그룹을 제거하는 방법에 대한 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\)) 또는 [Remove-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351205\(v=exchg.150\))를 참조하십시오.

## Active Directory 사용 권한 분할에서 공유 사용 권한으로 전환

[역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "Active Directory 사용 권한 분할" 항목

Active Directory 사용 권한 분할을 Exchange 2013 공유 사용 권한으로 전환하려면 Exchange 설치를 다시 실행하여 Active Directory 조직에서 Exchange 사용 권한 분할을 사용하지 않도록 설정한 다음, 역할 그룹과 Mail Recipient Creation 역할 및 Security Group Creation and Membership 역할 사이에 역할 할당을 만들어야 합니다. 기본 공유 사용 권한 구성에서 조직 관리 역할 그룹에는 이러한 각 역할이 포함되어 있습니다. 따라서 조직 관리 역할 그룹이 이 절차에 있습니다.


> [!IMPORTANT]  
> 이 절차의 setup.com 명령은 Active Directory를 변경합니다. 이러한 변경을 수행하는 데 필요한 사용 권한이 있는 계정을 사용해야 합니다. 이 계정은 <STRONG>New-ManagementRoleAssignment</STRONG>&nbsp;cmdlet을 사용하여 역할 할당을 만들 사용 권한이 있는 계정과 같은 계정이 아닐 수도 있습니다. 이 절차의 각 단계를 완료하는 데 필요한 사용 권한이 있는 계정을 사용해야 합니다.



Active Directory 사용 권한 분할을 공유 사용 권한으로 전환하려면 다음을 수행합니다.

1.  Windows 명령 셸에서 Exchange 2013 설치 미디어로부터 다음 명령을 실행하여 Active Directory 사용 권한 분할을 사용하지 않도록 설정합니다.
    
    ```powershell
    setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    ```

2.  Exchange 관리 셸에서 다음 명령을 실행하여 Mail Recipient Creation 역할과 Security Group Creation and Management 역할 및 조직 관리와 Recipient Management 역할 그룹 사이에 일반 역할 할당을 추가합니다.
    
    ```powershell
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"
    ```
3.  조직에서 Exchange 2013 서버를 다시 시작합니다.
    

    > [!NOTE]
    > 조직에서 Exchange 2010 서버를 포함 하는 경우 이러한 서버를 다시 시작 해야할 수도 있습니다.



구문과 매개 변수에 대한 자세한 내용은 [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))를 참조하십시오.

