---
title: '역할 항목 변경: Exchange 2013 Help'
TOCTitle: 역할 항목 변경
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 50483187
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 항목 변경

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

관리 역할에 대한 각 관리 역할 항목은 단일 cmdlet을 나타냅니다. 역할 항목에 대해 매개 변수를 추가하거나 제거하여 이러한 변경 내용을 관리 역할에 추가함으로써 해당 cmdlet에서 매개 변수의 사용 여부를 제어할 수 있습니다. Microsoft Exchange Server 2013의 관리 역할 항목에 대한 자세한 내용은 [관리 역할 이해 (영문)](understanding-management-roles-exchange-2013-help.md)를 참조하십시오.

기본 제공 관리 역할에 대해서는 역할 항목을 수정할 수 없습니다.


> [!NOTE]
> 이 항목에서는 범위가 지정되지 않은 관리 역할에서 범위가 지정되지 않은 관리 역할 항목을 수정하는 방법에 대해 설명하지 않습니다. 범위가 지정되지 않은 역할 항목을 수정하는 방법에 대한 자세한 내용은 <A href="create-a-role-exchange-2013-help.md">역할 만들기</A>을 참조하십시오.




> [!WARNING]
> 역할 항목에서 매개 변수를 추가하거나 제거하려면 <EM>AddParameter</EM> 또는 <EM>RemoveParameter</EM> 매개 변수를 사용해야 합니다. <STRONG>Set-ManagementRoleEntry</STRONG> cmdlet을 실행할 때 <EM>AddParameter</EM> 또는 <EM>RemoveParameter</EM> 매개 변수를 생략하면 <EM>Parameters</EM> 매개 변수를 사용하여 지정한 매개 변수만 역할 항목에 포함됩니다. 역할 항목의 다른 모든 매개 변수는 제거됩니다.



역할과 관련된 다른 관리 작업에 대한 자세한 내용은 [고급 사용 권한](advanced-permissions-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 역할" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 역할 항목에 매개 변수를 추가하려면 추가하는 매개 변수가 상위 역할의 역할 항목에 있어야 합니다. 또한 지정한 cmdlet에도 매개 변수가 있어야 합니다.

  - 역할 항목에서 매개 변수를 제거하려면 제거하는 매개 변수가 하위 역할의 역할 항목에 없어야 합니다. 하위 역할의 역할 항목에서 매개 변수를 제거해야 합니다. 모든 하위 역할의 역할 항목에서 매개 변수를 제거하려면 이 항목의 뒷부분에 있는 "셸을 사용하여 역할 항목에서 하나 이상의 매개 변수 제거"를 사용하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 역할 항목에 하나 이상의 매개 변수 추가

역할 항목에 매개 변수를 추가하려면 *Parameters* 매개 변수를 사용하여 추가할 매개 변수를 지정해야 합니다. 그런 다음 *AddParameter* 매개 변수를 지정하여 추가 작업을 수행하고자 함을 나타내야 합니다.

역할 항목에 매개 변수를 추가하려면 다음 구문을 사용합니다.

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter

이 예에서는 Recipient Administrators 역할의 **Set-Mailbox** cmdlet에 *EmailAddresses* 및 *Type* 매개 변수를 추가합니다.

    Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 역할 항목에서 하나 이상의 매개 변수 제거

역할 항목에서 매개 변수를 제거하려면 *Parameters* 매개 변수를 사용하여 제거할 매개 변수를 지정해야 합니다. 그런 다음 *RemoveParameter* 매개 변수를 지정하여 제거 작업을 수행하고자 함을 나타내야 합니다.

역할 항목에서 매개 변수를 제거하려면 다음 구문을 사용하십시오.

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter

이 예에서는 Tier 1 Server Administrators 역할의 **Set-SendConnector** cmdlet에서 *Port*, *ProtocolLoggingLevel* 및 *SmartHostAuthMechanism* 매개 변수를 제거합니다.

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 역할 항목에서 모든 매개 변수 제거

역할 항목에서 모든 매개 변수를 제거하려면 *Parameters* 매개 변수에서 `$Null` 값을 지정해야 합니다. *RemoveParameters* 매개 변수는 포함하지 않아도 됩니다.

역할 항목에서 모든 매개 변수를 제거하는 작업은 cmdlet에서 몇 개의 매개 변수만 사용 가능하게 설정하고 다른 매개 변수는 모두 제외하려는 경우 가장 유용합니다. 역할이 cmdlet에 액세스하지 못하게 하려면 단순히 매개 변수만 제거하는 것이 아니라 역할에서 연결된 역할 항목을 완전히 제거해야 합니다. 역할에서 역할 항목을 제거하는 방법에 대한 자세한 내용은 [역할에서 역할 항목을 제거 합니다.](remove-a-role-entry-from-a-role-exchange-2013-help.md)를 참조하십시오.


> [!WARNING]
> 제거 작업은 실행 취소할 수 없습니다. 실수로 역할 항목에서 모든 매개 변수를 제거한 경우에는 수동으로 다시 추가해야 합니다.



역할 항목에서 모든 매개 변수를 제거하려면 다음 구문을 사용합니다.

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 

이 예에서는 Recipient Administrators 역할의 **Set-CASMailbox** cmdlet에서 매개 변수를 모두 제거합니다.

    Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 특정 매개 변수 집합 적용

역할 항목에 특정 매개 변수 집합만 포함하려면 *Parameters* 매개 변수만 지정하십시오. *AddParameter* 또는 *RemoveParameter* 매개 변수는 포함하지 마십시오. *Parameters* 매개 변수만 지정하는 경우 명령에서 지정한 매개 변수만 역할 항목에 포함됩니다. 그 밖의 모든 매개 변수는 제거됩니다.

특정 매개 변수 집합을 지정하려면 다음 구문을 사용하십시오.

    Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

이 예에서는 Seattle Mail Recipients 역할의 **Set-UMMailbox** cmdlet에 *Identity*, *DisplayName*, *MissedCallNotificationEnabled* 및 *PersonalAuthAttendantEnabled* 매개 변수만 포함합니다.

    Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled

구문과 매개 변수에 대한 자세한 내용은 [Set-ManagementRoleEntry](https://technet.microsoft.com/ko-kr/library/dd351162\(v=exchg.150\))를 참조하십시오.

