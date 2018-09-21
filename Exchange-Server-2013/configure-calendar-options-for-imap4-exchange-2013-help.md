---
title: 'IMAP4에 대 한 일정 옵션 구성: Exchange 2013 Help'
TOCTitle: IMAP4에 대 한 일정 옵션 구성
ms:assetid: 6679c8b2-3f0f-449a-a17c-a7b30001538c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998606(v=EXCHG.150)
ms:contentKeyID: 50556002
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IMAP4에 대 한 일정 옵션 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-27_

IMAP4 연결을 사용하여 사서함에 연결하는 사용자에 대해 셸에서 일정 관리 액세스 설정을 구성할 수 있습니다. 지정한 설정에 따라 IMAP4 사용자가 일정에 액세스하고 다른 사용자와 일정 정보를 교환(예: 모임 요청 보내기 또는 응답)하는 방법이 결정됩니다.

IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 "IMAP4 설정" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 IMAP4의 일정 옵션 설정

이 예에서는 IMAP4 사용자가 일정 정보 교환 표준인 iCalendar 표준을 사용하도록 설정합니다.

```powershell
Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

이 예에서는 IMAP4 사용자가 내부 서버를 통해 일정 정보에 액세스하도록 설정합니다.

    Set-ImapSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 

이 예에서는 IMAP4 사용자가 외부 서버에서 인터넷을 통해 일정 정보에 액세스하도록 설정합니다.

```powershell
Set-ImapSettings -CalendarItemRetrievalOption InternetUrl
```

이 예에서는 IMAP4 사용자가 직접 Outlook Web App URL을 사용하여 일정 정보에 액세스하도록 설정합니다. `Custom`을 사용 중인 경우 *OWAServerUrl* 매개 변수를 사용하여 Outlook Web App URL을 지정해야 합니다.

```powershell
Set-Imap4Settings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

IMAP4의 일정 옵션을 지정한 후에는 IMAP4 서비스를 다시 시작해야 합니다. IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md)를 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

일정 옵션이 성공적으로 설정되었는지 확인하려면 다음을 수행하십시오.

셸에서 다음 명령을 실행합니다.

```powershell
Get-ImapSettings | format-list
```

일정 설정이 올바른지 확인합니다.

## 자세한 내용

IMAP4의 일정 옵션을 설정했으면 다음을 수행할 수 있습니다.

[POP3 및 IMAP4 메시지 검색 형식 옵션 구성](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[IMAP4에 대 한 연결 시간 제한 설정](set-connection-time-out-limits-for-imap4-exchange-2013-help.md)

