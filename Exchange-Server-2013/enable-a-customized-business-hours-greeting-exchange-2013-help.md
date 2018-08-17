---
title: '사용자 지정 된 업무 시간 인사말을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 사용자 지정 된 업무 시간 인사말을 사용 하도록 설정
ms:assetid: a2272b7d-de88-4d3f-81e6-ad81f0ee6c5e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232152(v=EXCHG.150)
ms:contentKeyID: 50556055
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자 지정 된 업무 시간 인사말을 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-04-19_

UM(통합 메시징) 자동 전화 교환에 대해 사용자 지정 업무 시간 인사말을 사용하도록 설정할 수 있습니다. 업무 시간 인사말은 발신자가 업무 시간 중에 건 전화를 UM 자동 전화 교환에서 받을 경우 맨 처음 듣게 되는 말입니다. 이 인사말을 사용자 지정할 수 있습니다.

통합 메시징에는 업무 시간 동안 사용할 기본 시스템 음성 안내가 포함되어 있습니다. 기본 시스템 음성 안내를 바꾸거나 변경하면 안 되지만 사용자 지정 인사말을 제공할 수는 있습니다. 발신자가 업무 시간 동안 UM 자동 전화 교환으로 전화를 걸 경우 사용할 사용자 지정 인사말을 .wav 또는 .wma 파일 형식으로 만들 수 있습니다. "Woodgrove 은행입니다."를 예로 들 수 있습니다.

기본 인사말의 일부로 조직이나 회사의 이름을 포함하려면 UN 자동 전화 교환의 **회사 이름** 상자에 이름을 입력하면 됩니다. 자세한 내용은 [회사 이름 입력](enter-a-business-name-exchange-2013-help.md)을 참조하십시오.

자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)을 참조하십시오.

  - 인사말에 사용할 .wav 또는 .wma 파일을 만듭니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자 지정 업무 시간 인사말을 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 사용자 지정 업무 시간 인사말을 사용하도록 설정할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지 \> **인사말**의 **업무 시간 인사말**에서 **변경**을 클릭한 다음 **찾아보기**를 클릭하여 이 절차를 시작하기 전에 만든 사용자 지정 업무 시간 인사말 파일을 찾습니다.
    

    > [!IMPORTANT]
    > 인사말에 사용할 파일은 .wav 또는 .wma 파일이어야 합니다.



4.  파일을 찾은 후 **열기**를 클릭하고 **저장**을 클릭합니다.

## 셸을 사용하여 사용자 지정 업무 시간 인사말을 사용하도록 설정

이 예에서는 UM 자동 전화 교환 `MyUMAutoAttendant`에 대해 `GreetingFile.wav`라는 사용자 지정 인사말 파일을 사용하는 업무 시간 인사말을 사용하도록 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursWelcomeGreetingEnabled $true -BusinessHoursWelcomeGreetingFilename GreetingFile.wav

이 예에서는 업무 시간이 10:45 ~13:15(일요일), 09:00~17:00(월요일), 09:00~16:30(토요일)으로 구성되고, 휴일 및 연결된 인사말이 2013년 1월 2일에 "`New Year`"로, 2013년 4월 24일~ 2013년 4월 28일에 "`Building Closed for Construction`"으로 구성되는 `MyUMAutoAttendant`라는 UM 자동 전화 교환을 구성합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -BusinessHoursSchedule 0.10:45-0.13:15,1.09:00-1.17:00,6.09:00-6.16:30 -HolidaySchedule "New Year,newyrgrt.wav,1/2/2013","Building Closed for Construction,construction.wav,4/24/2013,4/28/2013"

이 예에서는 `MyAutoAttendant`라는 UM 자동 전화 교환을 구성하고, 발신자가 1을 누를 경우 `SalesAutoAttendant`라는 다른 UM 자동 전화 교환에 전달되도록 업무 시간 키 매핑을 사용 설정합니다. 2를 누르면 `Support`를 위해 내선 번호 12345로 전달되고, 3을 누르면 오디오 파일을 재생하는 다른 자동 전화 교환으로 전송됩니다.

    Set-UMAutoAttendant -Identity MyAutoAttendant - BusinessHoursKeyMappingEnabled $true -BusinessHoursKeyMapping "1,Sales,,SalesAutoAttendant","2,Support,12345","3,Directions,,,directions.wav"

