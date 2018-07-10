---
title: '호출자가 음성 메시지를 남길 발신자 ID가 없는 허용: Exchange 2013 Help'
TOCTitle: 호출자가 음성 메시지를 남길 발신자 ID가 없는 허용
ms:assetid: 51367d98-e17c-4bcf-8b14-208bd1ac3af0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232040(v=EXCHG.150)
ms:contentKeyID: 50483115
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 호출자가 음성 메시지를 남길 발신자 ID가 없는 허용

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

UM 사용 가능 사용자가 익명 발신자의 음성 메일 메시지를 수신하는 것을 허용할 수도 있고 허용하지 않을 수도 있습니다. 기본적으로 사용자가 UM(통합 메시징) 및 음성 메일을 사용할 수 있는 경우 익명이고 발신자 번호 정보가 없는 전화를 받을 수 있습니다.

대부분의 경우 통합 메시징에서 수신되는 전화는 수신 전화의 출처를 확인하는 데 사용할 수 있는 발신자 번호를 포함합니다. 그러나 다음과 같은 이유로 인해 들어오는 호출에 발신자 번호 정보가 없을 수도 있습니다.

  - 조직의 전화 통신 장비가 발신자 번호 정보를 포함하지 않도록 구성되어 있습니다.

  - 수신 전화가 모바일 또는 외부 전화에서 온 것입니다.

  - 호출자가 전화에 호출자 ID를 사용할 수 없도록 설정했습니다.

*AnonymousCallersCanLeaveMessages* 매개 변수는 기본적으로 사용되므로 UM 사용 가능 사용자는 발신자 번호 정보가 포함되어 있지 않은 경우에도 음성 메시지를 받을 수 있습니다. *AnonymousCallersCanLeaveMessages* 옵션을 사용하지 않는 경우 UM 사용 가능 사용자가 발신자 번호가 없는 전화를 받으면 전화는 익명으로 식별되고 UM 사용 가능 사용자는 음성 메시지를 받지 않게 됩니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 익명 발신자의 음성 메일 메시지를 수신하도록 설정

이 예에서는 UM 사용 가능 사용자 tonysmith@contoso.com이 발신자 번호 정보가 없는 수신 전화에서 음성 메시지를 수신하도록 설정합니다.

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $true

