---
title: '전자 메일을 받도록 파트너에서 보안 수신 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 전자 메일을 받도록 파트너에서 보안 수신 커넥터 만들기
ms:assetid: 06aa692c-7940-4a14-a722-058c47440f85
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673037(v=EXCHG.150)
ms:contentKeyID: 50482425
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 전자 메일을 받도록 파트너에서 보안 수신 커넥터 만들기

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-10-03_

이 절차에서는 파트너의 보안 전자 메일을 받도록 수신 커넥터를 구성하는 방법을 보여 줍니다. 사용자 자신과 신뢰할 수 있는 파트너 간의 통신을 암호화해야 하는 경우에 이 절차를 사용하십시오. 커넥터는 TLS(전송 계층 보안)로 인증된 서버의 연결만 수락하도록 구성됩니다.

이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "수신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 수신 커넥터를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 파트너의 보안 메시지를 받을 수신 커넥터 만들기

1.  EAC에서 **메일 흐름** \> **수신 커넥터**로 이동합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 새 수신 커넥터를 만듭니다.

2.  **새 수신 커넥터** 페이지에서 수신 커넥터 이름을 지정하고 **역할**에 **프런트 엔드 전송**을 선택합니다. 이 절차의 경우 파트너의 메일을 받게 되므로 처음에 메일을 프런트 엔드 서버로 라우팅하여 메일 흐름을 간소화하고 통합하는 것이 좋습니다.

3.  유형으로 **파트너**를 선택합니다. 수신 커넥터는 신뢰할 수 있는 타사의 메일을 받게 됩니다.

4.  **네트워크 어댑터 바인딩**에서 **사용 가능한 모든 IPV4**가 **IP 주소** 목록에 나열되고 **포트**가 25인지 확인합니다(SMTP(Simple Mail Transfer Protocol)는 포트 25를 사용함). 이는 커넥터가 로컬 서버의 네트워크 어댑터에 할당된 모든 IP 주소에서 연결을 수신 대기함을 의미합니다. **다음**을 클릭합니다.

5.  원격 네트워크 설정 페이지에 0.0.0.0-255.255.255.255가 나열되면(수신 커넥터가 모든 IP 주소에서 연결을 수신함을 의미) **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하여 이를 제거합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하고 파트너 서버의 IP 주소를 추가한 다음 **저장**을 클릭합니다.
    

    > [!NOTE]
    > CIDR 표기법으로 된 IP 주소(예: 64.4.6.100/24)를 지정할 수도 있습니다.



6.  **마침**을 클릭하여 커넥터를 만듭니다.

수신 커넥터를 만들면 수신 커넥터 목록에 나타납니다. Cmdlet을 사용하여 수신 커넥터를 만드는 방법의 예제를 보려면 [New-ReceiveConnector](https://technet.microsoft.com/ko-kr/library/bb125139\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

파트너의 메시지를 받을 수신 커넥터를 성공적으로 만들었는지 확인하려면 파트너가 사용자 중 한 명에게 메일을 보낼 수 있는지와 해당 사용자가 메일을 성공적으로 받는지 테스트하십시오. 암호화된 메일을 받을 수 있으면 구성이 성공적으로 작동한 것입니다(메시지 헤더를 확인하여 TLS가 사용되는지 확인할 수 있음).

## 자세한 내용

[수신 커넥터](receive-connectors-exchange-2013-help.md)

