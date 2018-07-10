---
title: '스마트 호스트를 통해 아웃 바운드 전자 메일 라우팅에 대 한 송신 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 스마트 호스트를 통해 아웃 바운드 전자 메일 라우팅에 대 한 송신 커넥터 만들기
ms:assetid: 4a9ef08e-bd62-4c6b-8790-d24fb0f8f24b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ673059(v=EXCHG.150)
ms:contentKeyID: 50483046
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 스마트 호스트를 통해 아웃 바운드 전자 메일 라우팅에 대 한 송신 커넥터 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-07_

네트워크 어플라이언스로 아웃바운드 메시지에 대해 정책 확인을 수행하려는 경우와 같이 타사 스마트 호스트를 통해 전자 메일을 라우팅하려는 경우가 있습니다.


> [!NOTE]
> 타사 스마트 호스트는 전송에 SMTP를 사용해야 합니다. 그렇지 않을 경우 외부 커넥터나 배달 에이전트 커넥터를 사용해야 합니다.



이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "송신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 아웃바운드 커넥터를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## EAC를 사용하여 스마트 호스트를 통해 아웃바운드 전자 메일을 라우팅할 송신 커넥터 만들기

1.  EAC에서 **메일 흐름** \> **송신 커넥터**로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 송신 커넥터** 마법사에서 송신 커넥터에 대 한 이름을 지정 하 고 **형식** 에 대 한 **사용자 지정** 을 선택 합니다. 일반적으로이 옵션을이 선택 하지 Microsoft Exchange Server 2013 를 실행 하는 컴퓨터에 메시지를 라우팅 하려는 경우에 선택 합니다. **다음** 을 클릭 합니다.

3.  **스마트 호스트를 통해 메일 라우팅**을 선택하고 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. **스마트 호스트 추가** 창에서 192.168.100.1 같은 IP 주소나 contoso.com 같은 FQDN(정규화된 도메인 이름)을 지정하고 **저장**을 클릭합니다.
    
    **스마트 호스트 인증**에서 스마트 호스트에 필요한 인증 유형을 선택합니다. **기본 인증**을 선택할 경우 사용자 이름과 암호를 지정해야 합니다.
    

    > [!NOTE]
    > 기본 인증을 선택할 경우 사용자 이름 및 암호를 일반 텍스트로 보내므로 암호화된 연결을 사용하는 것이 좋습니다.



4.  **주소 공간** 아래에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. **도메인 추가** 창에서 **유형**에 SMTP가 나열되어 있는지 확인합니다. **FQDN(정규화된 도메인 이름)**에서 \*를 입력하여 모든 도메인으로 보내는 메시지에 이 송신 커넥터가 적용되도록 지정합니다. **저장**을 클릭합니다.

5.  **원본 서버** 대 한 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다. **서버 선택** 창에서 서버를 선택 하 고![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")**추가** 클릭 합니다. **확인** 을 클릭 합니다.

6.  **마침**을 클릭합니다.

송신 커넥터를 만들면 송신 커넥터 목록에 나타납니다.

## 작동 여부는 어떻게 확인합니까?

스마트 호스트를 통해 아웃바운드 전자 메일을 라우팅할 송신 커넥터가 만들어졌는지 확인하려면 조직의 사용자가 보내는 메시지를 **주소 공간**에 지정된 도메인으로 보냅니다(Outlook Web App 사용 가능). 받는 사람이 메시지를 받으면 송신 커넥터가 구성된 것입니다.

## 자세한 내용

[인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md)

[송신 커넥터](send-connectors-exchange-2013-help.md)

