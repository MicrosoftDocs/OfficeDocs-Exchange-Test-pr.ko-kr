---
title: '음성 메일 PIN 다시 설정: Exchange 2013 Help'
TOCTitle: 음성 메일 PIN 다시 설정
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50556076
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: MT
---

# 음성 메일 PIN 다시 설정

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-02-22_

UM(통합 메시징) 사용 가능 음성 메일 사용자가 올바르지 않은 PIN을 여러 번 사용하여 로그인을 시도함으로써 Outlook Voice Access를 사용하는 자신의 사서함을 잠근 경우 또는 자신의 PIN을 잊어버린 경우에는 다음 절차 중 하나를 사용하여 사용자의 PIN을 다시 설정할 수 있습니다. 사용자의 Outlook Voice Access PIN을 다시 설정할 때 PIN이 자동 생성되도록 UM을 구성하거나 수동으로 PIN을 지정할 수 있습니다. 새 PIN은 전자 메일로 사용자에게 보내집니다. 처음 로그인 시 PIN 다시 설정과 같은 추가 PIN 옵션을 지정할 수 있습니다.사용자는 PIN Outlook 또는 Outlook Web App을 사용하여도 UM PIN을 다시 설정할 수 있습니다..


> [!NOTE]
> UM 사용 가능 사서함에 액세스하려면 Outlook Voice Access 사용자는 DTMF(복합 주파수 부호)라고 하는 터치톤 입력을 사용해야 합니다. 음성 인식은 PIN 입력에 사용할 수 없습니다.



Outlook Voice Access PIN 보안과 관련된 추가 작업에 대한 자세한 내용은 [PIN 보안 절차](pin-security-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분 미만.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 통합 메시징 PIN 다시 설정

1.  EAC에서 **받는 사람**으로 이동합니다. 목록 보기에서 보려는 사용자 사서함을 선택합니다.

2.  세부 정보 창의 **전화 및 음성 기능** 아래 **통합 메시징** 아래에서 **자세히 보기**를 클릭합니다.

3.  **UM 사서함** 페이지의 **UM 사서함 설정** 아래에서 **PIN 다시 설정**을 클릭합니다.

4.  **UM 사서함 PIN 다시 설정** 페이지에서 다음 옵션을 사용해 UM 사용 가능 사용자의 PIN을 다시 설정합니다.
    
      - **자동으로 PIN 생성**   사용자가 Outlook Voice Access를 사용하는 자신의 사서함에 액세스하기 위해 사용하는 PIN을 자동으로 생성하려면 이 옵션을 사용합니다. 기본적으로 이 설정은 사용하도록 설정되어 있습니다.
        
        자동으로 생성된 PIN은 사용자의 사서함에 전자 메일 메시지로 보내집니다. PIN을 받아 해당 사서함에 로그인하면 PIN을 사용자와 더 친숙한 PIN으로 변경하라는 메시지가 사용자에게 표시됩니다.
        
        Outlook Web App 및 Microsoft Outlook에서도 사용자는 PIN을 다시 설정할 수 있습니다. PIN은 사용자의 사서함과 연결된 UM 사서함 정책에서 구성된 PIN 정책을 기반으로 자동 생성됩니다. Outlook Voice Access 사용자의 PIN은 자동으로 생성하는 것이 좋습니다.
    
      - **PIN 입력**   Outlook Voice Access 사용자에 대한 PIN을 수동으로 지정하려면 이 옵션을 사용합니다. 기본적으로 이 설정은 사용하지 않도록 설정됩니다.
        
        사용자에 대한 PIN을 지정하면 해당 PIN은 사용자의 사서함에 전자 메일 메시지로 보내집니다. PIN을 받아 해당 사서함에 로그인한 후에 Outlook Voice Access에서 개인 옵션을 구성하여 PIN을 변경할 수 있습니다. 하지만 Outlook Web App 및 Microsoft Outlook에는 수동으로 PIN을 지정하는 옵션이 없습니다.
    
      - **사용자에게 처음 로그인할 때 PIN 다시 설정 요구**   사용자가 Outlook Voice Access에 처음 로그인할 때 PIN을 다시 설정하도록 하려면 이 옵션을 사용합니다. 기본적으로 이 옵션은 사용하도록 설정되어 있습니다.
        
        사용자의 PIN을 자동으로 생성하는 옵션을 선택하면 이 옵션을 사용하여 사용자가 Outlook Voice Access에 처음 로그인할 때 PIN을 변경하도록 할 수 있습니다. 이는 사용자의 PIN을 보호하는 데 도움이 됩니다.

5.  **저장**을 클릭합니다.

## 셸을 사용하여 통합 메시징 PIN 다시 설정

이 예에서는 Tony Smith에 대한 음성 사서함 PIN을 1985848로 다시 설정합니다. 사용자는 Outlook Voice Access에 처음 로그인할 때 이 PIN을 변경해야 합니다.

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

