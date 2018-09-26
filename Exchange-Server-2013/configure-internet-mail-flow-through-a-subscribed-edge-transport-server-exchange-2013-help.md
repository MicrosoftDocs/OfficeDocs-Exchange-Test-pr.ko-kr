---
title: '구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성: Exchange 2013 Help'
TOCTitle: 구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61183431
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

Edge 전송 서버를 통해 인터넷 메일을 설정하려면 Active Directory 사이트에 Edge 전송 서버를 구독합니다. 그러면 인터넷 메일 흐름에 필요한 다음과 같은 송신 커넥터 두 개가 자동으로 만들어집니다.

  - 모든 인터넷 도메인에 아웃바운드 전자 메일을 보내도록 구성된 송신 커넥터

  - Edge 전송 서버에서 Exchange 2013 사서함 서버로 인바운드 전자 메일을 보내도록 구성된 송신 커넥터

Edge 전송 서버를 Active Directory 사이트에 구독하지 않으려는 경우 사서함 서버와 Edge 전송 서버 간에 메일 흐름을 설정하는 데 필요한 송신 커넥터를 수동으로 만들 수 있습니다. 자세한 내용은 [EdgeSync를 사용 하지 않고 Edge 전송 서버를 통해 인터넷 메일 흐름 구성](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md)을 참조하십시오. 그러나 가능한 경우에는 항상 Edge 전송 서버를 Active Directory 사이트에 구독하는 것이 좋습니다.

## 시작하기 전에

  - 예상 완료 시간: 20분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "Edge 전송 서버" 및 "EdgeSync" 항목

  - Edge 전송 서버를 조직에 구독하기 전에 먼저 Exchange 조직에 대해 권한 도메인 및 전자 메일 주소 정책을 구성해야 합니다.

  - 경계 네트워크와 Exchange 조직을 구분하는 방화벽을 통해 보안 LDAP 포트 50636/TCP를 사용하도록 설정합니다. Edge 전송 서버는 구독된 Active Directory 사이트에 있는 모든 Exchange 2013 사서함과 통신할 수 있어야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성

1.  Edge 전송 서버에서 다음 구문을 사용하여 Edge 구독 파일을 만듭니다.
    
    ```powershell
    New-EdgeSubscription -FileName <FileName>.xml [-Force]
    ```
    
    다음 예에서는 C:\\My Documents 폴더에 Edge 구독 파일 EdgeSubscriptionInfo.xml을 만듭니다. *Force* 매개 변수를 사용하는 경우 사용하지 않도록 설정할 명령을 확인하라는 메시지와 Edge 전송 서버에서 구성 데이터를 덮어쓴다는 경고가 표시되지 않습니다.
    
    ```powershell
    New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force
    ```

2.  작성된 Edge 구독 파일을 Edge 전송 서버를 구독하려는 Active Directory 사이트의 사서함 서버에 복사합니다.

3.  사서함 서버에서 Edge 구독 파일을 가져오려면 다음 구문을 사용합니다.
    
    ```powershell
    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    ```
    
    이 예에서는 D:\\Data 폴더에서 Edge 구독 파일 EdgeSubscriptionInfo.xml을 가져오며 Edge 전송 서버를 Active Directory 사이트 "Default-First-Site-Name"에 구독합니다.
    
    ```powershell
    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    ```   

    > [!NOTE]
    > <EM>CreateInternetSendConnector</EM> 또는 <EM>CreateInboundSendConnector</EM> 매개 변수를 사용하여 필수 커넥터 중 하나 또는 두 커넥터가 모두 자동으로 만들어지지 않도록 설정할 수 있습니다. 자세한 내용은 <A href="edge-subscriptions-exchange-2013-help.md">Edge 구독</A>를 참조하세요.

4.  사서함 서버에서 다음 명령을 실행하여 첫 번째 EdgeSync 동기화를 시작합니다.
    
    ```powershell
    Start-EdgeSynchronization
    ```

5.  작업이 완료되면 Edge 전송 서버와 사서함 서버에서 모두 Edge 구독 파일을 삭제하는 것이 좋습니다. Edge 구독 파일에는 LDAP 통신 프로세스 중에 사용되는 자격 증명에 대한 정보가 포함되어 있습니다.

