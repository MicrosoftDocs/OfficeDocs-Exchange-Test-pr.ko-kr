---
title: '음성 메일에 대 한 사용자를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 음성 메일에 대 한 사용자를 사용 하도록 설정
ms:assetid: ad027767-5e14-4cb1-9f8a-0791d9188db5
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124147(v=EXCHG.150)
ms:contentKeyID: 50483920
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.EnableUnifiedMessagingWizardForm.EnableUnifiedMessagingWizardPage
ms.translationtype: MT
---

# 음성 메일에 대 한 사용자를 사용 하도록 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

사용자가 UM(통합 메시징)을 사용하도록 설정하면 해당 사용자에게 기본 속성 집합이 적용되고 사용자는 통합 메시징에 포함된 음성 메일 기능을 사용할 수 있습니다. 사용자가 음성 메일을 사용하도록 설정한 후 SIP URI 다이얼 플랜에 연결된 UM 사서함 정책에 해당 사용자가 할당되면 사용자에 대한 SIP(Session Initiation Protocol) 주소를 추가할 수 있습니다. 또는 E.164 다이얼 플랜에 연결된 UM 사서함 정책에 해당 사용자가 할당되면 사용자에 대한 E.164 번호를 추가할 수 있습니다. 두 경우 모두 사용자에게 구성된 내선 번호가 있어야 합니다.

내선 번호는 내선 번호, SIP URI(Uniform Resource Identifier) 또는 E.164 다이얼 플랜과 연결된 각 사용자에게 필요합니다. 내선 번호는 UM 사서함 정책에 대한 UM 다이얼 플랜에 지정된 대로 올바른 자릿수로 구성되어야 합니다.


> [!NOTE]
> UM 사용 가능 사용자가 SIP URI 또는 E.164 다이얼 플랜에 연결된 경우에도 EAC 또는 셸을 사용하여 UM 사용 가능 모든 사용자에 대해 내선 번호를 추가, 제거 또는 수정해야 합니다. 사용자에 대한 SIP 주소 또는 E.164 번호를 추가, 제거 또는 수정하려면 EAC에서는 이러한 옵션을 사용할 수 없으므로 셸을 사용해야 합니다.



음성 메일을 사용하도록 설정된 사용자와 관련된 추가 관리 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)을 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자가 음성 메일을 사용하도록 설정

1.  EAC에서 **받는 사람**을 클릭합니다.

2.  목록 보기에서 통합 메시징을 사용하도록 설정할 사서함의 사용자를 선택합니다.

3.  세부 정보 창의 **전화 및 음성 기능**에서 **사용**을 클릭합니다.

4.  **UM 사서함 사용** 페이지에서 **UM 사서함 정책** 옆에 있는 **찾아보기** 단추를 클릭하고 목록에서 사용자를 할당할 UM 사서함 정책을 찾은 다음 **확인**을 클릭합니다.

