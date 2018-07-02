---
title: 'UM 다이얼 플랜을 변경 합니다.: Exchange 2013 Help'
TOCTitle: UM 다이얼 플랜을 변경 합니다.
ms:assetid: 4a6b6b6f-c61c-44e8-91dd-c5d28835f441
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee633465(v=EXCHG.150)
ms:contentKeyID: 50483038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 다이얼 플랜을 변경 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-05_

UM(통합 메시징)을 사용할 수 있는 사용자를 다른 UM 다이얼 플랜으로 전환하거나 해당 사용자와 연결된 다이얼 플랜을 변경해야 할 경우가 있습니다. 예를 들어 UM 사용 가능 사용자의 다이얼 플랜을 내선 번호에서 SIP URI로 변경해야 할 경우가 있습니다.

UM 다이얼 플랜을 변경하려면 사용자가 통합 메시징을 사용할 수 없도록 설정한 다음 새 UM 다이얼 플랜에서 사용자가 통합 메시징을 사용할 수 있도록 설정해야 합니다. 이는 다이얼 플랜마다 내선 번호 길이, URI 유형 등의 설정 및 요구 사항이 다를 수 있기 때문입니다. 예를 들어 SIP URI 다이얼 플랜에서는 각 UM 사용 가능 사서함에 SIP 리소스 식별자를 할당해야 하지만 내선 번호 다이얼 플랜에서는 그럴 필요가 없습니다. 또한 각 UM 사서함에는 UM 다이얼 플랜과 UM 사서함 정책에 대한 참조가 모두 포함되어 있습니다. UM 사서함 정책에도 UM 다이얼 플랜에 대한 참조가 포함되어 있습니다. UM 사용 가능 사용자의 기본 프록시 주소에서 다른 다이얼 플랜을 가리키도록 변경하면 UM 사서함 상태가 일치하지 않게 됩니다.

음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 10분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 기존의 Exchange 받는 사람이 통합 메시징을 사용할 수 있는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 어떻게 해야 합니까?

## 1단계: 새 UM 다이얼 플랜 만들기


> [!IMPORTANT]
> UM 사용 가능 사용자를 Microsoft Office Communications Server 2007 R2 또는 Microsoft Lync Server로 마이그레이션하는 경우 먼저 SIP URI 다이얼 플랜을 만들어야 합니다.



자세한 내용은 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

## 2단계: 사용자가 통합 메시징을 사용할 수 없도록 설정

자세한 내용은 [사용자에 대 한 음성 메일을 사용 하지 않도록 설정](disable-voice-mail-for-a-user-exchange-2013-help.md)를 참조하십시오.

## 3단계: 새 UM 다이얼 플랜에서 사용자가 통합 메시징을 사용할 수 있도록 설정


> [!IMPORTANT]
> Office Communications Server 2007 R2 또는 Lync Server가 있는 환경으로 사용자를 이동하는 경우 사용자가 UM을 사용할 수 있도록 설정할 때 사용자의 SIP 리소스 식별자도 포함해야 합니다. 또한 SIP 다이얼 플랜과 연결된 UM 사서함 정책을 선택해야 합니다.



자세한 내용은 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)를 참조하십시오.

