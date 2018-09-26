---
title: 'POP3 및 IMAP4 프로토콜 로깅 구성: Exchange 2013 Help'
TOCTitle: POP3 및 IMAP4 프로토콜 로깅 구성
ms:assetid: 451b337b-cb6b-4460-8687-be0b19c469bc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997690(v=EXCHG.150)
ms:contentKeyID: 50555981
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# POP3 및 IMAP4 프로토콜 로깅 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-11-27_

셸을 사용하여 POP3 및 IMAP4에 대한 프로토콜 로깅 설정을 사용하거나, 사용하지 않거나, 수정할 수 있습니다. 기본적으로 프로토콜 로깅은 사용할 수 없도록 설정되어 있습니다.

프로토콜 로깅을 사용하면 Exchange 환경의 POP3 및 IMAP4 연결을 검토할 수 있습니다. POP3 또는 IMAP4 성능 관련 문제를 해결하는 경우에 유용합니다. 자세한 내용은 [POP3 및 IMAP4 프로토콜 로깅](protocol-logging-for-pop3-and-imap4-exchange-2013-help.md)을 참조하십시오. POP3 및 IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md)의 \&quot;POP3 설정\&quot; 및 \&quot;IMAP4 설정\&quot; 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 POP3 또는 IMAP4에 대한 프로토콜 로깅 사용 설정

이 예에서는 클라이언트 액세스 서버 CAS01에서 IMAP4 또는 POP3에 대한 프로토콜 로깅을 사용 설정합니다.

```powershell
Set-ImapSettings -Server "CAS01" -ProtocolLogEnabled $true
Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true
```


> [!NOTE]
> POP3 또는 IMAP4에 대한 프로토콜 로깅 설정을 변경한 후에는 POP3 또는 IMAP4 서비스 중에서 사용할 서비스를 다시 시작해야 합니다. POP3 및 IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">시작 및 POP3 서비스를 중지 합니다.</A> 및 <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">시작 및 IMAP4 서비스를 중지 합니다.</A>을 참조하십시오.



구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\)) 및 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 POP3 또는 IMAP4에 대한 프로토콜 로깅을 사용하지 않도록 설정

이 예에서는 클라이언트 서버 CAS01에서 IMAP4 또는 POP3에 대한 프로토콜 로깅을 사용하지 않도록 설정합니다.

```powershell
Set-ImapSettings -Server "CAS01" -protocolLogEnabled $false
Set-PopSettings -Server "CAS01" -protocolLogEnabled $false
```


> [!NOTE]
> POP3 또는 IMAP4에 대한 프로토콜 로깅 설정을 변경한 후에는 POP3 또는 IMAP4 서비스 중에서 사용할 서비스를 다시 시작해야 합니다. POP3 및 IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">시작 및 POP3 서비스를 중지 합니다.</A> 및 <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">시작 및 IMAP4 서비스를 중지 합니다.</A>을 참조하십시오.



구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\)) 및 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))을 참조하십시오.

## 셸을 사용하여 POP3 또는 IMAP4에 대한 프로토콜 로깅 수정

