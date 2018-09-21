---
title: 'Edge 구독 관리: Exchange 2013 Help'
TOCTitle: Edge 구독 관리
ms:assetid: 27de4104-fb8e-4eab-9ad2-a64f81a4fb69
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996865(v=EXCHG.150)
ms:contentKeyID: 61183419
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 구독 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-04-16_

이 항목에서는 다양한 Edge 구독 관리 작업에 대해 자세히 설명합니다.

**목차**

Subscribe an Edge Transport server

Remove an Edge subscription

Resubscribe an Edge Transport Server

Add or remove a Mailbox Server

Run EdgeSync manually

Verify EdgeSync results

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 10분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md) 항목의 "Edge 전송 서버" 섹션 및 "EdgeSync" 항목

  - 인터넷 연결 Active Directory 사이트를 구독하는 Edge 서버가 필요합니다. 자세한 내용은 [구독된 Edge 전송 서버를 통한 인터넷 메일 흐름 구성](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## Edge 전송 서버 구독

하나 이상의 Edge 전송 서버를 단일 Active Directory 사이트에 구독할 수 없습니다. 경계 네트워크에서 Edge 전송 서버를 추가로 배포하고 Edge 구독이 이미 있는 동일한 Active Directory 사이트에 해당 서버를 구독하려면 다음 작업이 수행됩니다.

  - 새 Edge 구독 개체가 Active Directory에 만들어집니다.

  - Active Directory 사이트의 각 사서함 서버에 ESRA 계정이 추가로 만들어집니다. 이러한 계정은 AD LDS(Active Directory Lightweight Directory Services)로 복제되며 새 서버와의 동기화 중에 EdgeSync 동기화 프로세스에서 사용됩니다.

  - 새 Edge 구독이 인터넷에 대한 자동 송신 커넥터의 원본 서버 목록에 추가됩니다. 처리용으로 해당 커넥터로 전송된 메시지는 구독된 Edge 전송 서버 간에 부하 분산됩니다.

  - Edge 전송 서버에서 Exchange 조직으로의 인바운드 송신 커넥터가 자동으로 만들어집니다.

  - Edge 전송 서버에 대한 EdgeSync 동기화가 시작됩니다.

## Edge 구독 제거

Exchange 조직이나 Exchange 조직 및 Edge 전송 서버에서 모두 Edge 구독을 제거해야 하는 경우가 있습니다. 나중에 Edge 전송 서버를 Exchange 조직에 다시 구독하려는 경우 Edge 전송 서버에서 Edge 구독을 제거하지 마세요. Edge 전송 서버에서 Edge 구독을 제거하면 모든 복제된 데이터가 AD LDS에서 삭제됩니다. 받는 사람 데이터가 많으면 이 작업에 시간이 오래 걸릴 수 있습니다.

Edge 구독을 완전히 제거하려면 제거할 Edge 전송 서버와 해당 Edge 전송 서버가 구독된 Active Directory 사이트의 Exchange 2013 사서함 서버에서 이 절차를 수행해야 합니다.

Edge 구독을 제거하면 AD LDS에서 정보 동기화가 중지됩니다. AD LDS에 저장된 모든 계정이 제거되고 모든 송신 커넥터의 원본 서버 목록에서 Edge 전송 서버가 제거됩니다. Active Directory 데이터를 사용하는 Edge 전송 서버 기능은 더 이상 사용할 수 없습니다.

1.  Edge 전송 서버에서 Edge 구독을 제거하려면 다음 구문을 사용합니다.
    
    ```powershell
Remove-EdgeSubscription <EdgeTransportServerIdentity>
```
    
    예를 들어 Edge 전송 서버 Edge01에서 Edge 구독을 제거하려면 다음 명령을 실행합니다.
    
    ```powershell
Remove-EdgeSubscription Edge01
```

2.  사서함 서버에서 Edge 구독을 제거하려면 다음 구문을 사용합니다.
    
    ```powershell
Remove-EdgeSubscription <MailboxServerIdentity>
```
    
    예를 들어 사서함 서버 Mailbox01에서 Edge 구독을 제거하려면 다음 명령을 실행합니다.
    
    ```powershell
Remove-EdgeSubscription Mailbox01
```

다음의 경우 Edge 구독을 제거해야 합니다.

  - Edge 전송 서버가 더 이상 EdgeSync 동기화에 참가하지 않도록 하려는 경우. 이 경우 Edge 전송 서버와 Exchange 조직에서 모두 Edge 구독을 제거해야 합니다.

  - Edge 전송 서버가 해제된 경우. 이 시나리오에서는 Exchange 조직에서만 Edge 구독을 제거하면 됩니다. 컴퓨터에서 Edge 전송 서버 역할을 제거하면 AD LDS 인스턴스 및 AD LDS에 저장된 Active Directory 데이터도 모두 제거됩니다.

  - Edge 구독의 Active Directory 사이트 연결을 변경하려는 경우. 이 경우 Exchange 조직에서만 Edge 구독을 제거하면 됩니다. Exchange 조직에서 Edge 구독을 제거한 후에는 Edge 전송 서버를 다른 Active Directory 사이트에 다시 구독할 수 있습니다.

Exchange 조직에서 Edge 구독을 제거하면 다음 작업이 수행됩니다.

  - Active Directory에서 AD LDS로의 정보 동기화가 중지됩니다.

  - ESRA 계정이 Active Directory 및 AD LDS에서 모두 제거됩니다.

  - Edge 전송 서버가 송신 커넥터의 *SourceTransportServers* 속성에서 제거됩니다.

  - Edge 전송 서버에서 Exchange 조직으로의 자동 인바운드 송신 커넥터가 AD LDS에서 제거됩니다.

Edge 전송 서버에서 Edge 구독을 제거하면 다음 작업이 수행됩니다.

  - Active Directory 데이터를 사용하는 Edge 전송 서버 기능을 더 이상 사용할 수 없습니다.

  - 복제된 데이터가 AD LDS에서 제거됩니다.

  - Edge 구독을 만들 때 사용할 수 없도록 설정되었던 작업이 다시 사용할 수 있도록 설정되므로 로컬 구성을 수행할 수 있습니다.

## Edge 전송 서버 다시 구독

Edge 전송 서버를 Active Directory 사이트에 다시 구독해야 하는 경우가 있습니다. Edge 구독을 다시 만들면 새 자격 증명이 생성되므로 전체 Edge 구독 프로세스를 다시 실행해야 합니다. 다음과 같은 경우 Edge 전송 서버를 다시 구독해야 합니다.

  - 구독된 Active Directory 사이트에 새 사서함 서버를 추가하고 새 사서함 서버가 EdgeSync 동기화에 참가하도록 하려는 경우.

  - Edge 구독을 만든 후에 Edge 전송 서버의 라이선스 키를 적용한 경우. Edge 구독을 만들 때 Edge 전송 서버의 라이선스 정보가 캡처됩니다. 구독된 Edge 전송 서버를 사용이 허가된 것으로 표시하려면 라이선스 키를 Edge 전송 서버에 적용한 후 해당 서버를 Exchange 조직에 구독해야 합니다. Edge 구독 프로세스를 수행한 후 라이선스 키를 Edge 전송 서버에 적용하는 경우 Exchange 조직에서 라이선스 정보가 업데이트되지 않으므로 Edge 전송 서버를 다시 구독해야 합니다.

  - ESRA 자격 증명이 손상된 경우
    

    > [!IMPORTANT]
    > Edge 전송 서버를 다시 구독하려면 Edge 전송 서버에서 새 Edge 구독 파일을 내보낸 다음 사서함 서버에서 XML 파일을 가져옵니다. 이때 Edge 전송 서버를 원래 구독했던 Active Directory 사이트에 다시 구독해야 합니다. 다시 구독 프로세스에서 기존 Edge 구독을 덮어쓰므로 먼저 원본 Edge 구독을 제거할 필요는 없습니다.



## 사서함 서버 추가 또는 제거

Edge 전송 서버가 이미 구독되어 있는 Active Directory 사이트에 사서함 서버를 추가하는 경우 새 사서함 서버는 EdgeSync 동기화에 자동으로 참가하지 않습니다. 새로 배포한 사서함 서버가 EdgeSync 동기화 프로세스에 참가하도록 하려면 각 Edge 전송 서버를 Active Directory 사이트에 다시 구독해야 합니다.

사서함 서버를 Edge 전송 서버가 구독되어 있는 Active Directory 사이트에서 제거해도 해당 사이트에 사서함 서버가 하나뿐인 경우가 아니면 EdgeSync 동기화에는 아무런 영향이 없습니다. Edge 전송 서버가 구독되어 있는 Active Directory 사이트에서 모든 사서함 서버를 제거하는 경우 사이트에서 구독된 Edge 전송 서버의 연결이 해제됩니다.

## 수동으로 EdgeSync 실행

Active Directory에서 구성이나 받는 사람을 크게 변경하여 변경 내용을 즉시 동기화하려는 경우 EdgeSync를 수동으로 실행할 수 있습니다. 전체 동기화를 수행하거나 마지막 복제 이후 변경된 내용만 동기화할 수 있습니다.

수동 EdgeSync를 실행하면 EdgeSync 동기화 일정이 다시 설정됩니다. 다음 자동 동기화는 수동 동기화를 실행한 시기를 기준으로 합니다.

수동으로 EdgeSync를 실행하려면 다음 구문을 사용합니다.

    Start-EdgeSynchronization [-Server <MailboxServerIdentity>] [-TargetServer <EdgeTransportServerIdentity> [-ForceFullSync]

다음 예에서는 아래와 같은 옵션을 사용하여 EdgeSync를 시작합니다.

  - Exchange 2013 사서함 서버 Mailbox01에서 동기화를 시작합니다.

  - 모든 Edge 전송 서버가 동기화됩니다.

  - 마지막 복제 이후의 변경 내용만 동기화됩니다.

<!-- end list -->

```powershell
Start-EdgeSynchronization -Server Mailbox01
```

이 예에서는 다음 옵션을 사용하여 EdgeSync를 시작합니다.

  - 로컬 사서함 서버에서 동기화를 시작합니다.

  - Edge 전송 서버 Edge03만 동기화합니다.

  - 모든 받는 사람 및 구성 데이터가 완전히 동기화됩니다.

<!-- end list -->

```powershell
Start-EdgeSynchronization -TargetServer Edge03 -ForceFullSync
```

## EdgeSync 결과 확인

**Test-EdgeSynchronization** cmdlet을 사용하여 Edge 동기화가 작동하는지 확인할 수 있습니다. 이 cmdlet은 구독된 Edge 전송 서버의 동기화 상태를 보고합니다.

이 cmdlet의 출력을 통해 Edge 전송 서버로 동기화되지 않은 개체를 확인할 수 있습니다. 이 작업에서는 Active Directory에 저장된 데이터와 AD LDS에 저장된 데이터를 비교한 다음 데이터 불일치를 보고합니다.

**Test-EdgeSynchronization** cmdlet에서 *ExcludeRecipientTest* 매개 변수를 사용하여 받는 사람 데이터 동기화의 유효성 검사를 제외할 수 있습니다. 이 매개 변수를 포함하는 경우 구성 개체 동기화에만 유효성 검사를 수행합니다. 받는 사람 데이터 유효성 검사는 구성 데이터 유효성 검사만 수행하는 것보다 시간이 오래 걸립니다.

## 단일 받는 사람에 대한 EdgeSync 결과 확인

단일 받는 사람에 대해 EdgeSync 결과를 확인하려면 구독된 Active Directory 사이트의 사서함 서버에서 다음 구문을 사용합니다.

```powershell
Test-EdgeSynchronization -VerifyRecipient <emailaddress>
```

이 예에서는 사용자 kate@contoso.com에 대해 EdgeSync 결과를 확인합니다.

```powershell
Test-EdgeSynchronization -VerifyRecipient kate@contoso.com
```

맨 위로 이동

