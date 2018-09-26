---
title: '인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기: Exchange 2013 Help'
TOCTitle: 인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기
ms:assetid: 6deaefa8-1152-40d9-b1ba-9c19bdf8a928
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657457(v=EXCHG.150)
ms:contentKeyID: 50483333
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 인터넷에 보낸 전자 메일에 대 한 송신 커넥터 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-01-23_

기본적으로 Microsoft Exchange Server 2013 도메인 외부 메일을 보낼 수 있습니다를 허용 하지 않습니다. 도메인 외부 메일을 보내려고 송신 커넥터를 만들려면 필요 합니다. 다음 그림에서는 인터넷 메일을 보내려고 송신 커넥터를 만들 때 메일 흐름을 보여줍니다.

![connector\_send\_onprem\_internet](images/JJ657457.e8963e4f-7dce-461f-bbcf-660278cefa35(EXCHG.150).gif "connector_send_onprem_internet")

이 절차가 사용된 시나리오에 관심이 있으면 다음 항목을 참조하십시오.

  - [메일 흐름 및 클라이언트 액세스 구성](configure-mail-flow-and-client-access-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "송신 커넥터" 항목

  - 설치를 시작하는 경우 [Exchange 2013 새 설치 배포](deploy-a-new-installation-of-exchange-2013-exchange-2013-help.md)를 참조하십시오. 설치가 완료되면 이 항목의 단계를 사용하여 아웃바운드 커넥터를 만들 수 있습니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 인터넷에 보낸 전자 메일에 대 한 송신 커넥터를 만들려면

1.  EAC에서 **메일 흐름** \> **송신 커넥터**로 이동한 다음 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다.

2.  **새 송신 커넥터** 마법사에서 송신 커넥터에 대 한 이름을 지정 하 고 **형식** 에 대 한 **인터넷** 을 선택 합니다. **다음** 을 클릭 합니다.

3.  **받는 사람 도메인 연관 된 MX 레코드** 선택 되어 있음을 커넥터는 메일을 라우팅하 domain name system (DNS)를 사용 하도록 지정 하는 확인 합니다. **다음** 을 클릭 합니다.

4.  **주소 공간** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") **추가** 클릭 합니다. **추가 도메인** 창에서 SMTP **형식** 으로 표시 되는지 확인 합니다. **정규화 된 도메인 이름 (FQDN)** 대 한 입력 \*, 나타냅니다이 송신 커넥터는 모든 도메인에 보내는 메시지에 적용 됩니다. **저장** 을 클릭 합니다.

5.  **송신 커넥터 범위 이름** 선택 되지 않았는지 확인 하 고 을 클릭 합니다.

6.  **원본 서버** 대 한 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다. **서버 선택** 창에서 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 하 고 클라이언트 액세스 서버를 통해 인터넷 메일을 보낼에 사용 되는 사서함 서버를 선택 합니다. 서버를 선택한 후 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭 합니다. **확인** 을 클릭 합니다.

7.  **마침**을 클릭합니다.

한번 만든 송신 커넥터 송신 커넥터 목록에 나타납니다.

## 클라이언트 액세스 서버를 통해 메일 라우팅에 셸을 사용 하 여

Exchange 2013 클라이언트 액세스 서버를 통해 아웃 바운드 메시지를 라우팅할 **Set-SendConnector** cmdlet의 *FrontendProxyEnabled* 매개 변수를 사용할 수 있습니다. 기본적으로이 매개 변수 `$true` 로 설정 하지 되어 있지만 대부분의 경우에서 통합 및 많은 수의 메시징 서버를 사용 하는 환경을 사용 하는 경우에 특히 메일 흐름을 단순화할 수 있습니다.

송신 커넥터에 `$true` 를 *FrontendProxyEnabled* 매개 변수를 설정 하는이 예제입니다.

```powershell
Set-SendConnector "Contoso.com Send Connector" -FrontendProxyEnabled $true
```

## 작동 여부는 어떻게 확인합니까?

하는 인터넷에 보낸 전자 메일에 대 한 송신 커넥터를 성공적으로 만들어졌는지 확인 하 고 외부 받는 사람에 게 사용자 중 하나에서 메일을 보낼 메시지가 성공적으로 도착 있는지 확인 합니다.

## 자세한 내용

[송신 커넥터](send-connectors-exchange-2013-help.md)

[스마트 호스트를 통해 아웃 바운드 전자 메일 라우팅에 대 한 송신 커넥터 만들기](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md)

