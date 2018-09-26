---
title: 'Exchange 2013 분할 된 사용 권한 구성: Exchange 2013 Help'
TOCTitle: Exchange 2013 분할 된 사용 권한 구성
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 50483627
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2013 분할 된 사용 권한 구성

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2015-04-07_

사용 권한을 분할하면 Active Directory 관리자 및 Microsoft Exchange Server 2013 관리자와 같은 별개의 두 그룹에서 각자의 서비스, 개체 및 특성을 관리할 수 있습니다. Active Directory 관리자는 Active Directory 포리스트에 대한 액세스 권한을 제공하는 사용자 등의 보안 주체를 관리합니다. Exchange 관리자는 Active Directory 개체에 대한 Exchange 관련 특성을 관리하고 Exchange 관련 개체를 만들고 관리합니다.

Microsoft Exchange Server 2013은 다음과 같은 유형의 사용 권한 분할 모델을 제공합니다.

  - <strong>RBAC 사용 권한 분할</strong>   Active Directory 도메인 파티션에 보안 주체를 만드는 권한은 RBAC(역할 기반 액세스 제어)에서 제어합니다. 적절한 역할 그룹의 구성원만 보안 주체를 만들 수 있습니다.

  - <strong>Active Directory 분할 권한</strong>   Active Directory 도메인 파티션에서 보안 주체를 만들 권한이 Exchange 사용자, 서비스 또는 서버에서 완전히 제거됩니다. RBAC에는 보안 주체를 만들 수 있는 옵션이 제공되지 않습니다. Active Directory에서 보안 주체를 만들려면 Active Directory 관리 도구를 사용해야 합니다.
    

    > [!NOTE]
    > Active Directory 사용 권한 분할은 Microsoft Exchange Server 2010 SP1(서비스 팩 1) 이상, Exchange 2013 또는 Exchange의 두 버전을 모두 실행하는 조직에서 사용할 수 있습니다.



선택하는 모델은 조직의 구조와 요구 사항에 따라 결정됩니다. 구성하고자 하는 모델에 적합한 절차를 아래에서 선택하십시오. RBAC 사용 권한 분할 모델을 사용하는 것이 좋습니다. RBAC 사용 권한 분할 모델은 Active Directory 사용 권한 분할과 같은 수준의 관리 분리 기능을 제공하지만 유연성은 훨씬 뛰어납니다.

사용 권한 공유 및 분할에 대한 자세한 내용은 [분할 권한 이해](understanding-split-permissions-exchange-2013-help.md)를 참조하십시오.

관리 역할 그룹, 관리 역할과, 일반 및 위임 관리 역할 할당에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [역할 기반 액세스 제어 이해](understanding-role-based-access-control-exchange-2013-help.md)

  - [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)

  - [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)

  - [관리 역할 할당 이해 (영문)](understanding-management-role-assignments-exchange-2013-help.md)

사용 권한과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - [역할 관리 권한](role-management-permissions-exchange-2013-help.md) 항목의 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. "Active Directory 사용 권한 분할" 항목

  - Windows PowerShell이나 Windows 명령 셸 또는 둘 모두를 사용하여 이러한 절차를 수행해야 합니다. 자세한 내용은 각 절차를 참조하십시오.

  - 조직에서 Exchange 2010 서버를 포함 하는 경우에 선택 하는 사용 권한 모델 이러한 서버에 적용 됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## RBAC 사용 권한 분할로 전환

RBAC 사용 권한 분할에 맞게 Exchange 2013 조직을 구성할 수 있습니다. 구성이 완료되면 Active Directory 관리자만 Active Directory 보안 주체를 만들 수 있습니다. 즉, Exchange 관리자는 다음 cmdlet을 사용할 수 없습니다.

  - <strong>New-Mailbox</strong>

  - <strong>New-MailContact</strong>

  - <strong>New-MailUser</strong>

  - <strong>New-RemoteMailbox</strong>

  - <strong>Remove-Mailbox</strong>

  - <strong>Remove-MailContact</strong>

  - <strong>Remove-MailUser</strong>

  - <strong>Remove-RemoteMailbox</strong>

Exchange 관리자는 기존 Active Directory 보안 주체의 Exchange 특성만 관리할 수 있습니다. 하지만 전송 규칙 및 메일 그룹과 같은 Exchange 관련 개체는 만들고 관리할 수 있습니다. 자세한 내용은 [분할 권한 이해](understanding-split-permissions-exchange-2013-help.md)의 "RBAC 사용 권한 분할" 섹션을 참조하십시오.

