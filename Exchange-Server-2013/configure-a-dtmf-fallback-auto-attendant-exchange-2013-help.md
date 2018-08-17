---
title: 'DTMF 대체 자동 전화 교환 구성: Exchange 2013 Help'
TOCTitle: DTMF 대체 자동 전화 교환 구성
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 50483831
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DTMF 대체 자동 전화 교환 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-30_

DTMF(이중 톤 다중 주파수) 대체 시스템 자동 전화 교환 기능이 있는 음성 사용이 가능한 UM(통합 메시징) 자동 전화 교환을 구성할 수 있습니다. DTMF 대체 시스템 자동 전화 교환은 UM 음성 사용 가능 자동 전화 교환이 호출자가 제공하는 음성 입력을 이해하거나 인식할 수 없는 경우에 사용됩니다. DTMF 대체 시스템 자동 전화 교환을 구성한 경우에는 호출자가 터치톤 입력이라고 하는 DTMF 입력을 사용하여 자동 전화 교환 메뉴 시스템을 탐색하고 사용자 이름을 말하거나 사용자 지정 메뉴 음성 안내를 사용해야 합니다. DTMF 대체 시스템 자동 전화 교환이 구성되지 않았고 시스템이 호출자가 말한 내용을 이해하지 못하여 최대 음성 입력 수가 초과된 경우 시스템은 "죄송합니다. 도와드릴 수 없습니다. 나중에 다시 전화하십시오."라는 음성 안내로 응답할 수 있습니다.

기본적으로 자동 전화 교환은 음성을 사용할 수 없는 상태로 만들어집니다. 자동 전화 교환에서 음성을 사용하도록 설정하면 전화 건 사람은 음성 명령만 사용하여 자동 전화 교환 메뉴 시스템을 탐색할 수 있고 터치톤 입력은 사용할 수 없습니다. 반드시 필요한 것은 아니지만 음성 사용 가능 자동 전화 교환이 호출자가 말하는 단어를 인식 또는 이해하지 못하는 경우 호출자가 터치톤 입력을 사용할 수 있도록 각 음성 사용 가능 자동 전화 교환에 대해 DTMF 대체 시스템 자동 전화 교환을 구성하는 것이 좋습니다. 또한 DTMF 대체 시스템 자동 전화 교환에서 음성을 사용 가능하지 않도록 설정하는 것이 좋습니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 DTMF 대체 시스템 자동 전화 교환 기능이 있는 음성 사용이 가능한 자동 전화 교환 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경할 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 DTMF 대체 시스템 자동 전화 교환을 만들 UM 자동 전화 교환을 선택합니다. 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **일반**에서 **음성 명령이 제대로 작동하지 않을 때 이 자동 전화 교환을 사용합니다.** 옆의 확인란을 선택하고 **찾아보기**를 클릭합니다.

4.  **UM 자동 전화 교환 선택** 페이지에서 DTMF 대체 시스템 자동 전화 교환으로 사용할 자동 전화 교환을 선택한 다음 **저장**을 클릭합니다.


> [!IMPORTANT]
> 설정한 DTMF 대체 시스템 자동 전화 교환을 검색할 수 있으려면 먼저 자동 전화 교환에서 음성 사용이 가능하도록 설정해야 합니다.



## 셸을 사용하여 DTMF 대체 시스템 자동 전화 교환 기능이 있는 음성 사용 가능 자동 전화 교환 구성

이 예에서는 `MyDTMFAA`라는 DTMF 대체 시스템 자동 전화 교환을 사용하도록 `MySpeechEnabledAA`라는 UM 자동 전화 교환을 구성합니다.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

