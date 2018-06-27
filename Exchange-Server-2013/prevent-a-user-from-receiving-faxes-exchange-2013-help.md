---
title: '사용자 팩스를 받지 않도록 방지: Exchange 2013 Help'
TOCTitle: 사용자 팩스를 받지 않도록 방지
ms:assetid: b5d022b9-043a-4324-87fb-074d5e2c2ca3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201722(v=EXCHG.150)
ms:contentKeyID: 52057961
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 팩스를 받지 않도록 방지

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

UM (통합 메시징) 사용자에서 팩스를 받을 수 없도록 합니다. 기존 및 새 UM 사용자에 대 한 팩스 설정을 변경 하는 방법에 대해 알아봅니다.

기본적으로 사용자가 통합 메시징을 사용 하도록 설정 하는 경우는 것 팩스 기능을 설정 하 고 사용자에 게 연결 된 UM 사서함 정책에는 팩스 파트너의 URI를 구성 하는 경우 팩스를 받을 수 있습니다. UM에서 비활성화 된 다이얼 플랜, UM 사서함 정책 또는 UM 사용이 가능한 사용자의 사서함 하거나 팩스를 활성화할 수 있습니다.

기본적으로 사용자 사서함 및 해당 사용자와 연결된 다이얼 플랜에서는 수신 팩스를 허용합니다. 그러나 사용자가 팩스를 받도록 하려면 먼저 UM 사용 가능 사용자와 연결된 UM 사서함 정책에서 인바운드 팩스를 사용하도록 설정한 후에 팩스 파트너의 URI를 입력해야 합니다.


> [!NOTE]
> EAC를 사용 하 여 통합 메시징 사서함 정책에 대 한 팩스 설정을 변경 수 있습니다. 그러나 다이얼 플랜에서 또는 개별 사용자에 대 한 팩스 설정을 구성 하려면 셸을 사용 해야 합니다.



팩스 파트너에 대 한 자세한 내용은 [팩스 파트너에 대 한 Microsoft 적절치](https://go.microsoft.com/fwlink/?linkid=190238)를 참조 하십시오.

팩스와 관련된 추가 관리 작업에 대한 자세한 내용은 [절차를 팩스](faxing-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 사용자가 통합 메시징을 사용하도록 설정되었는지 확인하십시오. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용 하 여 UM 사용이 가능한 사용자가 팩스를 수신 하지 못하도록 하려면

이 예에서는 Tony라는 UM 사용 가능 사용자가 자신의 사서함에서 팩스 메시지를 수신할 수 없도록 차단합니다.

    Set-UMMailbox -Identity tony@contoso.com -FaxEnabled $false

