---
title: '메일 사용자에 게 주소록 정책 할당: Exchange 2013 Help'
TOCTitle: 메일 사용자에 게 주소록 정책 할당
ms:assetid: bdfe6575-24c0-47d0-9cfb-ece910db248b
ms:mtpsurl: https://technet.microsoft.com/ko-kr/library/Hh529942(v=EXCHG.150)
ms:contentKeyID: 50484032
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# 메일 사용자에 게 주소록 정책 할당

 

_**적용 대상:** Exchange Online, Exchange Server 2013_

_**마지막으로 수정된 항목:** 2012-10-11_

주소록 정책 (ABP)을 만든 후 사서함 사용자에 게 할당 해야 합니다. 사용자가 자신의 사용자 계정이 만들어질 때 기본 ABP를 할당 되지 않습니다. ABP을 사용자에 게 할당 하지 않은 경우에 전체 조직에 대 한 전체 주소 목록 (gal 전체) Outlook 및 Outlook Web App을 통해 사용자에 게 액세스할 수 있습니다. 자세한 내용은 [주소록 정책](address-book-policies-exchange-2013-help.md)를 참조 하십시오.

ABP와 관련된 추가 관리 작업에 대한 자세한 내용은 [주소 주소록 정책 절차](address-book-policy-procedures-exchange-2013-help.md) 항목을 참조하십시오.

이 절차를 사용하는 경우는 [시나리오: 주소록 정책 배포](scenario-deploying-address-book-policies-exchange-2013-help.md) 항목을 참조하십시오.

## 시작하기 전에 알아야 할 내용

  - 예상 완료 시간: 5분 미만

  - 이러한 절차를 수행하려면 먼저 사용 권한을 할당받아야 합니다. 필요한 사용 권한을 확인하려면 다음을 참조하세요. [이메일 주소 및 주소록 사용 권한](email-address-and-address-book-permissions-exchange-2013-help.md) 항목의 "주소록 정책" 항목

  - 이 항목의 절차에 적용할 수 있는 바로 가기 키에 대한 자세한 내용은 [Exchange 관리 센터의 바로 가기 키](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md)을 참조하세요.


> [!TIP]
> 문제가 있습니까? Exchange 포럼에서 도움을 요청하세요. 포럼 주소는 다음과 같습니다. <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, 또는 <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>



## 무슨 작업을 하고 싶으십니까?

## EAC를 사용 하 여 ABP 사서함 사용자에 게 할당 하려면

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서, 정책을 할당 하려는 사용자를 선택 하 고![편집 아이콘](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "편집 아이콘")**편집** 을 클릭 합니다.

3.  **사서함 기능** 을 클릭 합니다.

4.  **주소록 정책** 목록에서이 사용자에 게 적용 하려는 ABP를 선택 합니다.

5.  **저장**을 클릭합니다.

## EAC를 사용 하 여 여러 사서함 사용자에 게 ABP를 할당 하려면

1.  **받는 사람** \> **사서함**으로 이동합니다.

2.  목록 보기에서 Ctrl 키를 사용 하 여 여러 사용자를 선택 합니다.

3.  세부 정보 창에서 **기타 옵션**을 클릭합니다.

4.  **주소록 정책** **업데이트** 를 클릭 합니다.

5.  **주소록 정책 선택** 목록에서 해당이 사용자에 게 적용 하려는 ABP를 선택 합니다.

6.  **저장**을 클릭합니다.

## 셸을 사용 하 여 ABP 사서함 사용자에 게 할당 하려면

이 예제에서는 기존 사서함 사용자 joe@fabrikam.com에 ABP 모든 Fabrikam을 할당합니다.

    Set-Mailbox -Identity joe@fabrikam.com -AddressBookPolicy "All Fabrikam"

이 예에서는 `CustomAttribute11` 값을 가진 "엔지니어링 부서"를 포함 하는 모든 사서함 사용자에 게 ABP ABP\_EngineeringDepartment을 할당 합니다.

    Get-Mailbox -Filter {(CustomAttribute11 -like "Engineering Department")} | Set-Mailbox -AddressBookPolicy ABP_EngineeringDepartment

구문과 매개 변수에 대한 자세한 내용은 [Set-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123981\(v=exchg.150\)) 및 [Get-Mailbox](https://technet.microsoft.com/ko-kr/library/bb123685\(v=exchg.150\))를 참조하십시오.

