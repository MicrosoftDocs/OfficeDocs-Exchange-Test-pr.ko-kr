---
title: '사서함에 대 한 메시지 배달 제한 구성: Exchange 2013 Help'
TOCTitle: 사서함에 대 한 메시지 배달 제한 구성
ms:assetid: c4b8b89f-3dbe-4cb8-8839-9a4e8067e00c
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb397214(v=EXCHG.150)
ms:contentKeyID: 50556081
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 사서함에 대 한 메시지 배달 제한 구성

 

_**적용 대상:**Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:**2012-11-29_

EAC 또는 셸을 사용하면 메시지가 받는 사람에게 개별적으로 배달되는지에 대한 제한을 적용할 수 있습니다. 메시지 배달 제한은 조직의 사용자에게 메시지를 보낼 수 있는 사람을 제어할 때 유용합니다. 예를 들어 특정 사용자가 보낸 메시지를 수락 또는 거부하거나 Exchange 조직 내의 사용자에게서 온 메시지만 수락하도록 사서함을 구성할 수 있습니다.

이 항목에 설명된 메시지 배달 제한은 모든 받는 사람 유형에 적용됩니다. 각기 다른 받는 사람 유형에 대한 자세한 내용은 [받는 사람](recipients-exchange-2013-help.md)을 참조하십시오.

받는 사람에 관한 추가 관리 작업은 다음을 참조하십시오.

  - [사용자 사서함 관리](manage-user-mailboxes-exchange-2013-help.md)

  - [메일 그룹 만들기 및 관리](create-and-manage-distribution-groups-exchange-2013-help.md)

  - [동적 메일 그룹 관리](manage-dynamic-distribution-groups-exchange-2013-help.md)

  - [메일 사용자 관리](manage-mail-users-exchange-2013-help.md)

  - [메일 연락처 관리](manage-mail-contacts-exchange-2013-help.md)

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분.

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용하여 메시지 배달 제한 구성

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 메시지 배달 제한을 구성할 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **메시지 배달 제한** 아래에서 **세부 정보 보기**를 클릭하여 다음 제한을 보고 변경합니다.
    
      - **메시지 수락**   이 섹션을 사용하면 이 사용자에게 메시지를 보낼 수 있는 사람을 지정할 수 있습니다.
        
          - **모든 보낸 사람**   이 옵션은 사용자가 모든 보낸 사람이 보낸 메시지를 받을 수 있도록 지정합니다. 여기에는 Exchange 조직의 보낸 사람과 외부 보낸 사람이 모두 포함됩니다. 이것은 기본 옵션입니다. 외부 사용자는 **보낸 사람 모두 인증 필요** 확인란의 선택을 취소할 경우에만 여기에 포함됩니다. 이 확인란을 선택하면 외부 사용자가 보낸 메시지가 거부됩니다.
        
          - **다음 목록에 있는 보낸 사람만**   이 옵션은 Exchange 조직에서 지정된 보낸 사람이 보낸 메시지만 사용자가 받을 수 있도록 지정합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 Exchange 조직 내 모든 받는 사람의 목록을 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람 이름을 입력한 다음 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭하여 특정 받는 사람을 검색할 수도 있습니다.
        
          - **보낸 사람 모두 인증 필요**   이 옵션은 익명 사용자가 사용자에게 메시지를 보낼 수 없게 합니다. 여기에는 Exchange 조직 외부에 있는 외부 사용자도 포함됩니다.
    
      - **다음 사람이 보낸 메시지 거부**   이 섹션을 사용하면 이 사용자에게 메시지를 보내지 못하게 차단할 수 있습니다.
        
          - **보낸 사람 없음**   이 옵션은 Exchange 조직의 모든 보낸 사람이 보낸 메시지를 사서함에서 거부하지 않도록 지정합니다. 이것은 기본 옵션입니다.
        
          - **다음 목록에 있는 보낸 사람**   이 옵션은 Exchange 조직에서 지정된 보낸 사람이 보낸 메시지를 사서함에서 거부하도록 지정합니다. **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 Exchange 조직 내 모든 받는 사람의 목록을 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람 이름을 입력한 다음 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭하여 특정 받는 사람을 검색할 수도 있습니다.