POP3 또는 IMAP4 로깅 설정을 수정하려면 다음 매개 변수를 하나 이상 사용하여 **Set-ImapSettings** 또는 **Set-PopSettings** cmdlet을 실행합니다.

  - *LogFileLocation* 이 매개 변수는 POP3 또는 IMAP4 프로토콜 로그 파일의 위치를 지정합니다. 기본적으로 POP3 프로토콜 로그 파일은 C:\\Program Files\\Microsoft\\Exchange Server\\V15\\Logging\\Pop3 디렉터리에 있습니다. 이 예는 클라이언트 액세스 서버 CAS01에서 POP3 프로토콜 로깅을 설정합니다. 또한 POP3 프로토콜 로깅 디렉터리를 C:\\Pop3Logging으로 변경합니다.
    
    ```powershell
    Set-PopSettings -Server "CAS01" -ProtocolLogEnabled $true -LogFileLocation "C:\Pop3Logging"
    ```

  - *LogFileRollOverSettings* 이 매개 변수는 POP3 또는 IMAP4 프로토콜 로깅이 새 로그 파일을 만드는 빈도를 정의합니다. 기본적으로 새 로그 파일은 매일 생성됩니다. 가능한 값은 다음과 같습니다.
    
    매시간
    
    매일
    
    매주
    
    매월
    
    이 설정은 *LogPerFileSizeQuota* 매개 변수의 값이 0으로 설정된 경우에만 적용됩니다. 이 예에서는 매시간 새 로그 파일을 만들도록 클라이언트 액세스 서버 CAS01에서 POP3 프로토콜 로깅을 변경합니다.
    
    ```powershell
    Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 0 -LogFileRollOverSettings Hourly
    ```

  - *LogPerFileSizeQuota* 이 매개 변수는 POP3 또는 IMAP 4 프로토콜 로그 파일의 최대 크기(바이트)를 정의합니다. 기본적으로 이 값은 0으로 설정됩니다. 이 값이 0으로 설정된 경우 *LogFileRollOverSettings* 매개 변수에 지정된 빈도로 새 프로토콜 로그 파일이 만들어집니다.
    
    이 예에서는 로그 파일이 2MB 크기가 되면 새 로그 파일을 생성하도록 클라이언트 액세스 서버 CAS01에서 POP3 프로토콜 로깅을 변경합니다.
    
    ```powershell
    Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota 2000000
    ```
    
    이 예에서는 만든 날짜 및 크기에 관계없이 동일한 로그 파일을 사용하기 위해 클라이언트 액세스 서버 CAS01에서 POP3 프로토콜 로깅을 변경합니다.
    
    ```powershell
    Set-PopSettings -Server "CAS01" -LogPerFileSizeQuota unlimited
    ```


> [!NOTE]
> POP3 또는 IMAP4에 대한 프로토콜 로깅 설정을 변경한 후에는 POP3 또는 IMAP4 서비스 중에서 사용할 서비스를 다시 시작해야 합니다. POP3 및 IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 <A href="start-and-stop-the-pop3-services-exchange-2013-help.md">시작 및 POP3 서비스를 중지 합니다.</A> 및 <A href="start-and-stop-the-imap4-services-exchange-2013-help.md">시작 및 IMAP4 서비스를 중지 합니다.</A>을 참조하십시오.



구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\)) 및 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

셸에서 다음 명령을 실행하여 POP3 프로토콜 로깅 설정을 확인합니다. POP3 프로토콜 로깅을 사용하도록 설정된 경우 값은 *ProtocolLogEnabled* 매개 변수의 값은 `True`입니다. POP3 프로토콜을 사용하지 않도록 설정된 경우 값은 `False`입니다. 또한 *LogFileLocation*, *LogPerFileSizeQuota* 및 *LogFileRollOverSettings* 매개 변수의 값이 올바른지 확인할 수 있습니다.

```powershell
Get-PopSettings | format-list
```

셸에서 다음 명령을 실행하여 IMAP4 프로토콜 로깅 설정을 확인합니다. IMAP4 프로토콜 로깅을 사용하도록 설정된 경우 값은 *ProtocolLogEnabled* 매개 변수의 값은 `True`입니다. IMAP4 프로토콜을 사용하지 않도록 설정된 경우 값은 `False`입니다. 또한 *LogFileLocation*, *LogPerFileSizeQuota* 및 *LogFileRollOverSettings* 매개 변수의 값이 올바른지 확인할 수 있습니다.

```powershell
Get-ImapSettings | format-list
```

## 자세한 내용

POP3 및 IMAP4에 대해 프로토콜 로깅 설정을 구성한 후 다음 작업을 고려할 수도 있습니다.

[시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md)

[시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)

