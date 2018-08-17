---
title: '최대 통화 기간 구성: Exchange 2013 Help'
TOCTitle: 최대 통화 기간 구성
ms:assetid: 01aa40d2-f918-472b-bace-158222143484
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423535(v=EXCHG.150)
ms:contentKeyID: 50482391
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 최대 통화 기간 구성

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-09_

들어오는 호출이 종료되기 전까지 유효한 내선 번호로 전환되지 않고 시스템에 연결될 수 있는 최대 시간(분)을 지정할 수 있습니다. 대부분의 조직에서는 이 값을 기본값으로 설정해야 합니다. 30분. 이 설정은 들어오는 Outlook Voice Access 호출, 조직 내부의 음성 호출, UM(통합 메시징) 자동 전화 교환으로 수신되는 음성 호출 및 조직 외부에서 걸려오는 팩스 호출을 포함한 모든 호출에 적용됩니다.

이 값은 10 ~ 120 사이의 숫자로 설정할 수 있습니다. 이 값을 너무 작게 설정하면 들어오는 호출이 완료되기 전에 끊어질 수 있습니다. 예를 들어 조직에서 아주 많은 팩스 메시지를 받는 경우 팩스 메시지의 모든 페이지가 수신되도록 하려면 이 값을 늘립니다.

UM 다이얼 플랜과 관련된 추가 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 최대 통화 시간 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **설정**의 **최대 통화 시간(분)**에 숫자(분)를 입력합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 최대 통화 시간 구성

다음은 `MyUMDialPlan`이라는 UM 다이얼 플랜의 최대 통화 시간을 10분으로 설정하는 예입니다.

    Set-UMDialPlan -identity MyUMDialPlan -MaxCallDuration 10

