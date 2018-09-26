---
title: '기본 제공 역할 그룹을 미러링 하는 연결 된 역할 그룹 만들기: Exchange 2013 Help'
TOCTitle: 기본 제공 역할 그룹을 미러링 하는 연결 된 역할 그룹 만들기
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 50483604
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 기본 제공 역할 그룹을 미러링 하는 연결 된 역할 그룹 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

Microsoft Exchange Server 2013에서 연결된 관리 역할 그룹을 사용하면 Exchange 2013 리소스 포리스트에 있는 역할 그룹을 외부 사용자 포리스트에 있는 USG(유니버설 보안 그룹)와 연결할 수 있습니다. 사용자 포리스트에 계정이 있는 관리자가 리소스 포리스트에서 Exchange를 실행하는 서버를 관리하게 하려는 경우 이 방법이 유용합니다. 연결된 역할 그룹에 대한 자세한 내용은 [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)를 참조하십시오.

기본적으로 Exchange 2013에는 다양한 기능과 작업을 관리할 권한을 제공하는 여러 기본 제공 역할 그룹이 포함되어 있습니다. 각 역할 그룹은 각 기능과 작업에 특정 권한을 제공하도록 구성됩니다. 그러나 이러한 역할 그룹은 외부 포리스트에 있는 USG에 연결할 수 없습니다. 이러한 역할 그룹에는 로컬 리소스 포리스트에 있는 사용자 및 USG만 포함할 수 있습니다. 다행히 연결된 역할 그룹을 사용하면 이러한 기본 제공 역할 그룹을 복제할 수 있습니다.

각 기본 제공 역할 그룹을 연결된 역할 그룹으로 다시 만들 수 있습니다. 각 역할 그룹에 할당된 모든 관리 역할과 관리 범위가 새로운 연결된 역할 그룹에 추가됩니다. 관리 역할 및 범위에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)

  - [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)

역할 그룹과 관련된 다른 관리 작업에 대한 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 그룹" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 연결된 역할 그룹을 구성하려면 연결된 역할 그룹이 상주할 리소스 Active Directory 포리스트와 사용자 또는 USG가 상주하는 외부 Active Directory 포리스트 사이에 단방향 트러스트가 필요합니다. 리소스 포리스트는 외부 포리스트를 신뢰해야 합니다.

  - 외부 Active Directory 포리스트에 대한 다음 정보가 있어야 합니다.
    
      - **자격 증명** 외부 Active Directory 포리스트에 액세스할 수 있는 사용자 이름과 암호가 있어야 합니다. 이 정보는 **New-RoleGroup** cmdlet에서 *LinkedCredential* 매개 변수에 사용됩니다. 이 정보는 **Get-Credential** cmdlet을 실행하여 얻을 수 있습니다. 사용자 이름의 형식은 *domain*\\*username*입니다.
    
      - **도메인 컨트롤러**   외부 Active Directory 포리스트에 Active Directory 도메인 컨트롤러의 FQDN(정규화된 도메인 이름)이 있어야 합니다. 이 정보는 **New-RoleGroup** cmdlet에서 *LinkedDomainController* 매개 변수에 사용됩니다.
    
      - **외부 USG**   외부 Active Directory 포리스트에 연결된 역할 그룹과 연결할 구성원이 포함된 USG의 전체 이름이 있어야 합니다. 이 정보는 **New-RoleGroup** cmdlet에서 *LinkedForeignGroup* 매개 변수에 사용됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 기본 제공 역할 그룹을 복제하는 연결된 역할 그룹 만들기

다음 각 섹션에서는 각 역할 그룹을 연결된 역할 그룹으로 다시 만드는 방법을 보여 줍니다. 모든 기본 제공 역할 그룹을 연결된 역할 그룹으로 다시 만들려면 각 섹션에 있는 절차를 완료하십시오.

## 조직 관리 연결된 역할 그룹 만들기

조직 관리 역할 그룹을 연결된 역할 그룹으로 다시 만들려면 다른 기본 제공 역할 그룹을 다시 만드는 데 사용되는 것과 다른 절차를 수행해야 합니다. 이는 조직 관리 역할 그룹과 모든 관리 역할 사이에 위임 역할 할당이 있기 때문입니다. 위임 역할 할당을 다시 만들려면 추가 단계가 필요합니다.

