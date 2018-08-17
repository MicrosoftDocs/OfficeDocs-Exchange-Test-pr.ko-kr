---
title: '전자 메일을 받도록 하지 Exchange를 실행 하는 시스템에서 수신 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 전자 메일을 받도록 하지 Exchange를 실행 하는 시스템에서 수신 커넥터 만들기
ms:assetid: 85f0864a-6502-49db-8804-16755a7292b4
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657467(v=EXCHG.150)
ms:contentKeyID: 50483583
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전자 메일을 받도록 하지 Exchange를 실행 하는 시스템에서 수신 커넥터 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-03_

Exchange를 실행하지 않는 시스템에서 보낸 메시지를 받아야 하는 상황이 발생할 수 있습니다. 예를 들어 정책 확인을 수행한 다음 메시지를 Exchange 서버로 라우팅하는 네트워크 어플라이언스가 있는 경우가 그에 해당합니다. 이 경우 해당 어플라이언스에서 SMTP를 사용한다고 가정합니다. 그렇지 않으면 외부 커넥터나 배달 에이전트 커넥터를 사용해야 합니다.

이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "수신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 수신 커넥터를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 메시징 어플라이언스에서 보낸 메시지를 받을 수신 커넥터 만들기

1.  EAC에서 **메일 흐름** \> **수신 커넥터**로 이동합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 수신 커넥터를 만듭니다.

2.  **새 수신 커넥터** 페이지에서 수신 커넥터 이름을 지정하고 **역할**에 **허브 전송**을 선택합니다. 이 시나리오의 경우 전송 서비스를 실행하는 사서함 서버가 어플라이언스에서 보낸 메시지를 받아야 합니다.

3.  유형으로 **사용자 지정**을 선택합니다. 수신 커넥터가 Microsoft Exchange Server 2013을 실행하지 않는 어플라이언스에서 보낸 메일을 받을 것이기 때문입니다.

4.  **네트워크 어댑터 바인딩**에서 **사용 가능한 모든 IPV4**가 **IP 주소** 목록에 나열되었는지 확인합니다. **다음**을 클릭합니다.

5.  **원격 네트워크 설정**에서 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하여 **IP 주소** 목록에서 **0.0.0.0-255.255.255.255**를 제거합니다. 커넥터가 특정 어플라이언스에서 보낸 메일을 수락하도록 지정해야 하기 때문입니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 새 IP 주소를 추가하고 **IP 주소 추가** 창에서 어플라이언스의 IP 주소를 추가합니다. **저장**을 클릭합니다.

6.  **마침** 단추를 클릭하여 커넥터를 만듭니다.

수신 커넥터를 만들면 수신 커넥터 목록에 나타납니다. Cmdlet을 사용하여 수신 커넥터를 만드는 방법의 예제를 보려면 [New-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125139\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

메시징 어플라이언스에서 보낸 메시지를 받을 수신 커넥터를 성공적으로 만들었는지 확인하려면 어플라이언스에서 보낸 메일을 받을 수 있는지 테스트하십시오. 메일을 받을 수 있으면 구성이 성공적으로 작동하는 것입니다.

## 자세한 내용

[인터넷에서 전자 메일을 수신 하도록 수신 커넥터 만들기](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

