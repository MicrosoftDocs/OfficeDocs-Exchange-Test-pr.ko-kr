---
title: '사용자에 대 한 메시지 대기 표시기 (MWI)를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 메시지 대기 표시기 (MWI)를 사용 하도록 설정
ms:assetid: 3d0ca657-00b6-4108-a850-b092fede1f75
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335216(v=EXCHG.150)
ms:contentKeyID: 50555968
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 메시지 대기 표시기 (MWI)를 사용 하도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-21_

UM(통합 메시징) 사서함 정책과 연결된 사용자에 대해 MWI(Message Waiting Indicator)를 사용하거나 사용하지 않도록 설정할 수 있습니다. MWI(메시지 대기 표시기)는 대부분의 레거시 음성 메일 시스템에 있는 기능입니다. 가장 일반적인 형태는 새 음성 메일 메시지가 있음을 알리기 위해 음성 메일 구독자의 전화기 램프가 켜지는 것입니다. 또한 Message Waiting Indicator는 UM 사용 가능 사용자의 휴대폰으로 문자 메시지를 보낼 수도 있습니다. 기본적으로 사용하도록 설정되어 있습니다.

UM IP 게이트웨이에서 MWI(Message Waiting Indicator)를 사용하지 않도록 설정하면 UM 사서함 정책과 연결된 UM 사용 가능 사용자가 이 기능을 사용할 수 없습니다.

UM 사서함 정책에 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 MWI(Message Waiting Indicator)를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 사서함 정책** 아래에서 관리할 UM 사서함 정책을 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지에서 **MWI(Message Waiting Indicator) 허용** 옆에 있는 확인란을 선택합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 MWI(Message Waiting Indicator)를 사용하도록 설정

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자에 대해 MWI(Message Waiting Indicator)를 사용하도록 설정합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMessageWaitingIndicator $true

