---
title: '업무 시간을 구성 합니다.: Exchange 2013 Help'
TOCTitle: 업무 시간을 구성 합니다.
ms:assetid: 96b4be99-af94-4fa4-959a-48413387a044
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232133(v=EXCHG.150)
ms:contentKeyID: 50483743
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 업무 시간을 구성 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-04-19_

UM(통합 메시징) 자동 전화 교환에 대한 업무 시간을 구성할 때는 조직의 하루 중 업무 시간과 발신자가 자동 전화 교환에 구성된 내선 번호로 전화를 걸었을 때 듣게 될 업무 시간 인사말 및 메뉴 음성 안내를 정의합니다. 정의한 업무 시간 외의 시간에 발신자가 자동 전화 교환에 연결할 경우 발신자는 업무 시간 외 음성 안내 및 인사말을 듣게 됩니다.

EAC에서는 몇 가지 기본 일정 옵션을 사용할 수 있습니다. 예를 들어, 대부분의 업무 시간은 오전 8시부터 오후 5시까지 월요일부터 금요일 사이입니다. 그러나 기본 옵션이 필요에 맞지 않아 일정을 사용자 지정해야 하는 경우도 있습니다. 업무 시간이 시스템에서 정의된 일정과 다른 경우 자동 전화 교환을 위해 사용자 지정 일정을 정의할 수 있습니다.

기본적으로 UM 자동 전화 교환에서는 발신자가 자동 전화 교환에 전화를 거는 시간에 관계없이 업무 시간 음성 안내 및 인사말을 재생합니다.


> [!NOTE]
> UM 자동 전화 교환에서 업무 시간과 업무 외 시간에 대한 일정을 설정할 때는 표준 시간대가 정확하게 구성되었는지 확인해야 합니다.



UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 자동 전화 교환에 대한 업무 시간 지정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환** 아래에서 업무 시간을 설정할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **업무 시간**의 **업무 시간**에서 **업무 시간 구성**을 클릭합니다.

4.  **업무 시간 구성** 페이지에서 각 요일마다 업무 시간으로 사용할 시간을 선택합니다.

5.  **확인**을 클릭한 다음 **저장**을 클릭합니다.

## 셸을 사용하여 UM 자동 전화 교환에 대해 업무 시간 지정

이 예에서는 `MyUMAutoAttendant`라는 UM 자동 전화 교환에 대해 업무 시간을 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30

