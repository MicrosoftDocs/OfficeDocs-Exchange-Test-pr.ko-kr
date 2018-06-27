---
title: '인터넷에서 전자 메일을 수신 하도록 수신 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 인터넷에서 전자 메일을 수신 하도록 수신 커넥터 만들기
ms:assetid: 534bbd32-a0db-4d50-9579-4933b156d7b3
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657447(v=EXCHG.150)
ms:contentKeyID: 50483118
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 인터넷에서 전자 메일을 수신 하도록 수신 커넥터 만들기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-15_

이 절차에서는 인터넷에서 보낸 전자 메일을 받도록 수신 커넥터를 구성하는 방법을 보여 줍니다.


> [!NOTE]
> 인터넷에서 보낸 메일을 수락하는 수신 커넥터는 Exchange를 설치할 때 암시적으로 만들어지므로 대부분의 경우에는 인터넷에서 메일을 받도록 명시적으로 수신 커넥터를 설정해야 합니다. 자세한 내용은 <A href="receive-connectors-exchange-2013-help.md">수신 커넥터</A> 항목을 참조하십시오.



이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "수신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 수신 커넥터를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 인터넷에서 보낸 메시지를 받는 수신 커넥터 만들기

1.  EAC에서 **메일 흐름** \> **수신 커넥터**로 이동합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 수신 커넥터를 만듭니다.

2.  **새 수신 커넥터** 페이지에서 수신 커넥터 이름을 지정하고 **역할**에 **프런트 엔드 전송**을 선택합니다. 이 예에서는 인터넷에서 보낸 메일을 받으려고 하므로 처음부터 메일을 프런트 엔드 서버로 라우팅하여 메일 흐름을 간소화하고 통합하는 것이 좋습니다.

3.  유형으로 **인터넷**을 선택합니다. 수신 커넥터가 인터넷에서 보낸 메일을 받습니다.

4.  **네트워크 어댑터 바인딩**에서 **사용 가능한 모든 IPV4**에 **네트워크 어댑터 바인딩**이 나열되고 **포트**가 25인지 확인합니다. SMTP(Simple Mail Transer Protocol)는 포트 25를 사용합니다. 이는 커넥터가 로컬 서버의 네트워크 어댑터에 할당된 모든 IP 주소에서 연결을 수신 대기함을 의미합니다.
    

    > [!NOTE]
    > 네트워크 어댑터를 여러 개 사용하는 경우 이 페이지에서 로컬 서버의 특정 네트워크 어댑터에 할당된 IP 주소를 추가할 수는 있지만, 꼭 필요한 작업은 아닙니다.



5.  **마침** 단추를 클릭하여 커넥터를 만듭니다.

수신 커넥터를 만들면 수신 커넥터 목록에 나타납니다. Cmdlet을 사용하여 수신 커넥터를 만드는 방법의 예제를 보려면 [New-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125139\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

인터넷에서 보낸 메시지를 받는 수신 커넥터가 만들어졌는지 확인하려면 외부 원본에서 메일을 보내고 사용자 중 한 명이 이 메일을 받을 수 있는지 테스트합니다. 메일을 받을 수 있으면 구성이 성공적으로 작동하는 것입니다.

## 자세한 내용

[전자 메일을 받도록 파트너에서 보안 수신 커넥터 만들기](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

[전자 메일을 받도록 하지 Exchange를 실행 하는 시스템에서 수신 커넥터 만들기](create-a-receive-connector-to-receive-email-from-a-system-not-running-exchange-exchange-2013-help.md)

