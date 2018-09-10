---
title: 'Outlook Voice Access 사용자에 대 한 정보 알림을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 정보 알림을 사용 하도록 설정
ms:assetid: b69ed0e1-f978-498a-963e-42a047678db4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124344(v=EXCHG.150)
ms:contentKeyID: 50556073
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 정보 알림을 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

UM(통합 메시징) 다이얼 플랜에서 정보 알림을 사용하도록 설정할 수 있습니다. 정보 알림은 환영 인사말보다 더 자주 변경되는 일반 알림과 회사 규정 준수 정책에 필요한 알림에 사용됩니다.

기본적으로 구성된 Outlook Voice Access 번호로 전화를 거는 Outlook Voice Access 사용자를 비롯하여 발신자에게는 정보 알림이 재생되지 않습니다. 정보 알림이 재생되도록 하려면 UM 다이얼 플랜을 만든 후에 정보 알림으로 사용할 .wav 또는 .wma 파일을 만들고 다이얼 플랜에서 해당 정보 알림을 사용하도록 설정해야 합니다.

발신자가 전체 정보 알림을 듣도록 해야 하는 경우 알림을 무중단으로 구성할 수 있습니다. 그러면 발신자는 키를 누르거나 음성 명령을 사용하여 알림을 중단 또는 중지할 수 없게 됩니다.

Outlook Voice Access 사용자가 사용할 수 있는 메뉴 옵션에 대 한 자세한 내용은 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=272767)에서 사용할 수 있는 Outlook Voice Access에 대 한 빠른 참조 가이드를 참조 합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](https://docs.microsoft.com/ko-kr/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 정보 알림을 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **Outlook Voice Access**의 **정보 알림**에서 **변경**을 클릭한 다음 **찾아보기**를 클릭하여 알림 파일을 찾습니다.
    

    > [!IMPORTANT]
    > 정보 알림에 사용할 파일은 .wav 또는 .wma 파일이어야 합니다.



5.  파일을 찾은 후 **열기**를 클릭하고 **저장**을 클릭합니다.

## 셸을 사용하여 정보 알림을 사용하도록 설정

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜에서 informational.wav 정보 알림 파일을 사용하는 정보 알림을 사용하도록 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -InfoAnnouncementEnabled $true-InfoAnnouncementFilename c:\UMGreetings\informational.wav

