---
title: '사서함 보존에 원본 위치 유지: Exchange 2013 Help'
TOCTitle: 사서함 보존에 원본 위치 유지
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 50482700
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함 보존에 원본 위치 유지

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-14_

사서함을 보존 상태로 두면 해당 사서함의 보존 정책 또는 관리되는 폴더 사서함 정책의 처리를 일시 중단합니다. 보존은 사용자가 휴가 중이거나 임시로 자리를 비울 때와 같은 시나리오를 위해 디자인되었습니다.

보존 중일 때 사용자는 자신의 사서함에 로그온하여 항목을 변경하거나 삭제할 수 있습니다. 사서함 검색을 수행할 경우 삭제 항목 보존 기간을 경과한 삭제 항목은 검색 결과에 반환되지 않습니다. 법적 보유가 필요한 상황에서 사용자가 변경하거나 삭제한 항목을 보유하려면 사서함을 법적 보유 상태로 두어야 합니다. 자세한 내용은 [만들기 또는 In-place Hold 제거](create-or-remove-an-in-place-hold-exchange-2013-help.md) 항목을 참조하십시오.

보존 상태로 둔 사서함에 보존 설명을 추가할 수도 있습니다. 설명은 지원되는 버전의 Microsoft Outlook에 표시됩니다.

MRM(메시징 레코드 관리)과 관련된 추가 관리 작업에 대한 자세한 내용은 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 1분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md) 항목의 "메시징 레코드 관리" 항목

  - 사서함을 보존 상태로 전환하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 사서함을 보존 상태로 두기

다음은 Michael Allen의 사서함을 보존 상태로 두는 예입니다.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) 항목을 참조하십시오.

## 셸을 사용하여 사서함의 보존 상태 제거

다음은 Michael Allen의 사서함에서 보존 상태를 제거하는 예입니다.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) 항목을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함을 성공적으로 보존 상태로 전환했는지 확인하려면 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) cmdlet을 사용하여 사서함의 *RetentionHoldEnabled* 속성을 검색합니다.

이 명령은 Michael Allen의 사서함에 대한 *RetentionHoldEnabled* 속성을 검색합니다.

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

이 명령은 Exchange 조직에서 모든 사서함을 검색하고, 보존 상태인 사서함을 필터링하고, 각각에 적용된 보존 정책과 함께 이를 나열합니다.


> [!IMPORTANT]
> <EM>RetentionHoldEnabled</EM>는 Exchange 2013의 필터링 가능 속성이 아니기 때문에 <EM>Filter</EM> 매개 변수와 <STRONG>Get-Mailbox</STRONG> cmdlet을 사용하여 서버 측에서 보존 상태가 된 사서함을 필터링할 수 없습니다. 이 명령은 셸 세션을 실행하는 클라이언트에서 모든 사서함 및 필터의 목록을 검색합니다. 사서함이 수천 개인 대규모 환경에서는 이 명령이 완료되는 데 오래 걸릴 수 있습니다.



    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

