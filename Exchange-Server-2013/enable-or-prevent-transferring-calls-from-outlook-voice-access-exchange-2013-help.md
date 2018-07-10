---
title: '활성화 하거나 금지 하는 Outlook Voice Access에서 통화를 전송 합니다.: Exchange 2013 Help'
TOCTitle: 활성화 하거나 금지 하는 Outlook Voice Access에서 통화를 전송 합니다.
ms:assetid: b80c57f1-394c-4608-8ad3-52a3e6d697db
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423554(v=EXCHG.150)
ms:contentKeyID: 52058027
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 활성화 하거나 금지 하는 Outlook Voice Access에서 통화를 전송 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

Outlook Voice Access 사용자가 UM(통합 메시징) 다이얼 플랜에 연결된 사용자에게 통화를 전송할 수 있도록 설정하거나 전송하지 못하도록 차단할 수 있습니다. 기본적으로는 이 옵션과 **사용자 전화를 울리지 않고 음성 메시지 남기기** 옵션은 모두 사용하도록 설정되므로 Outlook Voice Access 사용자가 같은 UM 다이얼 플랜의 사용자에게 통화를 전송하고 음성 메시지를 남길 수 있습니다. 이 설정은 PIN을 입력했으며 인증된 Outlook Voice Access 사용자에게만 적용됩니다.

UM 다이얼 플랜과 관련된 추가 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EMC를 사용하여 Outlook Voice Access 사용자의 통화 전송 설정 또는 차단

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

3.  **전송 및 검색**의 **전화 건 사람의 다음 작업 허용**에서 **사용자에게 전송** 옆의 확인란을 선택하여 전화 건 사람이 다이얼 플랜 내의 다른 사용자에게 통화를 전송하도록 설정합니다. Outlook Voice Access 사용자가 다른 사용자에게 통화를 전송하지 못하도록 차단하려면 이 확인란 선택을 취소합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 Outlook Voice Access 사용자의 통화 전송 설정 또는 차단

이 예에서는 Outlook Voice Access 사용자가 `MyUMDialPlan`이라는 UM 다이얼 플랜에서 같은 다이얼 플랜의 사용자에게 통화를 전송할 수 있도록 설정합니다.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $true

이 예에서는 Outlook Voice Access 사용자가 `MyUMDialPlan`이라는 UM 다이얼 플랜에서 같은 다이얼 플랜의 사용자에게 통화를 전송할 수 없도록 차단합니다.

    Set-UMDialPlan -identity MyUMDialPlan -AllowDialPlanSubscribers $false

