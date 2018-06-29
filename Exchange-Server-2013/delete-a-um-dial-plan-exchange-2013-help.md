---
title: 'UM 다이얼 플랜을 삭제: Exchange 2013 Help'
TOCTitle: UM 다이얼 플랜을 삭제
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 50484162
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 다이얼 플랜을 삭제

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2012-11-11_

기존 UM(통합 메시징) 다이얼 플랜을 삭제할 수 있습니다. UM 다이얼 플랜을 삭제할 경우 UM IP 게이트웨이, UM 사서함 정책 및 UM 헌트 그룹을 더 이상 사용할 수 없게 됩니다. UM 사서함 정책, UM 자동 전화 교환, UM IP 게이트웨이 또는 UM 헌트 그룹에서 참조되거나 여기에 연결되어 있는 UM 다이얼 플랜은 삭제할 수 없습니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 기존 UM 다이얼 플랜 삭제

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 삭제할 UM 다이얼 플랜을 선택하고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

3.  경고 페이지에서 **예**를 클릭합니다.

## 셸을 사용하여 기존 UM 다이얼 플랜 삭제

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜을 삭제합니다.

    RemoveUMDialplan -identity MyUMDialPlan

