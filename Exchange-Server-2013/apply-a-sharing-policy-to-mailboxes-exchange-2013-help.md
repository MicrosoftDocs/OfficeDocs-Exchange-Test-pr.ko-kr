---
title: '사서함에 공유 정책 적용: Exchange 2013 Help'
TOCTitle: 사서함에 공유 정책 적용
ms:assetid: dd4cc765-8469-4176-bb6e-d5b0f5235927
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657501(v=EXCHG.150)
ms:contentKeyID: 50484306
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 공유 정책 적용

 

_**적용 대상:**Exchange Server 2013_

_**마지막으로 수정된 항목:**2014-02-15_

공유 정책은 페더레이션 공유의 일부로, 일정 정보를 여러 유형의 외부 사용자와 함께 사용자가 설정한 대로 사용자 간에 공유할 수 있도록 합니다. 관리자가 사용자 사서함에 적용하는 공유 정책에 따라 사용자가 공유할 수 있는 액세스 권한 수준 및 공유 대상이 결정됩니다. 아무 항목도 변경하지 않으면 기본 공유 정책이 모든 사용자에게 적용됩니다. 직접 만든 공유 정책은 사서함에 적용해야 유효한 상태가 됩니다. 공유 정책을 단일 사용자 사서함에 적용하거나 동시에 여러 사용자 사서함에 적용할 수 있습니다. 관리자는 사용자의 공유 정책을 사용하지 않도록 설정하여 일정에 대한 외부 액세스를 금지할 수도 있습니다.

페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 *Recipient Provisioning Permissions* 항목을 참조하십시오.

  - 공유 정책은 반드시 있어야 합니다. 자세한 내용은 [공유 정책 만들기](create-a-sharing-policy-exchange-2013-help.md)를 참조하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 단일 사서함에 공유 정책 적용

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 원하는 사서함을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **사용자 사서함**에서 **사서함 기능**을 클릭합니다.

4.  **공유 정책** 목록에서 이 사서함에 적용하려는 공유 정책을 선택합니다.

5.  **저장**을 클릭하여 공유 정책을 적용합니다.

## EAC를 사용하여 여러 사서함에 공유 정책 적용

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 Ctrl 키를 누른 상태로 여러 사서함을 선택합니다.

3.  세부 정보 창에서 사서함 속성은 대량 편집이 가능하게 구성됩니다. **기타 옵션**을 클릭합니다.

4.  **공유 정책**에서 **업데이트**를 클릭합니다.

5.  **공유 정책 일괄 할당**에서 **공유 정책 선택** 목록을 사용하여 사서함에 할당할 공유 정책을 선택합니다.

6.  **저장**을 클릭하여 선택한 사서함에 공유 정책을 적용합니다.

## 셸을 사용하여 하나 이상의 사서함에 공유 정책 적용

이 예제는 사용자 Barbara의 단일 사서함에 Contoso 공유 정책을 적용합니다.

    Set-Mailbox -Identity Barbara -SharingPolicy "Contoso"

이 예에서는 Marketing 부서의 모든 사용자 사서함이 Contoso Marketing 공유 정책을 사용하도록 지정합니다.

    Get-Mailbox -Filter {Department -eq "Marketing"} | Set-Mailbox -SharingPolicy "Contoso Marketing"

이 예에서는 공유 Contoso 공유 정책이 적용된 모든 사서함을 반환하고 사용자를 별칭과 전자 메일 주소만 표시하는 테이블로 정렬합니다.

    Get-Mailbox -ResultSize unlimited | Where {$_.SharingPolicy -eq "Contoso" } | format-table Alias, EmailAddresses

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) 및 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))을 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사용자 사서함에 공유 정책을 성공적으로 적용했는지 확인하려면 다음 중 하나를 수행합니다.

  - EAC에서 **받는 사람** \> **사서함**으로 이동한 다음 공유 정책을 적용한 사서함을 선택합니다. **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭하고 **사서함 기능**을 클릭한 다음 **공유 정책** 목록에 올바른 공유 정책이 표시되는지 확인합니다.

  - 다음 셸 명령을 실행하여 공유 정책이 사용자 사서함에 할당되었는지 확인합니다. 올바른 공유 정책이 *SharingPolicy* 매개 변수에 표시되는지 확인합니다.
    
        Get-Mailbox <user name> | format-list


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


