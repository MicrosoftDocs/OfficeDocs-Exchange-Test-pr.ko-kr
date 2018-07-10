---
title: '오프 라인 주소록 다운로드에 대 한 받는 사람 프로 비전: Exchange 2013 Help'
TOCTitle: 오프 라인 주소록 다운로드에 대 한 받는 사람 프로 비전
ms:assetid: 141751ac-16d3-4e3c-b70c-004aeedcb5a0
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Aa996345(v=EXCHG.150)
ms:contentKeyID: 50482532
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 오프 라인 주소록 다운로드에 대 한 받는 사람 프로 비전

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2013-02-15_

조직에서 OAB(오프라인 주소록)를 여러 개 사용하는 경우 받는 사람 중 누가 어떤 OAB를 다운로드할지 지정하는 몇 가지 방법이 있습니다.

  - **사서함 데이터베이스 단위**   EAC 또는 셸을 사용하여 사서함 데이터베이스를 Office Outlook 2007, Outlook 2010 및 Outlook 2013 클라이언트의 기본 OAB에 연결하는 방법으로 받는 사람의 OAB 다운로드를 프로비전할 수 있습니다.

  - **받는 사람 단위**   셸에서 **Set-Mailbox** cmdlet을 사용하면 OAB를 받는 사람의 사서함에 직접 연결하여 다운로드되는 OAB를 지정할 수 있습니다.

  - **여러 받는 사람 단위**   공통된 특성을 기반으로, 셸에서 파이프라인된 명령을 사용하여 여러 명의 받는 사람이 다운로드하는 OAB를 지정할 수 있습니다.

  - **주소록 정책에 따라**   사서함의 사용자 계정에 ABP(주소록 정책)을 할당하여 받는 사람의 사서함으로 다운로드할 OAB를 지정할 수 있습니다. 이미 OAB가 할당된 사용자 계정에 ABP를 할당하면 해당 사서함에 명시적으로 할당된 OAB가 우선합니다. 자세한 내용은 [메일 사용자에 게 주소록 정책 할당](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)을 참조하십시오.

OAB와 관련된 추가 관리 작업에 대한 자세한 내용은 [오프 라인 주소록 절차](offline-address-book-procedures-exchange-2013-help.md)를 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 각 절차의 예상 완료 시간: 5분

  - 이 절차를 수행하는 데 EAC(Exchange 관리 센터)를 사용할 수 없습니다. 셸을 사용해야 합니다.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## 셸을 사용하여 사서함 데이터베이스를 공용 폴더 데이터베이스 또는 기본 OAB에 연결하는 방법으로 받는 사람의 OAB 다운로드 프로비전

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "사서함 데이터베이스" 항목

다음은 기본 사서함 데이터베이스에 대한 My OAB의 웹 기반 배포를 설정하는 예입니다.

    Set-MailboxDatabase -Identity "Mailbox Database" -OfflineAddressBook "My OAB"

구문과 매개 변수에 대한 자세한 내용은 [Set-MailboxDatabase](https://technet.microsoft.com/ko-kr/library/bb123971\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 OAB를 받는 사람의 사서함에 직접 연결함으로써 다운로드될 OAB 지정

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

OAB를 받는 사람 사서함에 직접 연결하여 다운로드될 OAB를 지정하려면 다음 구문을 사용합니다.

    Set-Mailbox -Identity <MailboxIDParameter> -OfflineAddressBook <OfflineAddressBookIdParameter>


> [!NOTE]
> <EM>Identity</EM> 매개 변수는 사서함을 식별하며 GUID, ADObjectID, DN(고유 이름), <EM>domain\account</EM>, UPN(사용자 이름), LegacyExchangeDN, SmtpAddress 및 별칭을 값으로 사용할 수 있습니다.



다음은 사용자 Kim이 My OAB라는 OBA를 다운로드하도록 지정하는 예입니다.

    Set-Mailbox -Identity Kim -OfflineAddressBook "My OAB"

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

## 셸을 사용하여 여러 명의 받는 사람이 다운로드할 OAB 지정

이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [받는 사람에 게 사용 권한](recipients-permissions-exchange-2013-help.md)의 "받는 사람의 프로비전 권한" 섹션

다음은 Contoso에서 United States의 모든 사용자 사서함이 Contoso United States라는 OAB를 다운로드하도록 지정하는 예입니다.

    Get-User -ResultSize Unlimited -Filter { Company -eq "Contoso" -and RecipientType -eq "UserMailbox" } | Where { $_.CountryOrRegion -eq "United States"} | Set-Mailbox -OfflineAddressBook "Contoso United States"

구문과 매개 변수에 대한 자세한 내용은 [Get-User](https://technet.microsoft.com/ko-kr/library/aa996896\(v=exchg.150\)) 및 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\))를 참조하십시오.

