---
title: '허용 하거나 사용자가 동일한 UM 사서함 정책에서 전화 응답 규칙 만들기 (영문) 하지 못하도록: Exchange 2013 Help'
TOCTitle: 허용 하거나 사용자가 동일한 UM 사서함 정책에서 전화 응답 규칙 만들기 (영문) 하지 못하도록
ms:assetid: e44acaa6-d5a8-41e8-94aa-100be0bd6391
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd351209(v=EXCHG.150)
ms:contentKeyID: 50556098
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 허용 하거나 사용자가 동일한 UM 사서함 정책에서 전화 응답 규칙 만들기 (영문) 하지 못하도록

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

전화 응답 규칙을 구성 하는 UM (통합 메시징) 사서함 정책과 사용 하 여 연관 된 사용자를 허용 하거나에서 작업을 금지 수 있습니다. UM 다이얼 플랜에서 전화 응답 규칙을 구성 하는 옵션을 비활성화 하는 경우에 전화 응답 규칙 기능 UM 사서함 정책에 연결 된 UM 사용이 가능한 사용자에 게 사용할 수 없습니다. 기본 설정은 사용 됩니다.

사용자의 착신 전환 허용과 관련된 추가 관리 작업에 대한 자세한 내용은 [프로시저를 호출 하는 착신 전환](forwarding-calls-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 사용 하도록 설정 하거나 전화 응답 UM 사서함 정책에 대 한 규칙을 사용 하지 않도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 사서함 정책** 아래에서 관리할 UM 사서함 정책을 선택한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지에서 선택 하거나 **사용자가 전화 응답 규칙을 구성 하도록 허용** 옆에 있는 확인란의 선택을 취소 합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 하거나 전화 응답 UM 사서함 정책에 대 한 규칙을 사용 하지 않도록 설정

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy` 전화 응답 규칙을 만들 수와 연관 된 사용자를 허용 합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $true

이 예에서는 UM 사서함 정책 `MyUMMailboxPolicy` 전화 응답 규칙 만들기 (영문)에서 연관 된 사용자 수 없습니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowCallAnsweringRules $false

