---
title: '수정, 비활성화 또는 공유 정책 제거: Exchange 2013 Help'
TOCTitle: 수정, 비활성화 또는 공유 정책 제거
ms:assetid: 714af42d-ca29-4bb4-ac48-f0b3d4fd1c15
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ657460(v=EXCHG.150)
ms:contentKeyID: 50483346
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 수정, 비활성화 또는 공유 정책 제거

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-02-15_

Exchange 조직의 개별 사용자는 공유 정책을 사용하여 다른 페더레이션 Exchange 조직, 페더레이션되지 않은 Exchange 조직 및 개별 인터넷 사용자와 약속 있음/없음 일정 정보를 공유할 수 있습니다. 일반적인 작업을 수행하는 동안 공유 규칙 수정, 약속 있음/없음 액세스 수준 변경, 일시적으로 공유 정책을 사용하지 않도록 설정 또는 공유 정책을 완전히 제거와 같이 일부 공유 정책 속성을 변경하려고 할 수 있습니다.

페더레이션 공유에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md) 항목을 참조하십시오.

공유 정책을 만드는 방법에 대한 자세한 내용은 [공유 정책 만들기](create-a-sharing-policy-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md) 항목의 "일정 및 공유 권한" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 공유 정책 수정

1.  **조직** \> **공유**로 이동합니다.

2.  **개별 공유**에서 정책 공유를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **공유 정책**에서 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

4.  **공유 규칙**에서 공유 규칙을 적절히 수정합니다. 정보를 공유할 도메인, 일정 약속에 대한 공유 수준 등의 설정을 변경할 수 있습니다. 작업을 마친 후 **저장**을 클릭하여 **공유 규칙** 대화 상자를 닫습니다.

5.  **공유 정책**에서 **저장**을 클릭하여 공유 정책을 업데이트합니다.

## EAC를 사용하여 공유 정책을 기본 공유 정책으로 설정

1.  **조직** \> **공유**로 이동합니다.

2.  **개별 공유**에서 정책 공유를 선택한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  **공유 정책**에서 **이 정책을 내 기본 공유 정책으로 설정** 확인란을 선택합니다.

4.  **저장**을 클릭하여 공유 정책을 업데이트합니다.

## EAC를 사용하여 공유 정책을 사용하지 않도록 설정

1.  **조직** \> **공유**로 이동합니다.

2.  **개별 공유**에서 공유 정책을 선택합니다.

3.  **설정** 열에서 사용하지 않도록 설정할 공유 정책의 확인란을 선택 취소합니다.

## EAC를 사용하여 공유 정책 제거


> [!IMPORTANT]
> 공유 정책을 제거하려면 먼저 공유 정책을 모든 사용자 사서함에서 제거해야 합니다.



1.  **조직** \> **공유**로 이동합니다.

2.  **개별 공유**에서 공유 정책을 선택하고 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭합니다.

3.  경고에서 **예**를 클릭하여 공유 정책을 삭제합니다.

## 셸을 사용하여 공유 정책 수정, 사용하지 않도록 설정 또는 제거

  - 이 예에서는 조직 외부의 도메인인 contoso.com에 대한 공유 정책 Contoso를 수정합니다. 이 정책을 사용하면 Contoso 도메인의 사용자가 간단한 약속 있음/없음 정보를 볼 수 있습니다.
    
        Set-SharingPolicy -Identity Contoso -Domains 'sales.contoso.com: CalendarSharingFreeBusySimple'

  - 이 예에서는 공유 정책 Contoso에 두 번째 도메인을 추가합니다. 기존 정책에 도메인을 추가하는 경우 이전에 포함된 도메인을 모두 포함해야 합니다.
    
        Set-SharingPolicy -Identity Contoso -Domains 'contoso.com: CalendarSharingFreeBusySimple', 'atlanta.contoso.com: CalendarSharingFreeBusyReviewer', 'beijing.contoso.com: CalendarSharingFreeBusyReviewer'

  - 이 예에서는 공유 정책 Contoso를 기본 공유 정책으로 설정합니다.
    
        Set-SharingPolicy -Identity Contoso -Default $True

  - 이 예에서는 공유 정책 Contoso를 사용하지 않도록 설정합니다.
    
        Set-SharingPolicy -Identity "Contoso" -Enabled $False

  - 첫 번째 예에서는 공유 정책 Contoso를 제거합니다. 두 번째 예에서는 공유 정책 Contoso를 제거하고 정책 제거를 확인하는 메시지를 생략합니다.
    
        Remove-SharingPolicy -Identity Contoso
    
        Remove-SharingPolicy -Identity Contoso -Confirm

구문과 매개 변수에 대한 자세한 내용은 [Set-SharingPolicy](https://technet.microsoft.com/ko-kr/library/dd297931\(v=exchg.150\)) 및 [Remove-SharingPolicy](https://technet.microsoft.com/ko-kr/library/dd351071\(v=exchg.150\))을 참조하십시오.

