---
title: '팩스를 받을 수 있도록 설정: Exchange 2013 Help'
TOCTitle: 팩스를 받을 수 있도록 설정
ms:assetid: a0505001-aac0-41ef-824f-76e5e56d7675
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201712(v=EXCHG.150)
ms:contentKeyID: 52057946
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 팩스를 받을 수 있도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

UM(통합 메시징) 사용자가 팩스를 수신하도록 설정할 수 있습니다. 기본적으로 사용자가 통합 메시징을 사용할 수 있도록 설정할 때 해당 사용자에게 연결된 UM 사서함 정책에서 팩스를 사용하도록 설정하고 팩스 파트너 URI를 구성하면 사용자가 팩스를 수신할 수 있습니다. UM 다이얼 플랜, UM 사서함 정책 또는 UM 사용 가능 사용자의 사서함에 대해 팩스를 사용하거나 사용하지 않도록 설정할 수 있습니다.

기본적으로 사용자 사서함 및 해당 사용자와 연결된 다이얼 플랜에서는 수신 팩스를 허용합니다. 그러나 사용자가 팩스를 받도록 하려면 먼저 UM 사용 가능 사용자와 연결된 UM 사서함 정책에서 인바운드 팩스를 사용하도록 설정한 후에 팩스 파트너의 URI를 입력해야 합니다.


> [!NOTE]
> EAC를 사용하여 UM 사서함 정책에서 팩스 설정을 구성할 수 있습니다. 그러나 개별 사용자 또는 다이얼 플랜에 대해 팩스 설정을 구성하려면 셸을 사용해야 합니다.



팩스 파트너에 대 한 자세한 내용은 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238)를 참조 하십시오.

팩스와 관련된 추가 관리 작업에 대한 자세한 내용은 [절차를 팩스](faxing-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 사용자에게 할당된 UM 사서함 정책에서 팩스를 사용하도록 설정했으며 팩스 파트너의 URI를 올바르게 구성했는지 확인합니다.

  - 이러한 절차를 수행하기 전에 사용자가 통합 메시징을 사용하도록 설정되었는지 확인하십시오. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 UM 사용자가 팩스를 수신하도록 설정

이 예에서는 Tony Smith가 수신 팩스를 받을 수 있도록 설정합니다.

    Set-UMMailbox -Identity tonysmith@contoso.com -FaxEnabled $true

