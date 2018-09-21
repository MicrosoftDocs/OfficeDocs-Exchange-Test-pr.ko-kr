---
title: '역할 보기: Exchange 2013 Help'
TOCTitle: 역할 보기
ms:assetid: 1875b15f-22db-4ede-b310-ea894d6211c8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335117(v=EXCHG.150)
ms:contentKeyID: 50482611
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 보기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

원하는 정보에 따라 다양한 방식으로 관리 역할을 나열할 수 있습니다. 예를 들어 특정 역할 유형의 역할만 반환하거나, 특정 cmdlet과 매개 변수만 포함된 역할을 반환하거나, 특정 관리 역할의 세부 정보를 표시하도록 선택할 수 있습니다. Microsoft Exchange Server 2013의 관리 역할에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

역할의 모든 관리 역할 항목 목록을 보려면 [역할 항목 보기](view-role-entries-exchange-2013-help.md)를 참조하십시오.

역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목에서는 파이프라이닝과 **Format-List** 및 **Format-Table** cmdlet을 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.
    
      - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))
    
      - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 특정 관리 역할 보기

**Get-ManagementRole** cmdlet을 사용하여 특정 역할을 검색하고 그 출력을 **Format-List** cmdlet으로 파이프하여 특정 역할의 세부 정보를 볼 수 있습니다.

특정 역할의 세부 정보를 보려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRole <role name> | Format-List
```

이 예에서는 Mail Recipients 관리 역할의 세부 정보를 검색합니다.

```powershell
Get-ManagementRole "Mail Recipients" | Format-List
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))을 참조하십시오.

## 모든 관리 역할 표시

**Get-ManagementRole** cmdlet을 실행할 때 역할을 지정하지 않으면 조직의 모든 관리 역할 목록을 볼 수 있습니다. 기본적으로 각 역할의 역할 이름과 역할 유형이 결과에 포함됩니다.

이 예에서는 조직의 모든 역할 목록이 반환됩니다.

```powershell
Get-ManagementRole
```

조직에 있는 모든 역할의 특정 속성 목록을 반환하려면 **Format-Table** cmdlet의 결과를 파이프하고 결과 목록에서 원하는 속성을 지정할 수 있습니다. 다음 구문을 사용합니다.

```powershell
Get-ManagementRole | Format-Table <property 1>, <property 2...>
```

이 예에서는 조직의 모든 역할 목록을 반환하고 속성 이름이 **Implicit**로 시작하는 모든 속성과 **Name** 속성을 포함합니다.

    Get-ManagementRole | Format-Table Name, Implicit*

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))를 참조하십시오.

## 특정 cmdlet이 포함된 관리 역할 표시

**Get-ManagementRole** cmdlet에 *Cmdlet* 매개 변수를 사용하면 지정한 cmdlet이 포함된 역할 목록을 반환할 수 있습니다.

지정한 cmdlet이 포함된 역할 목록을 반환하려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRole -Cmdlet <cmdlet>
```

이 예에서는 **New-Mailbox** cmdlet이 포함된 역할 목록을 반환합니다.

```powershell
Get-ManagementRole -Cmdlet New-Mailbox
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))를 참조하십시오.

## 특정 매개 변수가 포함된 관리 역할 표시

**Get-ManagementRole** cmdlet에 *CmdletParameters* 매개 변수를 사용하면 지정한 하나 이상의 매개 변수가 포함된 역할 목록을 반환할 수 있습니다. 지정한 매개 변수가 모두 포함된 역할만 반환됩니다.

*CmdletParameters* 매개 변수를 사용하는 경우 *Cmdlet* 매개 변수를 포함할 수 있습니다. *Cmdlet* 매개 변수를 포함하면 지정한 cmdlet에서 지정한 매개 변수가 포함된 역할만 반환됩니다. *Cmdlet* 매개 변수를 포함하지 않으면 매개 변수가 위치한 cmdlet에 관계없이 지정한 매개 변수가 포함된 역할이 반환됩니다.

지정한 매개 변수가 포함된 역할 목록을 반환하려면 다음 구문을 사용합니다.

    Get-ManagementRole [-Cmdlet <cmdlet>] -CmdletParameters <parameter 1>, <parameter 2...>

이 예에서는 매개 변수가 위치한 cmdlet에 관계없이 *Database* 및 *Server* 매개 변수가 포함된 역할 목록을 반환합니다.

```powershell
Get-ManagementRole -CmdletParameters Database, Server
```

이 예에서는 *EmailAddresses* 매개 변수가 **Set-Mailbox** cmdlet에만 있는 역할 목록을 반환합니다.

```powershell
Get-ManagementRole -Cmdlet Set-Mailbox -CmdletParameters EmailAddresses
```

*Cmdlet* 또는 *CmdletParameters* 매개 변수에 와일드카드 문자(\*)를 사용하여 cmdlet 또는 매개 변수의 부분 이름을 일치시킬 수도 있습니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))를 참조하십시오.

## 특정 역할 유형의 관리 역할 표시

**Get-ManagementRole** cmdlet에 *RoleType* 매개 변수를 사용하면 지정한 역할 유형에 따라 역할 목록을 반환할 수 있습니다.

지정한 역할 유형과 일치하는 역할 목록을 반환하려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRole -RoleType <roletype>
```

이 예에서는 `UmMailboxes` 역할 유형에 따라 역할 목록을 반환합니다.

```powershell
Get-ManagementRole -RoleType UmMailboxes
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))를 참조하십시오.

## 상위 역할의 직접 하위 역할 표시

**Get-ManagementRole** cmdlet에 *GetChildren* 매개 변수를 사용하면 지정한 상위 역할의 직접 하위인 역할 목록을 반환할 수 있습니다. 상위 역할로 지정한 역할이 포함된 역할만 반환됩니다.

상위 역할의 직접 하위 역할 목록을 반환하려면 다음 구문을 사용합니다.

```powershell
Get-ManagementRole <parent role name> -GetChildren
```

이 예에서는 Disaster Recovery 역할의 직접 하위 목록을 반환합니다.

```powershell
Get-ManagementRole "Disaster Recovery" -GetChildren
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))를 참조하십시오.

## 상위 역할 아래의 모든 하위 역할 표시

**Get-ManagementRole** cmdlet에 *Recurse* 매개 변수를 사용하면 지정한 상위 역할에서 마지막 하위 역할까지 전체 역할 체인 목록을 반환할 수 있습니다. *Recurse* 매개 변수를 포함하면 **Get-ManagementRole** cmdlet이 마지막 하위 역할에 도달할 때까지 찾은 모든 상위 및 하위 관계를 재귀적으로 사용합니다. 상위 역할이 반환되는 목록에 포함됩니다.

이 예에서는 상위 역할의 모든 하위 역할 목록을 반환합니다.

```powershell
Get-ManagementRole <parent role name> -Recurse
```

이 예에서는 Mail Recipients 역할의 모든 하위 역할을 반환합니다.

```powershell
Get-ManagementRole "Mail Recipients" -Recurse
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351125\(v=exchg.150\))를 참조하십시오.

