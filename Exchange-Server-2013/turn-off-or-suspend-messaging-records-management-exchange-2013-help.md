---
title: '메시징 레코드 관리를 일시 중단 또는 해제: Exchange 2013 Help'
TOCTitle: 메시징 레코드 관리를 일시 중단 또는 해제
ms:assetid: 631191aa-3bba-4ebf-a727-c48ed2ebe176
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa998580(v=EXCHG.150)
ms:contentKeyID: 52058086
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메시징 레코드 관리를 일시 중단 또는 해제

 

_**적용 대상:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-14_

개인, IT 또는 비즈니스 요구 사항을 충족시키기 위해 개인 사용자 또는 사서함 서버용 MRM(메시징 레코드 관리)을 해제하거나 일시적으로 중단해야 할 수도 있습니다. MRM을 해제하거나 일시적으로 중단해야 하는 이유는 다음과 같습니다.

  - 사서함 사용자가 사무실에 없거나 전자 메일에 액세스할 수 없는 경우 사서함을 보존 상대로 두어 사서함의 MRM을 일시적으로 사용하지 않도록 설정할 수 있습니다. 사서함이 보존 상태에 있는 경우 관리되는 폴더 도우미가 더 이상 처리할 수 없습니다. 사서함 사용자가 돌아오거나 사서함에 다시 액세스할 수 있는 경우 사서함에서 보존 상태를 제거할 수 있습니다.

  - 성능 문제를 테스트하거나 해결해야 하는 경우 관리되는 폴더 도우미의 일정을 지워서 일시적으로 해당 서버에서 MRM을 해제할 수 있습니다.

  - 사서함에서 보존 태그(적용된 태그가 있는 보존 정책 포함)를 제거해야 하는 경우 정책에서 태그를 제거할 수 있습니다.

  - 더 이상 사서함에 보존 정책이나 관리되는 폴더 사서함 정책을 적용하지 않으려면 사서함에서 정책을 제거할 수 있습니다.

  - 조직이 MRM 기능을 사용하지 않도록 결정하는 경우 전체 조직에서 MRM을 영구적으로 해제할 수 있습니다. 나중에 MRM을 배포하기로 결정하는 경우 해당 작업을 수행할 수 있습니다.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), 또는 [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)

## 무슨 작업을 하고 싶으십니까?

## 사서함 보존 설정

사서함을 보존 상태로 두어 MRM을 일시적으로 해제할 수 있습니다(예: 사용자가 휴가를 떠나는 경우). 그러면 보존을 사용하지 않도록 설정할 때까지 사서함의 보존 정책의 처리가 일시 중단됩니다. 이는 원본 위치 유지나 소송 보존에 사서함을 배치하는 것과는 다릅니다.

사서함을 보존 상태로 두는 방법에 대한 자세한 내용은 [사서함 보존에 원본 위치 유지](place-a-mailbox-on-retention-hold-exchange-2013-help.md)를 참조하십시오.

원본 위치 유지 및 소송 보존에 대한 자세한 내용은 [원본 위치 유지 및 소송 보존](in-place-hold-and-litigation-hold-exchange-2013-help.md)를 참조하십시오.

## 사서함에서 보존 태그 제거

사서함에서 보존 태그를 제거하려면 보존 정책에서 태그의 연결을 해제합니다. 기본 폴더에 대한 RPT(보존 정책 태그)의 연결을 해제하는 경우 기본 사서함 태그가 해당 폴더의 모든 항목에 적용됩니다. 개인 태그의 연결을 해제하는 경우 해당 사용자가 더 이상 사용할 수 없습니다. 기존의 메시지에 적용된 태그는 사용자가 Exchange 조직에서 태그를 제거하지 않는 한 계속 처리됩니다.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "메시지 레코드 관리" 항목

