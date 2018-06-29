---
title: '받는 사람 필터링 관리: Exchange 2013 Help'
TOCTitle: 받는 사람 필터링 관리
ms:assetid: a7f4b3e1-2970-45ad-911e-a9f46d880d3d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb124087(v=EXCHG.150)
ms:contentKeyID: 50483897
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람 필터링 관리

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

보낸 사람 필터링은 보낸 사람 필터 에이전트에서 제공됩니다. 보낸 사람 필터 에이전트는 **MAIL FROM:**: SMTP 헤더를 사용하여 인바운드 전자 메일 메시지에 대해 수행할 작업을 확인합니다.

Exchange 서버에서 보낸 사람 필터링 기능을 사용하도록 설정되어 있으면 해당 컴퓨터의 모든 수신 커넥터를 통해 들어오는 메시지가 모두 필터링됩니다.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 보낸 사람 필터링을 사용하거나 사용하지 않도록 설정

보낸 사람 필터링을 사용하지 않으려면 다음 명령을 실행합니다.

    Set-SenderFilterConfig -Enabled $false

보낸 사람 필터링을 사용하도록 설정하려면 다음 명령을 실행합니다.

    Set-SenderFilterConfig -Enabled $true


> [!NOTE]
> 보낸 사람 필터링을 사용하지 않도록 설정하더라도 기본 보낸 사람 필터 에이전트는 그대로 사용됩니다. 이 보낸 사람 필터 에이전트를 사용하지 않도록 설정하려면 다음 명령을 실행합니다. <CODE>Disable-TransportAgent "Sender Filter Agent"</CODE>.



## 작동 여부는 어떻게 확인합니까?

보낸 사람 필터링을 사용하거나 사용하지 않도록 성공적으로 설정했는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
        Get-SenderFilterConfig | Format-List Enabled

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 수신 거부 및 도메인 구성

기존 값을 바꾸려면 다음 명령을 실행합니다.

    Set-SenderFilterConfig -BlockedSenders <sender1,sender2...> -BlockedDomains <domain1,domain2...> -BlockedDomainsAndSubdomains <domain1,domain2...>

다음 예에서는 kim@contoso.com 및 john@contoso.com의 메시지, fabrikam.com 도메인의 메시지, northwindtraders.com 및 모든 하위 도메인의 메시지를 차단하도록 보낸 사람 필터 에이전트를 구성합니다.

    Set-SenderFilterConfig -BlockedSenders kim@contoso.com,john@contoso.com -BlockedDomains fabrikam.com -BlockedDomainsAndSubdomains northwindtraders.com

기존 값을 수정하지 않고 항목을 추가 또는 제거하려면 다음 명령을 실행합니다.

    Set-SenderFilterConfig -BlockedSenders @{Add="<sender1>","<sender2>"...; Remove="<sender1>","<sender2>"...} -BlockedDomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...} -BlockedDomainsAndSubdomains @{Add="<domain1>","<domain2>"...; Remove="<domain1>","<domain2>"...}

다음 예에서는 아래 정보를 사용하여 보낸 사람 필터 에이전트를 구성합니다.

  - chris@contoso.com 및 michelle@contoso.com을 기존 수신 거부 목록에 추가합니다.

  - tailspintoys.com을 기존 수신 거부 도메인 목록에서 제거합니다.

  - blueyonderairlines.com을 기존 수신 거부 도메인 및 하위 도메인 목록에 추가합니다.

<!-- end list -->

    Set-SenderFilterConfig -BlockedSenders @{Add="chris@contoso.com","michelle@contoso.com"} -BlockedDomains @{Remove="tailspintoys.com"} -BlockedDomainsAndSubdomains @{Add="blueyonderairlines.com"}

## 작동 여부는 어떻게 확인합니까?

수신 거부 목록이 성공적으로 구성되었는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
        Get-SenderFilterConfig | Format-List BlockedSenders,BlockedDomains,BlockedDomainsAndSubdomains

2.  표시된 값이 구성한 값인지 확인합니다.

## 셸을 사용하여 보낸 사람이 비어 있는 메시지 차단을 사용하거나 사용하지 않도록 설정

보낸 사람이 비어 있는 메시지 차단을 사용하거나 사용하지 않도록 설정하려면 다음 명령을 실행합니다.

    Set-SenderFilterConfig -BlankSenderBlockingenabled <$true | $false>

다음 예에서는 MAIL: FROM SMTP 명령에서 보낸 사람이 지정되지 않은 메시지를 차단하도록 보낸 사람 필터 에이전트를 구성합니다.

    Set-SenderFilterConfig -BlankSenderBlockingEnabled $true

## 작동 여부는 어떻게 확인합니까?

보낸 사람이 비어 있는 메시지 차단을 사용하거나 사용하지 않도록 성공적으로 설정했는지 확인하려면 다음을 수행하십시오.

1.  다음 명령을 실행합니다.
    
        Get-SenderFilterConfig | Format-List BlankSenderBlockingEnabled

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

