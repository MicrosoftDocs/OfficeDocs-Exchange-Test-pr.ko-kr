---
title: '사서함에 할당 정책 변경: Exchange 2013 Help'
TOCTitle: 사서함에 할당 정책 변경
ms:assetid: 011690a5-233a-4c03-8842-92276f899a89
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd638076(v=EXCHG.150)
ms:contentKeyID: 50482375
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 할당 정책 변경

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-08_

사서함에 할당된 관리 역할 할당 정책을 변경할 수 있습니다. 사서함의 할당 정책을 변경하면 다음에 사용자가 사서함에 로그인하거나 사서함 옵션 페이지를 여는 등 연결을 새로 고치는 즉시 변경 내용이 적용됩니다. Microsoft Exchange Server 2013의 할당 정책에 대한 자세한 내용은 [관리 역할 할당 정책 이해 (영문)](understanding-management-role-assignment-policies-exchange-2013-help.md)를 참조하십시오.

사용 권한과 관련된 다른 관리 작업에 대한 자세한 내용은 [사용 권한](permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "역할 그룹" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 사서함의 할당 정책 변경

1.  EAC(Exchange 관리 센터)에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  할당 정책을 변경하려는 사용자 또는 리소스 사서함을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **사서함 기능**을 선택합니다.

4.  **역할 할당 정책** 목록에서 사서함에 할당하려는 할당 정책을 선택하고 **저장**을 클릭합니다.

## 셸을 사용하여 사서함 할당 정책 변경

사서함에 할당된 할당 정책을 변경하려면 다음 구문을 사용합니다.

    Set-Mailbox <mailbox alias or name> -RoleAssignmentPolicy <assignment policy>

이 예에서는 Brian 사서함의 할당 정책을 Unified Messaging Users로 설정합니다.

    Set-Mailbox Brian -RoleAssignmentPolicy "Unified Messaging Users"

## 셸을 사용하여 특정 할당 정책이 할당된 사서함 그룹의 할당 정책 변경


> [!NOTE]
> EAC를 사용하여 사서함 그룹의 할당 정책을 한 번에 변경할 수는 없습니다.



이 절차에서는 파이프라이닝, **Where** cmdlet 및 *WhatIf* 매개 변수를 사용합니다. 이 개념에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [파이프라이닝](https://technet.microsoft.com/ko-kr/library/aa998260\(v=exchg.150\))

  - [명령 출력 (영문)](working-with-command-output-exchange-2013-help.md)

  - [WhatIf, Confirm 및 ValidateOnly 스위치](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

특정 정책이 할당된 사서함 그룹의 할당 정책을 변경하려는 경우 다음 구문을 사용합니다.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<assignment policy to find>" } | Set-Mailbox -RoleAssignmentPolicy <assignment policy to set>

이 예에서는 Redmond Users - No Voicemail 할당 정책에 할당된 사서함을 모두 찾아서 할당 정책을 Redmond Users - Voicemail Enabled로 변경합니다.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled"

이 예에는 변경 내용을 커밋하지 않고도 변경되는 사서함을 모두 확인할 수 있도록 *WhatIf* 매개 변수가 포함되어 있습니다.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Redmond Users - No Voicemail" } | Set-Mailbox -RoleAssignmentPolicy "Redmond Users - Voicemail Enabled" -WhatIf

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 또는 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

