---
title: '역할을 제거 합니다.: Exchange 2013 Help'
TOCTitle: 역할을 제거 합니다.
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 50482757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할을 제거 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

더 이상 필요 없는 관리 역할은 조직에서 제거할 수 있습니다. 직접 만든 관리 역할만 제거할 수 있고 기본 제공 관리 역할은 제거할 수 없습니다. Microsoft Exchange Server 2013의 관리 역할에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 관리 역할을 제거하려면 먼저 관리 역할 할당을 모두 제거해야 합니다. 역할 할당을 제거하는 방법에 대한 자세한 내용은 [사용자 또는 USG에서 역할을 제거 합니다.](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 하위 역할이 없는 관리 역할 제거

하위 역할이 없는 역할을 제거하려면 다음 구문을 사용합니다.

```powershell
Remove-ManagementRole <role name>
```

이 예에서는 Seattle Server Administrators 역할을 제거합니다.

```powershell
Remove-ManagementRole "Seattle Server Administrators"
```

구문과 매개 변수에 대한 자세한 내용은 [Remove-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351170\(v=exchg.150\))을 참조하십시오.

## 하위 역할이 있는 관리 역할 제거

제거하려는 역할에 하위 역할이 있으면 하위 역할도 모두 제거해야 합니다. *Recurse* 스위치를 사용하지 않는 경우 하위 역할이 있는 역할을 제거하려고 하면 오류 메시지가 표시됩니다. 역할을 제거할 때 *Recurse* 스위치를 사용하면 지정한 역할과 모든 하위 역할이 제거됩니다.


> [!WARNING]
> <EM>Recurse</EM> 스위치를 사용하면 제거하도록 지정한 역할의 모든 하위 역할도 제거됩니다. 이 명령을 실행하기 전에 제거될 역할을 알고 있어야 합니다.



제거할 역할만 제거하려면 명령에 *WhatIf* 스위치를 사용하여 명령이 올바른지 확인합니다. 다음 구문을 사용합니다.

```powershell
Remove-ManagementRole <role name> -Recurse -WhatIf
```

*WhatIf* 스위치는 변경 내용을 커밋하지 않고 명령을 수행한 다음 제거했을 역할을 보고합니다. *WhatIf* 스위치에 대한 자세한 내용은 [WhatIf, Confirm 및 ValidateOnly 스위치](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)를 참조하십시오.

제거할 역할만 제거되는지 확인한 후 *WhatIf* 스위치 없이 동일한 명령을 실행합니다. 이 예에서는 London Administrators 역할 및 모든 하위 역할을 제거합니다.

```powershell
Remove-ManagementRole "London Administrators" -Recurse
```

구문과 매개 변수에 대한 자세한 내용은 [Remove-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351170\(v=exchg.150\))를 참조하십시오.

## 범위가 지정되지 않은 관리 역할 제거

범위가 지정되지 않은 역할을 제거하려면 이 항목의 앞부분에 있는 Remove a management role with no child roles 및 Remove a management role with child roles에 제공된 것과 동일한 절차를 사용할 수 있습니다. 유일한 차이점은 범위가 지정되지 않은 역할을 제거하는 경우 명령을 실행할 때 *UnScopedTopLevel* 스위치를 지정해야 한다는 것입니다. 이 예에서는 범위가 지정되지 않은 역할 및 모든 하위 역할을 제거합니다.

```powershell
Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel
```

다른 역할 제거와 마찬가지로 *WhatIf* 스위치를 사용하여 올바른 역할이 제거되는지 확인해야 합니다.

구문과 매개 변수에 대한 자세한 내용은 [Remove-ManagementRole](https://technet.microsoft.com/ko-kr/library/dd351170\(v=exchg.150\))를 참조하십시오.

