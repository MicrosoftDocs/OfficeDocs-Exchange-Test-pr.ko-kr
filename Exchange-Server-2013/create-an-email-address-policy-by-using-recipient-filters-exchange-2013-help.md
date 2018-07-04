---
title: '받는 사람 필터를 사용 하 여 전자 메일 주소 정책 만들기: Exchange 2013 Help'
TOCTitle: 받는 사람 필터를 사용 하 여 전자 메일 주소 정책 만들기
ms:assetid: e3f446bd-1511-479c-8d87-2dfce5547c90
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Bb232194(v=EXCHG.150)
ms:contentKeyID: 50484404
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 받는 사람 필터를 사용 하 여 전자 메일 주소 정책 만들기

 

_**적용 대상:** Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-16_

셸을 사용 하 여 받는 사람 필터를 사용 하 여 전자 메일 주소 정책을 만들 수 있습니다. 전자 메일 주소 정책에 대 한 자세한 내용은, [전자 메일 주소 정책](email-address-policies-exchange-2013-help.md)를 참조 하십시오.

전자 메일 주소 정책에 관련된 추가 관리 작업은 [전자 메일 주소 정책 절차](email-address-policy-procedures-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 사항은 무엇입니까?

  - 예상 완료 시간: 5분

  - 사용자 지정 필터를 만드는 *RecipientFilter* 매개 변수를 사용 하는 필터에 대 한 문자열을 지정 해야 합니다. 셸을 OPath 필터링 구문을 사용합니다. OPath은 쿼리 개체 데이터 원본에 설계 하는 쿼리 언어입니다.
    

    > [!IMPORTANT]
    > 만들기 또는 전자 메일 주소 정책을 편집 하는 받는 사람 필터를 사용 하는 경우에 전자 메일 주소 정책을 편집 하려면 Exchange 관리 센터 (EAC)를 사용할 수 없습니다. 셸을 사용 해야 합니다. 자세한 구문 및 매개 변수 정보에 대 한 <A href="https://technet.microsoft.com/ko-kr/library/bb124517(v=exchg.150)">Set-EmailAddressPolicy</A>를 참조 하십시오.



  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [전자 메일 주소 및 주소록](email-addresses-and-address-books-exchange-2013-help.md)의 "전자 메일 주소 정책" 항목

  - 전자 메일 주소 정책에서 SMTP 주소 도메인을 사용할 수 있습니다, 전에 허용된 도메인을 구성 해야 합니다. 자세한 내용을 보려면 [허용 도메인](accepted-domains-exchange-2013-help.md)를 참조 하십시오.

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.

> [!CAUTION]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <a href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</a>, <a href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</a>, 또는 <a href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</a>


## 셸을 사용 하 여 받는 사람 필터를 사용 하 여 전자 메일 주소 정책을 만들려면

전자 메일 주소 정책을 받는 사람 필터를 사용 하 여를 만들려면 다음 구문을 사용 합니다.

    New-EmailAddressPolicy -Name <String> -RecipientFilter <String>

이 예제는 전자 메일 주소의 로컬 부분으로 이루어져 자신의 이름 및 전체 성을의 처음 두 문자가 및 모든 중역에 게 적용 되는 전자 메일 주소 정책을 만듭니다.

    New-EmailAddressPolicy -Name 'Execs' -EnabledEmailAddressTemplates 'SMTP:%2g%s@contoso.com' -RecipientFilter {((RecipientType -eq 'UserMailbox') -and (Title -like 'executive'))}

자세한 구문 및 매개 변수 정보에 대 한 [New-EmailAddressPolicy](https://technet.microsoft.com/ko-kr/library/aa996800\(v=exchg.150\))를 참조 하십시오.

