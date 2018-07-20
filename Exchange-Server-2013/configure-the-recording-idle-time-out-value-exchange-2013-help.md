---
title: '녹음/녹화 유휴 시간 제한 값을 구성: Exchange 2013 Help'
TOCTitle: 녹음/녹화 유휴 시간 제한 값을 구성
ms:assetid: a7fb9a09-fde9-447d-ad2c-95598405e99b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423550(v=EXCHG.150)
ms:contentKeyID: 50483899
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 녹음/녹화 유휴 시간 제한 값을 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-11_

통화가 종료되기 전에 음성 메시지가 녹음될 때 시스템에서 소리가 나지 않아도 되게 허용하는 시간(초)을 지정할 수 있습니다. 대부분의 조직에서 기본값인 5초로 설정합니다.

이 값은 2~10으로 설정할 수 있습니다. 이 값을 너무 낮게 설정하면 호출자가 음성 메시지를 남기는 도중에 시스템과 호출자의 연결이 끊길 수 있습니다. 이 값을 너무 큰 값으로 설정하면 음성 메시지에서 소리가 나지 않는 시간이 길어질 수 있습니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 녹음 유휴 시간 제한 값 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **설정**의 **녹음 유휴 시간 제한(초)**에 시간(초)을 입력합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 녹음 유휴 시간 제한 값 구성

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜의 녹음 유휴 시간 제한 값을 10으로 설정합니다.

    Set-UMDialPlan -identity MyUMDialPlan -RecordingIdleTimeout 10

