---
title: '유사한 이름을 가진 사용자에 대 한 다이얼 플랜을 구성 합니다.: Exchange 2013 Help'
TOCTitle: 유사한 이름을 가진 사용자에 대 한 다이얼 플랜을 구성 합니다.
ms:assetid: 14783f45-95f5-49de-8215-0a3aef7dc034
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266943(v=EXCHG.150)
ms:contentKeyID: 51407667
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 유사한 이름을 가진 사용자에 대 한 다이얼 플랜을 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-21_

UM(통합 메시징) 다이얼 플랜을 구성하여 사용자의 이름이 같거나 비슷할 때 발신자에게 제공되는 정보를 지정할 수 있습니다. UM은 이 설정을 사용하여 이름이 같거나 비슷한 사용자를 구분해 발신자에게 해당 정보를 제공합니다. 발신자 또는 Outlook Voice Access 사용자에게 특정 사용자를 찾을 문자를 입력하라는 메시지가 들리는 경우 발신자의 입력과 일치하는 이름이 두 개 이상 있을 수도 있습니다. 연결하려는 사용자를 찾는 데 도움이 되는 추가 정보를 발신자에게 제공하기 위해 여러 가지 옵션 중 하나를 사용할 수 있습니다.

이 설정은 UM 다이얼 플랜과 UM 자동 전화 교환 둘 다에 대해 지정할 수 있습니다. UM 자동 전화 교환을 만들면 자동 전화 교환과 연결된 다이얼 플랜에서 이 설정을 상속받습니다. 기본적으로 다이얼 플랜에 대해서는 이 설정이 구성되지 않으므로 발신자가 올바른 사용자를 찾는 데 도움이 되는 추가 정보는 제공되지 않습니다.


> [!NOTE]
> 이름이 비슷한 사용자에 대해 포함할 정보가 제대로 작동하려면 Microsoft Exchange 조직의 받는 사람에 대한 직함, 부서 및 위치 정보를 제공해야 합니다.



다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 이름이 비슷한 사용자에 대해 UM 다이얼 플랜 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지에서 **구성** \> **전송 및 검색**을 클릭하고 **이름이 같은 사용자에 대해 포함할 정보**에서 다음 옵션 중 하나를 선택합니다.
    
      - **직함**   다이얼 플랜에서 이름이 비슷한 둘 이상의 사용자를 찾을 때 각 사용자의 직함을 포함합니다.
    
      - **부서**   다이얼 플랜에서 이름이 비슷한 둘 이상의 사용자를 찾을 때 각 사용자의 부서를 포함합니다.
    
      - **위치**   다이얼 플랜에서 이름이 비슷한 둘 이상의 사용자를 찾을 때 각 사용자의 위치를 포함합니다.
    
      - **없음** 다이얼 플랜에서 이름이 비슷한 사용자가 있을 때 추가 정보를 포함하지 않습니다. 없음이 기본 설정이기는 하지만 발신자에 대해 사용 가능한 옵션 중 하나를 포함하는 것이 좋습니다. 그렇지 않으면 발신자가 이름이 비슷한 둘 이상의 사용자를 구분할 수 없습니다.
    
      - **별칭 확인**   다이얼 플랜에서 발신자에게 사용자 별칭을 입력하라는 메시지가 들립니다. 별칭은 사용자의 전자 메일 또는 SMTP 주소에서 @ 기호 앞에 표시되는 부분입니다.

3.  **저장**을 클릭합니다.

## 셸을 사용하여 이름이 비슷한 사용자에 대해 UM 다이얼 플랜 구성

이 예에서는 `MyDialPlan`이라는 UM 다이얼 플랜에서 이름이 비슷한 사용자에 대해 포함할 정보를 사용자 별칭 확인으로 설정합니다.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod PromptForAlias

이 예에서는 `MyDialPlan`이라는 UM 다이얼 플랜에서 이름이 비슷한 사용자에 대해 포함할 정보를 부서로 설정합니다.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Department

이 예에서는 `MyDialPlan`이라는 UM 다이얼 플랜에서 이름이 비슷한 사용자에 대해 포함할 정보를 위치로 설정합니다.

    Set-UMDialplan -Identity MyDialPlan -MatchedNameSelectionMethod Location