5.  **확인**을 클릭하여 **메시지 배달 제한** 페이지를 닫은 후 **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 메시지 배달 제한 구성

다음 예에서는 셸을 사용하여 사서함에 대한 메시지 배달 제한을 구성하는 방법을 보여줍니다. 다른 받는 사람 유형의 경우 해당 **Set-** cmdlet를 동일한 매개 변수와 함께 사용합니다.

이 예에서는 Lori Penor, Jeff Phillips 및 메일 그룹 Legal Team 1 구성원의 메시지만 수락하도록 Robin Wood의 사서함을 구성합니다.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom "Lori Penor","Jeff Phillips" -AcceptMessagesOnlyFromDLMembers "Legal Team 1"


> [!NOTE]
> 개별 보낸 사람의 메시지만 수락하도록 사서함을 구성하려면 <EM>AcceptMessagesOnlyFrom</EM> 매개 변수를 사용해야 합니다. 특정 메일 그룹의 구성원인 보낸 사람의 메시지만 수락하도록 사서함을 구성하려면 <EM>AcceptMessagesOnlyFromDLMembers</EM> 매개 변수를 사용해야 합니다.



이 예에서는 이름이 David Pelton인 사용자를 Robin Wood 사서함의 메시지 수락 사용자 목록에 추가합니다.

    Set-Mailbox -Identity "Robin Wood" -AcceptMessagesOnlyFrom @{add="David Pelton"}

이 예에서는 모든 보낸 사람이 인증 절차를 거치도록 Robin Wood의 사서함을 구성합니다. 따라서 사서함은 Exchange 조직의 다른 사용자가 보낸 메시지만 수락합니다.

    Set-Mailbox -Identity "Robin Wood" -RequireSenderAuthenticationEnabled $true

이 예에서는 Joe Healy, Terry Adams 및 메일 그룹 Legal Team 2 구성원의 메시지를 거부하도록 Robin Wood의 사서함을 구성합니다.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFrom "Joe Healy","Terry Adams" -RejectMessagesFromDLMembers "Legal Team 2"

이 예에서는 메일 그룹 Legal Team 3 구성원의 메시지도 거부하도록 Robin Wood의 사서함을 구성합니다.

    Set-Mailbox -Identity "Robin Wood" -RejectMessagesFromDLMembers @{add="Legal Team 3"}


> [!NOTE]
> 개별 보낸 사람의 메시지만 거부하도록 사서함을 구성하려면 <EM>RejectMessagesFrom</EM> 매개 변수를 사용해야 합니다. 특정 메일 그룹의 구성원인 보낸 사람의 메시지만 거부하도록 사서함을 구성하려면 <EM>RejectMessagesFromDLMembers</EM> 매개 변수를 사용해야 합니다.



받은 사람 유형별 배달 제한과 관련된 구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Set-DistributionGroup](https://technet.microsoft.com/ko-kr/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/ko-kr/library/bb123796\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))

  - [Set-MailContact](https://technet.microsoft.com/ko-kr/library/aa995950\(v=exchg.150\))

  - [Set-MailUser](https://technet.microsoft.com/ko-kr/library/aa995971\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

사용자 사서함에 대한 메시지 배달 제한을 성공적으로 구성했는지 확인하려면 다음을 수행합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용자 사서함 목록에서 메시지 배달 제한을 확인할 사서함을 클릭한 다음 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 기능**을 클릭합니다.

4.  **메시지 배달 제한** 아래에서 **세부 정보 보기**를 클릭하여 사서함에 대한 배달 제한을 확인합니다.

또는

셸에서 다음 명령을 실행합니다.

    Get-Mailbox <identity> | fl AcceptMessagesOnlyFrom,AcceptMessagesOnlyFromDLMembers,RejectMessagesFrom,RejectMessagesFromDLMembers,RequireSenderAuthenticationEnabled

