---
title: 'Outlook Voice Access 사용자가 문의할 수 있는 사용자 그룹을 구성 합니다.: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자가 문의할 수 있는 사용자 그룹을 구성 합니다.
ms:assetid: a8dc0f9e-dc86-4128-af63-d4e550aed5bb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423551(v=EXCHG.150)
ms:contentKeyID: 50483835
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자가 문의할 수 있는 사용자 그룹을 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-09_

Outlook Voice Access 사용자로부터 전달된 통화 또는 음성 사서함 메시지를 수신할 수 있는 사용자를 지정할 수 있습니다. 기본적으로 **이 다이얼 플랜에서만** 옵션이 선택되어 있습니다. 이 설정을 변경하여 Outlook Voice Access 사용자가 전체 조직에 있는 사용자, 기존 UM 자동 전화 교환 또는 특정 내선 번호에 통화를 전달하거나 음성 메시지를 보내도록 허용할 수 있습니다.

UM 다이얼 플랜과 관련된 추가 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Voice Access 사용자가 연결할 수 있는 사용자 그룹 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **전송 및 검색**의 **전화 건 사람이 사용자를 이름 또는 별칭으로 검색하도록 허용**에서 다음 옵션 중 하나를 선택합니다.
    
      - **이 다이얼 플랜에서만**   Outlook Voice Access 번호에 전화를 거는 Outlook Voice Access 사용자가 동일한 다이얼 플랜의 사용자를 찾고 연결할 수 있도록 하려면 이 옵션을 사용합니다.
    
      - **전체 조직에서**   Outlook Voice Access 번호에 전화를 거는 Outlook Voice Access 사용자가 전체 조직에서 사용자를 찾고 연결할 수 있도록 하려면 이 옵션을 사용합니다. 여기에는 사서함을 사용할 수 있는 모든 사용자가 포함됩니다.
    
      - **이 자동 전화 교환에서만**   Outlook Voice Access 번호에 전화를 거는 Outlook Voice Access 사용자가 특정 전화 교환에 연결할 수 있도록 하려면 이 옵션을 사용합니다. 지정하기 전에 먼저 자동 전화 교환을 만들어야 합니다. 그러면 Outlook Voice Access 사용자가 다른 자동 전화 교환에 연결할 수 있습니다. 여기서 선택한 자동 전화 교환은 음성 사용이 가능한 형식이거나 가능하지 않은 형식일 수 있습니다.
    
      - **이 내선 번호만**   Outlook Voice Access 사용자가 지정된 내선 번호에 연결할 수 있도록 하려면 이 옵션을 사용합니다. 내선 번호에는 숫자만 사용할 수 있습니다. 이 필드에 정의할 수 있는 자릿수는 UM 다이얼 플랜에 구성된 내선 번호의 자릿수와 일치해야 합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 Outlook Voice Access 사용자가 연결할 수 있는 사용자 그룹 구성

다음 예에서는 Outlook Voice Access 사용자가 `MyUMDialPlan`이라는 UM 다이얼 플랜에 대해 전체 조직에 연결할 수 있는 사용자 그룹을 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope 'GlobalAddressList' -UMAutoAttendant $null -AllowDialPlanSubscribers $false -AllowExtensions $false

다음 예에서는 Outlook Voice Access 사용자가 `MyUMDialPlan`이라는 UM 다이얼 플랜에 대해 `DialPlan`에 연결할 수 있는 사용자 그룹을 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -ContactScope DialPlan -AllowDialPlanSubscribers $false -AllowExtensions $false

