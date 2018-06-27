---
title: 'IP 주소와 POP3 및 IMAP4 액세스를 위한 포트 구성: Exchange 2013 Help'
TOCTitle: IP 주소와 POP3 및 IMAP4 액세스를 위한 포트 구성
ms:assetid: 8292747b-6626-4d7f-ba73-1e17f5d99fa4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123530(v=EXCHG.150)
ms:contentKeyID: 50556024
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# IP 주소와 POP3 및 IMAP4 액세스를 위한 포트 구성

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-11-28_

EAC와 셸을 사용하여 Microsoft Exchange POP3 및 IMAP4 서비스에서 기본 설정과는 다른 IP 주소 및 포트를 사용하도록 구성할 수 있습니다.


> [!NOTE]
> IPv4(Internet Protocol Version 4) 형식이나 IPv6(Internet Protocol Version 6) 형식 또는 두 형식으로 모두 IP 주소 및 IP 주소 범위를 입력합니다. Windows Server 2008을 기본 설정으로 설치하면 IPv4 및 IPv6을 사용할 수 있습니다.



POP3 및 IMAP4에 대한 자세한 내용은 [Exchange Server 2013의 POP3 및 IMAP4](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [클라이언트 및 모바일 장치 사용 권한](clients-and-mobile-devices-permissions-exchange-2013-help.md) 항목의 "POP3 설정" 및 "IMAP4 설정" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## POP3를 위한 IP 주소 및 포트 구성

## EAC를 사용하여 POP3를 위한 IP 주소 및 포트 구성

1.  EAC에서 **서버\>서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **POP3**를 클릭합니다.

4.  **TLS 또는 암호화되지 않은 연결**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **IP 주소 추가** 페이지의 **IP 주소**에서 다음 중 하나를 선택합니다.
    
      - **사용 가능한 모든 IPv4 주소**   서버에 사용 가능한 모든 IPv4 IP 주소를 사용합니다.
    
      - **사용 가능한 모든 IPv6 주소**   서버에 사용 가능한 모든 IPv6 IP 주소를 사용합니다.
    
      - **IP 주소 지정**   특정 IP 주소를 사용합니다.

6.  **포트**에서 포트 번호를 입력하거나 기본 포트를 적용합니다.

7.  **저장**을 클릭하여 변경 내용을 저장합니다.

POP3에 대해 IP 주소 및 포트 설정을 지정한 후에는 POP3 서비스를 다시 시작해야 설정이 적용됩니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)을 참조하십시오.

## 셸을 사용하여 POP3를 위한 IP 주소 및 포트 구성

이 예에서는 SSL(Secure Sockets Layer)을 지원하는 POP3를 통해 Exchange와 통신하는 데 사용할 IP 주소와 포트를 설정합니다.

    Set-PopSettings -SSLBindings: IPaddress:Port

이 예에서는 암호화 또는 TLS(전송 계층 보안) 암호화를 지원하지 않는 POP3를 통해 Exchange와 통신하는 데 사용할 IP 주소와 포트를 설정합니다.

    Set-PopSettings -UnencryptedOrTLSBindings IPaddress:Port

POP3에 대해 IP 주소 및 포트 설정을 지정한 후에는 POP3 서비스를 다시 시작해야 설정이 적용됩니다. POP3 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 POP3 서비스를 중지 합니다.](start-and-stop-the-pop3-services-exchange-2013-help.md)을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-PopSettings](https://technet.microsoft.com/ko-kr/library/aa997154\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

다음을 수행하여 서버의 POP3 IP 주소 및 포트 설정이 변경되었는지 확인합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-PopSettings | format-list

2.  *UnencryptedOrTLSBindings* 및 *SSLBindings* 설정이 올바른지 확인합니다.

## IMAP4를 위한 IP 주소 및 포트 구성

## EAC를 사용하여 IMAP4를 위한 IP 주소 및 포트 구성

1.  EAC에서 **서버\>서버**로 이동합니다.

2.  서버 목록에서 클라이언트 액세스 서버를 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  서버 속성 페이지에서 **IMAP4**를 클릭합니다.

4.  TLS 또는 암호화되지 않은 연결 설정을 지정하려면 **TLS 또는 암호화되지 않은 연결**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. SSL(Secure Sockets Layer) 연결 설정을 변경하려면 **SSL(Secure Sockets Layer) 연결**에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

5.  **IP 주소 추가** 페이지의 **IP 주소**에서 다음 중 하나를 선택합니다.
    
      - **사용 가능한 모든 IPv4 주소**   서버에 사용 가능한 모든 IPv4 IP 주소를 사용합니다.
    
      - **사용 가능한 모든 IPv6 주소**   서버에 사용 가능한 모든 IPv6 IP 주소를 사용합니다.
    
      - **IP 주소 지정**   특정 IP 주소를 사용합니다.

6.  **포트**에서 포트 번호를 입력하거나 기본 포트를 적용합니다.

7.  **저장**을 클릭하여 변경 내용을 저장합니다.

IMAP4에 대해 IP 주소 및 포트 설정을 지정한 후에는 IMAP4 서비스를 다시 시작해야 설정이 적용됩니다. IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md) 항목을 참조하십시오.

## 셸을 사용하여 IMAP4를 위한 IP 주소 및 포트 구성

이 예에서는 IMAP4를 통해 Exchange와 통신하는 데 사용할 IP 주소와 포트를 설정합니다.

    Set-ImapSettings -SSLBindings: IPaddress:Port

이 예에서는 암호화 또는 TLS 암호화를 지원하지 않는 IMAP4를 통해 Exchange와 통신하는 데 사용할 IP 주소와 포트를 설정합니다.

    Set-ImapSettings -UnencryptedOrTLSBindings IPaddress:Port 

IMAP4에 대해 IP 주소 및 포트 설정을 지정한 후에는 IMAP4 서비스를 다시 시작해야 설정이 적용됩니다. IMAP4 서비스를 다시 시작하는 방법에 대한 자세한 내용은 [시작 및 IMAP4 서비스를 중지 합니다.](start-and-stop-the-imap4-services-exchange-2013-help.md)을 참조하십시오.

구문과 매개 변수에 대한 자세한 내용은 [Set-ImapSettings](https://technet.microsoft.com/ko-kr/library/aa998252\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

다음을 수행하여 서버의 IMAP4 IP 주소 및 포트 설정이 변경되었는지 확인합니다.

1.  셸에서 다음 명령을 실행합니다.
    
        Get-ImapSettings | format-list

2.  *UnencryptedOrTLSBindings* 및 *SSLBindings* 설정이 올바른지 확인합니다.

## 자세한 내용

POP3 및 IMAP4를 위해 IP 주소와 포트를 구성한 후 다음 작업을 수행할 수도 있습니다.

[Exchange 2016에서 IMAP4를 사용 하도록 설정](enable-imap4-in-exchange-2013-exchange-2013-help.md)

[Exchange 2013에서 POP3 사용](enable-pop3-in-exchange-2013-exchange-2013-help.md)

