---
title: 'Telnet을 사용 하 여 SMTP 통신 테스트: Exchange 2013 Help'
TOCTitle: Telnet을 사용 하 여 SMTP 통신 테스트
ms:assetid: 8a5f6715-baa4-48dd-8600-02c6b3d1aa9d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb123686(v=EXCHG.150)
ms:contentKeyID: 52058105
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Telnet을 사용 하 여 SMTP 통신 테스트

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2016-12-09_

이 항목에서는 텔넷을 사용하여 메시징 서버 간의 SMTP(Simple Mail Transfer Protocol) 통신을 테스트하는 방법에 대해 설명합니다. 기본적으로 SMTP는 포트 25에서 수신 대기됩니다. 포트 25에서 텔넷을 사용하는 경우에는 SMTP 서버에 연결하는 데 사용되는 SMTP 명령을 입력한 다음 텔넷 세션이 SMTP 메시징 서버인 것과 같이 메시지를 보낼 수 있습니다. 연결 및 메시지 전송 프로세스에서 수행되는 각 단계의 성공 여부를 확인할 수 있습니다.

다음은 텔넷을 사용하여 Microsoft Exchange 조직에 있는 전송 서버에 대한 SMTP 통신을 테스트할 수 있는 시나리오입니다.

  - 경계 네트워크 외부에 있는 호스트에서 조직의 인터넷 연결 Exchange 서버에 연결하여 테스트 메시지를 보냅니다.

  - 조직의 인터넷 연결 Exchange 서버에서 원격 메시징 서버에 연결하여 테스트 메시지를 보냅니다.

이 항목의 절차에서는 Microsoft Windows에 포함된 구성 요소인 텔넷 클라이언트를 사용하는 방법을 보여줍니다. 타사 텔넷 클라이언트를 사용하려면 Windows 텔넷 구성 요소의 구문과 다른 구문이 필요할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 30분

  - 이 항목의 절차에는 Exchange 권한이 적용되지 않습니다. 이 절차는 Exchange Server나 클라이언트 컴퓨터의 운영 체제에서 수행됩니다.

  - 이 항목의 절차는 익명 연결을 허용하는 인터넷 연결 서버 간 연결하는 데 가장 적합합니다. 내부 Exchange 서버의 메시지 전송은 암호화 및 인증됩니다. 텔넷을 사용하여 사서함 서버의 허브 전송 서비스에 연결하려면 메시지를 받는 데 익명 액세스 또는 기본 인증을 허용하도록 구성된 수신 커넥터를 만들어야 합니다. 커넥터에서 기본 인증이 허용되는 경우 사용자 이름과 암호에 사용되는 텍스트 문자열을 Base64 형식으로 변환하는 유틸리티가 있어야 합니다. 기본 인증을 사용하는 경우에는 사용자 이름과 암호를 알아내기가 쉽기 때문에 암호화를 사용하지 않는 상태로 기본 인증을 사용하지 않는 것이 좋습니다.

  - 원격 메시징 서버에 연결할 경우 인터넷 연결 Exchange 서버에서 이 항목의 절차를 수행하는 것이 좋습니다. 그러면 원본 IP 주소, 해당하는 DNS(Domain Name System) 도메인 이름 및 해당 서버로 메시지를 보내려 하는 모든 인터넷 호스트의 역방향 조회 IP 주소에 대해 유효성 검사를 수행하도록 구성된 원격 메시징 서버에서 테스트 메시지가 거부되는 상황을 방지할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: Windows에 텔넷 클라이언트 설치

