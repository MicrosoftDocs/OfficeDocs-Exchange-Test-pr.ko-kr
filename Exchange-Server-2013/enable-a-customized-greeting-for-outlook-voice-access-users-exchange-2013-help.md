---
title: 'Outlook Voice Access 사용자에 대 한 사용자 지정된 인사말을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자에 대 한 사용자 지정된 인사말을 사용 하도록 설정
ms:assetid: abd418ec-2c65-4720-859d-c11a2698dc06
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124125(v=EXCHG.150)
ms:contentKeyID: 50556058
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자에 대 한 사용자 지정된 인사말을 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

기본적으로 각 UM(통합 메시징) 다이얼 플랜에서는 구성된 Outlook Voice Access 번호로 전화를 건 Outlook Voice Access 사용자를 비롯한 발신자에게 재생되는 환영 인사말로 표준 .wav 파일을 사용합니다. 하지만 환영 인사말로 사용할 .wav 또는 .wma 파일을 직접 만든 다음 UM 다이얼 플랜에서 이 파일을 사용하도록 설정할 수도 있습니다.

예를 들어 기본 환영 인사말을 변경하여 "안녕하세요. Woodgrove 은행의 Outlook Voice Access입니다." 등과 같이 회사 고유의 환영 인사말을 대신 제공할 수 있습니다. 이렇게 하려면 사용자 지정 환영 인사말을 녹음하고 .wav 또는 .wma 파일로 저장한 후 다이얼 플랜에서 사용자 지정 환영 인사말을 사용하도록 구성합니다.

Outlook Voice Access 사용자에 대해 사용할 수 있는 메뉴 옵션에 대 한 자세한 내용은 [Microsoft 다운로드 센터](https://go.microsoft.com/fwlink/p/?linkid=272767)에서 사용할 수 있는 Outlook Voice Access에 대 한 빠른 참조 가이드를 참조 합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자 지정 환영 인사말을 사용하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **Outlook Voice Access**의 **환영 인사말**에서 **변경**을 클릭한 다음 **찾아보기**를 클릭하여 인사말 파일을 찾습니다.
    

    > [!IMPORTANT]
    > 환영 인사말에 사용할 파일은 .wav 또는 .wma 파일이어야 합니다.



5.  파일을 찾은 후 **열기**를 클릭하고 **저장**을 클릭합니다.

## 셸을 사용하여 사용자 지정 환영 인사말을 사용하도록 설정

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜에서 C:\\UMPrompts\\welcome.wav 파일을 사용하는 환영 인사말을 사용하도록 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -WelcomeGreetingEnabled $true -WelcomeGreetingFilename c:\UMPrompts\welcome.wav