사용 권한 분할에 맞게 Exchange 2013을 구성하려면 Mail Recipient Creation 역할과 Security Group Creation and Membership을 Active Directory 관리자인 구성원이 포함된 역할 그룹에 할당해야 합니다. 그런 다음 그러한 역할 및 Exchange 관리자가 포함된 모든 역할 그룹 또는 USG(유니버설 보안 그룹) 사이에서 할당을 제거해야 합니다.

RBAC 사용 권한 분할을 구성하려면 다음을 수행합니다.

1.  조직이 현재 Active Directory 사용 권한 분할을 사용하도록 구성된 경우에는 Windows 명령 셸 프롬프트에서 다음을 수행합니다.
    
    1.  Exchange 2013 설치 미디어에서 다음 명령을 실행하여 Active Directory 사용 권한 분할을 사용하지 않도록 설정합니다.
        
        ```powershell
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
        ```
    
    2.  조직에서 Exchange 2013 서버를 다시 시작하거나 Active Directory 액세스 토큰이 모든 Exchange 2013 서버에 복제되기를 기다립니다.
        

        > [!NOTE]
        > 조직에서 Exchange 2010 서버를 포함 하는 경우 이러한 서버를 다시 시작 해야할 수도 있습니다.

2.  Exchange 관리 셸에서 다음을 수행합니다.
    
    1.  Active Directory 관리자의 역할 그룹을 만듭니다. 이 명령은 역할 그룹을 만드는 것 외에도 새 역할 그룹과 Mail Recipient Creation 역할 및 Security Group Creation and Membership 역할 사이에 일반 역할 할당을 만듭니다.
        
        ```powershell
        New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        ```

        > [!NOTE]
        > 이 역할 그룹의 구성원이 역할 할당을 만들 수 있게 하려면 Role Management 역할을 포함합니다. 지금은 이 역할을 추가할 필요가 없습니다. 하지만 Mail Recipient Creation 역할이나 Security Group Creation and Membership 역할을 다른 역할 담당자에게 할당하려는 경우에는 이 새 역할 그룹에 Role Management 역할을 할당해야 합니다. 다음 단계에서는 Active Directory 관리자 역할 그룹을 이러한 역할을 위임할 수 있는 유일한 역할 그룹으로 구성합니다.

    
    2.  다음 명령을 사용하여 새 역할 그룹과 Mail Recipient Creation 역할 및 Security Group Creation and Membership 역할 사이의 위임 역할 할당을 만듭니다.
        
        ```powershell
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
        ```
    
    3.  다음 명령을 사용하여 새 역할 그룹에 구성원을 추가합니다.
        
        ```powershell
        Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
        ```
    
    4.  역할 그룹 구성원만 구성원을 추가 또는 제거할 수 있도록 새 역할 그룹에서 위임 목록을 바꿉니다.
        
        ```powershell
        Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        ```      

        > [!IMPORTANT]  
        > 조직 관리 역할 그룹 구성원이나 직접 또는 다른 역할 그룹이나 USG를 통해 역할 관리 역할이 할당된 사용자는 이 위임 보안 검사를 무시할 수 있습니다. Exchange 관리자가 새 역할 그룹에 자신을 추가하지 못하게 하려면 Role Management 역할과 Exchange 관리자 사이의 모든 역할 할당을 제거하고 관리자를 다른 역할 그룹에 할당해야 합니다.

    
    5.  다음 명령을 사용하여 Mail Recipient Creation 역할에 대한 일반 및 위임 역할 할당을 모두 찾습니다. 이 명령은 <strong>Name</strong>, <strong>Role</strong> 및 <strong>RoleAssigneeName</strong> 속성을 표시합니다.

        ```powershell        
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
        ```
    
    6.  다음 명령을 사용하여 유지하고자 하는 새 역할 그룹이나 다른 역할 그룹, USG 또는 직접 할당과 관련되지 않은 Mail Recipient Creation 역할에 대한 일반 및 위임 역할 할당을 모두 제거합니다.
        
        ```powershell
        Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        ```       

        > [!NOTE]
        > Active Directory 관리자 역할 그룹이 아닌 역할 담당자에게서 Mail Recipient Creation 역할에 대한 모든 일반 및 위임 역할 할당을 제거하려면 다음 명령을 사용합니다. <EM>WhatIf</EM> 스위치를 사용하면 제거될 역할 할당을 볼 수 있습니다. <EM>WhatIf</EM> 스위치를 제거하고 명령을 다시 실행하면 역할 할당이 제거됩니다.

        ```powershell
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
        ```
    
    7.  다음 명령을 사용하여 Security Group Creation and Membership 역할에 대한 일반 및 위임 역할 할당을 모두 찾습니다. 이 명령은 <strong>Name</strong>, <strong>Role</strong> 및 <strong>RoleAssigneeName</strong> 속성을 표시합니다.
        
        ```powershell
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
        ```
    
    8.  다음 명령을 사용하여 유지하고자 하는 새 역할 그룹이나 다른 역할 그룹, USG 또는 직접 할당과 관련되지 않은 Security Group Creation and Membership 역할에 대한 일반 및 위임 역할 할당을 모두 제거합니다.
        
        ```powershell
        Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        ```       

        > [!NOTE]  
        > 이 예에서와 같이, 위 참고와 동일한 명령을 사용하여 Active Directory 관리자 역할 그룹이 아닌 모든 역할 담당자에게서 Security Group Creation and Membership 역할에 대한 일반 및 위임 할당을 모두 제거할 수 있습니다.

        ```powershell
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
        ```

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [New-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/ko-kr/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/ko-kr/library/dd351205\(v=exchg.150\))