기본적으로 텔넷 클라이언트는 대부분 클라이언트 또는 서버 버전의 Microsoft Windows 운영 체제에 설치 되지 않습니다. 를 설치 하려면 [텔넷 클라이언트 설치](https://go.microsoft.com/fwlink/p/?linkid=179054)를 참조 하십시오.

## 2단계: Nslookup을 사용하여 원격 SMTP 서버의 MX 레코드에서 FQDN 또는 IP 주소 찾기

포트 25에서 텔넷을 사용하여 대상 SMTP 서버에 연결하려면 해당 SMTP 서버의 FQDN(정규화된 도메인 이름) 또는 IP 주소를 사용해야 합니다. FQDN 또는 IP 주소를 모르는 경우 이 정보를 찾을 수 있는 가장 쉬운 방법은 Nslookup 명령줄 도구를 사용하여 대상 도메인에 대한 MX 레코드를 찾는 것입니다.

1.  명령 프롬프트에서 **nslookup**을 입력한 다음 Enter 키를 누릅니다. 이 명령을 입력하면 Nslookup 세션이 열립니다.

2.  **set type=mx**를 입력한 다음 Enter 키를 누릅니다.

3.  **set timeout=20**을 입력한 다음 Enter 키를 누릅니다. 기본적으로 Windows DNS 서버의 재귀 DNS 쿼리 시간 제한은 15초입니다.

4.  MX 레코드를 찾을 도메인의 이름을 입력합니다. 예를 들어 fabrikam.com 도메인의 MX 레코드를 찾으려면 **fabrikam.com.**을 입력한 다음 Enter 키를 누릅니다.
    

    > [!NOTE]
    > 마침표(<STRONG>.</STRONG>)는 FQDN을 나타냅니다. 이와 같이 도메인 이름 끝에 마침표를 추가하면 네트워크에 대해 구성된 기본 DNS 접미사를 실수로 도메인 이름에 추가하는 경우를 방지할 수 있습니다.

    
    이 명령을 실행하면 다음과 같은 출력을 확인할 수 있습니다.
    
        fabrikam.com mx preference=10, mail exchanger = mail1.fabrikam.com
        fabrikam.com mx preference=20, mail exchanger = mail2.fabrikam.com
        mail1.fabrikam.com internet address = 192.168.1.10
        mail2 fabrikam.com internet address = 192.168.1.20
    
    XM 레코드와 연결된 모든 호스트 이름 또는 IP 주소를 대상 SMTP 서버로 사용할 수 있습니다. 기본 설정 값이 낮은 항목이 기본 SMTP 서버입니다. 부하 분산 및 내결함성에 대해 여러 MX 레코드와 서로 다른 기본 설정 값을 사용할 수 있습니다.

5.  Nslookup 세션을 끝내려면 **exit**를 입력하고 Enter 키를 누릅니다.


> [!NOTE]
> 조직의 내부 네트워크에 적용되어 있는 방화벽 또는 인터넷 프록시 제한으로 인해 Nslookup 도구를 사용하여 인터넷에서 공용 DNS 서버를 쿼리하지 못할 수도 있습니다.



## 3단계: 포트 25에서 텔넷을 사용하여 SMTP 통신 테스트

이 예에서는 다음 값이 사용됩니다.

  - **대상 SMTP 서버**   mail1.fabrikam.com

  - **원본 도메인**   contoso.com

  - **보낸 사람의 전자 메일 주소**   chris@contoso.com

  - **받는 사람의 전자 메일 주소**   kate@fabrikam.com

  - **메시지 제목**   Test from Contoso

  - **메시지 본문**   This is a test message


> [!NOTE]
> <UL>
> <LI>
> <P>텔넷 클라이언트의 명령은 대/소문자를 구분하지 않습니다. 쉽게 구별할 수 있도록 SMTP 명령 동사는 대문자로 표기합니다.</P>
> <LI>
> <P>텔넷 세션 내에서 대상 SMTP 서버에 연결한 후에는 백스페이스 키를 사용할 수 없습니다. SMTP 명령을 실수로 잘못 입력한 경우에는 Enter 키를 누른 후에 해당 명령을 다시 입력해야 합니다. 인식할 수 없는 SMTP 명령이나 구문 오류가 있으면 다음과 같은 오류 메시지가 표시됩니다.</P><PRE><CODE>500 5.3.3 Unrecognized command</CODE></PRE></LI></UL>



1.  명령 프롬프트에서 **telnet**을 입력한 다음 Enter 키를 누릅니다. 이 명령을 입력하면 텔넷 세션이 열립니다.

2.  **set localecho**를 입력한 다음 Enter 키를 누릅니다. 이 옵션 명령을 사용하면 입력하는 문자를 볼 수 있습니다. 일부 SMTP 서버의 경우에는 이 설정이 필요할 수도 있습니다.

3.  **set logfile** *\<파일 이름\>*을 입력합니다. 이 옵션 명령을 사용하면 지정된 로그 파일에 텔넷 세션을 기록할 수 있습니다. 파일 이름만 지정하면 로그 파일의 위치는 현재 작업 디렉터리가 됩니다. 파일 이름과 경로를 모두 지정하는 경우에는 컴퓨터의 로컬 경로를 지정해야 합니다. 여기서 지정하는 경로와 파일 이름은 모두 Microsoft DOS 8.3 형식으로 입력해야 합니다. 또한 지정하는 경로가 존재해야 합니다. 존재하지 않는 로그 파일을 지정하면 새 로그 파일이 자동으로 만들어집니다.

4.  **open mail1.fabrikam.com 25**를 입력한 다음 Enter 키를 누릅니다.

5.  **EHLO contoso.com**을 입력한 다음 Enter 키를 누릅니다.

6.  **MAIL FROM:chris@contoso.com**을 입력한 다음 Enter 키를 누릅니다.

7.  **RCPT TO:kate@fabrikam.com NOTIFY=success,failure**를 입력한 다음 Enter 키를 누릅니다. 선택 NOTIFY 명령은 대상 SMTP 서버에서 보낸 사람에게 제공해야 하는 특정 DSN(배달 상태 알림) 메시지를 지정합니다. DSN 메시지는 RFC 1891에 정의되어 있습니다. 이 경우에는 메시지 배달 성공 또는 실패 관련 DSN 메시지를 요청하게 됩니다.

8.  **DATA**를 입력한 다음 Enter 키를 누릅니다. 그러면 다음과 같은 응답을 받게 됩니다.
    
        354 Start mail input; end with <CLRF>.<CLRF>

9.  **Subject: Test from Contoso**를 입력한 다음 Enter 키를 누릅니다.

10. Enter 키를 누릅니다. RFC 2822의 경우 `Subject:` 헤더 필드와 메시지 본문 사이에 빈 줄이 하나 필요합니다.

11. **This is a test message**를 입력하고 Enter 키를 누릅니다.

12. Enter 키를 누르고 마침표(**.**)를 입력한 다음 Enter 키를 누릅니다. 그러면 다음과 같은 응답을 받게 됩니다.
    
        250 2.6.0 <GUID> Queued mail for delivery

13. 대상 SMTP 서버와의 연결을 끊으려면 **QUIT**를 입력한 다음 Enter 키를 누릅니다. 그러면 다음과 같은 응답을 받게 됩니다.
    
        221 2.0.0 Service closing transmission channel

14. 텔넷 세션을 닫으려면 **quit**를 입력한 다음 Enter 키를 누릅니다.

## 4단계: 텔넷 세션의 결과 평가

이 섹션에는 이전 예에서 사용된 다음 명령에 제공할 수 있는 응답에 대한 정보가 나와 있습니다.

  - Open mail1.fabrikam.com 25

  - EHLO contoso.com

  - MAIL FROM:chris@contoso.com

  - RCPT TO:kate@fabrikam.com NOTIFY=success,failure
    

    > [!NOTE]
    > RFC 2821에 정의되어 있는 3자리의 SMTP 응답 코드는 모든 SMTP 메시징 서버에 대해 동일합니다. 일부 SMTP 메시징 서버의 경우에는 텍스트 설명이 약간 다를 수도 있습니다.



## Open mail1.fabrikam.com 25

**성공적인 응답**   `220 mail1.fabrikam.com Microsoft ESMTP MAIL Service ready at <day-date-time>`

**실패 응답**   `Connecting to mail1.fabrikam.com...Could not open connection to the host, on port 25: Connect failed`

**가능한 실패 이유**

  - 대상 SMTP 서비스를 사용할 수 없습니다.

  - 대상 방화벽에 제한이 적용되어 있습니다.

  - 원본 방화벽에 제한이 적용되어 있습니다.

  - 대상 SMTP 서버에 대해 잘못된 FQDN 또는 IP 주소를 지정했습니다.

  - 잘못된 포트 번호를 지정했습니다.

## EHLO contoso.com

**성공적인 응답**   `250 mail1.fabrikam.com Hello [<sourceIPaddress>]`

**실패 응답**   `501 5.5.4 Invalid domain name`

**가능한 실패 원인**   도메인 이름에 잘못된 문자가 있습니다. 또는 대상 SMTP 서버에 연결 제한이 적용되어 있습니다.


> [!NOTE]
> EHLO는 RFC 2821에 정의되어 있는 ESMTP(Extended Simple Message Transfer Protocol) 동사입니다. ESMTP 서버는 초기 연결 동안 해당 기능을 보급할 수 있습니다. 이러한 기능에는 수락되는 최대 메시지 크기 및 지원되는 인증 방법이 포함됩니다. HELO는 RFC 821에 정의되어 있는 이전 SMTP 동사입니다. 대부분의 SMTP 메시징 서버에서는 ESMTP 및 EHLO를 모두 지원합니다.



## MAIL FROM:chris@contoso.com

**성공적인 응답**   `250 2.1.0 Sender OK`

**실패 응답**   `550 5.1.7 Invalid address`

**가능한 실패 이유**   보낸 사람의 전자 메일 주소에 구문 오류가 있습니다.

**실패 응답**   `530 5.7.1 Client was not authenticated`

**가능한 실패 이유**   대상 서버에서 익명 메시지 전송을 수락하지 않습니다. 텔넷을 사용하여 메시지를 허브 전송 서버로 직접 전송하려고 하면 이 오류가 발생합니다.

## RCPT TO:kate@fabrikam.com NOTIFY=success,failure

**성공적인 응답**   `250 2.1.5 Recipient OK`

**실패 응답**   `550 5.1.1 User unknown`

**가능한 실패 이유**   지정한 받는 사람이 조직에 없습니다.

