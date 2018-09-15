---
title: '인터넷 일정 게시를 사용 하지 않도록 설정: Exchange 2013 Help'
TOCTitle: 인터넷 일정 게시를 사용 하지 않도록 설정
ms:assetid: f26dbf04-9dae-460f-a987-2ad3dfbc7b7e
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ853047(v=EXCHG.150)
ms:contentKeyID: 50556110
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 인터넷 일정 게시를 사용 하지 않도록 설정

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2014-02-15_

인터넷 일정 게시를 사용하지 않도록 설정하는 방법은 사용하도록 설정한 방법에 따라 다릅니다. 인터넷 일정 게시 전용 공유 정책을 만들었다면 정책을 사용하지 않도록 설정하거나 모두 삭제할 수 있습니다. 인터넷 일정 게시를 기본 공유 정책의 공유 규칙으로 구성했다면 **익명** 도메인에 대한 공유 규칙을 제거하기만 하면 됩니다.

인터넷 일정 게시를 사용하지 않도록 설정하면 공유 정책을 사용하도록 프로비전된 사용자는 정책에 지정된 **익명** 인터넷 도메인과 일정 정보를 공유할 수 없습니다. 인터넷 일정 게시 전용 공유 정책은 해당 정책을 사용하도록 프로비전된 모든 사용자가 자신의 사서함에서 공유 설정을 제거하기 전까지는 삭제하거나 사용하지 않도록 설정할 수 없습니다. 사용자의 공유 정책 설정 변경에 대한 자세한 내용은 [사용자 사서함 관리](https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-user-mailboxes/manage-user-mailboxes)를 참조하십시오.


> [!NOTE]
> 공유 정책을 사용하지 않도록 설정하거나 삭제할 경우 이 정책을 사용하도록 프로비전된 사용자는 공유 정책 도우미가 실행될 때까지 계속해서 정보를 공유합니다. 공유 정책 도우미의 실행 빈도를 지정하려면 <EM>SharingPolicySchedule</EM> 매개 변수가 <A href="https://technet.microsoft.com/ko-kr/library/aa998651(v=exchg.150)">Set-MailboxServer</A> cmdlet를 사용합니다.



인터넷 일정 게시 기능을 완전히 사용하지 않도록 하려면 일정 게시에 사용되는 Outlook Web App 가상 디렉터리도 사용하지 않도록 설정해야 합니다. 이렇게 하면 이전에 Exchange 조직 사용자가 외부 인터넷 사용자와 공유하던 게시된 일정 링크에 대한 액세스가 금지됩니다. 이 단계에 대해서는 이 항목 뒷부분에서 자세하게 설명합니다.

인터넷 일정 게시 및 공유 정책에 대한 자세한 내용은 [공유](sharing-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 이 작업의 예상 완료 시간: 15분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "일정 및 권한 공유" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 어떻게 해야 합니까?

## 1단계: EAC 또는 셸을 사용하여 인터넷 일정 게시를 위한 공유 정책을 사용하지 않도록 설정하거나 삭제합니다.

## EAC를 사용하여 다음을 수행합니다.

1.  **조직** \> **공유**로 이동합니다.

2.  목록 보기의 **개별 공유**에서 다음 단계를 수행합니다.
    
      - 인터넷 일정 게시만을 위한 공유 정책을 만들었을 경우 해당 정책을 선택하고 **설정** 열의 확인란 선택을 취소하여 공유 정책을 사용하지 않도록 설정하거나 **삭제**![삭제 아이콘](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "삭제 아이콘")를 클릭하여 정책을 삭제합니다.
    
      - 인터넷 일정 게시를 기본 공유 정책의 공유 규칙으로 구성한 경우 다음 단계를 수행합니다.
        
        1.  기본 공유 정책을 선택하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.
        
        2.  **공유 정책**에서 **익명** 공유 규칙을 선택한 후 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭하여 공유 규칙을 제거합니다.
        
        3.  **저장**을 클릭합니다.

## 셸 사용

이 예에서는 **인터넷**이라는 전용 인터넷 일정 게시 공유 정책을 사용하지 않도록 설정합니다.

    Set-SharingPolicy -Identity "Internet" -Enabled $false

이 예에서는 **인터넷**이라는 전용 인터넷 일정 게시 공유 정책을 삭제합니다.

    Remove-SharingPolicy -Identity "Internet"

구문과 매개 변수에 대한 자세한 내용은 [Set-SharingPolicy](https://technet.microsoft.com/ko-kr/library/dd297931\(v=exchg.150\))를 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

공유 정책이 성공적으로 제거되었거나 업데이트되었는지 확인하려면 다음 셸 명령을 실행하여 공유 정책 정보를 확인합니다.

    Get-SharingPolicy <policy name> | format-list

전용 인터넷 일정 게시 공유 정책을 제거하면 cmdlet 결과에서 정책을 볼 수 없습니다.

기본 공유 정책을 업데이트했다면 `Anonymous` 도메인이 *Domains* 매개 변수에서 제거되었는지 확인합니다.

구문과 매개 변수에 대한 자세한 내용은 [Get-SharingPolicy](https://technet.microsoft.com/ko-kr/library/dd335081\(v=exchg.150\))를 참조하십시오.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 2단계: 셸을 사용하여 Outlook Web App 가상 디렉터리 익명 기능을 사용하지 않도록 설정


> [!NOTE]
> Outlook Web App 가상 디렉터리에 대한 익명 기능은 EAC를 사용하여 사용하지 않도록 설정할 수 없습니다.



이 예에서는 클라이언트 액세스 서버 CAS01에서 Outlook Web App 가상 디렉터리에 대한 익명 기능을 사용하지 않도록 설정합니다.

    Set-OwaVirtualDirectory -Identity "CAS01" - AnonymousFeaturesEnabled -$false

구문과 매개 변수에 대한 자세한 내용은 [Set-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/bb123515\(v=exchg.150\))를 참조하십시오.

## 이 단계의 작동 여부는 어떻게 확인합니까?

클라이언트 액세스 서버에서 Outlook Web App 가상 디렉터리에 대한 익명 기능을 사용하지 않도록 설정했는지 확인하려면 다음 셸 명령을 실행하여 *AnonymousFeaturesEnabled* 매개 변수가 `$false`인지 확인합니다.

    Get-OwaVirtualDirectory | format-list

구문과 매개 변수에 대한 자세한 내용은 [Get-OwaVirtualDirectory](https://technet.microsoft.com/ko-kr/library/aa998588\(v=exchg.150\))를 참조하십시오.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


