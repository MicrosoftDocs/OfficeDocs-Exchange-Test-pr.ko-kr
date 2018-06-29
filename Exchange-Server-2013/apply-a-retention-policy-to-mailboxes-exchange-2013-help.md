---
title: '사서함에 보존 정책 적용: Exchange 2013 Help'
TOCTitle: 사서함에 보존 정책 적용
ms:assetid: 6ccc80db-d201-44f7-8d4b-473a89c14b2f
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Dd298052(v=EXCHG.150)
ms:contentKeyID: 50483391
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 보존 정책 적용

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-10-01_

보존 정책을 사용하여 하나 이상의 보존 태그를 그룹화하고 이를 사서함에 적용하여 메시지 보존 설정을 적용할 수 있습니다. 사서함에는 둘 이상의 보존 정책을 적용할 수 없습니다.


> [!WARNING]
> 메시지는 정책에 연결된 보존 태그에 정의된 설정을 기반으로 하여 만료됩니다. 이러한 설정에는 메시지를 보관함으로 이동하거나 영구적으로 삭제하는 등의 작업이 포함됩니다. 하나 이상의 사서함에 보존 정책을 적용하기 전에 정책을 테스트하고 정책과 연결된 각 보존 태그를 검사하는 것이 좋습니다.



MRM(메시징 레코드 관리)과 관련된 추가 관리 작업에 대한 자세한 내용은 [메시징 레코드 관리 절차](messaging-records-management-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [메시징 정책 및 규정 준수 권한](messaging-policy-and-compliance-permissions-exchange-2013-help.md)의 "보존 정책 적용" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 단일 사서함에 보존 정책 적용

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 보존 정책을 적용할 사서함을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **사용자 사서함**에서 **사서함 기능**을 클릭합니다.

4.  **보존 정책** 목록에서 사서함에 적용할 정책을 선택하고 **저장**을 클릭합니다.

## EAC를 사용하여 여러 사서함에 보존 정책 적용

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 Shift 또는 Ctrl 키를 사용하여 여러 개의 사서함을 선택합니다.

3.  세부 정보 창에서 **기타 옵션**을 클릭합니다.

4.  **보존 정책**에서 **업데이트**를 클릭합니다.

5.  **보존 정책 대량 할당**에서 사서함에 적용할 보존 정책을 선택하고 **저장**을 클릭합니다.

## 셸을 사용하여 단일 사서함에 보존 정책 적용

이한일의 사서함에 보존 정책 Rp-finance를 적용 하는이 예제입니다.

    Set-Mailbox "Morris" -RetentionPolicy "RP-Finance"

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 여러 사서함에 보존 정책 적용

이 예에서는 기존 정책 Old-Retention-Policy가 있는 모든 사서함에 새 보존 정책 New-Retention-Policy를 적용합니다.

    $OldPolicy={Get-RetentionPolicy "Old-Retention-Policy"}.distinguishedName
    Get-Mailbox -Filter {RetentionPolicy -eq $OldPolicy} -Resultsize Unlimited | Set-Mailbox -RetentionPolicy "New-Retention-Policy"

이 예에서는 RetentionPolicy-Corp이라는 보존 정책을 Exchange 조직의 모든 사서함에 적용합니다.

    Get-Mailbox -ResultSize unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Corp"

이 예에서는 RetentionPolicy-Finance라는 보존 정책을 Finance 조직 구성 단위의 모든 사서함에 적용합니다.

    Get-Mailbox -OrganizationalUnit "Finance" -ResultSize Unlimited | Set-Mailbox -RetentionPolicy "RetentionPolicy-Finance"

구문과 매개 변수에 대한 자세한 내용은 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) 및 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

보존 정책이 적용되었는지 확인하려면 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\)) cmdlet을 사용하여 사서함에 대한 보존 정책을 검색합니다.

이 예에서는 Morris의 사서함에 대 한 보존 정책을 검색 합니다.

    Get-Mailbox Morris | Select RetentionPolicy

이 명령은 RP-Finance라는 보존 정책이 적용된 사서함을 모두 검색합니다.

    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionPolicy -eq "RP-Finance"} | Format-Table Name,RetentionPolicy -Auto

