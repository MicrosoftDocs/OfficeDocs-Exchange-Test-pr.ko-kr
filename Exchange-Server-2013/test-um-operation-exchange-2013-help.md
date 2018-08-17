---
title: 'UM 작업 테스트: Exchange 2013 Help'
TOCTitle: UM 작업 테스트
ms:assetid: 06c9ab4e-8272-47b1-a217-e366f7e9dbaa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa995957(v=EXCHG.150)
ms:contentKeyID: 56270321
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# UM 작업 테스트

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2013-06-25_

이 항목에서는 셸을 사용하여 음성 메일 시스템의 작동을 테스트하는 방법을 설명합니다. 다음 절차를 수행할 때 사서함 서버는 Microsoft Exchange 통합 메시징 서비스를 실행하고 진단 SIP(Session Initiation Protocol) 호출을 시작한 다음 UM 서비스의 상태 변수를 반환합니다.

이 진단 테스트는 로컬 사서함 서버에서만 실행할 수 있으며, EMC를 사용하는 사서함 서버 작업을 테스트할 수는 없습니다.

클라이언트 액세스 및 사서함 서버와 관련된 추가 관리 작업에 대한 자세한 내용은 [UM 서비스 절차](um-services-procedures-exchange-2013-help.md)를 참조하세요.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md) 항목에서 "사서함 서버(UM 서비스)" 및 \&quot;클라이언트 액세스 서버(UM 호출 라우터 서비스)\&quot; 항목

  - 다음 절차를 수행하려면 로컬 관리자 그룹의 구성원인 계정을 사용하여 사서함 서버에 로그온해야 합니다.

  - 클라이언트 액세스 서버와 동일한 컴퓨터나 별도의 컴퓨터에 사서함 서버가 설치되어 있는지 확인합니다.

  - 사서함 서버와 동일한 컴퓨터나 별도의 컴퓨터에 클라이언트 액세스 서버가 설치되어 있는지 확인합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 셸을 사용하여 통합 메시징 서비스의 작업 테스트

이 예에서는 로컬 사서함 서버에서 연결 및 작동 테스트를 수행한 다음 VoIP(Voice over IP) 연결 정보를 표시합니다.

    Test-UMConnectivity

이 예에서는 TCP 포트 5060에서 암호화되지 않은 들어오는 SIP 요청을 수신 대기하는 로컬 클라이언트 액세스 서버의 기능을 테스트합니다.

    Test-UMConnectivity -ListenPort 5060

이 예에서는 TCP 포트 5061에서 암호화된 들어오는 SIP 요청을 수신 대기하는 로컬 클라이언트 액세스 서버의 기능을 테스트합니다.

    Test-UMConnectivity -ListenPort 5061


> [!NOTE]
> <CODE>-UMIPGateway</CODE> 매개 변수가 지정되지 않은 경우 모드 1을 사용합니다.




> [!NOTE]
> <CODE>-Timeout</CODE> 매개 변수를 5초보다 작은 값으로 설정할 수 있습니다. 그러나 이 매개 변수를 항상 5초 이상의 값으로 구성하는 것이 좋습니다.


