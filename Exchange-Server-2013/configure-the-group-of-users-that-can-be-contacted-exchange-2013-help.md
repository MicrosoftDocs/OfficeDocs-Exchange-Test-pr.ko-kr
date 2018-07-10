---
title: '연락할 수 있는 사용자 그룹을 구성 합니다.: Exchange 2013 Help'
TOCTitle: 연락할 수 있는 사용자 그룹을 구성 합니다.
ms:assetid: 45d9d6d5-c9d6-4b73-8aa2-a23599a4381c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423545(v=EXCHG.150)
ms:contentKeyID: 52057916
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 연락할 수 있는 사용자 그룹을 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-09_

UM(통합 메시징) 자동 전화 교환에 전화를 걸 때 발신자가 연결할 수 있는 사용자 그룹을 지정할 수 있습니다. 기본적으로 발신자는 UM 자동 전화 교환과 연결된 동일한 다이얼 플랜 내의 사용자에 연결할 수 있습니다. 그러나 발신자가 조직의 주소록에 있는 사용자나 특정 사용자 집합에 전화 연결하거나 음성 메시지를 보낼 수 있도록 하려는 경우 사용자 그룹을 변경할 수 있습니다.

자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 관리](manage-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 발신자가 연결할 수 있는 사용자 그룹 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 구성할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **주소록 및 교환원 액세스**의 **주소록 검색 옵션**에서 다음 옵션 중 하나를 선택합니다.
    
      - **이 다이얼 플랜에서만**   UM 자동 전화 교환에 연결된 발신자가 UM 자동 전화 교환과 연결된 다이얼 플랜 내의 사용자를 찾아 연락할 수 있도록 하려면 이 옵션을 선택합니다.
    
      - **전체 조직에서**   UM 자동 전화 교환에 연결된 발신자가 조직 주소록에 있는 사용자를 찾고 연결할 수 있도록 하려면 이 옵션을 선택합니다. 여기에는 사서함을 사용할 수 있는 모든 사용자가 포함됩니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 발신자가 연결할 수 있는 사용자 그룹 구성

이 예에서는 발신자가 `MyUMAutoAttendant`라는 UM 자동 전화 교환의 조직 주소록에 있는 모든 사용자에게 연결할 수 있도록 사용자 범위를 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -ContactScope GlobalAddressList

