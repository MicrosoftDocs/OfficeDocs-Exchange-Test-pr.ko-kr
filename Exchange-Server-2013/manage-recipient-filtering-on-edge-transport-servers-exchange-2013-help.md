---
title: 'Edge 전송 서버의 받는 사람 필터링 관리: Exchange 2013 Help'
TOCTitle: Edge 전송 서버의 받는 사람 필터링 관리
ms:assetid: f2d0041f-2872-4669-95ec-443233f4956d
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb125187(v=EXCHG.150)
ms:contentKeyID: 50484524
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Edge 전송 서버의 받는 사람 필터링 관리

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2015-04-08_

받는 사람 필터링은 받는 사람 필터 에이전트에서 제공됩니다. Exchange 서버에서 받는 사람 필터링이 사용 가능하게 설정되면 인터넷에서 오는 인증되지 않은 인바운드 메시지를 필터링합니다. 이러한 메시지는 외부 메시지로 처리됩니다.


> [!NOTE]
> 받는 사람 필터 에이전트를 사서함 서버에서 사용할 수 있지만 이를 구성할 수는 없습니다. 사서함 서버의 받는 사람 필터링을 통해 다른 유효한 받는 사람이 포함된 메시지에서 잘못되거나 차단된 받는 사람이 검색된 경우에는 메시지가 거부됩니다. 사서함 서버에 스팸 방지 에이전트를 설치하면 받는 사람 필터 에이전트가 기본적으로 사용됩니다. 그러나 받는 사람을 차단하도록 구성되지는 않습니다. 자세한 내용은 <A href="enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md">사서함 서버에서 스팸 방지 기능을 사용 하도록 설정</A>를 참조하세요.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [스팸 방지 및 맬웨어 방지 사용 권한](anti-spam-and-anti-malware-permissions-exchange-2013-help.md)의 "스팸 방지 기능" 항목

  - 이 절차는 셸을 사용해야 수행할 수 있습니다.

  - 기본적으로 스팸 방지 기능은 사서함 서버의 전송 서비스에서 사용되지 않도록 설정되어 있습니다. 일반적으로 Exchange 조직에서 들어오는 메시지를 수락하기 전에 스팸 방지 필터링을 미리 수행하지 않은 경우에만 사서함 서버에서 스팸 방지 기능을 사용하도록 설정할 수 있습니다. 자세한 내용은 [사서함 서버에서 스팸 방지 기능을 사용 하도록 설정](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md)을 참조하세요.

  - **Set-AcceptedDomain** cmdlet의 *AddressBookEnabled* 매개 변수는 허용 도메인의 받는 사람에 대한 받는 사람 필터링을 사용하거나 사용하지 않도록 설정합니다. 기본적으로 받는 사람 필터링은 신뢰할 수 있는 도메인에 대해 사용되도록 설정되고, 내부 릴레이 도메인 및 외부 릴레이 도메인에 대해 사용되지 않도록 설정됩니다. 조직의 허용 도메인에 대한 *AddressBookEnabled* 매개 변수의 상태를 보려면 다음 명령을 실행합니다.
    
        Get-AcceptedDomain | Format-List Name,AddressBookEnabled

  - 이 항목의 절차를 사용하여 받는 사람 필터링을 사용되지 않게 설정하면 필터링 기능이 사용되지 않지만 기본 받는 사람 필터 에이전트는 사용됩니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 받는 사람 필터링을 사용하거나 사용하지 않도록 설정

받는 사람 필터링을 사용하지 않으려면 다음 명령을 실행합니다.

    Set-RecipientFilterConfig -Enabled $false

받는 사람 필터링을 사용하려면 다음 명령을 실행합니다.

    Set-RecipientFilterConfig -Enabled $true


> [!NOTE]
> 받는 사람 필터링을 사용하지 않을 경우 기본 받는 사람 필터 에이전트는 여전히 사용됩니다. 받는 사람 필터 에이전트를 사용하지 않도록 설정하려면 다음 명령을 실행합니다. <CODE>Disable-TransportAgent "Recipient Filter Agent"</CODE>.



## 작동 여부는 어떻게 확인합니까?

받는 사람 필터링이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-RecipientFilterConfig | Format-List Enabled

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 받는 사람 차단 목록을 사용하거나 사용하지 않도록 설정

다음 명령을 실행합니다.

    Set-RecipientFilterConfig -BlockListEnabled <$true | $false>

이 예에서는 받는 사람 차단 목록을 사용하도록 설정합니다.

    Set-RecipientFilterConfig -BlockListEnabled $true

## 작동 여부는 어떻게 확인합니까?

받는 사람 차단 목록이 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-RecipientFilterConfig | Format-List BlockListEnabled

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 받는 사람 차단 목록 구성

기존 값을 바꾸려면 다음 명령을 실행합니다.

    Set-RecipientFilterConfig -BlockedRecipients <recipient1,recipient2...>

이 예에서는 valuesmark@contoso.com 및 kim@contoso.com을 사용하여 받는 사람 차단 목록을 구성합니다.

    Set-RecipientFilterConfig -BlockedRecipients mark@contoso.com,kim@contoso.com

기존 값을 수정하지 않고 항목을 추가 또는 제거하려면 다음 명령을 실행합니다.

    Set-RecipientFilterConfig -BlockedRecipients @{Add="<recipient1>","<recipient2>"...; Remove="<recipient1>","<recipient2>"...}

이 예에서는 받는 사람 차단 목록의 받는 사람 목록에 chris@contoso.com을 추가하고 받는 사람 목록에서 michelle@contoso.com을 제거합니다.

    Set-RecipientFilterConfig -BlockedRecipients @{Add="chris@contoso.com"; Remove="michelle@contoso.com"}

## 작동 여부는 어떻게 확인합니까?

받는 사람 차단 목록이 구성되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-RecipientFilterConfig | Format-List BlockedRecipients

2.  표시된 값이 구성한 값인지 확인합니다.

## 셸을 사용하여 받는 사람 조회를 사용하거나 사용하지 않도록 설정

다음 명령을 실행합니다.

    Set-RecipientFilterConfig -RecipientValidationEnabled <$true | $false>

조직에 없는 받는 사람에게 보내는 메시지를 차단하려면 다음 명령을 실행합니다.

    Set-RecipientFilterConfig -RecipientValidationEnabled $true

## 작동 여부는 어떻게 확인합니까?

받는 사람 조회가 사용하거나 사용하지 않도록 설정되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-RecipientFilterConfig | Format-List RecipientValidationEnabled

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

