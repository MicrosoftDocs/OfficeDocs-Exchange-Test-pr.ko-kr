---
title: '역할에서 역할 항목을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 역할에서 역할 항목을 제거 합니다.
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 50483013
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할에서 역할 항목을 제거 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

관리 역할의 관리 역할 항목에 따라 관리 역할에서 사용할 수 있는 cmdlet 및 매개 변수가 결정됩니다. 역할 항목 또는 역할 항목의 매개 변수를 제거하여 관리 역할이 할당된 사용자가 수행할 수 있는 작업을 제한할 수 있습니다. Microsoft Exchange Server 2013의 관리 역할 항목에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 역할에서 단일 전체 역할 항목 제거

역할에서 역할 항목을 제거하면 해당 역할이 할당된 사용자가 관련 cmdlet 또는 스크립트에 액세스할 수 있는 기능이 제거됩니다.

다음 구문을 사용하여 역할에서 전체 관리 역할 항목을 제거할 수 있습니다.

```powershell
Remove-ManagementRoleEntry <management role>\<management role entry>
```

이 예에서는 Seattle Server Administrators 역할에서 **Enable-MailUser** cmdlet을 제거합니다.

```powershell
Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"
```

구문과 매개 변수에 대한 자세한 내용은 [Remove-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351187\(v=exchg.150\))를 참조하십시오.

## 역할에서 여러 전체 역할 항목 제거

역할에서 여러 역할 항목을 제거하면 해당 역할이 할당된 사용자가 관련 cmdlet 또는 스크립트에 액세스할 수 있는 기능이 제거됩니다.

역할에서 여러 역할 항목을 제거하려면 **Get-ManagementRoleEntry** cmdlet을 사용하여 제거할 역할 항목 목록을 검색해야 합니다. 그런 다음 **Remove-ManagementRoleEntry** cmdlet으로 출력을 파이프해야 합니다. **Get-ManagementRoleEntry** cmdlet와 함께 와일드카드 문자를 사용하여 여러 역할 항목을 일치시킬 수 있습니다. *WhatIf* 스위치를 사용하여 올바른 역할 항목을 제거했는지 확인하는 것이 좋습니다. 다음 구문을 사용합니다.

```powershell
Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf
```

이 예에서는 Seattle Server Administrators 역할에서 journal이라는 단어가 포함된 모든 역할 항목을 제거합니다.

```powershell
Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf
```

*WhatIf* 스위치를 사용하여 명령을 실행하면 cmdlet은 제거되는 모든 역할 항목 목록을 반환합니다. 목록에 문제가 없어 보이면 *WhatIf* 스위치 없이 명령을 다시 실행하여 역할 항목을 제거합니다.

```powershell
Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry
```

구문과 매개 변수에 대한 자세한 내용은 [Get-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd335210\(v=exchg.150\)) 및 [Remove-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351187\(v=exchg.150\))를 참조하십시오.

## 역할의 역할 항목에서 매개 변수 제거

역할의 역할 항목에서 매개 변수를 제거하면 해당 역할이 할당된 사용자는 이러한 매개 변수를 더 이상 사용할 수 없습니다.

다음 구문을 사용하여 역할 항목에서 매개 변수를 제거할 수 있습니다.

```powershell
Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter
```

이 예에서는 Seattle Server Administrators 역할의 **Set-Mailbox** 역할 항목에서 *MaxSafeSenders*, *MaxSendSize*, *SecondaryAddress* 및 *UseDatabaseQuotaDefaults* 매개 변수를 제거합니다.

```powershell
Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

