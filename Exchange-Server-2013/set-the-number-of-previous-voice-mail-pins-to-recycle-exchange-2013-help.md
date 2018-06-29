---
title: '이전 음성 메일 재생 되도록 핀의 수를 설정 합니다.: Exchange 2013 Help'
TOCTitle: 이전 음성 메일 재생 되도록 핀의 수를 설정 합니다.
ms:assetid: b094e68e-c493-4576-a6b1-4c780e635405
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124254(v=EXCHG.150)
ms:contentKeyID: 50556063
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 이전 음성 메일 재생 되도록 핀의 수를 설정 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

Outlook Voice Access 사용자가 Outlook Voice Access 번호로 전화를 걸면 음성 메일 시스템에서 사용자를 인증할 수 있도록 PIN을 입력하라는 메시지가 표시됩니다. 인증 후 사용자는 모든 전화기에서 사서함에 있는 음성 메일, 전자 메일, 일정 및 개인 연락처 정보에 액세스할 수 있습니다.

UM(통합 메시징) 사서함 정책에 대해 몇 가지 PIN 관련 설정을 구성할 수 있습니다. **PIN 재활용 횟수** 설정은 이전 PIN을 다시 사용하기 전에 사용자가 사용해야 하는 고유 PIN 수를 지정합니다. 이 설정 값은 1에서 20 사이로 지정할 수 있으며 대부분의 조직에서는 기본값인 5개 PIN으로 설정해야 합니다. 이 값을 너무 높게 설정하면 많은 수의 PIN을 만들고 기억하기가 어려워질 수 있으므로 사용자에게 불편을 줄 수 있습니다. 너무 낮은 값을 설정하면 네트워크의 보안이 취약해질 수 있습니다.


> [!IMPORTANT]
> PIN 재활용 횟수는 사용하지 않도록 설정할 수 없습니다.



Outlook Voice Access PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 PIN 재활용 횟수 변경

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 변경하려는 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 변경하려는 UM 사서함 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **PIN 정책**을 클릭하고 **PIN 재활용 횟수** 옆에 1에서 20 사이의 값을 입력합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 PIN 재활용 횟수 변경

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy`의 PIN 재활용 횟수를 10으로 설정합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -PINHistoryCount 10

