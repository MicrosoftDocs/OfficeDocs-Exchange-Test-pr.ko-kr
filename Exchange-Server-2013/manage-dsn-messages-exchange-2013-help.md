---
title: 'DSN 메시지 관리: Exchange 2013 Help'
TOCTitle: DSN 메시지 관리
ms:assetid: 23c9d844-6fc7-44c9-a308-587338281611
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996803(v=EXCHG.150)
ms:contentKeyID: 50482663
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# DSN 메시지 관리

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-20_

Microsoft Exchange Server 2013에서는 DSN(배달 상태 알림)을 사용하여 메시지를 보낸 사람에게 배달 못 함 보고서(NDR) 및 기타 상태 메시지를 제공합니다. 기본 제공 DSN을 사용하거나 조직의 필요에 맞게 사용자 지정 DSN 메시지를 만들 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 15분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메일 흐름 사용 권한](mail-flow-permissions-exchange-2013-help.md)의 "DSN" 항목

  - Exchange에 포함된 기본 제공 DSN 메시지는 제거할 수 없습니다. 기본 제공 DSN 메시지를 변경하려면 사용자 지정할 DSN 코드에 대한 사용자 지정 DSN 메시지를 만들어야 합니다. 사용자 지정 DSN 메시지를 제거하면 해당 메시지와 연결된 DSN 코드는 Exchange에 포함된 기본 제공 DSN 메시지로 되돌아갑니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 기본 제공 및 사용자 지정 DSN 메시지 보기

Exchange 2013에 포함된 모든 기본 제공 DSN 메시지의 요약 목록을 보려면 다음 명령을 실행합니다.

    Get-SystemMessage -Original

조직의 모든 사용자 지정 DSN 메시지의 요약 목록을 보려면 다음 명령을 실행합니다.

    Get-SystemMessage

내부 보낸 사람에게 영어로 전송된 DSN 코드 5.1.2에 대한 사용자 지정 DSN 메시지의 자세한 정보를 보려면 다음 명령을 실행합니다.

    Get-SystemMessage En\Internal\5.1.2 | Format-List

## 셸을 사용하여 사용자 지정 DSN 메시지 만들기

다음 명령을 실행합니다.

    New-SystemMessage -Internal <$true | $false> -Language <Locale> -DSNCode <x.y.z> -Text "<DSN text>"

이 예에서는 영어로 내부 보낸 사람에게 전송된 DSN 코드 5.1.2에 대한 사용자 지정 일반 텍스트 DSN 메시지를 만듭니다.

    New-SystemMessage -Internal $true -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

이 예에서는 영어로 외부 보낸 사람에게 전송된 DSN 코드 5.1.2에 대한 사용자 지정 일반 텍스트 DSN 메시지를 만듭니다.

    New-SystemMessage -Internal $false -Language En -DSNCode 5.1.2 -Text "You tried to send a message to a disabled mailbox that's no longer accepting messages. Please contact your System Administrator for more information."

이 예에서는 영어로 내부 보낸 사람에게 전송된 DSN 코드 5.1.2에 대한 사용자 지정 HTML DSN 메시지를 만듭니다.

    New-SystemMessage -DSNCode 5.1.2 -Internal $true -Language En -Text 'You tried to send a message to a <B>disabled</B> mailbox. Please visit <A HREF="http://it.contoso.com">Internal Support</A> or contact &quot;InfoSec&quot; for more information.'

## 작동 여부는 어떻게 확인합니까?

사용자 지정 DNS 메시지가 만들어졌는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다.
    
        Get-SystemMessge -DSNCode <x.y.z> | Format-List Name,Internal,Text,Language

2.  표시된 값이 구성한 값인지 확인합니다.

3.  구성한 사용자 지정 DSN을 생성하는 테스트 메시지를 보냅니다.

## 셸을 사용하여 사용자 지정 DSN 메시지의 텍스트 변경

사용자 지정 DSN 메시지의 텍스트를 변경하려면 다음 명령을 사용합니다.

    Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> -Text "<DSN text>"

이 예에서는 내부 보낸 사람에게 영어로 전송된 DSN 코드 5.1.2에 대한 사용자 지정 DSN 메시지에 할당된 텍스트를 변경합니다.

    Set-SystemMessage En\Internal\5.1.2 -Text "The mailbox you tried to send an e-mail message to is disabled and is no longer accepting messages. Please contact the Help Desk at extension 123 for assistance."

## 작동 여부는 어떻게 확인합니까?

사용자 지정 DNS 메시지의 텍스트가 변경되었는지 확인하려면 다음을 수행합니다.

1.  다음 명령을 실행합니다. `Get-SystemMessage`.
    
        Set-SystemMessage <Locale>\<Internal | External>\<DSNcode> | Format-List -Text

