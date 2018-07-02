---
title: '활성화 또는 비활성화 하는 Outlook Voice Access에서 음성 메시지 보내기: Exchange 2013 Help'
TOCTitle: 활성화 또는 비활성화 하는 Outlook Voice Access에서 음성 메시지 보내기
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52057986
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 활성화 또는 비활성화 하는 Outlook Voice Access에서 음성 메시지 보내기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2012-12-13_

Outlook Voice Access 사용자가 같은 다이얼 플랜에 연결된 다른 UM 사용 가능 사용자에게 음성 메일 메시지를 보내도록 설정하거나 보내지 못하도록 설정할 수 있습니다.

기본적으로 이 설정은 사용하도록 설정되어 있습니다. 이 설정을 사용하지 않도록 설정하면 Outlook Voice Access 사용자에게 전화를 거는 Outlook Voice Access 사용자는 같은 다이얼 플랜 내 사용자에게 음성 메시지를 보낼 수 없습니다.

UM 다이얼 플랜과 관련된 추가 작업에 대한 자세한 내용은 [UM 다이얼 플랜 절차](um-dial-plan-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 다이얼 플랜" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Voice Access 사용자가 같은 다이얼 플랜의 사용자에게 음성 메시지를 보내도록 설정하거나 보내지 못하도록 설정

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다.

2.  목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 다이얼 플랜** 페이지에서 **구성**을 클릭합니다.

4.  음성 메시지를 보내도록 허용하려면 **전송 및 검색**의 **전화 건 사람이 다음을 수행하도록 허용**에서 **사용자 전화를 울리지 않고 음성 메시지 남기기**를 선택합니다. 사용자가 음성 메시지를 보내지 못하도록 하려면 이 설정을 선택 취소합니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 Outlook Voice Access 사용자가 같은 다이얼 플랜의 사용자에게 음성 메시지를 보내도록 설정하거나 보내지 못하도록 설정

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜에 연결된 Outlook Voice Access 사용자가 같은 다이얼 플랜에 연결된 사용자에게 음성 메시지를 보낼 수 있도록 설정합니다.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

이 예에서는 `MyUMDialPlan`이라는 UM 다이얼 플랜에 연결된 Outlook Voice Access 사용자가 같은 다이얼 플랜에 연결된 사용자에게 음성 메시지를 보내지 못하도록 설정합니다.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

