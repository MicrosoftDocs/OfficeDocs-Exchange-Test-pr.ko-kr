---
title: '표준 시간대를 구성 합니다.: Exchange 2013 Help'
TOCTitle: 표준 시간대를 구성 합니다.
ms:assetid: 30d769e1-3657-4622-bc9a-643c63cf46d9
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997162(v=EXCHG.150)
ms:contentKeyID: 50555964
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 표준 시간대를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-17_

기본적으로 UM(통합 메시징) 자동 전화 교환은 자동 전화 교환이 만들어진 사서함 서버의 표준 시간대를 사용합니다. 그러나 UM 자동 전화 교환의 표준 시간대를 다른 표준 시간대로 변경해야 하는 경우가 있습니다. 예를 들어, 두 개의 UM 다이얼 플랜이 있고 각 다이얼 플랜이 나타내는 표준 시간대가 서로 다른 경우 하나의 UM 자동 전화 교환을 구성하여 사서함 서버와 동일한 표준 시간대를 갖게 하고 다른 UM 자동 전화 교환은 사서함 서버와는 다른 표준 시간대를 갖도록 합니다.

자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 표준 시간대 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 표준 시간대를 설정할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지에서 **업무 시간**을 클릭한 다음 **표준 시간대**의 드롭다운 목록에서 표준 시간대를 선택합니다.

4.  변경 사항을 저장하려면 **확인**을 클릭한 다음 **저장**을 클릭합니다.

## 셸을 사용하여 표준 시간대 구성

이 예에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환의 표준 시간대를 Pacific 표준 시간대로 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -TimeZoneName Pacific

