---
title: '사용자 지정 된 업무 시간 외 메뉴 음성 안내를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사용자 지정 된 업무 시간 외 메뉴 음성 안내를 사용 하도록 설정
ms:assetid: 094c50b2-072b-4929-aaf8-f7db5b19e9b6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266919(v=EXCHG.150)
ms:contentKeyID: 50555936
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 지정 된 업무 시간 외 메뉴 음성 안내를 사용 하도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-03-22_

업무 시간 외에 UM(통합 메시징) 자동 전화 교환에서 메뉴 음성 안내를 사용하도록 사용자 지정할 수 있습니다. UM 자동 전화 교환을 만들면 기본 시스템 음성 안내("통합 메시징 시작")가 발신자에게 업무 시간 외 인사말이 재생된 다음에 들리는 메뉴 음성 안내로 사용됩니다. 시스템 음성 안내는 바꾸거나 변경할 수 없지만 UM 자동 전화 교환에 사용되는 인사말과 메뉴 음성 안내는 사용자 지정할 수 있습니다. 사용자 지정 업무 시간 외 메뉴 음성 안내 오디오 파일을 만든 후에는 업무 시간 외의 UM 자동 전화 교환에서 메뉴 탐색 항목을 사용하도록 설정해야 합니다.

기본 시스템 음성 안내의 일부로 조직이나 회사의 이름을 포함하려면 UM 자동 전화 교환의 **회사 이름** 상자에 이름을 입력하면 됩니다. 자세한 내용은 [회사 이름 입력](enter-a-business-name-exchange-2013-help.md)을 참조하십시오.


> [!IMPORTANT]
> 자동 전화 교환에서 업무 시간을 구성해야 합니다. 업무 시간을 구성하면 업무 외 시간은 자동으로 설정됩니다. 자세한 내용은 <A href="configure-business-hours-exchange-2013-help.md">업무 시간을 구성 합니다.</A>을 참조하십시오.



자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)을 참조하십시오.

  - 메뉴 음성 안내에 사용할 .wav 또는 .wma 파일을 만듭니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자 지정 업무 시간 외 메뉴 음성 안내를 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 사용자 지정 업무 시간 외 메뉴 음성 안내를 사용할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **메뉴 탐색** 아래에 있는 **업무 시간 외 메뉴 탐색**에서 **변경**을 클릭한 다음 **찾아보기**를 클릭하여 사용자 지정 업무 시간 외 메뉴 음성 안내 파일을 찾습니다.
    

    > [!IMPORTANT]
    > 메뉴 음성 안내에 사용할 파일은 .wav 또는 .wma 파일이어야 합니다.



4.  파일을 찾은 후 **열기**를 클릭하고 **저장**을 클릭합니다.

## 셸을 사용하여 사용자 지정 업무 시간 외 메뉴 음성 안내를 사용하도록 설정

이 예에서는 업무 시간이 10:45~13:15(일요일), 09:00~17:00(월요일), 09:00~16:30(토요일) 및 휴일로 구성되고 연결된 인사말이 2013년 1월 1일에 "`New Year`"로, 2013년 4월 24일~2013년 4월 28일에 "`Building Closed for Construction`"으로 구성되는 `MyUMAutoAttendant`라는 UM 자동 전화 교환을 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

이 예에서는 `MyAutoAttendant`라는 UM 자동 전화 교환을 구성하고, 발신자가 1을 누를 경우 `SalesAutoAttendant`라는 다른 UM 자동 전화 교환에 전달되도록 업무 시간 외 탐색 메뉴를 사용 설정합니다. 2를 누르면 `Support`를 위해 내선 번호 12345로 전달되고, 3을 누르면 오디오 파일을 재생하는 다른 UM 자동 전화 교환으로 전송됩니다.

    Set-UMAutoAttendant -Identity MyAutoAttendant - 
    AfterHoursKeyMappingEnabled $true -
    AfterHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

