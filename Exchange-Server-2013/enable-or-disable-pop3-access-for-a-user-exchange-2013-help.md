---
title: '사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정
ms:assetid: 57e12f07-3b14-45bd-9a82-e6032d14214f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb691018(v=EXCHG.150)
ms:contentKeyID: 50483158
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-01-06_

사용자에 대해 POP3를 사용하거나 사용하지 않도록 설정할 수 있습니다.


> [!NOTE]
> 사용자에 대해 POP3를 사용하거나 사용하지 않도록 설정한 후에는 Microsoft Exchange POP3 서비스 및 Microsoft Exchange POP3 Backend 서비스를 다시 시작해야 합니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">시작 및 POP3 서비스를 중지 합니다.</A>을 참조하십시오.



사용자 사서함을 관리하는 방법에 대한 자세한 내용은 [사용자 사서함 관리](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)를 참조하십시오.

POP3 및 IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 사용자에 대해 POP3를 사용하거나 사용하지 않도록 설정

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  결과 창에서 POP3를 사용하거나 사용하지 않도록 설정할 사용자를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **사용자 사서함** 대화 상자의 콘솔 트리에서 **사서함 기능**을 클릭합니다.
    
    결과 창의 **전자 메일 연결**에서 다음 중 하나를 수행하십시오.
    
      - 사용자에 대해 POP3를 사용하지 않도록 설정하려면 **POP3: 사용**에서 **사용 안 함**을 클릭합니다.
    
      - 사용자에 대해 POP3를 사용하도록 설정하려면 **POP3: 사용 안 함**에서 **사용**을 클릭합니다.

4.  **저장**을 클릭합니다.

## 셸을 사용하여 사용자에 대해 POP3를 사용하거나 사용하지 않도록 설정

이 예제에서는 사용자 John Smith에 대해 POP3를 사용하도록 설정합니다.

```powershell
Set-CASMailbox -Identity "John Smith" -POPEnabled $true
```

이 예제에서는 사용자 John Smith에 대해 POP3를 사용하지 않도록 설정합니다.

```powershell
Set-CASMailbox -Identity "John Smith" -POPEnabled $false
```

## 작동 여부는 어떻게 확인합니까?

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  결과 창에서 POP3를 사용하거나 사용하지 않도록 설정할 사용자를 선택하고 **편집**을 클릭합니다.

3.  **사용자 사서함** 대화 상자의 콘솔 트리에서 **사서함 기능**을 클릭합니다.
    
    결과 창에서 **전자 메일 연결** 아래 내용을 확인합니다.
    
      - 사용자에 대해 POP3를 사용하도록 설정되어 있는 경우 **POP3: 사용**으로 표시됩니다.
    
      - 사용자에 대해 POP3를 사용하지 않도록 설정되어 있는 경우 **POP3: 사용 안 함**으로 표시됩니다.

4.  **저장**을 클릭합니다.

