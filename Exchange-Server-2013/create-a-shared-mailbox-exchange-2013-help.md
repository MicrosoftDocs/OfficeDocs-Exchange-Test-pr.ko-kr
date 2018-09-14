---
title: '공유 사서함 만들기: Exchange 2013 Help'
TOCTitle: 공유 사서함 만들기
ms:assetid: d34bc827-1e83-4a7f-a219-8ba9c19fe24b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/JJ150570(v=EXCHG.150)
ms:contentKeyID: 50484258
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 공유 사서함 만들기

 

_**적용 대상:** Exchange Online, Exchange Server 2013, Office 365 Enterprise_

_**마지막으로 수정된 항목:** 2016-12-09_

**예상 완료 시간: 5분**

공유 사서함 쉽게 모니터링 하 고 info@contoso.com 또는 support@contoso.com 등의 일반적인 계정에서 전자 메일 보내기 회사에는 사용자의 그룹에 대 한 합니다. 그룹에서 사람 공유 사서함에 전송 된 메시지에 회신 하는 경우 전자 메일은 개별 사용자 로부터 하지는 공유 사서함에서 보낸와 동일 하 게 확인 합니다.


> [!IMPORTANT]
> 비즈니스를 위한 Office 365를 사용 하는 경우 Office 365 관리 센터에서 공유 사서함을 만들어야 합니다. 
> <UL>
> <LI>
> <P><A href="https://go.microsoft.com/fwlink/p/?linkid=834766">Office 365의 공유 사서함 만들기</A></P></LI></UL>



조직에서 하이브리드 Exchange 환경을 사용 하는 경우에 공유 사서함 만들기 및 관리를 온-프레미스 Exchange 관리 센터 (EAC)를 사용 해야 합니다. 공유 사서함에 대 한 자세한 내용은, [공유 사서함](shared-mailboxes-exchange-2013-help.md)를 참조 하십시오.

## EAC를 사용하여 공유 사서함 만들기

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사용자 사서함" 항목

1.  **받는 사람** \> **공유** \> **추가**![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")로 이동합니다.

2.  필수 필드에 채워야 할 사항은 다음과 같습니다.
    
      - **표시 이름**
    
      - **전자 메일 주소**

3.  모든 권한 또는 다른 사람 이름으로 보내기 권한을 부여하려면 **추가**(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가"))를 클릭한 다음 권한을 부여하려는 사용자를 선택합니다. **CTRL** 키를 사용하면 여러 사용자를 선택할 수 있습니다. 권한을 사용하는 방법에 대한 자세한 내용은 이 항목 뒷부분에 나오는 Which permission should you use?을 참조하세요.
    

    > [!NOTE]
    > 모든 액세스 권한을 사용하면 사서함을 열 수 있을 뿐만 아니라 사서함에서 항목을 만들고 수정할 수 있습니다. 다른 사람 이름으로 보내기 권한을 사용하면 사서함 소유자가 아닌 사용자가 공유 사서함에서 전자 메일을 보낼 수 있습니다. 두 권한 모두 공유 사서함 작업에 필요합니다.



4.  **저장**을 클릭하여 변경 사항을 저장하고 공유 사서함을 만듭니다.

## EAC를 사용하여 공유 사서함 위임 편집

1.  **받는 사람** \> **공유** \> **편집**(![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘"))으로 이동합니다.

2.  **사서함 위임**을 클릭합니다.

3.  모든 권한 또는 다른 사람 이름으로 보내기 권한을 부여하려면 **추가**(![아이콘 추가](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "아이콘 추가")) 또는 **제거**(![아이콘 제거](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "아이콘 제거"))를 클릭한 다음 권한을 부여하려는 사용자를 선택합니다.
    

    > [!NOTE]
    > 모든 액세스 권한을 사용하면 사서함을 열 수 있을 뿐만 아니라 사서함에서 항목을 만들고 수정할 수 있습니다. 다른 사람 이름으로 보내기 권한을 사용하면 사서함 소유자가 아닌 사용자가 공유 사서함에서 전자 메일을 보낼 수 있습니다. 두 권한 모두 공유 사서함 작업에 필요합니다.



4.  **저장**을 클릭하여 변경 내용을 저장합니다.

## 공유 사서함을 사용 하 여

사용자 수에 액세스 하 고 공유 사서함을 사용 하는 방법을 알아보려면 다음을 확인 합니다.

  - [열기 및 사용 하 여 Outlook 2016 및 Outlook 2013의 공유 사서함](https://go.microsoft.com/fwlink/p/?linkid=834764)

  - [열기 및 사용 하 여 Outlook에서 비즈니스에 대 한 웹에 공유 사서함](https://go.microsoft.com/fwlink/p/?linkid=834766)

## 셸을 사용하여 공유 사서함 만들기

이 예에서는 공유 사서함 Sales Department를 만들고 보안 그룹 MarketingSG에 대해 모든 권한 및 대신 보내기 권한을 부여합니다. 이 보안 그룹의 구성원인 사용자에게 해당 사서함에 대한 권한이 부여됩니다.


> [!NOTE]
> 이 예에서는 MarketingSG 보안 그룹을 이미 만들었고 해당 보안 그룹이 메일을 사용할 수 있는 것으로 가정합니다. <A href="https://docs.microsoft.com/ko-kr/exchange/recipients-in-exchange-online/manage-mail-enabled-security-groups">메일 사용이 가능한 보안 그룹 관리</A>를 참조하세요.



    New-Mailbox -Shared -Name "Sales Department" -DisplayName "Sales Department" -Alias Sales | Set-Mailbox -GrantSendOnBehalfTo MarketingSG | Add-MailboxPermission -User MarketingSG -AccessRights FullAccess -InheritanceType All

구문과 매개 변수에 대한 자세한 내용은 [New-Mailbox](https://technet.microsoft.com/ko-kr/library/aa997663\(v=exchg.150\))를 참조하십시오.

## 사용해야 하는 권한

공유 사서함에 다음과 같은 사용 권한을 사용할 수 있습니다.

  - **모든 권한**   모든 권한이 있는 사용자는 공유 사서함을 열고 해당 사서함의 소유자로서 작업할 수 있습니다. 사용자는 공유 사서함에 액세스한 후에 일정 항목을 만들고, 전자 메일 메시지를 읽고 보고 삭제하고 변경하며, 작업 및 일정 연락처를 만들 수 있습니다. 그러나 모든 권한이 있는 사용자는 다른 사람 이름으로 보내기 또는 대신 보내기 권한도 함께 가지고 있지 않다면 공유 사서함에서 전자 메일을 보낼 수 없습니다.

  - **다른 사람 이름으로 보내기**   다른 사람 이름으로 보내기 권한이 있는 사용자는 메일을 보낼 때 공유 사서함을 가장할 수 있습니다. 예를 들면 Kweku가 마케팅 부서 공유 사서함에 로그인하여 이메일을 보내면, 마케팅 부서에서 이메일을 보낸 것처럼 표시됩니다.

  - **대신 보내기**   대신 보내기 권한이 있는 사용자는 공유 사서함 대신 이메일을 보낼 수 있습니다. 예를 들면 John이 Reception Building 32 공유 사서함에 로그인하여 이메일을 보내면, "Reception Building 32 대신 John"이 보낸 것처럼 메일이 표시됩니다. EAC를 사용하여 대신 보내기 권한을 부여할 수 없으며, [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) cmdlet을 *GrantSendonBehalf* 매개 변수와 함께 사용해야 합니다.

## 추가 정보

이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>


