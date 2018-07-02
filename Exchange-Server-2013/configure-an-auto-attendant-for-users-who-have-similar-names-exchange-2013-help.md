---
title: '유사한 이름을 가진 사용자에 대 한 자동 전화 교환을 구성합니다: Exchange 2013 Help'
TOCTitle: 유사한 이름을 가진 사용자에 대 한 자동 전화 교환을 구성합니다
ms:assetid: 2e7318a0-67f9-4d7b-8300-5f0ef77656a8
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997135(v=EXCHG.150)
ms:contentKeyID: 52057902
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 유사한 이름을 가진 사용자에 대 한 자동 전화 교환을 구성합니다

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-16_

자동 전화 교환의 **주소록 및 교환원 액세스** 옵션에서 이름이 비슷한 사용자에 대해 사용할 방법을 구성할 수도 있고, 자동 전화 교환의 기본 설정은 그대로 유지하고 자동 전화 교환과 연결된 다이얼 플랜에서 이 설정을 구성할 수도 있습니다. 기본적으로 자동 전화 교환은 이름이 같거나 비슷한 둘 이상의 사용자를 구분할 수 없습니다. 자동 전화 교환의 기본 설정은 **다이얼 플랜에서 상속**이기 때문입니다.


> [!NOTE]
> 이름이 비슷한 사용자에 대해 포함할 정보가 제대로 작동하려면 Microsoft Exchange 조직의 받는 사람에 대한 직함, 부서 및 위치 정보를 제공해야 합니다.



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

## EAC를 사용하여 이름이 비슷한 사용자에 대해 UM 자동 전화 교환 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 구성할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **주소록 및 교환원 액세스**를 클릭하고 **이름이 같은 사용자에 대해 포함할 정보**에서 다음 중 하나를 선택합니다.
    
      - **직함**   일치하는 이름이 나열되는 경우 자동 전화 교환에서 각 사용자의 직함을 포함시킵니다.
    
      - **부서** 일치하는 이름이 나열되는 경우 자동 전화 교환에서 각 사용자의 부서를 포함시킵니다.
    
      - **위치** 일치하는 이름이 나열되는 경우 자동 전화 교환에서 각 사용자의 위치를 포함시킵니다.
    
      - **없음** 일치하는 이름이 나열되어도 자동 전화 교환에서 추가 정보를 포함시키지 않습니다.
    
      - **별칭 확인**   다이얼 플랜에서 발신자에게 사용자 별칭을 입력하라는 메시지가 들립니다.
    
      - **다이얼 플랜에서 상속**   자동 전화 교환에서 해당 자동 전화 교환과 연결된 다이얼 플랜의 기본 설정을 사용합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 이름이 비슷한 사용자에 대해 UM 자동 전화 교환 구성

이 예에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환에서 이름이 비슷한 사용자에 대해 포함할 정보를 별칭 확인으로 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod PromptForAlias

이 예에서는 이름이 비슷한 사용자에 대해 포함할 정보를 사용자의 직함으로 설정하고, 이름 조회를 사용하도록 설정하고, 자동 전화 교환에 전화를 거는 발신자가 \*를 눌러 `MyUMAutoAttendant`라는 UM 자동 전화 교환에 대한 Outlook Voice Access 환영 인사말을 들을 수 있도록 합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -MatchedNameSelectionMethod Title -NameLookupEnabled $true -StarOutToDialPlanEnabled $true

