---
title: '정보 알림을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 정보 알림을 사용 하도록 설정
ms:assetid: 07f6c13e-3781-4127-9321-f0f85f054259
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb266918(v=EXCHG.150)
ms:contentKeyID: 50555934
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 정보 알림을 사용 하도록 설정

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-04-19_

UM(통합 메시징) 자동 전화 교환에 대해 정보 알림을 사용할 수 있습니다. 정보 알림을 사용하도록 설정하면 업무 시간 또는 업무 시간 외 인사말이 제공된 직후에 재생됩니다. 기본적으로 정보 알림은 구성되어 있지 않습니다. 정보 알림을 사용하려면 정보 알림으로 사용할 .wav 또는 .wma 파일을 만든 후 이 사운드 파일을 사용하도록 자동 전화 교환을 구성합니다.

자동 전화 교환과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 자동 전화 교환 절차](um-auto-attendant-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 정보 안내에 사용할 .wav 또는 .wma 파일을 만듭니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 정보 알림을 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환** 아래에서 정보 알림을 사용할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 자동 전화 교환** 페이지에서 \> **인사말** 아래에 있는 **정보 알림**에서 **변경**을 클릭한 다음 **찾아보기**를 클릭하여 이 절차를 시작하기 전에 만든 정보 알림 파일을 찾습니다.
    

    > [!IMPORTANT]
    > 인사말에 사용할 파일은 .wav 또는 .wma 파일이어야 합니다.



4.  파일을 찾은 후 **열기**를 클릭하고 **저장**을 클릭합니다.

## 셸을 사용하여 정보 알림을 사용하도록 설정

이 예에서는 `MyInfoAnnouncement.wav`라는 UM 자동 전화 교환에 대해 `MyUMAutoAttendant` 파일을 사용하는 정보 알림을 사용하도록 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -InfoAnnouncementEnabled $true -InfoAnnouncementFilename MyInfoAnnouncement.wav

