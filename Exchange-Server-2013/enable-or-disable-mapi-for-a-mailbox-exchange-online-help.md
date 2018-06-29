---
title: '사서함에 대 한 MAPI를 사용 하지 않도록 설정 하거나 사용: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 MAPI를 사용 하지 않도록 설정 하거나 사용
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50556079
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 MAPI를 사용 하지 않도록 설정 하거나 사용

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2017-12-31_

사용자 사서함에 대 한 MAPI를 사용할지 여부를 Exchange 관리 센터 또는 Exchange 관리 셸 를 사용할 수 있습니다. MAPI를 사용 하는 경우 Outlook 또는 다른 MAPI 전자 메일 클라이언트에서 사용자의 사서함에 액세스할 수 있습니다. MAPI를 사용 하지 않도록 설정 하는 경우에 Outlook 또는 다른 MAPI 클라이언트에서 액세스할 수 없습니다. 그러나 전자 메일 메시지를 받을 계속 사서함 및 사용자 Outlook Web App, POP 전자 메일 클라이언트를 또는 IMAP 클라이언트를 사용 하 여 전자 메일을 송수신 하는 사서함에 액세스할 수에 대 한 액세스를 지원 하기 위해 해당 클라이언트에서 사서함을 사용 합니다.


> [!NOTE]
> Outlook Web App과 MAPI, POP3 및 IMAP4 전자 메일 클라이언트에 대한 지원은 사용자 사서함이 만들어질 때 기본적으로 설정됩니다.



전자 메일 클라이언트에서의 사서함 액세스를 관리하는 데 관련된 추가 관리 작업에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [사서함에 대 한 Outlook Web App를 사용 하지 않도록 설정 하거나 사용](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [사용 하도록 설정 하거나 사용자에 대 한 IMAP4 액세스를 사용 하지 않도록 설정](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "클라이언트 액세스 사용자 설정" 항목.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 MAPI를 사용하도록 또는 사용하지 않도록 설정

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 MAPI를 사용하도록 또는 사용하지 않도록 설정할 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **전자 메일 연결** 아래에서 다음 작업 중 하나를 수행합니다.
    
      - MAPI를 사용하지 않도록 설정하려면 **MAPI: 사용**에서 **사용 안 함**을 클릭합니다.
        
        MAPI를 사용하지 않도록 설정할 것인지 묻는 경고 메시지가 표시됩니다. **예**를 클릭합니다.
    
      - MAPI를 사용하도록 설정하려면 **MAPI: 사용 안 함**에서 **사용**을 클릭합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## Exchange 관리 셸을 사용 하 여 하거나 MAPI를 사용 하지 않도록 설정

이 예에서는 Ken Sanchez의 사서함에 대해 MAPI를 사용하지 않도록 설정합니다.

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

이 예에서는 Esther Valle의 사서함에 대해 MAPI를 사용하도록 설정합니다.

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-CASMailbox](https://technet.microsoft.com/ko-kr/library/bb125264\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

MAPI를 사용하도록 또는 사용하지 않도록 설정했는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동하여 사서함을 클릭한 후 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

  - 사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

  - **전자 메일 연결** 아래에서 MAPI가 사용하도록 또는 사용하지 않도록 설정되었는지 확인합니다.

또는

  - Exchange 관리 셸 에서 다음 명령을 실행 합니다.
    
        Get-CASMailbox <identity>
    
    MAPI가 사용하도록 설정되어 있을 경우 *MapiEnabled* 속성의 값은 `True`입니다. MAPI가 사용하지 않도록 설정되어 있을 경우 값은 `False`입니다.

