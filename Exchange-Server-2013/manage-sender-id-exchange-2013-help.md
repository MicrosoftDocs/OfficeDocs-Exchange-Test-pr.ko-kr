---
title: '보낸사람 ID 관리: Exchange 2013 Help'
TOCTitle: 보낸사람 ID 관리
ms:assetid: 2e7b646a-8a66-4be7-a7c1-0bd43bb79a5b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa997136(v=EXCHG.150)
ms:contentKeyID: 50482782
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 보낸사람 ID 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2015-04-08_

보낸 사람 ID 기능은 보낸 사람 ID 에이전트에서 제공됩니다. 보낸 사람 ID 기능은 전자 메일을 보낸 사람 도메인의 알려진 소유자와 대조하여 보낸 사람의 IP 주소를 확인함으로써 전자 메일 메시지의 출처에 대한 유효성을 검사합니다. 보낸 사람 ID 필터링은 인터넷에서 제공되지만 인증되지 않은 인바운드 메시지에 대해 수행됩니다. 이러한 메시지는 외부 메시지로 처리됩니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 보낸 사람 ID를 사용하거나 사용하지 않도록 설정

보낸 사람 ID를 사용하지 않으려면 다음 명령을 실행합니다.

```powershell
Set-SenderIDConfig -Enabled $false
```

보낸 사람 ID를 사용하려면 다음 명령을 실행합니다.

```powershell
Set-SenderIDConfig -Enabled $true
```


> [!NOTE]
> 보낸 사람 ID를 사용하지 않도록 설정하는 경우 기본 보낸 사람 ID 에이전트는 여전히 사용하도록 설정되어 있습니다. 보낸 사람 ID 에이전트를 사용하지 않도록 설정하려면 다음 명령을 실행합니다. <CODE>Disable-TransportAgent "Sender ID Agent"</CODE>.



## 작동 여부는 어떻게 확인합니까?

보낸 사람 ID를 성공적으로 사용하도록 설정하거나 사용하지 않도록 설정했는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-SenderIDConfig | Format-List Enabled
```

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 스푸핑된 메시지에 대한 보낸 사람 ID의 작업 구성

스푸핑된 메시지에 대한 보낸 사람 ID의 작업을 구성하려면 다음 명령을 실행합니다.

```powershell
Set-SenderIDConfig -SpoofedDomainAction <StampStatus | Reject | Delete>
```

이 예에서는 보내는 도메인에 대한 DNS SPF(보낸 사람 정책 프레임워크) 레코드에 보내는 서버의 IP 주소가 신뢰할 수 있는 SMTP 보내는 서버로 나열되지 않은 메시지를 거부하도록 보낸 사람 ID 에이전트를 구성합니다.

```powershell
Set-SenderIDConfig -SpoofedDomainAction Reject
```

## 작동 여부는 어떻게 확인합니까?

스푸핑된 메시지에 대한 보낸 사람 ID의 작업을 성공적으로 구성했는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-SenderIDConfig | Format-List SpoofedDomainAction
```

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 일시적인 오류에 대한 보낸 사람 ID의 작업 구성

일시적인 오류에 대한 보낸 사람 ID의 작업을 구성하려면 다음 명령을 실행합니다.

```powershell
Set-SenderIDConfig -TempErrorAction <StampStatus | Reject | Delete>
```

이 예에서는 일시적인 DNS 서버 오류로 인해 보낸 사람 ID 상태를 확인할 수 없는 메시지를 스탬프 처리하도록 보낸 사람 ID 에이전트를 구성합니다. 메시지는 다른 스팸 방지 에이전트에 의해 처리되며 콘텐츠 필터 에이전트는 메시지에 대한 SCL 값을 확인할 때 이 표시를 사용합니다.

```powershell
Set-SenderIDConfig -TempErrorAction StampStatus
```

`StampStatus`는 *TempErrorAction* 매개 변수의 기본값입니다.

## 작동 여부는 어떻게 확인합니까?

일시적인 오류에 대한 보낸 사람 ID의 작업을 성공적으로 구성했는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-SenderIDConfig | Format-List TempErrorAction
```

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 받는 사람 및 보낸 사람 도메인 예외 구성

기존 값을 바꾸려면 다음 명령을 실행합니다.

    Set-SenderIDConfig -BypassedRecipients <recipient1,recipient2...> -BypassedSenderDomains <domain1,domain2...>

이 예에서는 kim@contoso.com 및 john@contoso.com으로 전송된 메시지에 대한 보낸 사람 ID 확인을 무시하고 fabrikam.com 도메인에서 전송된 메시지에 대한 보낸 사람 ID 확인을 무시하도록 보낸 사람 ID 에이전트를 구성합니다.

    Set-SenderIDConfig -BypassedRecipients kim@contoso.com,john@contoso.com -BypassedSenderDomains fabrikam.com

기존 값을 수정하지 않고 항목을 추가 또는 제거하려면 다음 명령을 실행합니다.

    Set-SenderIDConfig -BypassedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...} -BypassedSenderDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

이 예에서는 다음 정보를 사용하여 보낸 사람 ID 에이전트를 구성합니다.

  - chris@contoso.com 및 michelle@contoso.com을 보낸 사람 ID 확인을 무시하는 기존 받는 사람의 목록에 추가합니다.

  - tailspintoys.com을 보낸 사람 ID 확인을 무시하는 기존 도메인의 목록에서 제거합니다.

<!-- end list -->

    Set-SenderIDConfig -BypassedRecipients @{Add="chris@contoso.com","michelle@contoso.com"} -BypassedSenderDomains @{Remove="tailspintoys.com"}

## 작동 여부는 어떻게 확인합니까?

받는 사람 및 보낸 사람 도메인 예외를 성공적으로 구성했는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
    ```powershell
Get-SenderIDConfig | Format-List BypassedRecipients,BypassedSenderDomains
```

2.  표시된 값이 구성한 값인지 확인합니다.

