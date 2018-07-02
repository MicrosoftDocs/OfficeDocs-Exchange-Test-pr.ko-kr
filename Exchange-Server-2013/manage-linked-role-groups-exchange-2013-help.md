---
title: '연결 된 역할 그룹 관리: Exchange 2013 Help'
TOCTitle: 연결 된 역할 그룹 관리
ms:assetid: e2a07395-90c2-4d62-b15d-ac3ff28fe786
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657502(v=EXCHG.150)
ms:contentKeyID: 50484399
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 연결 된 역할 그룹 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-09_

자원 Active Directory 포리스트에서 Microsoft Exchange Server 2013 조직 관리에 외부 Active Directory 포리스트에서 유니버설 보안 그룹 (USG)의 구성원을 사용 하도록 설정 하면 연결 된 관리 역할 그룹을 사용할 수 있습니다. 연결 된 역할 그룹과 외래 포리스트에 USG를 연결 하 여 그 구성원 USG의 사용 권한은 부여 받습니다 연결 된 역할 그룹에 할당 된 관리 역할에서 제공 합니다. 연결 된 역할 그룹에 대 한 자세한 내용은 [관리 역할 그룹 이해 (영문)](understanding-management-role-groups-exchange-2013-help.md)을 참조 하십시오.

을 만들고 연결 된 역할 그룹을 구성 하려면 **New-RoleGroup** 및 **Set-RoleGroup** cmdlet을 사용 하 여 지정 해야 합니다. 자세한 구문 및 매개 변수 정보에 대 한 다음 항목을 참조 합니다.

  - [New-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638181\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/ko-kr/library/dd638182\(v=exchg.150\))