1.  조직 관리 역할 그룹에 연결할 USG를 외부 포리스트에 만듭니다.

2.  외부 Active Directory 포리스트 자격 증명을 변수에 저장합니다.
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

3.  조직 관리 역할 그룹에 할당된 모든 역할을 변수에 저장합니다.
    
    ```powershell
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    ```

4.  조직 관리 연결된 역할 그룹을 만들고 기본 제공 조직 관리 역할 그룹에 할당된 역할을 추가합니다.
    
    ```powershell
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    ```

5.  새로운 조직 관리 연결된 역할 그룹과 My\* 형식의 최종 사용자 역할 사이의 모든 일반 할당을 제거합니다.
    
    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    ```

6.  새 조직 관리 연결된 역할 그룹과 모든 관리 역할 사이의 위임 역할 할당을 추가합니다.
    
    ```powershell
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating
    ```

이 예에서는 각 매개 변수에 다음 값이 사용되는 경우를 가정합니다.

  - **LinkedForeignGroup**   `Organization Management Administrators`

  - **LinkedDomainController**   `DC01.users.contoso.com`

이 예에서는 앞의 값을 사용하여 조직 관리 역할 그룹을 연결된 역할 그룹으로 다시 만듭니다.

```powershell
$ForeignCredential = Get-Credential
```
```powershell
$OrgMgmt  = Get-RoleGroup "Organization Management"
New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating
```

## 다른 모든 연결된 역할 그룹 만들기

조직 관리 역할 그룹이 아닌 기본 제공 역할 그룹을 연결된 역할 그룹으로 다시 만들려면 각 그룹에 대해 다음 절차를 사용합니다.

1.  각각의 새 역할 그룹에 연결할 USG를 각 역할 그룹의 외부 포리스트에 만듭니다.

2.  외부 Active Directory 포리스트 자격 증명을 변수에 저장합니다. 이 과정은 한 번만 수행하면 됩니다.
    
    ```powershell
    $ForeignCredential = Get-Credential
    ```

3.  다음 cmdlet을 사용하여 역할 그룹 목록을 검색합니다.
    
    ```powershell
    Get-RoleGroup
    ```

4.  조직 관리 역할 그룹이 아닌 각 역할 그룹에 대해 다음 작업을 수행합니다.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to re-create>
    New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    ```

5.  연결된 역할 그룹으로 다시 만들려는 각 기본 제공 역할 그룹에 대해 앞의 단계를 반복합니다.

이 예에서는 각 매개 변수에 다음 값이 사용되는 경우를 가정합니다.

  - **LinkedDomainController**   `DC01.users.contoso.com`

  - **연결된 역할 그룹으로 다시 만들 기본 제공 역할 그룹**   `Recipient Management, Server Management`

  - **받는 사람 관리 연결된 역할 그룹에 대한 외부 그룹**   `Recipient Management Administrators`

  - **서버 관리 연결된 역할 그룹에 대한 외부 그룹**   `Server Management Administrators`

이 예에서는 앞의 값을 사용하여 Recipient Management 및 서버 관리 역할 그룹을 연결된 역할 그룹으로 다시 만듭니다.

```powershell
$ForeignCredential = Get-Credential
```
```powershell
Get-RoleGroup
```
```powershell
$RoleGroup = Get-RoleGroup "Recipient Management"
New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
$RoleGroup = Get-RoleGroup "Server Management"
New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
```

## 다른 작업

연결된 역할 그룹을 만들었으면 다음 작업을 수행할 수 있습니다.

외부 포리스트에 있는 Active Directory 사용자 및 컴퓨터를 사용하여 외부 USG에 구성원을 추가합니다.

기본 제공 역할 그룹의 구성원을 제거합니다. 자세한 내용은 [역할 그룹 구성원 관리](manage-role-group-members-exchange-2013-help.md) 항목을 참조하십시오.

새로 연결된 역할 그룹에서 역할의 범위를 추가, 제거 또는 변경합니다. 자세한 내용은 [역할 그룹 관리](manage-role-groups-exchange-2013-help.md) 항목을 참조하십시오.

연결된 역할 그룹을 추가로 만듭니다. 자세한 내용은 [연결 된 역할 그룹 관리](manage-linked-role-groups-exchange-2013-help.md) 항목을 참조하십시오.

