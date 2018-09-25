---
title: 'P o p 3에 대 한 일정 옵션 구성: Exchange 2013 Help'
TOCTitle: P o p 3에 대 한 일정 옵션 구성
ms:assetid: ac3d60a0-8697-4c06-9e93-f8d2c4b157b6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124133(v=EXCHG.150)
ms:contentKeyID: 50556061
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# P o p 3에 대 한 일정 옵션 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-27_

셸을 사용하여 POP3 연결을 통해 사서함에 연결하는 사용자에 대한 일정 액세스 설정을 구성할 수 있습니다. 지정한 설정에 따라 POP3 사용자가 자신의 일정에 액세스하고 다른 사용자와 일정 정보를 교환(예: 모임 요청 보내기 또는 모임 요청에 응답)하는 방법이 결정됩니다.

POP3에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 설정" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 POP3 일정 옵션 설정

이 예에서는 POP3 사용자가 일정 정보 교환을 위한 표준인 iCalendar 표준을 사용할 수 있도록 설정합니다.

```powershell
Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption iCalendar
```

이 예에서는 POP3 사용자가 내부 서버의 일정 정보에 액세스할 수 있도록 설정합니다.

```powershell
Set-PopSettings -Identity CAS01 -CalendarItemRetrievalOption IntranetUrl 
```
이 예에서는 POP3 사용자에게 외부 서버의 인터넷에서 일정 정보에 액세스하도록 허용합니다.

```powershell
Set-PopSettings -CalendarItemRetrievalOption InternetUrl
```

이 예에서는 POP3 사용자가 직접 Outlook Web App URL을 사용하여 일정 정보에 액세스할 수 있도록 설정합니다. `Custom`을 사용할 경우 *OWAServerUrl* 매개 변수를 사용하여 Outlook Web App URL을 지정해야 합니다.

```powershell
Set-PopSettings -CalendarItemRetrievalOption Custom -OwaServerUrl "https://OwaServer01"
```

POP3에 대한 일정 옵션을 지정한 후에는 POP3 서비스를 다시 시작해야 합니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md) 항목을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

일정 옵션이 설정되었는지 확인하려면 다음을 수행합니다.

셸에서 다음 명령을 실행합니다.

```powershell
Get-PopSettings | format-list
```

일정 설정이 올바른지 확인합니다.

## 자세한 내용

POP3에 대한 일정 옵션을 설정한 후 다음 작업을 수행할 수도 있습니다.

[POP3 및 IMAP4 메시지 검색 형식 옵션 구성](configure-pop3-and-imap4-message-retrieval-format-options-exchange-2013-help.md)

[P o p 3에 대 한 연결 시간 제한 설정](set-connection-time-out-limits-for-pop3-exchange-2013-help.md)

