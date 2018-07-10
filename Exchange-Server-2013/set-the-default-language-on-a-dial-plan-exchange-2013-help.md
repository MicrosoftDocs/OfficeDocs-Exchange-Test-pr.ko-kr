---
title: '다이얼 플랜에 기본 언어 설정: Exchange 2013 Help'
TOCTitle: 다이얼 플랜에 기본 언어 설정
ms:assetid: 7a1d2e7e-4053-40af-9ec1-ec714df12ad4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998914(v=EXCHG.150)
ms:contentKeyID: 50556016
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 다이얼 플랜에 기본 언어 설정

 

_**적용 대상:** Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2016-12-09_

UM(통합 메시징) 다이얼 플랜의 기본 언어를 설정할 수 있습니다. 만든 각 다이얼 플랜은 처음에 기본 언어로 영어(en-US)가 사용됩니다. 영어(en-US) 언어 팩은 MicrosoftExchange Server 2013의 모든 버전에 설치되며 제거할 수 없습니다.

예: 독일어 (DE-DE)를 기본 언어로 다른 언어를 선택 하려면 먼저 [Exchange Server 2013 UM 언어팩](https://go.microsoft.com/fwlink/p/?linkid=266542) 에서 독일어 UM 언어 팩.exe 파일을 다운로드 및 UMLanguagePack.de de.exe 설치 파일을 사용 하 여 사서함 서버에 해당 언어팩을 설치 해야 있습니다. 언어팩을 설치한 후에 UM 다이얼 플랜과에 기본 언어를 영어 (EN-US) 이외의 언어로 설정할 수 있습니다.

UM 언어와 관련된 추가 작업에 대한 자세한 내용은 [UM 언어, 프롬프트 및 인사말 절차](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 다이얼 플랜에서 기본 언어 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  **설정** 페이지의 **오디오 언어**에 있는 드롭다운 목록에서 설정할 언어를 선택합니다.

5.  **저장**을 클릭하여 변경 내용을 적용합니다.

## 셸을 사용하여 UM 다이얼 플랜에서 기본 언어 설정

이 예에서는 이름이 `MyUMDialPlan`인 UM 다이얼 플랜에서 기본 언어를 독일어로 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage de-DE

이 예에서는 이름이 `MyUMDialPlan`인 UM 다이얼 플랜에서 기본 언어를 일본어로 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage ja-JP

이 예에서는 이름이 `MyUMDialPlan`인 UM 다이얼 플랜에서 기본 언어를 오스트레일리아 영어로 설정합니다.

    Set-UMDialPlan -Identity MyUMDialPlan -DefaultLanguage en-AU

