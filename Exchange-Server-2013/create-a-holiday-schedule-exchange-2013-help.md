---
title: '휴일 일정을 만들려면: Exchange 2013 Help'
TOCTitle: 휴일 일정을 만들려면
ms:assetid: 0c5c51e4-5b51-451b-ab93-2cebf644dc96
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266921(v=EXCHG.150)
ms:contentKeyID: 50482455
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 휴일 일정을 만들려면

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-19_

조직에서 휴일 및 기타 이유로 인해 쉬는 날짜 및 시간을 정의할 수 있습니다. 지정한 시작 날짜와 끝 날짜 사이에 UM(통합 메시징) 자동 전화 교환에 연결되는 발신자는 사용자가 휴일 일정을 구성할 때 지정한 휴일 인사말을 듣게 됩니다. 발신자가 지정된 휴일 인사말을 듣고 나면 업무 시간 외 인사말과 메뉴 음성 안내가 발신자에게 재생됩니다.

기존 휴일 일정 내에 휴일 일정을 만들 수도 있습니다. 여러 개의 휴일 일정을 만들 때 통합 메시징을 통해 예약된 휴일 시간을 덮어쓸 수 있습니다. 예를 들어 조직이 공사로 인해 쉬는 경우 12월 15일부터 12월 31일까지 휴일 일정을 정의할 수 있으며 12월 24일부터 12월 26일까지 또 다른 휴일 일정을 정의할 수 있습니다. 발신자가 12월 15일부터 12월 23일 또는 12월 27일부터 12월 31일 사이에 자동 전화 교환에 전화를 걸면 이 일정에 대해 사용자가 지정한 휴일 인사말이 제공됩니다. 예를 들면 "현재 공사로 휴업 중입니다." 등이 있습니다. 발신자가 12월 24일부터 12월 26일 사이에 자동 전화 교환으로 전화를 걸면 "직원 휴가 중이므로 현재 업무를 하지 않습니다."와 같은 다른 인사말이 제공됩니다.

UM 자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 자동 전화 교환에 대해 휴일 일정 지정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 휴일 일정을 설정할 UM 자동 전화 교환을 선택합니다. 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **업무 시간**의 **휴일 일정**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

4.  **새 휴일** 페이지에서 다음을 구성합니다.
    
      - **이름**   휴일 일정의 이름을 입력합니다.
    
      - **휴일 인사말**   인사말로 사용할 .wav 파일을 찾습니다. 이 항목은 필수 필드입니다.
    
      - **시작 날짜**   이 목록을 사용하여 휴일이 시작되는 날짜를 선택합니다. 휴일 일정이 이 목록에 지정한 날짜의 자정에 시작됩니다.
    
      - **끝 날짜**   이 목록을 사용하여 휴일이 종료되는 날짜를 선택합니다. 휴일 일정이 이 목록에 지정한 날짜의 오후 11시 59분에 종료됩니다.

5.  휴일 일정을 구성한 후에 **확인**을 클릭한 다음 **저장**을 클릭합니다.

## 셸을 사용하여 UM 자동 전화 교환에 대해 휴일 일정 지정

이 예에서는 업무 시간이 10:45~13:15(일요일), 09:00~17:00(월요일), 09:00~16:30(토요일)으로 구성되고 휴일 시간 및 관련 인사말이 2013년 1월 2일에 "New Year"로, 2013년 4월 24일~2013년 4월 28일에 "Building Closed for Construction"으로 구성되는 `MyUMAutoAttendant`라는 UM 자동 전화 교환을 구성합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

