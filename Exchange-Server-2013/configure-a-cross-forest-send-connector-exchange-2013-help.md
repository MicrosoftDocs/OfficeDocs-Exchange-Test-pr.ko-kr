---
title: " 크로스 포리스트 송신 커넥터를 구성 합니다.: Exchange 2013 Help"
TOCTitle: " 크로스 포리스트 송신 커넥터를 구성 합니다."
ms:assetid: 7840d172-071e-4f13-9379-2fe1eee1a7cc
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ945053(v=EXCHG.150)
ms:contentKeyID: 52058089
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# [Wave15] 크로스 포리스트 송신 커넥터를 구성 합니다.

 

_<strong>적용 대상:</strong> Exchange Server 2013_

_<strong>마지막으로 수정된 항목:</strong> 2013-02-21_

Active Directory에서 *포리스트*는 디렉터리 서비스의 바깥쪽 경계를 나타냅니다. 송신 커넥터를 만들어 포리스트 간 통신이 가능하도록 설정할 수 있습니다. 이 예에서는 커넥터에서 기본 인증이 사용됩니다.

커넥터 구성과 관련된 추가 관리 작업에 대한 자세한 내용은 [커넥터](connectors-exchange-2013-help.md)를 참조하십시오.

이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [크로스 포리스트 토폴로지에서 Exchange 2013 배포](deploy-exchange-2013-in-a-cross-forest-topology-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 20분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "송신 커넥터" 항목 및 "수신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 커넥터를 만들어 포리스트 간 토폴로지를 구성할 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 각 포리스트에서 사용자 계정 만들기

각 포리스트에서 기본 인증에 사용할 사용자 계정을 만들어야 합니다. 각 포리스트에서 계정을 만들고 이러한 각 계정을 통신에 사용되는 Exchange Server의 유니버설 보안 그룹에 추가합니다. 이 계정은 송신 커넥터가 다른 포리스트에서 메일을 받는 서버를 인증하는 데 사용됩니다. 예를 들어 Contoso 도메인의 Exchange 서버로 메일을 보내는 경우 Fourth Coffee 도메인의 Exchange 서버에서 인증에 사용해야 하는 자격 증명으로 UPN(사용자 계정 이름) FourthCoffee@Contoso.com을 가진 사용자 계정을 제공합니다.

## EAC를 사용하여 송신 커넥터를 만들어 전자 메일을 다른 Exchange 2013 포리스트로 라우팅

기본 인증을 사용하여 포리스트 간 메일 흐름을 설정합니다.

1.  EAC에서 <strong>메일 흐름</strong> \> <strong>송신 커넥터</strong>로 이동합니다. <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  <strong>새 송신 커넥터</strong> 마법사에서 송신 커넥터의 이름을 지정하고 <strong>유형</strong>으로 <strong>인터넷</strong>을 선택합니다. <strong>다음</strong>을 클릭합니다.

3.  <strong>스마트 호스트를 통해 메일 라우팅</strong>을 선택하고 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. <strong>스마트 호스트 추가</strong> 창에서 두 번째 포리스트의 대상 서버에 대한 IP 주소를 지정합니다(예: 64.4.6.100). <strong>저장</strong>을 클릭한 후 <strong>다음</strong>을 클릭합니다.
    
    <strong>스마트 호스트 인증</strong>에 대해 <strong>기본 인증</strong>을 선택하고 사용자 이름과 암호를 입력합니다. 여기에서 TLS를 통한 보안 통신을 위해 <strong>TLS를 시작한 후에만 기본 인증 제공</strong>을 선택할 수 있습니다.
    

    > [!NOTE]
    > TLS를 통한 기본 인증을 사용할 경우 X.509 인증서를 사용하도록 대상 서버를 구성해야 합니다.



4.  <strong>주소 공간</strong> 아래에서 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭합니다. <strong>도메인 추가</strong> 창에서 <strong>유형</strong>에 SMTP가 나열되어 있는지 확인합니다. <strong>FQDN(정규화된 도메인 이름)</strong>에 수신 도메인을 입력합니다(예: fourthcoffee.com). <strong>저장</strong>을 클릭한 후 <strong>다음</strong>을 클릭합니다.

5.  <strong>원본 서버</strong>에 대해 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")을 클릭합니다. <strong>서버 선택</strong> 창에서 사용할 서버를 선택하고 <strong>추가</strong>![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. <strong>확인</strong>을 클릭합니다.

6.  <strong>마침</strong>을 클릭합니다. 송신 커넥터 목록에 커넥터가 표시됩니다.

송신 커넥터를 만든 후 원본 포리스트에 메일을 보내는 두번째 포리스트에 송신 커넥터를 만듭니다. 이 경우에 정규화 된 도메인 이름 (FQDN) 지정 하면 첫번째 포리스트의 도메인 이름이 됩니다. 예: contoso.com

## 셸을 사용하여 송신 커넥터에 대해 사용 권한 설정

이 예에서는 셸에서 Enable-CrossForestConnector.ps1 스크립트를 사용하여 포리스트 간 토폴로지에서 사용할 송신 커넥터에 대해 사용 권한을 설정합니다.

    .\Enable-CrossForestConnector.ps1 -Connector "Cross-Forest" -user "ANONYMOUS LOGON"

## 작동 여부는 어떻게 확인합니까?

전자 메일을 두 번째 포리스트로 라우팅할 송신 커넥터가 만들어졌는지 확인하려면 조직의 사용자가 보내는 메시지를 <strong>주소 공간</strong>에 지정된 도메인으로 보냅니다(Outlook Web App 사용 가능). 받는 사람이 메시지를 받으면 송신 커넥터가 구성된 것입니다.

## 자세한 내용

[인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[송신 커넥터](send-connectors-exchange-2013-help.md)

