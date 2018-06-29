---
title: '때 PIN을 다시 설정 하는 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.: Exchange 2013 Help'
TOCTitle: 때 PIN을 다시 설정 하는 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51407769
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 때 PIN을 다시 설정 하는 전송 되는 전자 메일 메시지와 텍스트를 포함 합니다.

 

_**적용 대상:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:**2013-02-22_

해당 UM (통합 메시징) 또는 음성 메일 PIN 다시 설정 하는 경우 사용자에 게 전송 된 전자 메일 메시지에 추가 텍스트를 포함할 수 있습니다. UM 사서함 정책에 대 **한 사용자의 Outlook Voice Access PIN 다시 설정 하는 경우** 상자에 사용자 지정 텍스트를 입력 하 여이 작업을 수행 합니다. 사용자 지정 된 텍스트를 포함할 수 등 UM 사용이 가능한 사용자에 대 한 보안 관련 정보입니다.

기본적으로 Outlook Voice Access에 사용 되는 PIN 실패 한 로그인 시도 수가 5를 초과 하는 경우에 통합 메시징 또는 음성 메일 시스템에 의해 재설정 됩니다. 사용자가 Outlook Web App 또는 Outlook 2010에 포함 하거나 또는 나중에 Outlook Voice Access는 전화를 통해를 사용 하 여 UM 기능을 사용 하 여 자신의 Pin 다시 설정할 수도 있습니다.


> [!NOTE]
> 이 상자에 입력 하 고 텍스트 512 자로 제한 됩니다와 간단한 HTML 텍스트를 포함할 수 있습니다.



Outlook Voice Access PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 자신의 PIN 다시 설정 하는 경우 사용자에 게 보내는 전자 메일 메시지에 텍스트를 추가 하려면

1.  EAC에서 **통합 메시징** \> **UM 다이얼 플랜**으로 이동합니다. 목록 보기에서 변경하려는 UM 다이얼 플랜을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

2.  **UM 다이얼 플랜** 페이지의 **UM 사서함 정책**에서 관리할 UM 사서함 정책을 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **UM 사서함 정책** 페이지에서 \> **메시지 텍스트** 를 **사용자의 Outlook Voice Access PIN 다시 설정 하는 경우** 를 실행 하는 것에 대 한 텍스트 상자에서 사용자의 PIN을 다시 설정 하는 경우 전송 된 전자 메일 메시지에 포함 하려는 텍스트를 입력 합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용 하 여 자신의 PIN 다시 설정 하는 경우 사용자에 게 보내는 전자 메일 메시지에 텍스트를 추가 하려면

이 예제에서는 포함 추가 텍스트, "다른 사용자와 PIN를 공유지 않습니다. 발생할 수 있으므로 징계 조치에 ", 전자 메일 메시지에서 자신의 PIN 다시 설정 하는 경우에 연결 된 UM 사서함 정책 `MyUMMailboxPolicy` 인 사용자에 게 전송 합니다.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

