---
title: '받는 사람에 대 한 사용 권한 관리: Exchange 2013 Help'
TOCTitle: 받는 사람에 대 한 사용 권한 관리
ms:assetid: 749cdfe3-496b-453f-96eb-20a0bf28fd52
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ919240(v=EXCHG.150)
ms:contentKeyID: 51407629
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람에 대 한 사용 권한 관리

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2018-04-20_

EAC 또는 셸을 사용하여 사용자나 그룹이 다른 사서함에서 메시지를 열거나 보낼 수 있도록 사용자나 그룹에 사용 권한을 할당할 수 있습니다(*대리인*이라고 함). 사용 권한은 사용자 사서함, 연결된 사서함, 리소스 사서함 및 공유 사서함에 할당될 수 있으며, 메일 그룹, 동적 메일 그룹, 메일 사용 가능 보안 그룹에 할당하여 그룹을 대신하여 대리인이 메시지를 보내도록 할 수도 있습니다. 대리인에게 다음 사용 권한을 할당하여 대리인이 사서함이나 그룹을 대신하여 사서함에 액세스하거나 메시지를 보낼 수 있습니다.

  - **모든 권한**   이 사용 권한은 대리인이 사용자 사서함을 열고 사서함의 내용에 액세스할 수 있도록 허용합니다. 하지만 "모든 권한" 권한을 할당해도 대리인이 사서함에서 메일을 보낼 수는 없습니다. 대리인이 메일을 보내려면 대리인에게 "다른 사람 이름으로 보내기" 또는 "대신 보내기" 권한을 할당해야 합니다.
    
    그룹에 대해 사용 권한을 구성할 때는 "모든 권한" 권한을 사용할 수 없습니다.

  - **다른 사람 이름으로 보내기**   이 사용 권한은 대리인이 사서함을 사용하여 메시지를 보낼 수 있도록 허용합니다. 대리인에게 이 사용 권한이 할당되면 대리인이 이 사서함에서 보내는 모든 메시지는 사서함 소유자가 보낸 것처럼 표시됩니다. 그러나 이 사용 권한은 대리인이 사용자 사서함에 로그인하도록 허용하지는 않습니다. 사용자만 사서함을 열 수 있습니다. 이 사용 권한이 그룹에 할당된 경우 대리인이 보내는 메시지는 그룹에서 보낸 것처럼 표시됩니다.

  - **대신 보내기**   이 사용 권한도 대리인이 이 사서함을 사용하여 메시지를 보낼 수 있도록 허용합니다. 이 사용 권한이 대리인에게 할당되고 나면 대리인이 보내는 모든 메시지의 **보낸 사람** 주소는 사서함 소유자를 대신하여 대리인이 메시지를 보낸 것으로 나타납니다.


> [!NOTE]
> 사람 이름으로 보내기 전체 액세스 권한을 할당 하거나 주소 목록에서 숨겨져 있는 사서함에 액세스 하려면를 대신 하 여 권한을 보낼 경우 대리인은 사서함을 열거나 메시지를 보낼 수 없습니다.



## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 2분

  - 이 항목의 절차는 특정 사용 권한이 필요합니다. 사용 권한 정보에 대한 각 절차를 참조하세요.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## 무슨 작업을 하고 싶으십니까?

## 사서함에 사용 권한 할당

앞서 언급했듯이 사용자 사서함, 연결된 사서함, 리소스 사서함 및 공유 사서함에 대리인 권한을 할당할 수 있으며, 셸을 사용하여 대리인 권한을 할당하여 검색 사서함에 액세스할 수도 있습니다.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션에서 "권한 및 위임" 항목

## EAC를 통해 사용 권한 할당

다음 절차에서는 사용자 사서함에 사용 권한을 할당하는 방법을 보여줍니다. EAC에서 **리소스** 또는 **공유** 페이지로 이동한 후 사용 권한을 할당할 사서함을 선택하여 리소스나 공유 사서함에 사용 권한을 할당할 때와 비슷한 절차를 수행하면 됩니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사서함 목록에서 사용 권한을 할당하려는 사서함을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 위임**을 클릭합니다.