이 셸의 예에서는 보존 정책 Corp-Users에서 보존 태그 Delete - 3 Days의 연결을 해제합니다.

    $tags = (Get-RetentionPolicy "Corp-Users").RetentionPolicyTagLinks
    $tags -= "Deleted Items - 3 Days"
    Set-RetentionPolicy "Corp-Users" -RetentionPolicyTagLinks $tags

구문과 매개 변수에 대한 자세한 내용은 [Get-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd298086\(v=exchg.150\)) 및 [Set-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd335196\(v=exchg.150\))를 참조하십시오.

## 사서함에서 보존 정책 제거

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "보존 정책 적용" 항목

사서함 사용자의 속성에서 보존 정책을 제거하여 사서함에 대한 보존 정책 적용을 중지할 수 있습니다.

이 셸의 예에서는 사서함 jpeoples에서 보존 정책을 제거합니다.

    Set-Mailbox jpeoples -RetentionPolicy $null.

이 셸의 예에서는 Exchange 조직의 모든 사서함에서 보존 정책을 제거합니다.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -ne $null} | Set-Mailbox -RetentionPolicy $null

이 셸의 예에서는 보존 정책 Corp-Finance를 적용한 모든 사서함 사용자에게서 해당 정책을 제거합니다.

    Get-Mailbox -ResultSize unlimited -Filter {RetentionPolicy -eq "Corp-Finance"} | Set-Mailbox -RetentionPolicy $null

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) 및 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))를 참조하십시오.

## 전체 조직에서 MRM을 영구적으로 해제

조직에 대해 MRM을 해제하려면 Exchange 설치 프로그램에서 만들어진 ArbitrationMailbox 정책을 제외한 모든 보존 태그 및 보존 정책을 삭제합니다. 삭제가 완료되면 보존 정책이 적용되지 않습니다.


> [!WARNING]
> 보존 정책에는 메시지를 사용자의 보관 사서함으로 옮기는 "보관 사서함으로 이동" 태그도 포함됩니다. "보관 사서함으로 이동" 태그가 있는 보존 정책을 제거하면 정책이 적용된 사용자의 메시지는 더 이상 관리되는 폴더 도우미에 의해 보관함으로 이동되지 않습니다.<BR>이를 방지하려면 조직에서 "복구 삭제 및 허용", "영구 삭제" 태그만 제거하고 "보관으로 이동" 태그가 적용된 정책은 유지하십시오. 또는 보관함을 사용하도록 설정된 사용자가 Outlook 또는 Outlook Web App을 사용하여 자신의 보관 사서함으로 항목을 수동으로 이동할 수 있습니다.<BR>보존 태그나 보존 정책을 제거하기 전에 제거할 태그의 설정을 확인하는 것이 좋습니다. "보관으로 이동" 보존 작업이 있는 태그는 삭제하지 마십시오.



이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "메시지 레코드 관리" 항목


> [!NOTE]
> 명령에 의해 수행된 작업을 시뮬레이트하려면 다음 명령에 <EM>WhatIf</EM> 스위치를 포함합니다.



이 예에서는 Exchange 설치 프로그램에서 만들어진 ArbitrationMailbox 정책에 사용되는 "삭제 안 함" 태그를 제외한, Exchange 조직의 모든 삭제 태그를 제거합니다.

    Get-RetentionPolicyTag | ? {$_.RetentionAction -ne "MoveToArchive" -and $_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

이 예에서는 "삭제 안 함" 태그를 제외한 모든 보존 태그를 제거합니다.

    Get-RetentionPolicyTag | ? {$_.Name -ne "Never Delete"} | Remove-RetentionPolicyTag

이 명령에서는 Exchange 조직의 Corp-Users 보존 정책을 제거합니다.

    Remove-RetentionPolicy Corp-Users

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Get-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd298009\(v=exchg.150\))

  - [Remove-RetentionPolicyTag](https://technet.microsoft.com/ko-kr/library/dd335092\(v=exchg.150\))

  - [Remove-RetentionPolicy](https://technet.microsoft.com/ko-kr/library/dd297962\(v=exchg.150\))