2.  표시되는 값이 자신이 구성한 값인지 확인합니다.

## 셸을 사용하여 사용자 지정 DSN 메시지 제거

다음 명령을 실행합니다.

    Remove-SystemMessage <Local>\<Internal | External>\<DSNcode>

이 예에서는 영어로 내부 보낸 사람에게 전송된 DSN 코드 5.1.2에 대한 사용자 지정 DSN 메시지를 제거합니다.

    Remove-SystemMessage En\Internal\5.1.2

## 작동 여부는 어떻게 확인합니까?

사용자 지정 DNS 메시지가 제거되었는지 확인하려면 다음을 수행합니다.

1.  명령을 실행합니다. `Get-SystemMessage`.

2.  로캘, 내부 또는 외부 받는 사람에 대한 DSN 및 삭제한 DSN 코드가 나열되지 않는지 확인합니다.

## DSN 메시지의 복사본을 Exchange 받는 사람 사서함으로 전달

DSN 메시지가 Exchange 받는 사람의 사서함으로 복사되도록 하여 모니터링할 DSN 코드의 목록을 지정할 수 있습니다. 하지만 기본적으로 Exchange 받는 사람에게 사서함이 할당되지 않으므로 Exchange 받는 사람에게 전송된 메시지가 삭제됩니다. DSN 메시지의 복사본을 Exchange 받는 사람 사서함으로 보내려면 Exchange 받는 사람에게 사서함을 할당한 다음 모니터링할 DSN 코드를 지정해야 합니다. 기본적으로 다음 DSN 코드가 모니터링됩니다. `5.4.8`, `5.4.6`, `5.4.4`, `5.2.4`, `5.2.0` 및 `5.1.4`입니다.

## 1단계: 셸을 사용하여 Exchange 받는 사람에게 사서함 할당

Exchange 받는 사람에게 사서함을 할당하려면 다음 단계를 수행합니다.

1.  전자 메일의 양이 많아질 수 있으므로 Exchange 받는 사람에 대한 전용 사서함 및 Active Directory 사용자 계정을 만드는 것을 고려하십시오. 자세한 내용은 [사용자 사서함 만들기](create-user-mailboxes-exchange-2013-help.md)를 참조하십시오. 또는 Exchange 받는 사람과 연결할 기존 사서함을 찾습니다.

2.  다음 명령을 실행합니다.
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient <MailboxIdentity>
    
    예를 들어 Exchange 받는 사람에게 "Contoso System Mailbox"라는 기존 사서함을 할당하려면 다음 명령을 실행합니다.
    
        Set-OrganizationConfig -MicrosoftExchangeRecipientReplyRecipient "Contoso System Mailbox"

## 2단계: 모니터링할 DSN 코드 지정

## EAC를 사용하여 DSN 코드 지정

1.  EAC에서 **메일 흐름** \> **수신 커넥터** \> **기타 옵션**![기타 옵션 아이콘](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "기타 옵션 아이콘") \> **조직 전송 설정** \> **배달**로 이동합니다.

2.  **DNS 코드** 섹션에서 *\<x.y.z\>* 형식을 사용하여 모니터링할 DSN 코드를 입력하고 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭합니다. 기존 항목을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하여 수정하거나 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하여 제거합니다. 작업을 마치면 **저장**을 클릭합니다.

## 셸을 사용하여 DSN 코드 지정

기존 값을 바꾸려면 다음 명령을 실행합니다.

    Set-TransportConfig -GenerateCopyOfDSNFor <x.y.z>,<x.y.z>...

이 예에서는 DSN 코드가 5.7.1, 5.7.2 및 5.7.3인 DSN 메시지를 모두 Exchange 받는 사람에게 전달하도록 Exchange 조직을 구성합니다.

    Set-TransportConfig -GenerateCopyOfDSNFor 5.7.1,5.7.2,5.7.3

기존 값을 수정하지 않고 항목을 추가 또는 제거하려면 다음 명령을 실행합니다.

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="<x.y.z>","<x.y.z>"...; Remove="<x.y.z>","<x.y.z>"...}

이 예에서는 DSN 코드 5.7.5를 추가하고 Exchange 받는 사람에게 전달되는 DSN 메시지의 기존 목록에서 DSN 코드 5.7.1을 제거합니다.

    Set-TransportConfig -GenerateCopyOfDSNFor @{Add="5.7.5"; Remove="5.7.1"}

## 작동 여부는 어떻게 확인합니까?

DNS 메시지의 복사본을 Exchange 받는 사람의 사서함으로 전송하도록 구성되었는지 확인하려면 Exchange 받는 사람과 연결된 사서함을 모니터링하고 DSN 메시지에 지정한 DSN 코드가 포함되어 있는지 확인합니다.