역할 그룹에 관련된 추가 관리 작업은 [사용 권한](permissions-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5~10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 그룹" 항목

  - 만들거나 연결 된 역할 그룹을 구성 하려면 Exchange 관리 센터 (EAC)를 사용할 수 없습니다. Exchange 관리 셸을 사용 해야 합니다.

  - 여기에 최소한 연결 된 역할 그룹을 구성 해야는 연결 된 역할 그룹 상주할 리소스 Active Directory 포리스트 및 사용자 또는 Usg 있는 외래 Active Directory 포리스트 간에 단방향 트러스트 설정 되어 있는지 합니다. 리소스 포리스트 외부 포리스트를 신뢰 해야 합니다.

  - 외부 Active Directory 포리스트에 대한 다음 정보가 있어야 합니다.
    
      - **자격 증명**   사용자 이름 및 암호 외래 Active Directory 포리스트에 액세스할 수 있는 있어야 합니다. 이 정보는 **New-RoleGroup** 및 **Set-RoleGroup** cmdlet에서 *LinkedCredential* 매개 변수와 함께 사용 됩니다.
    
      - **도메인 컨트롤러**   외래 Active Directory 포리스트에서 Active Directory 도메인 컨트롤러의 정규화 된 도메인 이름 (FQDN) 있어야 합니다. 이 정보는 **New-RoleGroup** 및 **Set-RoleGroup** cmdlet에서 *LinkedDomainController* 매개 변수와 함께 사용 됩니다.
    
      - **외부 USG**   연결 된 역할 그룹에 연결 하려는 멤버를 포함 하는 외래 Active Directory 포리스트에 USG의 전체 이름이 있어야 합니다. 이 정보는 **New-RoleGroup** 및 **Set-RoleGroup** cmdlet에서 *LinkedForeignGroup* 매개 변수와 함께 사용 됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 연결 된 역할 그룹 만들기

## 셸을 사용하여 범위 없이 연결된 역할 그룹 만들기

연결된 역할 그룹을 만들고 연결된 역할 그룹에 관리 역할을 할당하려면 다음을 수행합니다.

1.  외부 Active Directory 포리스트 자격 증명을 변수에 저장합니다.
    
        $ForeignCredential = Get-Credential

2.  다음 구문을 사용하여 연결된 역할 그룹을 만듭니다.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  외부 Active Directory 포리스트에 있는 컴퓨터에서 Active Directory 사용자 및 컴퓨터를 사용하여 외부 USG에 대해 구성원을 추가하거나 제거합니다.

이 예에서는 다음을 수행합니다.

  - users.contoso.com 외부 Active Directory 포리스트의 자격 증명을 검색합니다. 이 자격 증명은 외부 포리스트의 DC01.users.contoso.com 도메인 컨트롤러에 연결하는 데 사용됩니다.

  - Exchange 2013 가 설치 되어있는 리소스 포리스트에서 준수 역할 그룹 이라고 하는 연결 된 역할 그룹을 만듭니다.

  - users.contoso.com 외부 Active Directory 포리스트의 Compliance Administrators USG에 새 역할 그룹을 연결합니다.

  - 새 연결된 역할 그룹에 전송 규칙 및 저널링 관리 역할을 할당합니다.

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles "Transport Rules", "Journaling"

## 셸을 사용하여 사용자 지정 관리 범위로 연결된 역할 그룹 만들기

사용자 지정 받는 사람 관리 범위, 사용자 지정 구성 관리 범위 또는 둘 다를 지정하여 연결된 역할 그룹을 만들 수 있습니다. 연결된 역할 그룹을 만들고 사용자 지정 범위로 연결된 역할 그룹에 관리 역할을 할당하려면 다음을 수행합니다.

1.  외부 Active Directory 포리스트 자격 증명을 변수에 저장합니다.
    
        $ForeignCredential = Get-Credential

2.  다음 구문을 사용하여 연결된 역할 그룹을 만듭니다.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -CustomConfigWriteScope <name of configuration scope> -CustomRecipientWriteScope <name of recipient scope> -LinkedCredential $ForeignCredential -Roles <role1, role2, role3...>

3.  외부 Active Directory 포리스트에 있는 컴퓨터에서 Active Directory 사용자 및 컴퓨터를 사용하여 외부 USG에 대해 구성원을 추가하거나 제거합니다.

이 예에서는 다음을 수행합니다.

  - users.contoso.com 외부 Active Directory 포리스트의 자격 증명을 검색합니다. 이 자격 증명은 외부 포리스트의 DC01.users.contoso.com 도메인 컨트롤러에 연결하는 데 사용됩니다.

  - Exchange 2013 가 설치 되어있는 리소스 포리스트에서 시애틀 준수 역할 그룹 이라고 하는 연결 된 역할 그룹을 만듭니다.

  - users.contoso.com 외부 Active Directory 포리스트의 Seattle Compliance Administrators에 새 역할 그룹을 연결합니다.

  - Seattle Recipients 사용자 지정 받는 사람 범위로 새 연결된 역할 그룹에 전송 규칙 및 저널링 관리 역할을 할당합니다.

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Seattle Compliance Role Group" -LinkedForeignGroup "Seattle Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -CustomRecipientWriteScope "Seattle Recipients" -Roles "Transport Rules", "Journaling"

관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

## 셸을 사용하여 OU 범위로 연결된 역할 그룹 만들기

OU 받는 사람 범위를 사용하는 연결된 역할 그룹을 만들 수 있습니다. 연결된 역할 그룹을 만들고 OU 범위로 연결된 역할 그룹에 관리 역할을 할당하려면 다음을 수행합니다.

1.  외부 Active Directory 포리스트 자격 증명을 변수에 저장합니다.
    
        $ForeignCredential = Get-Credential

2.  다음 구문을 사용하여 연결된 역할 그룹을 만듭니다.
    
        New-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope <OU name> -Roles <role1, role2, role3...>

3.  외부 Active Directory 포리스트에 있는 컴퓨터에서 Active Directory 사용자 및 컴퓨터를 사용하여 외부 USG에 대해 구성원을 추가하거나 제거합니다.

이 예에서는 다음을 수행합니다.

  - users.contoso.com 외부 Active Directory 포리스트의 자격 증명을 검색합니다. 이 자격 증명은 외부 포리스트의 DC01.users.contoso.com 도메인 컨트롤러에 연결하는 데 사용됩니다.

  - Exchange 2013 가 설치 되어있는 리소스 포리스트에서 임원 준수 역할 그룹 이라고 하는 연결 된 역할 그룹을 만듭니다.

  - users.contoso.com 외부 Active Directory 포리스트의 Executives Compliance Administrators USG에 새 역할 그룹을 연결합니다.

  - OU 받는 사람 범위인 Executives OU를 지정하여 새 연결된 역할 그룹에 전송 규칙 및 저널링 관리 역할을 할당합니다.

<!-- end list -->

    $ForeignCredential = Get-Credential
    New-RoleGroup "Executives Compliance Role Group" -LinkedForeignGroup "Executives Compliance Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -RecipientOrganizationalUnitScope "Executives OU" -Roles "Transport Rules", "Journaling"

관리 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

## 연결 된 역할 그룹에 있는 외부 USG를 변경 합니다.

## 셸을 사용하여 연결된 역할 그룹의 외부 USG 변경

연결된 역할 그룹과 관련된 외부 USG를 변경하려면 다음을 수행하십시오.

1.  외부 Active Directory 포리스트 자격 증명을 변수에 저장합니다.
    
        $ForeignCredential = Get-Credential

2.  다음 구문을 사용 하 여 기존 연결 된 역할 그룹에 있는 외부 USG를 변경 합니다.
    
        Set-RoleGroup <role group name> -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential 

이 예에서는 다음을 수행합니다.

  - users.contoso.com 외부 Active Directory 포리스트의 자격 증명을 검색합니다. 이 자격 증명은 외부 포리스트의 DC01.users.contoso.com 도메인 컨트롤러에 연결하는 데 사용됩니다.

  - Compliance Role Group 역할 그룹의 외부 USG를 Regulatory Compliance Officers로 변경합니다.

<!-- end list -->

    $ForeignCredential = Get-Credential
    Set-RoleGroup "Compliance Role Group" -LinkedForeignGroup "Regulatory Compliance Officers" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential

