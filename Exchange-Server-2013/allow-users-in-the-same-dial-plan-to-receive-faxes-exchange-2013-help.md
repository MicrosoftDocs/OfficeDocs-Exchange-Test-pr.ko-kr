---
title: '사용자가 팩스를 받을 동일한 다이얼 플랜의 수 있게 합니다.: Exchange 2013 Help'
TOCTitle: 사용자가 팩스를 받을 동일한 다이얼 플랜의 수 있게 합니다.
ms:assetid: cb245028-0b86-4171-879e-934dd35fa626
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124557(v=EXCHG.150)
ms:contentKeyID: 52058032
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자가 팩스를 받을 동일한 다이얼 플랜의 수 있게 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

UM(통합 메시징) 다이얼 플랜에 연결된 모든 사용자가 사서함에서 팩스 메시지를 받도록 설정할 수 있습니다. 기본적으로 통합 메시징을 사용할 수 있고 UM 다이얼 플랜과 연결되어 있는 사용자는 팩스 메시지를 받을 수 있습니다. UM 사용 가능 사용자가 사서함에 팩스 메시지를 받을 수 있도록 하려면 수신 팩스 통화를 수락하도록 다이얼 플랜을 구성해야 합니다. 또한 UM 사서함 정책과 해당 사용자에 대해 팩스를 사용하도록 설정해야 합니다. 기본적으로는 다이얼 플랜, UM 사서함 정책 및 사용자에 대해 팩스가 사용하도록 설정됩니다. 그러나 이러한 기본 설정이 변경되어 UM 사용 가능 사용자가 팩스 메시지를 받을 수 없는 경우가 있습니다.

다이얼 플랜에서 팩스 메시지를 받지 못하도록 차단하면 해당 다이얼 플랜과 연결된 모든 사용자는 팩스 메시지를 받지 못하게 됩니다. 팩스 메시지 수신을 허용하도록 개별 사용자의 속성을 구성하는 경우에도 마찬가지입니다. UM 다이얼 플랜에서 팩스를 사용하거나 사용하지 않도록 설정하는 것은 UM 사서함 정책 또는 개별 UM 사용 가능 사용자에 대한 팩스 설정보다 우선합니다.


> [!NOTE]
> EAC를 사용하여 UM 사서함 정책에서 팩스 설정을 구성할 수 있습니다. 그러나 개별 사용자 또는 다이얼 플랜에 대해 팩스 설정을 구성하려면 셸을 사용해야 합니다.



팩스 파트너에 대 한 자세한 내용은 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238)를 참조 하십시오.

팩스와 관련된 추가 관리 작업에 대한 자세한 내용은 [절차를 팩스](faxing-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 다이얼 플랜과 연결된 사용자가 팩스를 받도록 허용

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜과 연결된 UM 사용 가능 사용자가 수신 팩스를 받을 수 있도록 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -FaxEnabled $true

