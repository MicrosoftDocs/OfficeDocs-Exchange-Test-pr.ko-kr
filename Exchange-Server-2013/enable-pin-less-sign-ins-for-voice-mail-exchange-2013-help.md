---
title: '음성 메일에 대 한 PIN이 필요 없는 로그인을 사용 하도록 설정: Exchange 2013 Help'
TOCTitle: 음성 메일에 대 한 PIN이 필요 없는 로그인을 사용 하도록 설정
ms:assetid: 54133753-317c-42ef-9b0d-ca9f2d2d6bd7
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Gg602127(v=EXCHG.150)
ms:contentKeyID: 54651814
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 음성 메일에 대 한 PIN이 필요 없는 로그인을 사용 하도록 설정

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**마지막으로 수정된 항목:** 2015-04-08_

사용자가 PIN을 사용하지 않고 음성 메일에 로그인할 수 있도록 UM(통합 메시징)을 설정할 수 있습니다. 기본적으로 Outlook Voice Access 사용자가 사서함에 로그인하여 음성 메일, 전자 메일, 일정, 개인 연락처, 디렉터리 및 개인 옵션에 액세스하려고 하면 PIN을 입력하라는 메시지가 표시됩니다.

<table>
<thead>
<tr class="header">
<th><img src="images/Bb125224.warning(EXCHG.150).gif" title="경고" alt="경고" />경고:</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>음성 메일을 사용할 수 있는 단일 사용자나 사용자 그룹에 대해 PIN 없이 로그인할 수 있도록 설정하면 음성 메일의 보안 수준이 떨어지고 조직이 보안 위험에 노출될 수 있습니다.</td>
</tr>
</tbody>
</table>


PIN 없는 로그인을 사용하도록 설정하려면 UM 사서함 정책에서 매개 변수 *AllowPinlessVoiceMailAccess*를 `$true`로 설정하고 UM 사서함에서 매개 변수 *PinlessAccessToVoiceMailEnabled*를 `$true`로 설정해야 합니다. 기본적으로 두 매개 변수 모두 `$false`로 설정되므로, Outlook Voice Access 사용자는 음성 메일에 액세스할 때 PIN을 입력해야 합니다.

두 매개 변수를 `$true`로 설정하면 UM 사서함과 연결된 대규모 사용자 그룹의 음성 메일에 대해 PIN 없는 로그인을 사용하도록 설정할 수 있으며, 단일 UM 사서함 또는 UM 사서함의 하위 집합에 대해서도 PIN 없는 로그인을 사용하도록 설정할 수 있습니다. UM 사용 가능 사용자 그룹 또는 단일 UM 사용 가능 사용자의 음성 메일에 대해 PIN 없는 로그인을 사용하도록 설정하더라도 전자 메일, 일정, 개인 연락처, 디렉터리 또는 개인 옵션에 액세스하면 PIN을 입력하라는 메시지가 표시됩니다.

사용자의 음성 메일에 대해 PIN 없는 로그인을 사용하도록 설정하려면 다음 조건이 충족되어야 합니다.

  - UM 사서함 정책에서 다음 cmdlet을 실행해야 합니다. `Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true`

  - UM 사용 가능 사용자의 사서함에서 다음 cmdlet을 실행해야 합니다. `Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true`

  - UM 사용 가능 사용자를 PIN 없는 로그인을 사용하도록 설정한 동일한 UM 사서함 정책과 연결합니다.

  - UM 사용 가능 사용자가 자신에게 할당된 전화 번호로 Outlook Voice Access에 전화를 겁니다.

  - 이 절차는 셸을 사용해야 수행할 수 있습니다. 온-프레미스 Exchange 조직에서 Exchange 관리 셸을 여는 방법을 확인하려면 organization, see [셸을 엽니다.](https://technet.microsoft.com/ko-kr/library/dd638134\(v=exchg.150\))을 참조하세요. Windows PowerShell을 사용하여 Exchange Online에 연결하는 방법을 알아보려면 [Exchange Online PowerShell에 연결](https://go.microsoft.com/fwlink/p/?linkid=396554)을 참조하세요.

UM 사서함 정책과 관련된 추가 작업에 대한 자세한 내용은 [UM 사서함 정책 절차](um-mailbox-policy-procedures-exchange-2013-help.md)를 참조하십시오.

UM 사서함과 관련된 추가 작업에 대한 자세한 내용은 [음성 메일 사용이 가능한 사용자 절차](voice-mail-enabled-user-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 3분

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함 정책" 항목

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [통합된 메시징 사용 권한](unified-messaging-permissions-exchange-2013-help.md)의 "UM 사서함" 항목

  - 이러한 절차를 수행하기 전에 UM 다이얼 플랜을 만들었는지 확인합니다. 자세한 단계는 [UM 다이얼 플랜 만들기](create-a-um-dial-plan-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 UM 사서함 정책을 만들었는지 확인합니다. 자세한 단계는 [UM 사서함 정책 만들기](create-a-um-mailbox-policy-exchange-2013-help.md)를 참조하십시오.

  - 이러한 절차를 수행하기 전에 사용자가 UM 및 음성 메일을 사용할 수 있는지 확인하십시오. 자세한 단계는 [음성 메일에 대 한 사용자를 사용 하도록 설정](enable-a-user-for-voice-mail-exchange-2013-help.md)을 참조하십시오.

## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 UM 사서함 정책에서 UM 사용 가능 사용자의 음성 메일에 PIN 없는 액세스가 가능하도록 설정

이 예에서는 Outlook Voice Access로 전화를 거는 사서함 정책과 연결된 사용자에 대해 `MyUMMailboxPolicy`라는 UM 사서함 정책에서 PIN 없는 음성 메일 액세스를 사용하도록 설정합니다.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowPinlessVoiceMailAccess $true

## 셸을 사용하여 UM 사용 가능 사용자의 사서함에서 음성 메일 대해 PIN 없는 액세스가 가능하도록 설정

이 예에서는 Outlook Voice Access로 전화를 걸어 `tonys@contoso.com`이라는 사서함에 연결하는 사용자에 대해 PIN 없는 음성 메일 액세스를 사용하도록 설정합니다.

    Set-UMMailbox -id tonys@contoso.com -PinlessAccessToVoiceMailEnabled $true

