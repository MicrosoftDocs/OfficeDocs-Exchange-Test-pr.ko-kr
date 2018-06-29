---
title: '내부 Exchange 서버에서 메시지를 받는 수신 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 내부 Exchange 서버에서 메시지를 받는 수신 커넥터 만들기
ms:assetid: 546cead9-7a2d-4332-a5f6-35343d56c619
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657448(v=EXCHG.150)
ms:contentKeyID: 50483129
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 내부 Exchange 서버에서 메시지를 받는 수신 커넥터 만들기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

Exchange 서버에서 보낸 메일을 받으려는 경우 **내부** 유형의 수신 커넥터를 만듭니다. 이 유형의 커넥터를 사용하면 조직 내의 메일 라우팅을 제어할 수 있습니다. 사서함 서버의 전송 서비스에서 보낸 메일을 특정 Edge 전송 서버로 라우팅하거나 사서함 서버 간에 메일을 라우팅하려는 경우를 예로 들 수 있습니다.

이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "수신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 수신 커넥터를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 내부 Exchange 서버에서 메시지를 받을 수신 커넥터 만들기

1.  EAC에서 **메일 흐름** \> **수신 커넥터**로 이동합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 새 수신 커넥터를 만듭니다.

2.  **새 수신 커넥터** 페이지에서 수신 커넥터 이름을 지정하고 **역할**에 **허브 전송**을 선택합니다. 여기서는 메일을 네트워크 내, 외부가 아니라 조직 내에서 라우팅하려 한다고 가정합니다.

3.  유형으로 **내부**를 선택합니다. Exchange 서버 인증을 사용하여 커넥터가 구성됩니다.

4.  원격 네트워크 설정 페이지에 0.0.0.0-255.255.255.255가 나열되면(수신 커넥터가 모든 IP 주소에서 연결을 수신함을 의미) **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하여 이를 제거합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 메일을 받을 서버의 IP 주소(예: 192.168.1.1)를 추가한 다음 **저장**을 클릭합니다.

5.  **마침**을 클릭하여 커넥터를 만듭니다.

수신 커넥터를 만들면 수신 커넥터 목록에 나타납니다. Cmdlet을 사용하여 수신 커넥터를 만드는 방법의 예제를 보려면 [New-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125139\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

내부 서버에서 보낸 메일을 받을 수신 커넥터가 만들어졌는지 확인하려면 보내는 서버에서 보낸 메시지가 받는 사람의 서버로 전송되는지 테스트합니다. 이렇게 하려면 만든 수신 커넥터에 대해 Exchange 관리 셸에서 [Set-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125140\(v=exchg.150\)) cmdlet을 사용하여 *ProtocolLoggingLevel*을 `Verbose`로 설정하고 로그에 메시지가 배달된 것으로 나타나는지 확인합니다.

## 자세한 내용

[인터넷에서 전자 메일을 수신 하도록 수신 커넥터 만들기](create-a-receive-connector-to-receive-email-from-the-internet-exchange-2013-help.md)

[전자 메일을 받도록 파트너에서 보안 수신 커넥터 만들기](create-a-secure-receive-connector-to-receive-email-from-a-partner-exchange-2013-help.md)

