---
title: '사용자가 UM 사용이 가능 하지 건 전화를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사용자가 UM 사용이 가능 하지 건 전화를 사용 하도록 설정
ms:assetid: 3c39c6df-6d7a-469f-b92b-85b3f14bad31
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb267006(v=EXCHG.150)
ms:contentKeyID: 50482896
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자가 UM 사용이 가능 하지 건 전화를 사용 하도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-05_

UM(통합 메시징)을 사용할 수 없는 사용자의 호출을 사용하거나 사용하지 않도록 설정할 수 있습니다. 기본적으로 통합 메시징은 자동 전화 교환을 통해 인증되지 않은 발신자로부터의 수신 전화가 UM 사용이 가능한 사용자로 전달될 수 있도록 합니다. 이 옵션을 사용하도록 설정하면 조직 외부의 사용자가 UM 사용이 가능한 사용자에게 호출을 전달할 수 있습니다.

UM 사용 가능 사용자에 대해 이 설정을 사용하지 않도록 설정한 경우에도 디렉터리 검색을 사용하여 사용자의 사서함을 찾을 수 있습니다. 그러나 외부 발신자가 사용자에게 연결하려고 하면 시스템에서 "죄송합니다. 이 사용자에게 전화를 전송할 수 없습니다."라는 메시지가 표시됩니다. 자동 전화 교환에 교환원이 구성된 경우 발신자가 교환원에게 전송됩니다. 자동 전화 교환에 교환원이 구성되지 않고 다이얼 플랜 교환원이 구성된 경우 호출은 해당 다이얼 플랜 교환원에게 전송됩니다. 음성 사용이 가능한 자동 전화 교환, DTMF(복합 주파수 부호) 대체 시스템 자동 전화 교환 또는 다이얼 플랜에 교환원 내선 번호가 구성되지 않은 경우 시스템에서 "죄송합니다. 교환원 및 터치톤 서비스를 모두 사용할 수 없습니다."라는 메시지가 표시됩니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 절차를 수행하기 전에 사용자 사서함에서 UM을 사용하도록 설정했는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 UM을 사용할 수 없는 사용자의 호출 사용

이 예에서는 Tony Smith가 UM을 사용할 수 없는 발신자의 음성 호출을 받을 수 있도록 합니다.

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers SearchEnabled

