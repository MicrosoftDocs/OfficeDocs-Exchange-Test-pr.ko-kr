---
title: '역할 범위를 제거 합니다.: Exchange 2013 Help'
TOCTitle: 역할 범위를 제거 합니다.
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 50483854
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 역할 범위를 제거 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-02_

관리 역할 범위는 사용자가 사용할 수 있는 개체를 지정하며, 사용자는 자신에게 할당된 cmdlet 및 매개 변수를 사용하여 개체를 변경할 수 있습니다. 범위를 더 이상 사용하지 않는 경우 제거할 수 있습니다. Microsoft Exchange Server 2013의 관리 역할 범위에 대한 자세한 내용은 [관리 역할 범위 이해 (영문)](understanding-management-role-scopes-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [역할 관리 권한](role-management-permissions-exchange-2013-help.md)의 "관리 범위" 항목

  - 셸을 사용하여 이러한 절차를 수행해야 합니다.

  - 범위를 제거하려면 이 범위를 사용하는 관리 역할 할당에서 범위를 제거해야 합니다. 역할 할당에서 범위를 제거하는 방법에 대한 자세한 내용은 [역할 할당을 변경](change-a-role-assignment-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 범위 제거

범위를 제거하려면 다음 구문을 사용합니다.

    Remove-ManagementScope <scope name>

예를 들어, "Dublin Servers" 범위를 제거하려면 다음 명령을 사용합니다.

    Remove-ManagementScope "Dublin Servers"

