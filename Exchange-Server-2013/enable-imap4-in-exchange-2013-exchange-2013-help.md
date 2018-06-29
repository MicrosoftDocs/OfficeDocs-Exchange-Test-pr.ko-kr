﻿---
title: 'Exchange 2016에서 IMAP4를 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: Exchange 2016에서 IMAP4를 사용 하도록 설정
ms:assetid: c1ae10dd-14da-4400-b38d-2aeafde8abe6
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124489(v=EXCHG.150)
ms:contentKeyID: 50484082
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exchange 2016에서 IMAP4를 사용 하도록 설정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2016-06-02_

Exchange 2016 (MMC (Microsoft Management Console) 또는 Exchange 관리 셸 (EMS) 사용 하 여에서 IMAP4 클라이언트 연결을 사용 하도록 설정 하는 방법에 알아봅니다.

Exchange Server 2016 를 설치 하면 IMAP4 클라이언트 연결이 활성화 되지 않습니다. IMAP4 클라이언트 연결을 사용 하도록 설정 하려면 두 IMAP 서비스, Microsoft Exchange IMAP4 서비스 및 Microsoft Exchange IMAP4 백엔드 서비스를 시작 해야 합니다. IMAP4 사용 하도록 설정 하면 Exchange 2016 포트 143 및 포트 993 Secure Sockets Layer (SSL) 사용을 통해 보안 되지 않은 IMAP4 클라이언트 통신을 허용 합니다.

사서함 서버 역할을 실행 하는 동일한 Exchange 2016 컴퓨터에서 IMAP4와 IMAP4 백엔드 서비스를 관리 합니다. Exchange 2016 클라이언트 액세스 서비스의 일부인 사서함 서버 역할 서비스를 별도로 관리할 더이상 있도록 합니다.

POP3 및 IMAP4 설정 하는 방법에 대 한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md)을 참조 합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 2분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 및 IMAP4 권한" 섹션.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## (MMC (Microsoft Management Console)을 사용 하 여 IMAP4를 사용 하도록 설정 하려면

사서함 서버 역할을 실행하는 컴퓨터에서

1.  **서비스** 스냅인의 콘솔 트리에서 **서비스(로컬)**를 클릭합니다.

2.  결과 창에서 **Microsoft Exchange IMAP4**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

3.  결과 창에서 **Microsoft Exchange IMAP4 백 엔드**를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.

4.  **일반** 탭의 **시작 유형**에서 **자동**을 선택한 다음 **적용**을 클릭합니다.

5.  **서비스 상태**에서 **시작**, **확인**을 차례로 클릭합니다.

## Exchange 관리 셸 를 사용 하 여 IMAP4를 사용 하도록 설정 하려면

사서함 서버 역할을 실행하는 컴퓨터에서

1.  Microsoft Exchange IMAP4 서비스를 자동으로 시작하도록 설정합니다.
    
        Set-service msExchangeIMAP4 -startuptype automatic

2.  Microsoft Exchange IMAP4 서비스를 시작합니다.
    
        Start-service msExchangeIMAP4

3.  Microsoft Exchange IMAP4 백 엔드 서비스를 자동으로 시작하도록 설정합니다.
    
        Set-service msExchangeIMAP4BE -startuptype automatic

4.  Microsoft Exchange IMAP4 백 엔드 서비스를 시작합니다.
    
        Start-service msExchangeIMAP4BE

## 작동 여부는 어떻게 확인합니까?

Exchange 2016 사서함 서버에서 Windows 작업 관리자를 엽니다. **서비스** 탭에서 **MSExchangeIMAP4BE** 및 **MSExchangeIMAP4** 에 대 한 상태 IMAP4 사용 하도록 설정 하는 경우에 **실행** 으로 표시 됩니다.

