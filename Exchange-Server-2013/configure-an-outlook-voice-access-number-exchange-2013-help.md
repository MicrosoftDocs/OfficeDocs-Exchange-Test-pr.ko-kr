---
title: 'Outlook Voice Access 번호를 구성 합니다.: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 번호를 구성 합니다.
ms:assetid: 443c838e-f266-4893-b6b2-e5fc96579b55
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997680(v=EXCHG.150)
ms:contentKeyID: 50555976
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 번호를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

Outlook Voice Access 번호를 사용하면 UM(통합 메시징) 및 음성 메일 사용 가능 사용자가 Outlook Voice Access를 통해 사서함에 액세스할 수 있습니다. 다이얼 플랜에서 Outlook Voice Access 또는 구독자 액세스 번호를 구성하는 경우 UM 사용 가능 사용자는 해당 번호로 전화를 걸고, 자신의 사서함에 로그인하고, 전자 메일, 음성 메일, 일정 및 개인 연락처 정보에 액세스할 수 있습니다.

기본적으로 UM 다이얼 플랜을 만들 때 Outlook Voice Access 번호는 구성되지 않습니다. Outlook Voice Access 번호를 구성하려면 먼저 다이얼 플랜을 만든 다음 다이얼 플랜의 **Outlook Voice Access** 옵션에서 Outlook Voice Access를 구성해야 합니다. Outlook Voice Access 번호가 꼭 필요한 것은 아니지만 UM 사용 가능 사용자가 Outlook Voice Access를 사용하여 자신의 사서함에 액세스할 수 있으려면 Outlook Voice Access 번호를 하나 이상 구성해야 합니다. 하나의 다이얼 플랜에 대해 Outlook Voice Access 번호를 여러 개 구성할 수도 있습니다.

Outlook Voice Access 번호에는 알파벳, 숫자, 특수 문자, 구분 기호 및 공백이 포함될 수 있습니다. 예를 들면 다음과 같습니다.

  - \+14255551010

  - \+1-425-555-1010

  - 4255551010

  - \+1 425 555 1010

  - 1-800-555-CALL

Outlook Voice Access 사용자에 대해 사용할 수 있는 메뉴 옵션에 대 한 자세한 내용은 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=64645)에서 사용할 수 있는 Outlook Voice Access에 대 한 빠른 참조 가이드를 참조 합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Voice Access 번호 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정할 UM 다이얼 플랜을 선택하고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **Outlook Voice Access**의 **Outlook Voice Access 번호**에서 사용할 번호를 상자에 입력한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 Outlook Voice Access 번호 구성

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜의 Outlook Voice Access 번호를 4255550100으로 설정합니다.

    Set-UMDialPlan -identity MyUMDialPlan -AccessTelephoneNumbers 4255550100

