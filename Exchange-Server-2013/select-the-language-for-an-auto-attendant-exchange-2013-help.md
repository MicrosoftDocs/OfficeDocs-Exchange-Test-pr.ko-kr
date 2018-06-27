---
title: '자동 전화 교환에 대 한 언어를 선택 합니다.: Exchange 2013 Help'
TOCTitle: 자동 전화 교환에 대 한 언어를 선택 합니다.
ms:assetid: 3a1c1ec0-c726-41fb-a294-59faab205609
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997306(v=EXCHG.150)
ms:contentKeyID: 50555969
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 자동 전화 교환에 대 한 언어를 선택 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2016-12-09_

UM(통합 메시징) 자동 전화 교환의 기본 음성 안내 언어 설정을 구성할 수 있습니다. UM 자동 전화 교환에서 사용할 수 있는 언어 설정을 통해 자동 전화 교환에서 기본 음성 안내 언어를 구성할 수 있습니다. 자동 전화 교환에 대해 기본 시스템 음성 안내를 사용하는 경우 이 언어는 자동 전화 교환이 수신 전화에 응답할 때 발신자가 듣게 되는 언어입니다. 이 언어 설정은 Microsoft Exchange 통합 메시징 서비스를 실행 중인 사서함 서버를 설치하면 제공되는 기본 시스템 음성 안내에만 적용되며, 자동 전화 교환에 구성된 사용자 지정 음성 안내에는 영향을 주지 않습니다. 사용 가능한 언어는 사서함 서버에 설치된 통합 메시징 언어 팩에 따라 달라집니다.

처음 만들면 각 자동 전화 교환을 기본 언어로 영어 (EN-US)을 사용 합니다. 영어 (EN-US) 언어팩 Microsoft Exchange 2013의 모든 버전에는 기본적으로 설치 되 고 제거할 수 없습니다. 다른 언어를 독일어 (DE-DE), 예를 선택 하려면 먼저 [Exchange Server 2013 UM 언어팩](https://go.microsoft.com/fwlink/?linkid=266542) 에서 독일어 UM 언어 팩.exe 파일을 다운로드 및 UMLanguagePack.de de.exe 설치 파일을 사용 하 여 사서함 서버에서 UM 언어팩을 설치 해야 있습니다. UM 언어팩을 설치한 후에 UM 자동 전화 교환에서 언어를 영어 (EN-US) 외에 기본 언어를 설정할 수 있습니다.

UM 언어와 관련된 추가 작업에 대한 자세한 내용은 [UM 언어, 프롬프트 및 인사말 절차](um-languages-prompts-and-greetings-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 자동 전화 교환" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 자동 전화 교환을 만들었는지 확인합니다. 자세한 단계는 [UM 자동 전화 교환 만들기](create-a-um-auto-attendant-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 기본 언어 설정 구성

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 수정하려는 UM 다이얼 플랜을 선택하고 도구 모음에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지의 **UM 자동 전화 교환**에서 변경할 UM 자동 전화 교환을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **일반** 페이지에 있는 **자동 음성 인터페이스 언어**의 드롭다운 목록에서 필요한 언어를 선택합니다.

5.  **저장**을 클릭하여 변경 내용을 적용합니다.

## 셸을 사용하여 기본 언어 설정 구성

이 예에서는 UM 자동 전화 교환 `MyUMAutoAttendant`의 기본 언어를 영어(영국)로 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language en-GB

이 예에서는 UM 자동 전화 교환 `MyUMAutoAttendant`의 기본 언어를 독일어로 설정합니다.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -Language de-DE