## Active Directory 사용 권한 분할로 전환

Exchange 2013 조직을 Active Directory 사용 권한 분할에 맞게 구성할 수 있습니다. Active Directory 사용 권한 분할은 Exchange 관리자 및 서버가 Active Directory에서 보안 주체를 만들거나 해당 개체에서 비 Exchange 특성을 수정하도록 해 주는 사용 권한을 완전히 제거합니다. 구성이 완료되면 Active Directory 관리자만 Active Directory 보안 주체를 만들 수 있습니다. 즉, Exchange 관리자는 다음 cmdlet을 사용할 수 없습니다.

  - <strong>Add-DistributionGroupMember</strong>

  - <strong>New-DistributionGroup</strong>

  - <strong>New-Mailbox</strong>

  - <strong>New-MailContact</strong>

  - <strong>New-MailUser</strong>

  - <strong>New-RemoteMailbox</strong>

  - <strong>Remove-DistributionGroup</strong>

  - <strong>Remove-DistributionGroupMember</strong>

  - <strong>Remove-Mailbox</strong>

  - <strong>Remove-MailContact</strong>

  - <strong>Remove-MailUser</strong>

  - <strong>Remove-RemoteMailbox</strong>

  - <strong>Update-DistributionGroupMember</strong>

Exchange 관리자 및 서버는 기존 Active Directory 보안 주체의 Exchange 특성만 관리할 수 있습니다. 하지만 전송 규칙 및 통합 메시징 다이얼 플랜과 같은 Exchange 관련 개체를 만들고 관리할 수 있습니다.


> [!WARNING]  
> Active Directory 사용 권한 분할을 사용하도록 설정하면 Exchange 관리자 및 서버는 더 이상 Active Directory에 보안 주체를 만들 수 없으며 메일 그룹 구성원도 관리할 수 없습니다. 이러한 작업은 필요한 Active Directory 사용 권한을 갖춘 Active Directory 관리 도구를 사용하여 수행해야 합니다. 이 변경을 수행하기 전에 Exchange 2013 및 RBAC 사용 권한 모델과 통합되는 관리 프로세스 및 타사 응용 프로그램에 미치는 영향을 이해해야 합니다.<BR>자세한 내용은 <A href="understanding-split-permissions-exchange-2013-help.md">분할 권한 이해</A>의 "Active Directory 사용 권한 분할" 섹션을 참조하십시오.



공유 또는 RBAC 사용 권한 분할에서 Active Directory 사용 권한 분할로 전환하려면 다음을 수행합니다.

1.  Windows 명령 셸에서 Exchange 2013 설치 미디어로부터 다음 명령을 실행하여 Active Directory 사용 권한 분할을 사용하도록 설정합니다.
    
    ```powershell
    setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true
    ```

2.  조직에 여러 Active Directory 도메인이 있으면 Exchange 서버 또는 개체가 포함된 하위 도메인 각각에서 `setup.exe /PrepareDomain`를 실행하거나 모든 도메인에서 Active Directory 서버가 있는 사이트로부터 `setup.exe /PrepareAllDomains`를 실행해야 합니다.

3.  조직에서 Exchange 2013 서버를 다시 시작하거나 Active Directory 액세스 토큰이 모든 Exchange 2013 서버에 복제되기를 기다립니다.
    

    > [!NOTE]
    > 조직에서 Exchange 2010 서버를 포함 하는 경우 이러한 서버를 다시 시작 해야할 수도 있습니다.