4.  대리인에게 사용 권한을 할당하려면 해당 사용 권한 아래의 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 사용 권한이 할당될 수 있는 Exchange 조직 내의 모든 받는 사람이 표시되는 페이지를 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람 이름을 입력한 다음 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭하여 특정 받는 사람을 검색할 수도 있습니다.
    
    받는 사람의 사용 권한을 제거하려면 해당 사용 권한에서 받는 사람을 선택하고 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## EAC를 대량으로 사용 하 여 사용 권한 할당

사용 권한 대량 할당 하려면 다음 단계를 사용 합니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사용 권한을 할당 하려는 사서함을 선택 합니다.

3.  클릭 하거나 탭 **기타 옵션** 아래 **사서함 위임** 하 고 오른쪽 창에서 **추가** 선택 합니다.

4.  **대량 추가 위임** 페이지에서 클릭 하거나 권한을 할당할 수 있는 Exchange 조직에서 모든 받는 사람을 나열 하는 페이지를 표시 하려면 적절 한 사용 권한에서 **추가** ![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가") 를 누릅니다. 원하는, 하는 목록에 추가 하 고 **확인** 을 클릭 한 다음 받는 사람을 선택 합니다.
    
    적절 한 사용 권한에서 받는 사람에 대 한 권한을 제거 하려면 받는 사람을 선택 하 고![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")**제거** 를 클릭 합니다.

## EAC를 통해 사용자 권한을 할당하여 다른 사용자 사서함에서 전자 메일 보내기

다음 절차에서는 사용자 권한을 할당하여 다른 사용자 사서함에서 전자 메일을 보내는 방법을 보여줍니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사서함 목록에서 다른 사람 이름으로 보내기 권한을 할당하려는 사서함을 클릭한 다음 **편집**(![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘"))을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 위임**을 클릭합니다.

4.  사용 권한을 대리인에게 할당하려면 **다른 사람 이름으로 보내기** 또는 **대신 보내기**에서 **추가**(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가"))를 클릭하여 Exchange 조직 내에서 사용 권한이 할당될 수 있는 받는 사람을 모두 나열하는 페이지를 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람의 이름을 입력한 다음 **검색**(![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘"))을 클릭하여 특정한 받는 사람을 검색할 수도 있습니다.
    
    **다른 사람 이름으로 보내기** 권한을 사용하면 대리인이 이 사서함에서 전자 메일을 보낼 수 있습니다.
    
    **대신 보내기** 권한을 사용하면 대리인이 이 사서함 대신 전자 메일을 보낼 수 있습니다. 대리인이 보낸 메시지의 **보낸 사람** 줄에는 대리인이 사서함 소유자를 대신하여 이 메시지를 보낸 사실이 나타납니다.
    

    > [!NOTE]
    > 사용자가 사서함의 내용을 보거나 열어야 하는 경우에도 사용자에게 <STRONG>모든 액세스</STRONG> 권한을 할당해야 합니다.



5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## EAC를 통해 사용자 권한을 할당하여 그룹에서 전자 메일 보내기

다음 절차에서는 사용자 권한을 할당하여 그룹에서 전자 메일을 보내는 방법을 보여줍니다.

1.  EAC에서 **받는 사람** \> **그룹**으로 이동합니다.

2.  그룹 목록에서 다른 사람 이름으로 보내기 권한을 할당하려는 그룹을 클릭한 다음 **편집**(![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘"))을 클릭합니다.

3.  그룹 속성 페이지에서 **그룹 위임**을 클릭합니다.

4.  사용 권한을 대리인에게 할당하려면 **다른 사람 이름으로 보내기** 또는 **대신 보내기**에서 **추가**(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가"))를 클릭하여 Exchange 조직 내에서 사용 권한이 할당될 수 있는 받는 사람을 모두 나열하는 페이지를 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람의 이름을 입력한 다음 **검색**(![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘"))을 클릭하여 특정한 받는 사람을 검색할 수도 있습니다.
    
    **다른 사람 이름으로 보내기** 권한을 사용하면 대리인이 이 그룹에서 전자 메일을 보낼 수 있습니다.
    
    **대신 보내기** 권한을 사용하면 대리인이 이 그룹 대신 전자 메일을 보낼 수 있습니다. 대리인이 보낸 메시지의 **보낸 사람** 줄에는 대리인이 그룹을 대신하여 이 메시지를 보낸 사실이 나타납니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## EAC를 통해 모든 액세스 권한 할당

다음 절차에서는 사용자 사서함에 모든 액세스 권한을 할당하는 방법을 보여줍니다.

1.  EAC에서 **받는 사람** \> **사서함**으로 이동합니다.

2.  사서함 목록에서 모든 액세스 권한을 할당하려는 사서함을 클릭한 다음 **편집**(![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘"))을 클릭합니다.

3.  사서함 속성 페이지에서 **사서함 위임**을 클릭합니다.

4.  권한을 위임하도록 할당하려면 **모든 권한**에서 **추가**(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가"))를 클릭하여 권한을 할당할 수 있는 Exchange 조직 내의 받는 사람이 모두 나열되는 페이지를 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람의 이름을 입력한 다음 **검색**(![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘"))을 클릭하여 특정한 받는 사람을 검색할 수도 있습니다.
    
    **모든 액세스** 권한을 사용하면 대리인이 사용자의 사서함을 열고 사서함의 내용에 액세스할 수 있습니다.
    

    > [!NOTE]
    > 그러나 <STRONG>모든 액세스</STRONG> 권한을 할당해도 대리인이 사서함에서 메일을 보낼 수는 없습니다. 대리인이 메일을 보내려면 <STRONG>다른 사람 이름으로 보내기</STRONG> 또는 <STRONG>대신 보내기</STRONG> 권한을 할당해야 합니다.



5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 사용 권한 할당

다음 섹션에서는 셸을 사용하여 사서함에 대한 "모든 권한", "다른 사람 이름으로 보내기" 및 "대신 보내기" 권한을 관리하는 방법을 보여줍니다.

## "모든 권한" 권한 관리

이 예에서는 **Add-MailboxPermission** 및 **Remove-MailboxPermission** cmdlet을 사용하여 "모든 권한" 권한을 관리하는 방법을 보여줍니다.

이 예에서는 대리인 Raymond Sam에게 Terry Adams의 사서함에 대한 "모든 권한" 권한을 할당합니다.

    Add-MailboxPermission -Identity "Terry Adams" -User raymonds -AccessRights FullAccess -InheritanceType all

이 예에서는 Esther Valle에게 조직의 기본 검색 사서함에 대한 "모든 권한" 권한을 할당합니다.

    Add-MailboxPermission -Identity "DiscoverySearchMailbox{D919BA05-46A6-415f-80AD-7E09334BB852}" -User estherv -AccessRights FullAccess -InheritanceType all

이 예에서는 지원 센터 메일 그룹 구성원에게 Helpdesk Tickets 공유 사서함에 대한 "모든 권한" 권한을 할당합니다.

    Add-MailboxPermission "HelpdeskTickets" -User helpdesk -AccessRights FullAccess -InheritanceType all

이 예에서는 Ayla Kol의 사서함에 대한 Jim Hance의 "모든 권한" 권한을 제거합니다.

    Remove-MailboxPermission -Identity ayla -User "Jim Hance" -AccessRights FullAccess -Inheritance

구문 및 매개 변수에 대한 자세한 내용은 다음 항목을 참조하십시오.

  - [Add-MailboxPermission](https://technet.microsoft.com/ko-kr/library/bb124097\(v=exchg.150\))

  - [Remove-MailboxPermission](https://technet.microsoft.com/ko-kr/library/bb125153\(v=exchg.150\))

## "다른 사람 이름으로 보내기" 권한 관리

이 예에서는 Exchange Server 2013 및 Exchange Online에서 "다른 사람 이름으로 보내기" 권한을 관리하는 방법을 보여줍니다. Exchange 2013에서는 **Add-ADPermission** 및 **Remove-ADPermission** cmdlet을 사용해야 하고 Exchange Online에서는 **Add-RecipientPermission** 및 **Remove-RecipientPermission** cmdlet을 사용해야 합니다. 두 경우 모두 *Identity* 매개 변수를 사용하여 "다른 사람 이름으로 보내기" 권한을 추가 또는 제거해야 하는 사서함의 이름을 지정하고 *User* 또는 *Trustee* 매개 변수를 사용하여 "다른 사람 이름으로 보내기" 권한을 할당하거나 할당 취소할 대리인(예: 사용자나 그룹)을 지정합니다.


> [!TIP]
> <STRONG>Get-Recipient</STRONG> cmdlet을 사용하여 사서함 및 대리인에 대한 <EM>Name</EM> 속성을 검색할 수 있으며, 이 값을 사용하여 "다른 사람 이름으로 보내기" 권한을 할당할 수 있습니다.



## Exchange Server 2013

이 예에서는 공유 사서함 Helpdesk Support Team의 Helpdesk 그룹에 "다른 사람 이름으로 보내기" 권한을 할당합니다.

    Add-ADPermission -Identity helpdesksupport -User helpdeskgroup -ExtendedRights "Send As"

이 예에서는 James Alvord 사서함에서 사용자 Pilar Pinilla에 대한 "다른 사람 이름으로 보내기" 권한을 제거합니다.

    Remove-ADPermission -Identity "James Alvord" -User pilarp -ExtendedRights "Send As"

구문과 매개 변수에 대한 자세한 내용은 다음을 참조하십시오.

  - [Add-ADPermission](https://technet.microsoft.com/ko-kr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ko-kr/library/aa996048\(v=exchg.150\))

## Exchange Online

이 예에서는 공유 사서함 Contoso Printer Support의 Printer Support 그룹에 "다른 사람 이름으로 보내기" 권한을 할당합니다.

    Add-RecipientPermission -Identity "Contoso Printer Support" -Trustee "Printer Support" -AccessRights SendAs

이 예에서는 Yan Li의 사서함에서 사용자 Karen Toh에 대한 "다른 사람 이름으로 보내기" 권한을 제거합니다.

    Remove-RecipientPermission -Identity "Yan Li" -Trustee "Karen Toh" -ExtendedRights SendAs

구문과 매개 변수에 대한 자세한 내용은 다음을 참조하십시오.

  - [Add-RecipientPermission](https://technet.microsoft.com/ko-kr/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/ko-kr/library/ff945794\(v=exchg.150\))

## "대신 보내기" 권한 관리

다음 예에서는 **Set-Mailbox** cmdlet을 사용하여 "대신 보내기" 권한을 관리하는 방법을 보여줍니다.

이 예에서는 대리인 Holly Holt에게 Sean Chai의 사서함에 대한 "대신 보내기" 권한을 할당합니다.

    Set-Mailbox -Identity seanc@contoso.com -GrantSendOnBehalfTo hollyh

이 예에서는 Temporary Executive Assistants 그룹에 할당된 Contoso Executives 공유 사서함에서 "대신 보내기" 권한을 제거합니다.

    Set-Mailbox "Contoso Executives" -GrantSendOnBehalfTo @{remove="tempassistants@contoso.com"}

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 작동 여부는 어떻게 확인합니까?

사서함이나 공유 사서함에 사용 권한이 할당되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서:
    
    1.  **받는 사람** \> **사서함** 또는 **공유**로 이동한 후 사서함을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.
    
    2.  사서함 속성 페이지에서 **사서함 위임**을 클릭합니다.
    
    3.  받는 사람에게 사용 권한이 할당된 경우 사용자나 그룹이 해당 사용 권한 아래에 표시되는지 확인합니다. 사용 권한을 제거한 경우에는 받는 사람이 해당 사용 권한에 표시되지 않는지 확인합니다.

또는

  - 관리하는 사용 권한에 따라 셸에서 다음 명령 중 하나를 실행합니다.
    
      - **모든 권한**
        
            Get-MailboxPermission -Identity <mailbox>
        
        특정 대리인에게 사서함에 대한 "모든 권한" 권한이 할당되었는지 확인하려면 다음 명령을 실행합니다.
        
            Get-MailboxPermission -Identity <mailbox> -User <delegate>
    
      - **다른 사람 이름으로 보내기**
        
        Exchange Server 2013에서 다음 명령을 실행합니다.
        
            Get-ADPermission -Identity <name of mailbox> -User <delegate>
        
        Exchange Online에서 다음 명령을 실행합니다.
        
            Get-RecipientPermission -Identity <mailbox> -Trustee <delegate>
    
      - **대신 보내기**
        
            Get-Mailbox -Identity <mailbox> | FL GrantSendOnBehalfTo

## 그룹에 사용 권한 할당

앞서 언급했듯이 메일 그룹, 동적 메일 그룹, 메일 사용 가능 보안 그룹에 "다른 사람 이름으로 보내기" 및 "대신 보내기" 권한을 할당하여 대리인이 그룹으로 또는 그룹을 대신하여 메시지를 보내도록 할 수 있습니다.

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람 프로비전 권한" 섹션에 있는 "메일 그룹" 및 "동적 메일 그룹" 항목

## EAC를 통해 사용 권한 할당

1.  EAC에서 **받는 사람** \> **그룹**으로 이동합니다.

2.  그룹 목록에서 사용 권한을 할당하려는 그룹을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.

3.  그룹 속성 페이지에서 **그룹 위임**을 클릭합니다.

4.  대리인에게 권한을 할당하려면 해당 권한 아래의 **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")를 클릭하여 권한이 할당될 수 있는 Exchange 조직 내의 모든 받는 사람 목록이 표시되는 페이지를 표시합니다. 원하는 받는 사람을 선택하여 목록에 추가한 다음 **확인**을 클릭합니다. 또한 검색 상자에 받는 사람 이름을 입력한 다음 **검색**![검색 아이콘](images/Dd353189.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif "검색 아이콘")을 클릭하여 특정 받는 사람을 검색할 수도 있습니다.
    
    받는 사람의 사용 권한을 제거하려면 해당 사용 권한에서 받는 사람을 선택하고 **제거**![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거")를 클릭합니다.

5.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 셸을 사용하여 사용 권한 할당

다음 섹션에서는 셸을 사용하여 그룹에 대한 "다른 사람 이름으로 보내기" 및 "대신 보내기" 권한을 관리하는 방법을 보여줍니다.

## "다른 사람 이름으로 보내기" 권한 관리

이 예에서는 Exchange Server 2013 및 Exchange Online에서 그룹에 대한 "다른 사람 이름으로 보내기" 권한을 관리하는 방법을 보여줍니다. Exchange 2013에서는 **Add-ADPermission** 및 **Remove-ADPermission** cmdlet을 사용해야 하고 Exchange Online에서는 **Add-RecipientPermission** 및 **Remove-RecipientPermission** cmdlet을 사용해야 합니다. 두 경우 모두 *Identity* 매개 변수를 사용하여 "다른 사람 이름으로 보내기" 권한을 추가 또는 제거해야 하는 그룹의 이름을 지정하고 *User* 또는 *Trustee* 매개 변수를 사용하여 "다른 사람 이름으로 보내기" 권한을 할당하거나 할당 취소할 대리인(예: 사용자나 그룹)을 지정합니다.


> [!TIP]
> <STRONG>Get-Recipient</STRONG> cmdlet을 사용하여 그룹 및 대리인에 대한 <EM>Name</EM> 속성을 검색할 수 있습니다. 이 값을 사용하여 "다른 사람 이름으로 보내기" 권한을 할당할 수 있습니다.



## Exchange Server 2013

이 예에서는 Contoso Sales Info 그룹에 대한 Sales Admins 그룹에 "다른 사람 이름으로 보내기" 권한을 할당합니다. 그러면 Sales Admins 그룹의 구성원이 Contoso Sales Information 그룹으로 메시지를 보낼 수 있습니다.

    Add-ADPermission -Identity "Contoso Sales Info" -User "Sales Admins" -ExtendedRights "Send As"

이 예에서는 Corporate IT Admins 그룹에서 Alan Shen 사용자에 대한 "다른 사람 이름으로 보내기" 권한을 제거합니다.

    Remove-ADPermission -Identity "Corporate IT Admins" -User contoso\alans -ExtendedRights "Send As"

구문과 매개 변수에 대한 자세한 내용은 다음을 참조하십시오.

  - [Add-ADPermission](https://technet.microsoft.com/ko-kr/library/bb124403\(v=exchg.150\))

  - [Remove-ADPermission](https://technet.microsoft.com/ko-kr/library/aa996048\(v=exchg.150\))

## Exchange Online

이 예에서는 Emergency Broadcast Messages 동적 메일 그룹의 Contoso Admins 그룹에 "다른 사람 이름으로 보내기" 권한을 할당합니다.

    Add-RecipientPermission -Identity emergencybroadcast@contoso.com -Trustee "Contoso Admins" -AccessRights SendAs

이 예에서는 Printer Resources 보안 그룹에서 사용자 Walter Harp에 대한 "다른 사람 이름으로 보내기" 권한을 제거합니다.

    Remove-RecipientPermission -Identity "Printer Resources" -Trustee walterh@contoso.com ExtendedRights SendAs

구문과 매개 변수에 대한 자세한 내용은 다음을 참조하십시오.

  - [Add-RecipientPermission](https://technet.microsoft.com/ko-kr/library/ff935839\(v=exchg.150\))

  - [Remove-RecipientPermission](https://technet.microsoft.com/ko-kr/library/ff945794\(v=exchg.150\))

## "대신 보내기" 권한 관리

다음 예에서는 **Set-DistributionGroup** 및 **Set-DynamicDistributionGroup** cmdlet을 사용하여 그룹에 대한 "대신 보내기" 권한을 관리하는 방법을 보여줍니다.

이 예에서는 Printer Support 메일 그룹에 대한 "대신 보내기" 권한을 대리인 Sara Davis에게 할당합니다.

    Set-DistributionGroup -Identity printersupport@contoso.com -GrantSendOnBehalfTo sarad

이 예에서는 All Employees 동적 메일 그룹에 대한 "대신 보내기" 권한을 대리인 Administrator에게 할당합니다.

    Set-DynamicDistributionGroup -Identity "All Employees" -GrantSendOnBehalfTo administrator

이 예에서는 All Employees 동적 메일 그룹에서 관리자에게 할당된 "대신 보내기" 권한을 제거합니다.

    Set-DynamicDistributionGroup "All Employees" -GrantSendOnBehalfTo @{remove="administrator"}

구문과 매개 변수에 대한 자세한 내용은 다음을 참조하십시오.

  - [Set-DistributionGroup](https://technet.microsoft.com/ko-kr/library/bb124955\(v=exchg.150\))

  - [Set-DynamicDistributionGroup](https://technet.microsoft.com/ko-kr/library/bb123796\(v=exchg.150\))

## 작동 여부는 어떻게 확인합니까?

그룹에 사용 권한이 할당되었는지 확인하려면 다음 중 하나를 수행하십시오.

  - EAC에서:
    
    1.  **받는 사람** \> **그룹**으로 이동한 후 그룹을 클릭하고 **편집**![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")을 클릭합니다.
    
    2.  그룹 속성 페이지에서 **그룹 위임**을 클릭합니다.
    
    3.  받는 사람에게 사용 권한이 할당된 경우 사용자나 그룹이 해당 사용 권한 아래에 표시되는지 확인합니다. 사용 권한을 제거한 경우에는 받는 사람이 해당 사용 권한에 표시되지 않는지 확인합니다.

또는

  - 관리하는 사용 권한에 따라 셸에서 다음 명령 중 하나를 실행합니다.
    
      - **다른 사람 이름으로 보내기**
        
        Exchange Server 2013에서 다음 명령을 실행합니다.
        
            Get-ADPermission -Identity <name of group> -User <delegate>
        
        Exchange Online에서 다음 명령을 실행합니다.
        
            Get-RecipientPermission -Identity <group> -Trustee <delegate>
    
      - **대신 보내기**
        
            Get-DistributionGroup -Identity <group> | FL GrantSendOnBehalfTo
        
        또는
        
            Get-DynamicDistributionGroup -Identity <group> | FL GrantSendOnBehalfTo

