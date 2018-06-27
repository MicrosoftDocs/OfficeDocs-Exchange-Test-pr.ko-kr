---
title: '허용 또는 전화 응답 규칙 만들기 (영문)에서 사용자를 차단: Exchange 2013 Help'
TOCTitle: 허용 또는 전화 응답 규칙 만들기 (영문)에서 사용자를 차단
ms:assetid: 81863440-8b21-4523-bdab-6a2311889a0d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298097(v=EXCHG.150)
ms:contentKeyID: 50556022
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 허용 또는 전화 응답 규칙 만들기 (영문)에서 사용자를 차단

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

개별 사용자가 사서함 속성을 구성하여 고유의 전화 응답 규칙을 만들고 관리할 수 있도록 할지 여부를 지정할 수 있습니다. 기본적으로 개별 사용자는 전화 응답 규칙을 만들 수 있습니다.

UM 다이얼 플랜 또는 UM 사서함 정책에 대한 전화 응답 규칙을 구성하여 UM(통합 메시징)을 사용할 수 있는 여러 사용자에 대해 전화 응답 규칙을 사용하거나 사용하지 않도록 설정할 수 있습니다.


> [!NOTE]
> 이 기능을 구성하는 데 있어 EAC는 사용할 수 없습니다. 음성 메일 사용자에 대해 전화 응답 규칙을 사용하거나 사용하지 않도록 설정하려면 셸을 사용해야 합니다.



사용자의 착신 전환 허용과 관련된 추가 관리 작업에 대한 자세한 내용은 [프로시저를 호출 하는 착신 전환](forwarding-calls-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 UM 사용 가능 사용자에 대해 전화 응답 규칙을 사용하거나 사용하지 않도록 설정

이 예에서는 사용자 tony@contoso.com에 대해 전화 응답 규칙을 사용하도록 설정합니다.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $true

이 예에서는 사용자 tony@contoso.com에 대해 전화 응답 규칙을 사용하지 않도록 설정합니다.

    Set-UMMailbox -Identity tony@contoso.com -CallAnsweringRulesEnabled $false

