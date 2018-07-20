---
title: '사서함에 대 한 Outlook Web App를 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 Outlook Web App를 사용 하지 않도록 설정 하거나 사용
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50556057
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 Outlook Web App를 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-14_

EAC 또는 셸을 사용하여 사용자 사서함에 대해 Outlook Web App을 사용하거나 사용하지 않도록 설정할 수 있습니다. Outlook Web App을 사용하도록 설정하면 사용자는 Outlook Web App을 사용하여 전자 메일을 보내고 받을 수 있습니다. Outlook Web App을 사용하지 않도록 설정하면 사서함에서 계속 전자 메일 메시지를 받게 되고 사용자는 Microsoft Outlook 같은 MAPI 클라이언트나 POP 또는 IMAP 전자 메일 클라이언트를 통해 사서함에 액세스하여 전자 메일을 보내고 받을 수 있습니다(해당 클라이언트의 액세스를 지원하도록 사서함이 설정된 경우).


> [!NOTE]
> Outlook Web App과 MAPI, POP3 및 IMAP4 전자 메일 클라이언트에 대한 지원은 사용자 사서함이 만들어질 때 기본적으로 설정됩니다.



전자 메일 클라이언트에서의 사서함 액세스를 관리하는 데 관련된 추가 관리 작업에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [사서함에 대 한 MAPI를 사용 하지 않도록 설정 하거나 사용](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [사용 하도록 설정 하거나 사용자에 대 한 IMAP4 액세스를 사용 하지 않도록 설정](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "클라이언트 액세스 사용자 설정" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 Outlook Web App을 사용하거나 사용하지 않도록 설정

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 Outlook Web App을 사용하거나 사용하지 않도록 설정할 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **전자 메일 연결**에서 다음 중 하나를 수행합니다.
    
      - Outlook Web App을 사용하지 않도록 설정하려면 **Outlook Web App: 사용**에서 **사용 안 함**을 클릭합니다.
        
        Outlook Web App을 사용하지 않도록 설정할 것인지 묻는 경고 메시지가 표시됩니다. **예**를 클릭합니다.
    
      - Outlook Web App을 사용할 수 있도록 설정하려면 **Outlook Web App: 사용 안 함**에서 **사용**을 클릭합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.


> [!NOTE]
> EAC의 대량 편집 기능을 사용하면 여러 사용자 사서함에 대해 Outlook Web App을 사용하거나 사용하지 않도록 설정할 수 있습니다. 이 작업을 수행하는 방법에 대한 자세한 내용은 <A href="manage-user-mailboxes-exchange-2013-help.md">사용자 사서함 관리</A> 항목의 "사용자 사서함 대량 편집" 섹션을 참조하십시오.



## 셸을 사용하여 Outlook Web App을 사용하거나 사용하지 않도록 설정

이 예에서는 Yan Li의 사서함에 대해 Outlook Web App을 사용하지 않도록 설정합니다.

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

이 예에서는 Elly Nkya의 사서함에 대해 Outlook Web App을 사용하도록 설정합니다.

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용자 사서함에 대해 Outlook Web App을 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

  - 사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

  - **전자 메일 연결**에서 Outlook Web App의 사용 여부 설정을 확인합니다.

또는

  - 셸에서 다음 명령을 실행합니다.
    
        Get-CASMailbox <identity>
    
    Outlook Web App을 사용하도록 설정되었으면 *OWAEnabled* 속성 값이 `True`이고, Outlook Web App을 사용하지 않도록 설정되었으면 이 값이 `False`입니다.

