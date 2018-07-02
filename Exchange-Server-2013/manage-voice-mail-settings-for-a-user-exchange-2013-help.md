---
title: '사용자에 대 한 음성 메일 설정 관리: Exchange 2013 Help'
TOCTitle: 사용자에 대 한 음성 메일 설정 관리
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 50483424
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용자에 대 한 음성 메일 설정 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

UM(통합 메시징)과 음성 메일 기능 및 UM과 음성 메일을 사용하도록 설정한 사용자의 구성 설정을 보거나 설정할 수 있습니다. 예를 들어 다음을 수행할 수 있습니다.

  - Outlook Voice Access PIN 다시 설정

  - 개인 교환원 내선 번호 추가

  - 다른 내선 번호 추가

  - ASR(자동 음성 인식)을 사용하거나 사용하지 않도록 설정

  - 전화 응답 규칙을 사용하거나 사용하지 않도록 설정

  - 전자 메일 또는 일정에 대한 액세스를 사용하거나 사용하지 않도록 설정


> [!NOTE]
> 일부 설정 및 기능은 셸을 사용해야만 구성할 수 있습니다.



음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 기존 사용자가 현재 통합 메시징에 사용하도록 설정되어 있는지 확인합니다. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 UM 사용 가능 사용자의 속성 보기 또는 구성

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 UM 사서함 정책을 변경할 사서함을 선택합니다.

3.  세부 정보 창의 **전화 및 음성 기능** \> **통합 메시징**에서 **세부 정보 보기**를 클릭합니다.

4.  **UM 사서함** 페이지에서 **UM 사서함 설정**을 클릭하여 기존 UM 사용 가능 사용자의 다음 UM 속성을 보거나 변경합니다.
    
      - **PIN 상태**   이 표시 전용 필드에는 사용자 사서함의 상태가 표시됩니다. 기본적으로 사용자가 UM을 사용하면 PIN 상태가 **잠겨 있지 않음**으로 표시됩니다. 그러나 사용자가 잘못된 Outlook Voice Access PIN을 여러 번 입력하면 상태가 **잠겨 있음**으로 표시됩니다.
    
      - **UM 사서함 정책**   이 상자에는 UM 사용 가능 사용자와 연결되는 UM 사서함 정책의 이름이 표시됩니다. **찾아보기**를 클릭하여 이 UM 사서함과 연결되는 UM 사서함 정책을 찾아서 지정할 수 있습니다.
    
      - **개인 교환원 내선 번호**   사용자의 교환원 내선 번호를 지정하려면 이 상자를 사용합니다. 기본적으로 내선 번호는 구성되지 않습니다. 내선 번호는 1~20자까지 사용할 수 있습니다. UM 사용 가능 사용자에 대한 수신 전화를 이 상자에 지정하는 내선 번호로 전달할 수 있습니다.
        
        다이얼 플랜과 자동 전화 교환에서 다른 유형의 교환원 내선 번호를 구성할 수 있습니다. 그러나 해당 내선 번호는 일반적으로 회사 전체의 접수원이나 교환원에게 의미가 있습니다. 개인 교환원 내선 번호 설정은 특정 사용자가 응답하기 전에 관리자의 비서나 개인 비서가 수신되는 호출에 응답할 때 사용될 수 있습니다.

5.  **UM 사서함** 페이지의 **다른 내선 번호**에서 사용자의 내선 번호를 추가, 변경 및 확인할 수 있습니다.
    
      - 내선 번호를 추가하려면 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. **다른 내선 번호 추가** 페이지에서 **찾아보기**를 통해 UM 다이얼 플랜을 선택하고 **내선 번호** 상자에 내선 번호를 입력합니다.
    
      - 내선 번호를 제거하려면 제거할 내선 번호를 선택하고 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭합니다.

6.  변경한 내용이 있으면 **저장**을 클릭합니다.

## 셸을 사용하여 UM 사용 가능 사용자의 기능 구성

이 예에서는 전화에서 재생 및 부재 중 전화 알림을 사용하지 않도록 설정하지만 SMS(문자 메시지) 알림은 사용하도록 설정합니다.


> [!NOTE]
> 온-프레미스 및 하이브리드 배포의 경우 통합 메시징 및 Lync Server를 통합하면 Exchange 2007 또는 Exchange 2010 사서함 서버에 사서함이 있는 사용자는 부재 중 전화 알림을 사용할 수 없습니다. 부재 중 전화 알림은 전화가 사서함 서버에 전송되기 전에 사용자의 연결이 끊기는 경우 생성됩니다.



    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

이 예에서는 사용자가 Outlook Voice Access를 사용할 때 사용자의 일정 액세스를 차단하지만 전자 메일 액세스는 가능하도록 설정합니다.

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

이 예에서는 사용자가 Outlook Voice Access를 사용할 때 일정 및 전자 메일에 대한 액세스를 차단합니다.

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

이 예에서는 사용자가 전화 응답 규칙 만들기, 수신 팩스 받기 및 Outlook Voice Access를 차단하지만 ASR(자동 음성 인식)은 가능하도록 설정합니다.

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## 셸을 사용하여 UM 사용 가능 사용자의 속성 보기

이 예에서는 포리스트에서 UM 사용이 가능한 모든 사서함 목록을 서식 있는 목록으로 표시합니다.

    Get-UMMailbox | Format-List

이 예에서는 tonysmith@contoso.com의 UM 사서함 속성을 표시합니다.

    Get-UMMailbox -Identity tonysmith@contoso.com


> [!IMPORTANT]
> Exchange 2007 및 Exchange 2013을 실행 중이고 사용자의 사서함이 Exchange 2007 사서함 서버에 있는 경우 <STRONG>Get-UMMailbox</STRONG> cmdlet을 실행해도 제대로 작동하지 않습니다. 이 문제를 해결하려면 Exchange 2007 서버나 Exchange 2007 관리 도구를 실행 중인 컴퓨터에서 <STRONG>Get-UMMailbox</STRONG> cmdlet을 실행합니다.


