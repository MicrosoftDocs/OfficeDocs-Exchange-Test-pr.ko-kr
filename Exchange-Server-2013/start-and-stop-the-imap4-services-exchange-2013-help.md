---
title: '시작 및 IMAP4 서비스를 중지 합니다.: Exchange 2013 Help'
TOCTitle: 시작 및 IMAP4 서비스를 중지 합니다.
ms:assetid: a52db4bd-69a6-47b2-acf3-d9d8571c7a87
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124022(v=EXCHG.150)
ms:contentKeyID: 50483863
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 시작 및 IMAP4 서비스를 중지 합니다.

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-05_

기본적으로 Microsoft Exchange IMAP4 서비스와 Microsoft Exchange IMAP4 Backend 서비스라는 두 가지 IMAP4 서비스는 MicrosoftExchange Server 2013을 실행하는 컴퓨터에서 시작되지 않습니다. 전자 메일 클라이언트가 IMAP4를 사용하여 Exchange에 연결할 수 있도록 하려면 이 두 가지 서비스를 시작해야 합니다. 이 서비스가 실행 중이면 Exchange 2013에서는 포트 143과 포트 993에서 SSL(Secure Sockets Layer)을 사용한 보안되지 않은 IMAP4 클라이언트 통신을 수락합니다.

Microsoft Exchange IMAP4 서비스는 클라이언트 액세스 서버 역할을 실행 중인 Exchange 2013 컴퓨터에서 실행됩니다. Microsoft Exchange IMAP4 Backend 서비스는 사서함 서버 역할을 실행 중인 Exchange 2013 컴퓨터에서 실행됩니다. 클라이언트 액세스 및 사서함 서버 역할이 동일한 컴퓨터에서 실행되고 있는 환경에서는 두 서비스를 같은 컴퓨터에서 관리합니다.

POP3 및 IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 및 IMAP4 사용 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## Microsoft 관리 콘솔 서비스 스냅인을 사용하여 IMAP4 서비스 시작 또는 중지

IMAP4 서비스를 시작하려면

1.  클러스터 관리자를 실행 중인 컴퓨터에서 **시작**을 클릭하고 **프로그램**, **관리 도구**를 차례로 가리킨 다음 **서비스**를 클릭합니다. **Microsoft Exchange IMAP4**를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.

2.  사서함 서버 역할을 실행 중인 컴퓨터에서 **시작**을 클릭하고 **프로그램**, **관리 도구**를 차례로 가리킨 다음 **서비스**를 클릭합니다. **Microsoft Exchange IMAP4 Backend**를 마우스 오른쪽 단추로 클릭한 다음 **시작**을 클릭합니다.

IMAP4 서비스를 중지하려면

1.  클러스터 관리자를 실행 중인 컴퓨터에서 **시작**을 클릭하고 **프로그램**, **관리 도구**를 차례로 가리킨 다음 **서비스**를 클릭합니다. **Microsoft Exchange IMAP4**를 마우스 오른쪽 단추로 클릭한 다음 **중지**를 클릭합니다.

2.  사서함 서버 역할을 실행 중인 컴퓨터에서 **시작**을 클릭하고 **프로그램**, **관리 도구**를 차례로 가리킨 다음 **서비스**를 클릭합니다. **Microsoft Exchange IMAP4 Backend**를 마우스 오른쪽 단추로 클릭한 다음 **중지**를 클릭합니다.

## 셸을 사용하여 IMAP4 서비스 시작 또는 중지

IMAP4 서비스를 시작하려면

1.  클라이언트 액세스 서버 역할을 실행 중인 컴퓨터의 셸에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 서비스를 시작합니다.
    
    ```powershell
    Start-service msExchangeIMAP4
    ```

2.  사서함 서버 역할을 실행 중인 컴퓨터의 셸에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 Backend 서비스를 시작합니다.
    
    ```powershell
    Start-service msExchangeIMAP4BE
    ```

IMAP4 서비스를 중지하려면

1.  클라이언트 액세스 서버 역할을 실행 중인 컴퓨터의 셸에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 서비스를 중지합니다.
    
    ```powershell
    Stop-service msExchangeIMAP4
    ```

2.  사서함 서버 역할을 실행 중인 컴퓨터의 셸에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 Backend 서비스를 중지합니다.
    
    ```powershell
    Stop-service msExchangeIMAP4BE
    ```

## net start를 사용하여 IMAP4 서비스 시작 또는 중지

IMAP4 서비스를 시작하려면

1.  클라이언트 액세스 서버 역할을 실행 중인 컴퓨터의 명령 프롬프트에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 서비스를 시작합니다.
    
    ```powershell
    net start msExchangeIMAP4
    ```

2.  사서함 서버 역할을 실행 중인 컴퓨터의 명령 프롬프트에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 Backend 서비스를 시작합니다.
    
    ```powershell
    net start msExchangeIMAP4BE
    ```

IMAP4 서비스를 중지하려면

1.  클라이언트 액세스 서버 역할을 실행 중인 컴퓨터의 명령 프롬프트에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 서비스를 중지합니다.
    
    ```powershell
    Net Stop MSExchangeIMAP4
    ```

2.  사서함 서버 역할을 실행 중인 컴퓨터의 명령 프롬프트에서 다음 명령을 실행하여 Microsoft Exchange IMAP4 Backend 서비스를 중지합니다.
    
    ```powershell
    Net Stop MSExchangeIMAP4BE
    ```

## 작동 여부는 어떻게 확인합니까?

1.  Exchange 클라이언트 액세스 서버에서 Windows 작업 관리자를 엽니다. Microsoft Exchange IMAP4 서비스가 실행 중이면 **서비스** 탭에서 **MSExchangeIMAP4**의 상태가 **실행 중**으로 표시됩니다.

2.  Exchange 사서함 서버에서 Windows 작업 관리자를 엽니다. Microsoft Exchange IMAP4 Backend 서비스가 실행 중이면 **서비스** 탭에서 **MSExchangeIMAP4BE**의 상태가 **실행 중**으로 표시됩니다.

