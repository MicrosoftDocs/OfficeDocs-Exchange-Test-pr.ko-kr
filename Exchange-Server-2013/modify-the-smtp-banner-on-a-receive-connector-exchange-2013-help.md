---
title: '수신 커넥터의 SMTP 배너 수정: Exchange 2013 Help'
TOCTitle: 수신 커넥터의 SMTP 배너 수정
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52058138
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수신 커넥터의 SMTP 배너 수정

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

*SMTP 배너*는 원격 SMTP 메시징 서버가 Microsoft Exchange Server 2013을 실행하는 컴퓨터에 구성된 수신 커넥터에 연결된 후에 받는 SMTP 연결 응답입니다.

즉, 원격 SMTP 메시징 서버가 수신 커넥터에 연결된 후에 받는 기본 응답입니다.

    220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>

수신 커넥터에서 SMTP 배너의 사용자 지정 값을 지정할 경우 해당 SMTP 수신 커넥터에 연결되는 원격 SMTP 메시징 서버는 다음 응답을 받습니다.

    220 <Banner Text>

서버 이름과 메시징 서버 소프트웨어가 SMTP 배너를 통해 공개되지 않도록 인터넷 연결 SMTP 수신 커넥터의 SMTP 배너를 수정할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "수신 커넥터" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 대체 SMTP 배너 텍스트 문자열은 항상 `220`으로 시작해야 합니다. RFC 2821에 정의된 대로 기본 서비스 준비 SMTP 응답 코드는 220입니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 셸을 사용하여 수신 커넥터의 SMTP 배너 수정

다음 명령을 실행합니다.

    Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"

이 예에서는 From the Internet이라는 기존 수신 커넥터의 SMTP 배너를 수정하여 SMTP 배너에 `220 Contoso Corporation`이 표시되도록 합니다.

    Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"

이 예에서는 From the Internet이라는 수신 커넥터의 사용자 지정 SMTP 배너를 제거합니다. 그러면 SMTP 배너가 기본값으로 돌아갑니다.

    Set-ReceiveConnector "From the Internet" -Banner $null

## 작동 여부는 어떻게 확인합니까?

수신 커넥터의 SMTP 배너가 수정되었는지 확인하려면 다음을 수행합니다.

1.  수신 커넥터에 액세스할 수 있는 컴퓨터에서 텔넷 클라이언트를 열고 다음 명령을 실행합니다.
    
        open <Connector FQDN or IP address> <Port>

2.  수신 커넥터의 응답에 구성한 SMTP 배너가 포함되어 있는지 확인합니다.

이 절차는 익명 또는 기본 인증을 허용하는 수신 커넥터에서만 작동합니다. 자세한 내용은 [Telnet을 사용 하 여 SMTP 통신 테스트](use-telnet-to-test-smtp-communication-exchange-2013-help.md)를 참조하십시오.

