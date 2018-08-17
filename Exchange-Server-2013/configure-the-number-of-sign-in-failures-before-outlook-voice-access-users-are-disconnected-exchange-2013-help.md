---
title: 'Outlook Voice Access 사용자의 연결이 끊어집니다 전에 로그인 실패 횟수를 구성 합니다.: Exchange 2013 Help'
TOCTitle: Outlook Voice Access 사용자의 연결이 끊어집니다 전에 로그인 실패 횟수를 구성 합니다.
ms:assetid: 02f93888-168c-44bb-8cf6-17f5fcc3d733
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423537(v=EXCHG.150)
ms:contentKeyID: 50482394
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Voice Access 사용자의 연결이 끊어집니다 전에 로그인 실패 횟수를 구성 합니다.

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-11-09_

발신자의 연결을 끊기 전에 허용되는 연속적으로 실패한 로그인 시도 횟수를 지정할 수 있습니다. 이 설정의 값은 1 ~ 20이 될 수 있습니다. 이 값을 너무 작은 값으로 설정하면 사용자가 불편할 수 있습니다. 대부분의 조직에서 기본값인 3회로 설정합니다.

다이얼 플랜과 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자의 연결을 끊기 전 로그인 오류 발생 횟수를 구성합니다.

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정할 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **설정**의 **연결 끊기 전 로그인 오류 발생 횟수**에 로그인 오류 발생 횟수를 입력합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 사용자 연결을 끊기 전 로그인 오류 횟수 구성

다음은 `MyUMDialPlan`이라는 UM 다이얼 플랜에 대해 사용자 연결을 끊기 전 로그인 오류 횟수를 5번으로 설정하는 예입니다.

    Set-UMDialPlan -identity MyUMDialPlan -LogonFailuresBeforeDisconnect 5

