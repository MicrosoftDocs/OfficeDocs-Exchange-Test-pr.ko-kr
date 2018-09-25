---
title: 'Outlook Web App의 최종 사용자가 POP3, IMAP4 및 SMTP 서버 설정을 볼 수 있음: Exchange 2013 Help'
TOCTitle: Outlook Web App의 최종 사용자가 POP3, IMAP4 및 SMTP 서버 설정을 볼 수 있음
ms:assetid: bd22bf7e-3bf7-45e6-8790-919b780166f6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg298947(v=EXCHG.150)
ms:contentKeyID: 50556075
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Outlook Web App의 최종 사용자가 POP3, IMAP4 및 SMTP 서버 설정을 볼 수 있음

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-28_

Microsoft Exchange Server 2013 사서함에 연결하는 데 POP3 또는 IMAP4를 사용하는 사용자는 올바른 서버 설정을 알아야만 이러한 사서함에 연결할 수 있습니다. 기본 Exchange 2013 설치가 끝난 후에는 사용자가 자신의 들어오는 POP3 또는 IMAP4 서버 설정이나 나가는 SMTP 서버 설정을 찾을 수 없습니다. 하지만 사용자가 MicrosoftOutlook Web App을 사용하여 자신의 설정을 찾을 수 있도록 Exchange를 구성할 수 있습니다.

이 절차를 수행하면 사용자가 다음과 같이 Outlook Web App에서 자신의 설정을 찾을 수 있습니다.

1.  Outlook Web App에서 **설정** \> **옵션**을 클릭합니다.

2.  **옵션**에서 **계정** \> **내 계정** \> **POP 또는 IMAP 액세스 설정**을 클릭합니다.

POP3 및 IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]  
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 POP3 및 IMAP4 사용자가 Outlook Web App에서 들어오는 POP3 및 IMAP4 설정을 볼 수 있도록 허용

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 설정" 및 "IMAP4 설정" 항목

이 예에서는 최종 사용자가 외부 POP3 서버 설정을 볼 수 있도록 허용합니다.

```powershell
Set-PopSettings -ExternalConnectionSettings {Dublin01.Contoso.com:995:SSL}
```

구문과 매개 변수에 대한 자세한 내용은 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

이 예에서는 최종 사용자가 외부 IMAP4 서버 설정을 볼 수 있도록 허용합니다.

```powershell
Set-ImapSettings -ExternalConnectionSettings {Dublin01.Contoso.com:993:SSL}
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\))를 참조하십시오.

이러한 변경 내용을 적용하려면 IIS를 다시 시작해야 합니다. POP3 서비스는 다시 시작할 필요가 없습니다. IIS를 다시 시작하려면 명령 프롬프트에서 다음을 입력합니다.

```powershell
iisreset
```

## 작동 여부는 어떻게 확인합니까?

Exchange에서 사용자가 POP3 서버 설정을 볼 수 있도록 구성되었는지 확인하려면

1.  셸에서 다음 명령을 실행합니다.
    
    ```powershell
    Get-PopSettings | format-list
    ```

2.  *ExternalConnectionSettings* 속성이 설정되었는지 확인합니다.

Exchange에서 사용자가 IMAP4 서버 설정을 볼 수 있도록 구성되었는지 확인하려면

1.  셸에서 다음 명령을 실행합니다.
    
    ```powershell
    Get-ImapSettings | format-list
    ```

2.  *ExternalConnectionSettings* 속성이 설정되었는지 확인합니다.

## 셸을 사용하여 POP3 및 IMAP4 사용자가 Outlook Web App에서 나가는 SMTP 설정을 볼 수 있도록 허용

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "수신 커넥터" 항목

이 예에서는 최종 사용자가 Outlook Web App을 사용하여 내부 및 외부 SMTP 서버 설정을 볼 수 있도록 허용합니다.

```powershell
Get-ReceiveConnector "*Client Frontend*" | Set-ReceiveConnector -Fqdn Server.Contoso.com -AdvertiseClientSettings $true 
```

구문과 매개 변수에 대한 자세한 내용은 [Set-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125140\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

Exchange에서 사용자가 SMTP 서버 설정을 볼 수 있도록 구성되었는지 확인하려면

1.  셸에서 다음 명령을 실행합니다.
    
    ```powershell
    Get-ReceiveConnector | format-list
    ```

2.  *AdvertiseClientSettings* 속성이 `true`로 설정되어 있으면 사용자가 Outlook Web App에서 SMTP 서버 설정을 볼 수 있습니다. *AdvertiseClientSettings*가 `false`로 설정되어 있으면 사용자가 Outlook Web App에서 SMTP 서버 설정을 볼 수 없습니다.

## 자세한 내용

최종 사용자가 POP3, IMAP4 및 SMTP 설정을 볼 수 있게 만든 후에 다음 작업을 수행할 수도 있습니다.

[사용 하도록 설정 하거나 사용자에 대 한 POP3 액세스를 사용 하지 않도록 설정](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

[사용 하도록 설정 하거나 사용자에 대 한 IMAP4 액세스를 사용 하지 않도록 설정](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

