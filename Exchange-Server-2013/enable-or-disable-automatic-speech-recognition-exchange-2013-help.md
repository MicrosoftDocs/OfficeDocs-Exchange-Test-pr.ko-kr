---
title: '사용 하도록 설정 하거나 자동 음성 인식 기능을 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용 하도록 설정 하거나 자동 음성 인식 기능을 사용 하지 않도록 설정
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52057943
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하도록 설정 하거나 자동 음성 인식 기능을 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-12_

ASR(자동 음성 인식)에 UM(통합 메시징) 자동 전화 교환을 사용하도록 설정할 수 있습니다. UM 자동 전화 교환에 음성을 사용하면 발신자가 자동 전화 교환 음성 안내에 음성으로 응답하고 자동 전화 교환의 메뉴 시스템으로 이동할 수 있습니다. 기본적으로 자동 전화 교환은 음성을 사용할 수 없는 상태로 만들어집니다. 자동 전화 교환에서 음성을 사용하도록 설정하면 전화 건 사람은 음성 명령만 사용하여 자동 전화 교환 메뉴 시스템을 탐색할 수 있고 터치톤 입력은 사용할 수 없습니다.

반드시 필요한 것은 아니지만 음성 사용 가능 자동 전화 교환이 말하는 단어를 인식하거나 이해하지 못하는 경우 발신자가 터치톤 입력을 사용할 수 있도록 각 음성 사용 가능 자동 전화 교환에 대해 DTMF(복합 주파수 부호) 폴백 자동 전화 교환을 구성하는 것이 좋습니다. DTMF 폴백 자동 전화 교환을 구성한 경우에는 발신자가 터치톤 입력이라고 하는 DTMF 입력을 사용하여 자동 전화 교환 메뉴 시스템을 탐색하고 사용자 이름을 말하거나 사용자 지정 메뉴 음성 안내를 사용해야 합니다. DTMF 폴백 자동 전화 교환에서 음성을 사용하지 않도록 설정하는 것이 좋습니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 자동 전화 교환에 음성을 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 음성을 사용하도록 설정할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **일반**에서 **음성 명령에 응답하도록 자동 전화 교환 설정** 옆의 확인란을 선택하여 음성 인식을 사용하도록 설정합니다. 자동 음성 인식을 사용하지 않도록 설정하려면 이 확인란의 선택을 취소합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 UM 자동 전화 교환에 음성을 사용하도록 설정

이 예에서는 `MySpeechEnabled AA`라는 UM 자동 전화 교환에서 ASR을 사용하도록 설정합니다.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

