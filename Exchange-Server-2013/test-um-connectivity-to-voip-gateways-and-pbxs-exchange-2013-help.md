---
title: 'VoIP 게이트웨이 및 Pbx에 대 한 UM 연결 테스트: Exchange 2013 Help'
TOCTitle: VoIP 게이트웨이 및 Pbx에 대 한 UM 연결 테스트
ms:assetid: 2aca8631-a99a-4e29-aff0-e462385f03b2
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996906(v=EXCHG.150)
ms:contentKeyID: 56270324
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# VoIP 게이트웨이 및 Pbx에 대 한 UM 연결 테스트

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2014-09-17_

UM(통합 메시징) 및 연결된 전화 통신 장비와 관련된 작업을 테스트할 수 있습니다. 다음 절차를 수행하면 클라이언트 액세스와 메시징 서버에서 음성 메일 시스템의 전체 종단 간 작업을 테스트합니다. 여기에는 VoIP 게이트웨이와 PBX(Private Branch eXchange), IP PBX 및 케이블 등 클라이언트 액세스 및 사서함 서버에 연결된 전화 통신 구성 요소가 포함됩니다.

UM 문제해결과 관련 된 추가 관리 작업에 대 한 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조 합니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목에서 "사서함 서버(UM 서비스)" 및 \&quot;클라이언트 액세스 서버(UM 호출 라우터 서비스)\&quot; 항목

  - 다음 절차를 수행하려면 로컬 관리자 그룹의 구성원인 계정을 사용하여 사서함 서버에 로그온해야 합니다.

  - 클라이언트 액세스 서버와 동일한 컴퓨터나 별도의 컴퓨터에 사서함 서버가 설치되어 있는지 확인합니다.

  - 사서함 서버와 동일한 컴퓨터나 별도의 컴퓨터에 클라이언트 액세스 서버가 설치되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 통합 메시징 및 전화 통신 구성 요소의 작업 테스트

이 예에서는 TCP 포트 5060에서 들어오는 SIP 요청을 수신 대기하는 UM IP 게이트웨이의 기능을 테스트합니다.

    Test-UMConnectivity -ListenPort 5060 -UMIPGateway MyIPGateway

이 예에서는 보안된 상호 TLS 연결 대신 보안되지 않은 TCP 연결을 사용하여 전화 56780번으로 `MyUMIPGateway`라는 UM IP 게이트웨이를 통해 호출을 실행하는 로컬 사서함 서버의 기능을 테스트합니다.

    Test-UMConnectivity -UMIPGateway MyUMIPGateway -Phone 56780 -Secured $false

이 예는 SIP URI를 사용하여 다이얼 플랜의 Outlook Voice Access 번호를 테스트하며, Lync Server가 포함된 환경에서 사용할 수 있습니다.

    Test-UMConnectivity -UMIPGateway OCSGateway1 -Phone "sip:SIPdialplan.contoso.com@contoso.com"


> [!NOTE]
> <CODE>-Timeout</CODE> 매개 변수를 5초보다 작은 값으로 설정할 수 있습니다. 그러나 이 매개 변수를 항상 5초 이상의 값으로 구성하는 것이 좋습니다. <CODE>&shy;UMIPGateway</CODE> 매개 변수가 명령줄 구문에 지정되어 있으면 모드 2를 사용합니다.