5.  **UM 사서함 사용** 페이지에서 다음 상자에 해당 정보를 입력합니다.
    
      - **SIP 주소** 또는 **E.164 번호**   **SIP 주소** 또는 **E.164 번호** 텍스트 상자에 사용자의 SIP 주소 또는 E.164 번호를 입력합니다. 통합 메시징을 사용할 수 있도록 설정한 사용자가 SIP URI 또는 E.164 다이얼 플랜에 연결된 UM 사서함 정책에 할당된 경우 이 옵션을 사용할 수 있습니다. 사용자가 내선 번호 다이얼 플랜에 연결되어 있으면 사용자의 SIP 주소 또는 E.164 번호를 추가할 수 없습니다.
        
        SIP URI 또는 E.164 다이얼 플랜에 연결된 UM 사서함 정책에 사용자를 할당할 때는 사용자의 내선 번호를 입력해야 합니다. 사용자는 Outlook Voice Access를 통해 사서함에 액세스할 때 이 내선 번호를 사용합니다. 이 상자에서 구성하는 자릿수는 SIP URI 또는 E.164 다이얼 플랜에 구성된 자릿수와 일치해야 합니다.
    
      - **내선 번호**   이 텍스트 상자에 UM을 사용하도록 설정 중인 사용자의 내선 번호를 직접 입력합니다.
        
        사용자에 대한 올바른 내선 번호를 입력하고, 다이얼 플랜에 지정된 자릿수와 일치하도록 해야 합니다. 1자리~20자리까지만 입력할 수 있습니다. 일반적인 내선 번호의 길이는 3~7자리입니다. 내선 번호의 자릿수는 사용자에게 할당된 UM 사서함 정책에 연결된 다이얼 플랜에서 설정됩니다.
    
      - **PIN 설정**에서 다음 상자에 해당 정보를 입력합니다.
        
          - **PIN 자동 생성**   UM 사용 가능 사용자가 Outlook Voice Access를 통한 음성 메일 액세스에 사용할 PIN을 자동으로 생성하려면 이 단추를 클릭합니다. 기본 설정입니다. 사용자에게 할당된 UM 사서함 정책에 구성된 PIN 정책을 기반으로 PIN이 자동으로 생성됩니다. 이 설정을 사용하면 사용자의 PIN을 보호하는 데 도움이 됩니다. PIN은 사용자가 UM을 사용하도록 설정된 이후에 받는 환영 메시지를 통해 전송됩니다. 기본적으로는 음성 메일을 받기 위해 사서함에 처음 로그인할 때 이 PIN을 변경해야 합니다.
        
          - **PIN 입력**   사용자가 음성 메일 시스템에 액세스하는 데 사용할 PIN을 입력하려면 이 단추를 클릭합니다. PIN은 이 UM 사용 가능 사용자와 연결된 UM 사서함 정책에 구성된 PIN 정책 설정을 따라야 합니다. 예를 들어, 7자릿수 이상의 PIN만 받도록 UM 사서함 정책을 구성한 경우에는 이 입력란에 입력하는 PIN의 길이가 7자릿수 이상이어야 합니다.
        
          - **사용자에게 처음 로그인할 때 PIN 다시 설정 요구**   사용자가 Outlook Voice Access를 사용하여 전화로 음성 메일 시스템에 처음으로 액세스할 때 음성 메일 PIN을 강제로 다시 설정하게 하려면 이 확인란을 선택합니다. 기억하기 좋은 PIN을 입력하라는 메시지가 표시됩니다. UM을 사용할 수 있는 사용자가 처음 로그인할 때 강제로 PIN을 변경하도록 하여 데이터 및 받은 편지함에 대한 무단 액세스로부터 보호하는 가장 좋은 보안 방법입니다. 이 확인란은 기본적으로 선택되어 있습니다.

6.  **UM 사서함 사용** 페이지에서 설정을 검토합니다. 사용자가 음성 메일을 사용하도록 설정하려면 **마침**을 클릭합니다. 구성을 변경하려면 **뒤로**를 클릭합니다.

## 셸을 사용하여 사용자가 음성 메일을 사용하도록 설정

다음 예에서는 tonysmith@contoso.com의 사서함에서 통합 메시징을 사용하도록 설정하고, 내선 번호를 51234로 설정하고, 사용자의 PIN을 5643892로 설정하고, 사용자를 `MyUMMailboxPolicy`라는 UM 사서함 정책에 할당합니다.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -PINExpired $true

다음 예에서는 tonysmith@contoso.com의 사서함에서 통합 메시징을 사용하도록 설정하고, 사용자를 `MyUMMailboxPolicy`라는 UM 사서함 정책에 할당하고, 사용자에 대한 내선 번호, SIP 주소 및 PIN을 설정합니다.

    Enable-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy -Extensions 51234 -PIN 5643892 -SIPResourceIdentifier "tonysmith@contoso.com" -PINExpired $true

