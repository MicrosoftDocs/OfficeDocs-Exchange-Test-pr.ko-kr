---
title: '음성 메일에 대 한 공통 PIN 패턴을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 음성 메일에 대 한 공통 PIN 패턴을 사용 하도록 설정
ms:assetid: 9940a8c2-f576-4089-ab96-8b318ad3da0f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673546(v=EXCHG.150)
ms:contentKeyID: 50556046
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일에 대 한 공통 PIN 패턴을 사용 하도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

Outlook Voice Access 사용자에 대해 공통 UM(통합 메시징) PIN 패턴을 사용하거나 사용하지 않도록 설정할 수 있습니다. UM 사서함 정책에서 공통 PIN 패턴 설정을 사용하거나 사용하지 않도록 설정하면 이 설정은 UM 사서함 정책과 연결된 모든 UM 사용 가능 사용자에게 적용됩니다. 기본적으로 UM 사용 가능 사용자는 PIN을 만들 때 공통 패턴을 사용할 수 없습니다.

UM 사서함 정책에서 몇 가지 PIN 관련 설정을 구성할 수 있습니다. **공통 PIN 패턴 허용** 설정은 사용자가 PIN을 만들 때 일반적인 숫자 패턴을 사용하는 것을 허용하거나 차단하는 데 사용됩니다. 기본적으로 이 설정은 사용할 수 없도록 설정되며 사용자는 다음과 같은 숫자 패턴을 사용할 수 없습니다.

  - **연속되는 번호**   연속되는 숫자만을 포함하는 PIN 값입니다. 연속되는 PIN 번호의 예로는 1234 및 65432를 들 수 있습니다.

  - **반복되는 번호**   반복되는 숫자만을 포함하는 PIN 값입니다. 반복 번호의 예로는 11111과 22222가 있습니다.

  - **사서함 확장의 접미사**   사용자 사서함 확장의 접미사를 포함하는 PIN 값입니다. 예를 들어 사용자의 사서함 확장이 36697이면 PIN으로 3669712를 사용할 수 없습니다.


> [!NOTE]
> <STRONG>공통 PIN 패턴 허용</STRONG> 설정을 사용하는 경우 사서함 확장의 접미사만 거부됩니다.



Outlook Voice Access PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 공통 PIN 패턴을 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리하려는 UM 사서함 정책을 선택한 다음 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지의 **PIN 정책**에서 **공통 PIN 패턴 허용** 옆의 확인란을 선택합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 공통 PIN 패턴을 사용하도록 설정

이 예에서는 `MyUMMailboxPolicy`라는 UM 사서함 정책과 연결된 사용자가 공통 패턴이 포함된 PIN을 사용할 수 있도록 합니다.

    Set-UMMailboxPolicy -Identity MyUMMailboxPolicy -AllowCommonPatterns $true

